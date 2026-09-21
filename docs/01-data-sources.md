# Data Sources

Every figure in the report comes from one of five linked sources. Which source
a metric draws on determines two things a reader needs before interpreting it:
**who is in the denominator**, and **what the data cannot see**.

## The sources

| Source | What it provides | Period used |
|---|---|---|
| **Newborn screening (NBS)** | Screening results and laboratory-confirmed SCD genotype for infants screened in California | 2014–2023 |
| **SCD clinical care centers** | Confirmed genotype and clinical contact for people seen at participating California SCD centers | Through 2023 |
| **Medi-Cal eligibility** | Month-by-month enrollment, plus CCS and GHPP program enrollment dates | 2021–2023 |
| **Medi-Cal claims** | Medical and pharmacy claims: outpatient visits, screenings, prescription fills | 2021–2023 |
| **HCAI** | Emergency department, inpatient discharge, and ambulatory surgery encounters, from the California Department of Health Care Access and Information | 2021–2023 for access metrics; 2019–2023 for maternal metrics |
| **Vital records** | Death records, including underlying cause of death | 2014–2023 |

These are linked to one another at the person level, and each person carries a
single study identifier across all of them. Two sources set the case
definition — newborn screening and clinical care centers supply genotype — and
the rest describe care and outcomes. See
[Cohort and Populations](02-cohort-and-populations.md) for how a person becomes
part of the cohort.

## The distinction that matters most: HCAI versus Medi-Cal

This single difference explains why denominators vary between report sections,
and it is the most common source of confusion when comparing figures.

**HCAI is all-payer.** An emergency department visit or inpatient admission is
recorded regardless of how it was paid for. Metrics built on HCAI therefore use
the **full surveillance cohort** as their denominator, and are not restricted by
insurance coverage.

**Medi-Cal data only sees Medi-Cal.** Outpatient visits, preventive screenings,
prescription fills, and program enrollment are observable only for people
enrolled in Medi-Cal, and only for care billed to it. Metrics built on Medi-Cal
data are therefore restricted to an enrolled population.

| Report section | Source | Denominator |
|---|---|---|
| Emergency department | HCAI | Full cohort |
| Inpatient admissions | HCAI | Full cohort |
| Revisits | HCAI | People with an index visit |
| Maternal morbidity | HCAI inpatient | Females of reproductive age with a delivery admission |
| Newborn screening | NBS | Newborns screening positive |
| Mortality | Vital records | Decedents |
| Medi-Cal enrollment | Medi-Cal eligibility | Full cohort (enrollment *is* the metric) |
| Preventive screenings | Medi-Cal claims | Enrolled, plus a per-screening age window |
| Medications | Medi-Cal pharmacy claims | Enrolled, plus a per-drug age window |
| Outpatient visits and provider access | Medi-Cal claims | Enrolled |
| ED and inpatient reliance | HCAI **and** Medi-Cal combined | Enrolled — the outpatient component requires it |

Reliance ratios combine ED, inpatient and
outpatient counts, and the outpatient component exists only for enrolled people.
So although two of its three inputs are all-payer, the metric as a whole is
restricted to the Medi-Cal population.

## What the data cannot see

**A zero is not evidence that nothing happened.** For any Medi-Cal-based metric,
a count of zero means "no Medi-Cal claim for this service was found." Care paid
for another way, delivered outside the billing system, or received while not
enrolled does not appear. This applies to screenings, medications, outpatient
visits and provider contact.

**Out-of-state care is not captured.** Both HCAI and Medi-Cal are California
systems. A person who received care in another state appears to have received
none.

**Enrollment gaps interact with everything.** A person enrolled for part of a
year can only be observed during the enrolled months. This is why several
metrics are reported for two coverage populations rather than one — see
[Cohort and Populations](02-cohort-and-populations.md) > *Medi-Cal coverage
populations*.


## Longer time periods for some metrics

Most metrics cover 2021–2023. Three sections deliberately use longer windows:

- **Newborn screening and mortality:** 2014–2023
- **Maternal morbidity:** 2019–2023

A figure from one of these sections is not directly comparable to a 2021–2023
figure from another section.
