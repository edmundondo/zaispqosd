# Changelog

All notable changes to the Zambia ISP Tracker public demo are recorded here.
Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/); versioning
follows [Semantic Versioning](https://semver.org/) (MAJOR.MINOR.PATCH).

The version number shown here matches the `<meta name="app-version">` tag in
`index.html` and the `v{version}` badge in the page's footer.

## [1.0.0] — 2026-09-13

### Added
- First build, replicating the zwispqosd (Zimbabwe) demo/backend split pattern for
  Zambia from day one — no export options here, brand footer/logo matching
  zwispqosd, versioning in place.
- Provider list (`DATA`): Zamtel, MTN Zambia, Airtel Zambia, Liquid Intelligent
  Technologies Zambia, Paratus Zambia and Zamnet — sourced from ZICTA's 2024
  Annual Market Report, plus liquid.tech/paratus.africa/Wikipedia for ownership
  details. None has a published per-operator subscriber count, so every entry's
  `subscribers` is `null` with an explanatory `note`, exactly like `zwispqosd`
  already does for its own IAPs with no published counts.
- Sector-wide 2024 ZICTA figures (23.2 million active mobile subscriptions,
  +9.5% YoY; 13.5 million internet subscriptions, +7% YoY) shown in the header's
  "last synced" summary line.
- **Real official/recognised language chips from day one**: English (the
  Constitution's sole official language, per Article 1 Clause 5 of the 2009
  constitution) plus Bemba, Nyanja, Tonga, Lozi, Kaonde, Luvale and Lunda
  (recognised regional/broadcast languages per Wikipedia's "Languages of
  Zambia" — explicitly not claimed as constitutional-text languages, unlike
  English). Nyanja and Tonga reuse zwispqosd's existing best-effort-draft
  translations for the same standard languages (Chewa/Nyanja share ISO 639-3
  code `nya`; Tonga is spoken on both sides of the Zambia–Zimbabwe border) —
  legitimate reuse, not fabrication, still marked unreviewed. Bemba, Lozi,
  Kaonde, Luvale and Lunda have no cross-border shortcut and no verified source
  yet, so they ship as chips with empty translation content, falling back to
  English with the standard "🚧 need translation" badge. The suggest/endorse
  community-translation flow covers all eight languages from launch.
- 11 real Zambian cities for GPS/nearest-city matching (Lusaka, Kitwe, Ndola,
  Kabwe, Chingola, Mufulira, Livingstone, Chipata, Kasama, Solwezi, Choma) and
  small, clearly-illustrative seed QoS/status/speed data across them.
- Zambia-correct phone number handling (`+260`, 10-digit local numbers with a
  leading 0) in `normalizePhone`/`isValidPhone`.

### Notes — deliberate v1 scope cuts (see README.md for the full list)
- `ISP_ASN` and `PHONE_ISP_PREFIXES` both start empty — no verified data compiled
  for this build; both already degrade gracefully when empty.
- Cloudflare Radar national-benchmark feature not invoked (Zimbabwe-only edge
  function; a second, unverified proxy wasn't built sight-unseen for this
  release). `refreshRadarBenchmark()` stays defined but its call at the bottom of
  the file is commented out.
