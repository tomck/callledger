# CallLedger

Browser-only CDR cost investigation app. It parses CSV exports in a Web Worker and persists the current analysis in IndexedDB; it has no backend and does not upload call records.

Licensed under the [Apache License 2.0](./LICENSE). Copyright 2026 Tom Koch.

## Run locally

Serve this directory with any static-file server, for example:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080`. Browsers block Web Workers when `index.html` is opened directly from the filesystem.

## Deploy with GitHub Pages

1. Create an empty GitHub repository and push this folder to its `main` branch.
2. In the repository’s **Settings → Pages**, set **Source** to **GitHub Actions**.
3. The included workflow deploys automatically after every push to `main`.

GitHub Pages serves this as a static site. Uploaded call records are processed in the browser and are not sent to GitHub or any other service. IndexedDB persistence is per browser and device.

## Supported import templates

- FreePBX CDR: common `calldate`, `src`, `dst`, `duration`, `billsec`, `disposition`, `uniqueid`, and `linkedid` columns.
- Telnyx detailed CDR: common origination/termination, timestamp, billable time, cost, rate, direction, connection, and SIP Call-ID columns.
- WiretapTelecom and T38Fax: use the built-in column mapping review until their anonymized sample exports are collected.

All mappings and analysis data stay in the browser's local storage. Use **Clear local analysis** to remove it.
