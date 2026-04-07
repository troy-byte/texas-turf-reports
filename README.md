# Texas Turf — Sales Reports

Standalone, password-gated sales reporting dashboard for Texas Turf Company.
Built per Stefan's spec — 7 reports across Weekly / Monthly / Quarterly cadences.

**Live URL:** https://troy-byte.github.io/texas-turf-reports/
**Password:** see Troy

## Architecture

- `index.html` — single-page app, password gate (SHA-256 client-side), 3 tabs, reads `data.json`
- `data.json` — committed by the puller; raw computed report data
- Stage-history log lives in this repo at `stage_history.jsonl` (appended by Modal webhook subscribed to `OpportunityStageUpdate`)

## Data pipeline

Puller script lives in the main AGM workspace:
`/Users/troyscott/YouTube Workspace (DOE)/execution/tt_sales_reports_pull.py`

Runs nightly via cron (Mac Mini). Pulls from AGM v2 API (Texas Turf / Ivana sub-account, location `OB9iUeaKGJSNz9ea3So1`), computes all 7 reports, writes `data.json`, commits + pushes.

## Rotating the password

```bash
python3 -c "import hashlib; print(hashlib.sha256(b'YOUR_NEW_PASSWORD').hexdigest())"
```

Replace `ACCEPTED_HASH` in `index.html`. Commit + push.
