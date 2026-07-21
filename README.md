# Climate Change and Global Mortality

Exploring the relationship between climate change and mortality across ~130 countries
and over a century of records, using WHO mortality data alongside World Bank / CRU
climate and population data.

**Authors:** Auston Balwinski, Natasha Soldin
**Course:** University of Michigan MADS — SIADS 593 (Milestone 1)

---

## Overview

Climate change is a complex global crisis, and understanding the nature of its effects
is important if solutions are to be sought. This project explores the relationship
between climate variables and human mortality: it builds a clean, integrated
country-year dataset from three raw sources, then uses exploratory and correlation
analysis to characterize how temperature, maximum temperature, and precipitation relate
to deaths across **age groups** and **causes of death**.

The full write-up is in
[`24-austonb-nsoldin-2025sprsum.pdf`](24-austonb-nsoldin-2025sprsum.pdf).

## Key findings

- **Every country in the dataset has warmed.** The temperature differential from the
  1950–1980 baseline shows a positive yearly trend (~+0.03 °C/yr).
- **Absolute temperature matters more than the anomaly.** Across nearly all age groups
  and cause categories, mortality correlates more strongly with absolute temperature
  than with the year-over-year climate anomaly — **cold temperatures have an outsized
  effect** (elderly mortality vs. temperature ≈ **−0.45**).
- **The climate-change anomaly effect is small but real.** The temperature-differential
  correlation with all-ages mortality is only ~**+0.09**, but statistically significant
  (p < 0.05), and it is concentrated in older age groups and in neoplasms, circulatory,
  and mental/behavioral causes.
- **Precipitation is the least influential** of the climate variables studied.

These are **correlational**, not causal, results. Socioeconomic development, healthcare
quality, and climate adaptation are likely confounders (see the report's limitations
section).

## Repository structure

```
.
├── README.md
├── requirements.txt
├── LICENSE
├── 24-austonb-nsoldin-2025sprsum.pdf            # Full project report
└── 24-austonb-nsoldin-2025sprsum/
    └── src/
        ├── Climate Change and Mortality Notebook.ipynb   # End-to-end analysis
        └── Data/
            ├── WBO Climate Data/                # Included (small)
            │   ├── temperature_means_cru_timeseries.csv
            │   ├── temperature_mean_max_cru_timeseries.csv
            │   ├── precipitation_cru_timeseries.csv
            │   └── wbo_pop.csv
            └── WHO Mortality/
                ├── country_codes                # Included (small)
                └── Morticd10_part1..6           # NOT included — see "Data" below
```

## Data

| Source | Provider | Access |
|--------|----------|--------|
| Temperature, max temperature, precipitation (CRU TS, yearly by country) | Climatic Research Unit, via the World Bank Climate Change Knowledge Portal | https://climateknowledgeportal.worldbank.org |
| Mortality by country, year, sex, age, and ICD-10 cause | WHO Mortality Database | https://www.who.int/data/data-collection-tools/who-mortality-database |
| Population by country-year | World Bank DataBank — World Development Indicators | https://databank.worldbank.org |

The small climate CSVs and the WHO `country_codes` lookup are committed to this repo.
The six raw WHO mortality files (`Morticd10_part1` … `Morticd10_part6`, **~442 MB total**)
are **not** committed. To reproduce the full pipeline, download them from the
[WHO Mortality Database](https://www.who.int/data/data-collection-tools/who-mortality-database)
and place them in:

```
24-austonb-nsoldin-2025sprsum/src/Data/WHO Mortality/
```

Exact download configurations for each source are documented in the report.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Running the analysis

```bash
cd "24-austonb-nsoldin-2025sprsum/src"
jupyter lab
```

Open **`Climate Change and Mortality Notebook.ipynb`** and run all cells (data paths are
relative to the `src/` directory). Static plot outputs are already embedded and render on
GitHub; the interactive Plotly maps and `ipywidgets` controls only render live inside a
running Jupyter session.

## License

The code and notebook in this repository are released under the [MIT License](LICENSE).
The underlying datasets remain subject to their original terms from the WHO and the
World Bank; please consult those sources for their respective licenses and attribution
requirements.
