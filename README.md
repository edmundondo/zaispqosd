# zaispqosd

Public demo for the Zambia ISP Tracker — crowdsourced quality-of-service ratings,
live status reports and speed tests for Zambia's internet providers, sourced from
ZICTA's published sector data and operators' own results.

Sibling of [zwispqosd](https://github.com/edmundondo/zwispqosd) (Zimbabwe),
[bwispqosd](https://github.com/edmundondo/bwispqosd) (Botswana) and
[saispqosd](https://github.com/edmundondo/saispqosd) (South Africa) — same codebase
pattern, same shared Supabase backend (multi-tenant via a `site` column), different
country data. See `zwispqosd`'s README/SETUP docs for the full technical background
on how the backend, live feeds (IODA) and speed test work — nothing about that
plumbing is Zambia-specific.

Formatted report exports (PDF/CSV/EPUB) will live on a privileged `zaispqosp`
backend once it's built — not here.

## Provider data

Six ISPs/operators, in order, all sourced from ZICTA's 2024 Annual Market Report
(and one operator page or Wikipedia where noted):

1. **Zamtel** — 100% Government of Zambia owned (reacquired 2012 after a reversed
   fraudulent 2010 sale to Libya's LAP Green Networks). Zambia's sole fixed-line
   operator (~80,000 lines) plus mobile/mobile-internet. No per-operator subscriber
   count published by ZICTA.
2. **MTN Zambia** — subsidiary of MTN Group (South Africa); some free-float shares
   trade on the Lusaka Securities Exchange.
3. **Airtel Zambia** — subsidiary of Airtel Africa plc, majority-owned by Bharti
   Airtel (India).
4. **Liquid Intelligent Technologies Zambia** — subsidiary of Cassava Technologies
   (Strive Masiyiwa's pan-African group); national fiber backbone, wholesale
   capacity, public Wi-Fi.
5. **Paratus Zambia** — part of Paratus Group (Namibia-headquartered, linked to
   Namibia's Capricorn Group); fiber, fixed wireless, satellite, enterprise
   connectivity.
6. **Zamnet** — Zambia's original ISP. Current ownership/status could not be
   confirmed in research for this build — flagged honestly in its `note` field
   rather than guessed.

None of the six has a published per-operator subscriber count from ZICTA, so every
entry's `subscribers` field is `null` with an explanatory `note` — the same pattern
`zwispqosd` uses for its own unpublished-count providers. Sector-wide 2024 figures
(23.2 million active mobile subscriptions, +9.5% YoY; 13.5 million internet
subscriptions, +7% YoY) are shown in the page's "last synced" summary line, sourced
to ZICTA's 2024 Annual Market Report.

## Languages

Zambia's Constitution (2009, as amended; Article 1, Clause 5) names English as the
country's **sole official language**. Bemba, Nyanja, Tonga, Lozi, Kaonde, Luvale and
Lunda are widely spoken regional languages recognised in national broadcasting and
education policy (source: Wikipedia, "Languages of Zambia") — **not** languages
named in the constitutional text itself. This site is careful to keep that
distinction honest rather than overstate it.

All eight ship as chips (English + the seven listed above):

- **Nyanja** reuses `zwispqosd`'s existing Chewa (`ny`) I18N block verbatim — Chewa
  and Nyanja are the same standard language (ISO 639-3: `nya`), so this is
  legitimate reuse, not fabrication. Only the outward-facing label changed
  ("Nyanja" instead of "Chewa"); the block is flagged as unreviewed, same as on
  the Zimbabwe site.
- **Tonga** reuses `zwispqosd`'s existing Tonga (`toi`) I18N block verbatim — the
  same language is spoken on both sides of the Zambia–Zimbabwe border by Lake
  Kariba.
- **Bemba, Lozi, Kaonde, Luvale and Lunda** have no cross-border shortcut and no
  verified translation source, so they ship as chips with literally empty I18N
  objects. They fall back cleanly to English via the existing `tt()` helper with
  the standard "🚧 need translation" badge — nothing was guessed to fill the gap.

The suggest/endorse community-translation flow covers all eight languages today.

## What's different about this site (v1.0.0 scope)

- **No backbone (RIPEstat/ASN) badges.** `ISP_ASN` is intentionally empty — no
  verified ASN-to-operator mapping has been compiled for Zambia yet. The badge
  simply doesn't render for any ISP without an entry, the same graceful fallback
  the Zimbabwe site already relies on for its own untracked ISPs.
- **No Cloudflare Radar national benchmark.** That feature calls a Supabase Edge
  Function that's hardcoded server-side to Zimbabwe's numbers only (and is a
  separately-tracked, not-fully-verified feature even there) — rather than build a
  second country-specific proxy sight-unseen, it's simply never invoked on this
  site (`refreshRadarBenchmark()` stays defined but uncalled).
- **No phone-prefix ISP detection.** `PHONE_ISP_PREFIXES` starts empty — no
  verified ZICTA numbering-plan-to-carrier mapping was available for this build.
  `normalizePhone`/`isValidPhone` do understand Zambia's numbering shape (10-digit
  local numbers with a leading 0, dialled internationally as +260).
- Provider list is intentionally small (6 tracked providers) and seed
  ratings/status/speed data is small and clearly illustrative (5–8 entries per
  category), not a real crowdsourced history — this is a fresh site with no real
  users yet.
- No export/download options anywhere on this page — matches the established,
  export-free public-demo pattern across the whole family.

See `CHANGELOG.md` for version history.
