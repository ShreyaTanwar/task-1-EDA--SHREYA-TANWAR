# CO2 Emissions and Economic Development: EDA Proposal (Week 1 Task)

A planning project for an exploratory data analysis (EDA) of national CO2 emissions against income, using two open datasets:

- **Our World in Data (OWID) CO2 and GHG emissions database** (one CSV from GitHub)
- **World Bank World Development Indicators**, pulled from the public Indicators API v2 (GDP per capita, PPP GDP per capita, population, urban population share, industry share of GDP)

The deliverable is a proposal, not a finished analysis. This repository holds the evidence behind it: real preliminary profiling of both datasets, the diagrams and wireframes, and the report text. Every number in the report comes from the code here.

## Repository layout

```
README.md
requirements.txt
data/
  raw/                           downloaded files (git-ignored; recreated by the script)
  processed/
    profiling/                   small profiling tables + profiling_summary.json
    joined_preview_owid_worldbank.csv   preview of the ISO3 + year join (git-ignored)
notebooks/
  01_preliminary_profiling.ipynb executed profiling notebook with commentary
src/
  profile_data.py                download + profile both datasets, write tables and 3 figures
  make_figures.py                draw flowcharts, Gantt chart and wireframes (matplotlib only)
  style.py                       shared colours and matplotlib style
figures/                         all PNG figures (200 dpi)
report/
  report_content.md              the full proposal, ready to paste into Word
  report_notes.md                notes for the author: figure map, checks, viva questions
```

## Setup

Python 3.11 or newer (developed on 3.13).

```bash
python -m venv .venv
# Windows (PowerShell):  .venv\Scripts\Activate.ps1
# macOS / Linux:         source .venv/bin/activate
pip install -r requirements.txt
```

## How to run

From the project root:

```bash
python src/profile_data.py            # downloads data if missing, writes tables + 3 profiling figures
python src/profile_data.py --refresh  # force a fresh download (counts may change slightly)
python src/make_figures.py            # flowcharts, Gantt chart, 4 wireframes (reads the profiling summary)
```

Run `profile_data.py` before `make_figures.py`, because the cleaning flowchart quotes numbers from `data/processed/profiling/profiling_summary.json`.

### The notebook

```bash
jupyter notebook notebooks/01_preliminary_profiling.ipynb
```

or execute it headlessly and save the outputs:

```bash
jupyter nbconvert --to notebook --execute --inplace notebooks/01_preliminary_profiling.ipynb
```

The first run downloads about 21 MB (14.4 MB OWID CSV plus five World Bank JSON files).

## What the profiling checks

Shape, dtypes, missing values by column, duplicate keys, year and country coverage, non-country entities, impossible and extreme values, skewness, ISO3-versus-name key matching across the two sources, a population cross-check, and a join preview for the 1990-2022 study window.

## Data sources and licences

| Source | URL | Licence |
|---|---|---|
| OWID CO2 data | https://github.com/owid/co2-data | OWID states its data, visualizations and code are open access under Creative Commons BY; third-party inputs keep their own terms |
| World Bank Indicators API | https://api.worldbank.org/v2/ (docs: https://datahelpdesk.worldbank.org/knowledgebase/articles/889392-about-the-indicators-api-documentation) | CC BY 4.0 by default (https://datacatalog.worldbank.org/public-licenses) |

Cite both Our World in Data and the underlying sources (for example the Global Carbon Project) when reusing the data.

## Notes

- Raw data and the large joined preview are git-ignored because the scripts recreate them.
- Figures are drawn with matplotlib only, so no extra system dependencies are needed.
- The wireframes use made-up placeholder shapes and contain no real data.
