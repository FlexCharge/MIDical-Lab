# MIDical Lab — Sample Reports

Static HTML samples from the MIDical Lab two-cohort MID-refresh experiment, hosted via GitHub Pages.

The experiment runs **two risk-stratified cohorts** — **LOW** (lower-dispute) and
**MED** (higher-dispute) — and each cohort has its own full, independent report set.
Compare the two by opening them side by side.

## Live links

- **Landing page** (both cohorts + per-cohort archives) — `https://flexcharge.github.io/MIDical-Lab/`

**LOW cohort**
- Weekly report — current: `.../low/weekly.html` · per-week archive: `.../low/weekly/YYYY-MM-DD.html`
- Life of Experiment (cumulative) — `.../low/life-of-experiment.html`
- Decision-tree walkthrough — current: `.../low/walkthrough.html` · archive: `.../low/walkthrough/YYYY-MM-DD.html`

**MED cohort**
- Weekly report — current: `.../med/weekly.html` · per-week archive: `.../med/weekly/YYYY-MM-DD.html`
- Life of Experiment (cumulative) — `.../med/life-of-experiment.html`
- Decision-tree walkthrough — current: `.../med/walkthrough.html` · archive: `.../med/walkthrough/YYYY-MM-DD.html`

## Layout

```
site/
├── index.html              Generated combined landing page (both cohorts + archives). Do not hand-edit.
├── low/                    LOW cohort report set
│   ├── index.html          Per-cohort landing
│   ├── weekly.html         Always-current weekly snapshot
│   ├── life-of-experiment.html   Single cumulative report (window grows; not archived per week)
│   ├── walkthrough.html    Always-current decision-tree walkthrough
│   ├── weekly/YYYY-MM-DD.html        Per-week archived weekly
│   └── walkthrough/YYYY-MM-DD.html   Per-week archived walkthrough
└── med/                    MED cohort report set (same structure)
```

## How to update

From the Flex Toolkit project, run the monitor once for **both** CAIDs, then run
`synthesize_weekly_and_monthly.py` **once per cohort** (cohort + CAID + site subfolder
passed via env vars), then build the combined landing page:

```bash
cd "C:\ClaudeProjects\Flex Toolkit"
# 1. Pull both cohorts' data into one output dir
python "MIDical Lab/scripts/mid_weekly_monitor.py" --caid <LOW_CAID> <MED_CAID> --window-days 56
# 2. Synthesize each cohort into its own subfolder
MIDICAL_COHORT=LOW MIDICAL_CAID=<LOW_CAID> MIDICAL_SITESUB=low python "MIDical Lab/scripts/synthesize_weekly_and_monthly.py"
MIDICAL_COHORT=MED MIDICAL_CAID=<MED_CAID> MIDICAL_SITESUB=med python "MIDical Lab/scripts/synthesize_weekly_and_monthly.py"
# 3. Build the combined landing page
MIDICAL_LOW_CAID=<LOW_CAID> MIDICAL_MED_CAID=<MED_CAID> python "MIDical Lab/scripts/build_landing.py"
# 4. Commit everything (use -A so new archive files + regenerated index are included)
cd "MIDical Lab/site"
git add -A && git commit -m "Refresh reports" && git push
```

GitHub Pages picks up the new files within ~1 minute.

## About the data

Samples are generated against two live Paysafe NX CAIDs from the FlexFactor portfolio
as structural stand-ins (LOW `937700006246` / MED `937700006857`). Production reports
point at the two experiment MIDs and regenerate every Monday.

The HTML files are self-contained — embedded CSS, Inter from Google Fonts with
system-sans fallback, no external assets. Inline SVG for all charts and sparklines.
