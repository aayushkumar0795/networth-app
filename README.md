# networth-app

A single-file, mobile-first net worth tracker. Self-contained HTML — no build
step, no dependencies, no server, no network calls except optional sync.

**Live app:** https://aayushkumar0795.github.io/networth-app/

## Screens

Home (hero + metric tiles + accounts + snapshots), metric explainers, account and
item detail, US-equity holdings book, snapshot detail, Trends, Structure tree,
X-Ray diagnostics (liquidity, runway, concentration, shocks, leverage), Goals,
EMI share ledger, accounts manager, snapshot entry, and Data settings.

Fonts (Barlow / Barlow Condensed) are embedded as woff2, so it works offline once
loaded. Light and dark themes, following the OS with a manual toggle.

## How it works

- Data lives in the browser's `localStorage` under `networth-v1`.
- Optional sync: commits a JSON file to a **separate private repo**
  (`networth-data`) via the GitHub contents API, using a fine-grained token
  entered in Data settings on each device.
- The token is stored per-device under `networth-gh`, never exported, never in
  this repo.

## ⚠️ This repo is PUBLIC — it must never contain personal data

App code only. No balances, no account names, no holdings, no people, no tokens.

The app ships with an **empty first-run state**. Two places have leaked real data
before, and both must be checked before any publish:

1. The **seed module** inside `__bundler/manifest` — gzip+base64, so a plaintext
   grep will not find it. Decode every entry and scan.
2. The **EMI defaults** in the `__bundler/template` script — these shipped with
   real names and balances from the design bundle.

Verify with a needle list drawn from the design bundle as well as from your own
data file. Grepping the raw HTML is not sufficient.

Backups are named `networth-*.json` and are gitignored. Personal financial data
belongs in the private `networth-data` repo, nowhere else.
