# hospital-price-history-raw

Bulk payer-level data for
[hospital-price-history](https://github.com/lkowalcz/hospital-price-history)
— a git-scraping archive of the machine-readable price files (MRFs) US
hospitals must publish under 45 CFR § 180.50.

This companion repo holds the **sharded** storage tier: MRFs too big to
store whole (45–600 MB) are split into 32 hash-bucketed, sorted shard files
(CSV rows or JSONL items) plus a `_header` file, under
`data/<slug>/`. Sorting and stable bucketing mean `git diff` between any
two commits shows exactly which negotiated rates changed.

Everything else — the roster, per-hospital `meta.json` and `summary.csv`
digests, the price index, methodology, and the website — lives in the
[main repo](https://github.com/lkowalcz/hospital-price-history). Each
sharded hospital's `meta.json` there pins the commit here (`raw_commit`)
that holds its current shards, and commits land here first, so the pair is
always consistent.

Shard history **before 2026-08-26** lives in the main repo's git history
(the layer moved here on that date to keep the main repo clonable); from
that date on, `git log data/<slug>/` in this repo is the payer-level
changelog per hospital.

Data is public domain (CC0), as published by the hospitals themselves.
