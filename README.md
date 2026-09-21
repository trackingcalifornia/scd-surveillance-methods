# Sickle Cell Disease in California: 2026 Surveillance Report — Methods

How the metrics in *Sickle Cell Disease in California: 2026 Surveillance Report*
are defined and calculated, so that a reader can see *how* a number was produced
and not just what it is.

## Start here

**Want a published figure cut a different way?** Open the **Report Metrics**
sheet in [`SCD-Surveillance-Reference.xlsx`](docs/SCD-Surveillance-Reference.xlsx),
or [`metrics.csv`](docs/metrics.csv). Every main-report table and figure is
listed against the dataset and variables behind it, which breakdowns are
available, and which are not.

## Documentation

| | |
|---|---|
| [01 — Data Sources](docs/01-data-sources.md) | The five linked sources, what each covers, and what the data cannot see. Includes the all-payer versus Medi-Cal distinction that drives every denominator difference in the report. |
| [02 — Cohort and Populations](docs/02-cohort-and-populations.md) | Case definition, cohort and study period, coverage populations, age, geography, and the suppression rule. |
| [03 — Metric Definitions](docs/03-metric-definitions.md) | Every metric, by report section. |
| [Data Dictionary](docs/data-dictionary.md) | Every variable in each analytic dataset, and which report elements it feeds. |
| [Code Lists](docs/code-lists.md) | How diagnosis, procedure and medication codes are matched, and what each list covers. |

## The same reference, as data

For anyone who would rather filter and sort than read:

| File | Contents |
|---|---|
| [`SCD-Surveillance-Reference.xlsx`](docs/SCD-Surveillance-Reference.xlsx) | One workbook, five sheets: Read Me, Report Metrics (45), Datasets (9), Variables (245), Code Lists (463) |
| [`metrics.csv`](docs/metrics.csv) | One row per main-report table and figure |
| [`datasets.csv`](docs/datasets.csv) | The twelve analytic datasets, with the unit each is observed at |
| [`data-dictionary.csv`](docs/data-dictionary.csv) | One row per variable |
| [`code-lists.csv`](docs/code-lists.csv) | One row per code |

Codes are stored as text, so leading zeros survive — an NDC such as
`00078088361` is not turned into a number.

## Requesting a custom summary

The datasets described here are not public: they hold person-level records
derived from restricted sources. What can be produced from them is *aggregate
summaries*.

Before requesting, two things are worth knowing:

- **Counts below 11 are not released**, nor percentages or totals from which a
  suppressed count could be recovered. Crossing several breakdowns at once often
  trips this even where each one is available on its own.
- **Not every dataset is one row per person.** Mortality and newborn screening
  figures are aggregated to county and year, and maternal figures are one row per
  delivery admission. See [02](docs/02-cohort-and-populations.md).

Send requests to [scdc@trackingcalifornia.org](mailto:scdc@trackingcalifornia.org),
saying which published table or figure you are starting from and which breakdown
you want.

## What is not here

Underlying data is not included or accessible from this repository. CA-SCDC data
includes information protected under data use agreements and privacy laws.

Analysis code is not published. This repository documents definitions and
methods rather than implementation.

The reference files in [`docs/`](docs) are generated from two internal
workbooks — the data dictionary, and the medical code workbook the analysis
pipeline reads to build its lookup table. Those workbooks are not published;
what they contribute to any reported figure is reproduced here in full.

## Source

Produced by the California Sickle Cell Data Collection program (Tracking
California) — [www.cascdc.org](https://www.cascdc.org),
[scdc@trackingcalifornia.org](mailto:scdc@trackingcalifornia.org). See
*Sickle Cell Disease in California: 2026 Surveillance Report* for results,
context and citations.

## Reuse

This documentation is published under [CC BY 4.0](LICENSE): reuse and adapt it
freely, with attribution. Cite the report itself for findings; see
[`CITATION.cff`](CITATION.cff) for citing this documentation.
