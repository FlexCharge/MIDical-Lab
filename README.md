# MIDical Lab — Sample Reports

Static HTML samples from the MIDical Lab experiment, hosted via GitHub Pages.

## Live links

- **Landing page** (current reports + archive of all prior weeks) — `https://flexcharge.github.io/MIDical-Lab/`
- **Weekly report** — current: `.../weekly.html` · per-week archive: `.../weekly/YYYY-MM-DD.html`
- **Decision-tree walkthrough** — current: `.../walkthrough.html` · per-week archive: `.../walkthrough/YYYY-MM-DD.html`
- **Monthly deep dive** (cumulative, life of experiment) — `https://flexcharge.github.io/MIDical-Lab/monthly.html`

## What's in here

| File | Source |
|---|---|
| `index.html` | **Generated** landing page — latest-report cards + a "Prior weeks" archive list. Do not hand-edit; `synthesize_weekly_and_monthly.py` regenerates it each run. |
| `weekly.html` / `walkthrough.html` | Always-current "latest" weekly + walkthrough (mirrors of the synthesized reports). |
| `monthly.html` | Single cumulative monthly deep dive for the life of the experiment (window grows each month; not archived per month). |
| `weekly/YYYY-MM-DD.html` | Per-week **archived snapshot** of the weekly report, frozen at each Monday run. |
| `walkthrough/YYYY-MM-DD.html` | Per-week archived snapshot of the walkthrough. |

## How to update

Re-run `synthesize_weekly_and_monthly.py` from the Flex Toolkit project. It
writes to `docs/sample_reports/`, mirrors the current reports here, writes the
per-week archive snapshots under `weekly/` and `walkthrough/`, and regenerates
`index.html` with the prior-weeks list. Then commit **everything** (use `-A` so
new archive files and the regenerated index are included):

```bash
git add -A
git commit -m "Refresh reports"
git push
```

GitHub Pages picks up the new files within ~1 minute.

## About the data

Samples are generated against live CAID 937700006246 (a FlexFactor merchant
CAID) as a structural reference. Production reports point at the two experiment
MIDs (LOW 937700011015 / MED 937700011639) and regenerate every Monday.

The HTML files are self-contained — embedded CSS, Inter from Google Fonts with
system-sans fallback, no external assets or JavaScript. Inline SVG for all
charts and sparklines.

## Auto-refresh

GitHub CLI is configured locally so Claude Code can push refreshes from a
synthesize run without manual git operations. To refresh:

```bash
cd "C:\ClaudeProjects\Flex Toolkit"
python "MIDical Lab/scripts/synthesize_weekly_and_monthly.py"
cd "MIDical Lab/site"
git add . && git commit -m "Refresh samples" && git push
```
