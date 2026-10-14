# CALIBER360 Ambulatory Intelligence — GitHub Pages Pilot

A static, serverless browser dashboard for the **limited HCAI facility sample**. It reads the four supplied Parquet files in-browser using DuckDB-Wasm; interactive charts use Plotly.js. Your existing Streamlit app is unchanged.

## Deploy without changing the homepage

1. Extract the ZIP. Copy the entire `ambulatory` folder (containing `index.html`, `styles.css`, `app.js`, `data/`) into the root of the GitHub Pages repository `alakhani33/caliber360ai`.
2. Commit and push to the branch used by GitHub Pages (typically `main`).
3. Open **https://caliber360ai.com/ambulatory/**. Do **not** overwrite the existing root `index.html`.
4. Check the browser developer console if a data file or CDN dependency fails to load.
5. Do not add a homepage navigation link until the pilot passes acceptance checks. An unlinked URL is still public.

## Local test on Windows

From the directory containing `ambulatory`:

```powershell
python -m http.server 8000
```

Open http://localhost:8000/ambulatory/ . `file://` won't work because browser fetches require a web server.

## Acceptance checks

- Verify facility and encounter totals against the V4.1 Streamlit app for the same year, quarter and facility filters.
- Check that 2026 partial quarters are not treated as full-year comparisons.
- Check category percentages against original Parquet/Streamlit results.
- Verify facility growth using only matched facility-quarter pairs.
- Confirm the Facility Strategy Profile prints/saves to PDF in the browser.
- Check mobile layout and network performance.

## Pilot limitations

- Not a statewide dataset. Competitive share is **selected-facility sample share** only.
- Facility Strategy Profile PDF uses the browser's Print/Save as PDF, not the ReportLab-generated V4.1 report.
- This is a first-pass functional port, not yet feature-identical to Streamlit. The demographic dimension selector and full-year comparative logic should be checked during acceptance testing.
- Requires public CDN access to DuckDB-Wasm and Plotly.js. For a production deployment, pin/vendor these dependencies and add caching.
- All Parquet files are publicly downloadable; only publish data approved for public release.
- No background scraping, private data storage, login or server-side AI features.
- Dataset refresh: replace the four Parquet files, commit, and redeploy. No code changes needed if schemas remain the same.

## Pilot v1.1 fixes
- Data Quality tab: corrected JavaScript temporal dead-zone error (`periods`).
- Long facility names: horizontal comparison chart, expanded axis margins and automatic Plotly margins for labels.
- After deployment, hard-refresh (Ctrl+Shift+R) to bypass browser cache.
