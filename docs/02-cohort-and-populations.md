# Cohort and Populations

Who is counted, how they were identified, and the population definitions that
apply across every metric in the report. Definitions specific to a single
measure are in [Metric Definitions](03-metric-definitions.md).

## Identifying people with SCD

The validated CA-SCDC case definition is applied across the linked sources in
[Data Sources](01-data-sources.md). Cases fall into two levels:

- **Confirmed SCD** — identified through California's newborn screening program
  or SCD clinical care center data, with a laboratory-confirmed SCD genotype
  from one of those sources.
- **Probable SCD** — no genotype available from newborn screening or clinical
  care records, but an SCD ICD-CM code (excluding sickle cell trait) on three
  or more separate health care encounters within a five-year period.

Both confirmed and probable cases are included in the report.

## Identifying the surveillance cohort

Among people identified with SCD, the report includes those confirmable as
California residents during 2021–2023. Residency in a given year was
established by meeting at least one of:

1. Born in California during that year; or
2. Enrolled in Medi-Cal during that year; or
3. Had at least one encounter in HCAI inpatient, emergency department, or
   ambulatory surgery data, or at a participating clinical site, during that
   year.

A person also counts as a California resident in a given year if criteria 2 or 3
were met in both the year before and the year after. Because the report relies
on encounter data to confirm residency, this three-year window captures people
who had no reason to access health care every single year but were nonetheless
living in California throughout.

Operationally, residency is checked against each year's ZIP code of residence. A
person is retained if at least one year's ZIP falls in California, or is one of a
small set of placeholder values used for people experiencing homelessness or
otherwise without a standard address. People whose ZIP is genuinely blank in all
three years are excluded.

## SCD-related claims

ICD-10 diagnosis codes identify SCD-related claims (`D57.x`), excluding sickle
cell trait (`D57.3`). SCD-related claims are deduplicated by date.

## Age

**One age variable underlies the report.** Age is calculated as of the end of
2023, or at date of death for people who died during the study period. It does
not vary by report year.

Three overlapping category schemes are used:

| Scheme | Categories |
|---|---|
| `age_cat_a` | <21, 21+ |
| `age_cat_b` | ≤10, 11–20, 21–30, 31–40, 41–50, 51–60, 60+ |
| `age_cat_c` | ≤2, 3–5, 6–10, 11–20, 21–30, 31–40, 41–50, 51–60, 60+ |

`age_cat_c` splits early childhood into ≤2 and 3–5 rather than collapsing
everyone under 10, which better supports metrics focused on young children.

Because these categories are fixed at a single point in time, **an age
breakdown cannot be produced per year** — a person sits in the same band for all
three years regardless of a birthday during the period.

### Age eligibility is derived differently for different metrics

**Medications — derived per calendar year from date of birth.** Each drug's
clinical age window is applied separately to each year, testing whether the
person's age fell inside that window at any point during that year. This is
computed from date of birth rather than from the `age` variable above.
Consequently:

- Decedents are excluded from years after their death.
- A child eligible for only part of a year is still in that year's denominator,
  which makes sustained-use percentages a conservative lower bound — a partial
  year cannot accrue a full year's supply days.

**Screenings — the `age` variable with a widened window.** Rather than shifting
per year, the eligible range is widened so it captures anyone who was
age-eligible at *any* point during 2021–2023. A metric described as "ages 2–16"
in the report is therefore implemented against a wider band, so that a child who
aged out mid-period is not wrongly excluded.

All 2021–2023 combined metrics include anybody eligible at any time during the
period.

## Sickle Cell Anemia (SCA) subpopulation

Several metrics are additionally reported for the subset with Sickle Cell Anemia
specifically — genotype HbSS or HbSB0 — since disease severity and recommended
care differ meaningfully across SCD genotypes.

## Medi-Cal coverage populations

Several metrics are reported for more than one coverage population, because both
eligibility for a service and the ability to observe it in claims depend on
enrollment:

- **Any Medi-Cal coverage** — enrolled in at least one month of the applicable
  year or years.
- **Continuous Medi-Cal coverage** — enrolled for all 12 months of the
  applicable year, or for 2021–2023 combined metrics, all 12 months of each of
  the three years.

A person missing a metric under continuous coverage may still have received the
service — while not enrolled, or billed somewhere this data cannot see.

## County of residence and Social Vulnerability Index

County and neighborhood-level SVI are assigned for each study year from that
year's ZIP code, using a standard ZIP-to-county crosswalk. SVI is converted to
quartiles by ZIP: Q1 (lowest vulnerability, percentile ≤0.25) through Q4
(highest, >0.75). ZIP codes with missing or invalid SVI are left blank.

Two person-level summaries are derived:

- **Main county of residence** — the most recent year in which a county could be
  resolved from ZIP: 2023 if available, otherwise 2022, otherwise 2021. A person
  is "Unknown" only if no county resolved in any of the three years.
- **Main SVI quartile** — the quartile reported most often across the three
  years. Ties resolve to the lower-vulnerability quartile.

## Suppression

**Counts below 11 are not released**, and neither are percentages or totals from
which a suppressed count could be recovered.

This is the most common reason a request for a custom breakdown cannot be
filled. Availability and releasability are different questions: a variable can
be present on every record and still be unreleasable in combination with others,
because each additional stratifier thins the cells. County crossed with almost
anything else will suppress for the smaller metrics — antibiotic prophylaxis,
sustained fills, individual complications, individual SMM indicators.

Where a published figure is already at or near the threshold, the metric
definition says so.
