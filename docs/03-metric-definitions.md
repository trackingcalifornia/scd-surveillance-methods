# Metric Definitions

Grouped by report section. Population, source and available breakdowns for each
report table and figure are in [`metrics.csv`](metrics.csv); codes are in
[`code-lists.csv`](code-lists.csv); variables in
[`data-dictionary.csv`](data-dictionary.csv).

See [Data Sources](01-data-sources.md) and
[Cohort and Populations](02-cohort-and-populations.md) for the rules that apply
throughout.

---

## Prevalence and demographics

Reported: cohort count; age in 10-year categories; sex overall and by age
category; race and ethnicity jointly; county of residence; SVI quartile by year
and overall; housing instability.

**Race and ethnicity.** Race is the most frequently reported single race
category across sources. A person is classified as multiple race only where
multi-race was itself the reported category on a record — not because different
single-race records appeared in different sources. Race and ethnicity are
cross-tabulated, not reported as independent distributions.

**Housing instability.** More than one ZIP code or county of residence recorded
across 2021–2023, as two independently computed indicators: moved counties, and
moved ZIPs. A residential move within one county changes ZIP but not county, so
a person can register on one indicator and not the other.

---

## Newborn screening

A person counts as an NBS-confirmed birth in the year matching their birth year.
Birth counts and genotype distributions reflect confirmed cases only.

- **Sex** is sex assigned at birth.
- **County** is birth county, from the mother's reported address at
  birth/screening.

---

## Mortality

Two levels of output, from different starting populations:

| Question | Level | Period |
|---|---|---|
| How many died, where, at what age | One row per county per year | 2014–2023 |
| What they died of | One row per decedent | 2021–2023 cohort |

- **Age at death** is as recorded on the death certificate.
- **Cause of death** is the *underlying* cause, ICD-10 coded. Cardiovascular and
  external causes carry a further subcategory; other body systems do not.
- **Death rates** are per 10,000, using the identified SCD population captured
  in SCDC data for that year as the denominator — the surveillance population,
  not the general California population.
- Deaths occurring outside California may not be captured.

---

## Maternal morbidity

**Population.** Built directly from the case-ascertainment extract, not the
report's standard cohort, because the window is 2019–2023:

- Sex recorded as female
- Born 1964–2011 — no older than 55 in 2019, no younger than 12 in 2023 — and,
  if deceased, death in 2019 or later
- A California ZIP (or unhoused/unknown placeholder) on file for at least one
  year in the window

**Unit of observation is the delivery admission.** A woman with multiple
deliveries contributes one row each. Row counts are deliveries; distinct-person
counts are women.

**Maternal age** is age at that delivery, from birth date and the admission's
service date, so the same woman appears at different ages across her records.
Grouped 12–20, 21–30, 31–40, 41–50, 51–55.

**Severe Maternal Morbidity** uses the CDC 21-indicator list, applied to all
diagnosis and procedure codes on the delivery admission. An admission is flagged
for an indicator if a matching code appears anywhere on the record; "any SMM" is
set if one or more indicators is present.

Two percentages, which are not the same calculation:

| Metric | Level | Definition |
|---|---|---|
| Annual SMM % | Admission | SMM admissions in a year ÷ delivery admissions that year |
| Overall SMM % | Individual | Women with ≥1 SMM admission ÷ women with a delivery admission, 2019–2023 |

**Rate of SMM** = (delivery admissions with SMM ÷ total delivery admissions) ×
10,000. An admission counts once regardless of how many indicators it carries.

Also reported by SVI quartile, using the quartile for the calendar year of the
delivery.

---

## Medi-Cal enrollment and program coverage

Enrollment is assessed monthly.

| Population | Definition |
|---|---|
| Any coverage | Enrolled ≥1 month of the applicable year(s) |
| Full coverage, single year | Enrolled all 12 months of that year |
| Full coverage, 2021–2023 | Full coverage in each of 2021, 2022 and 2023 individually |

The three-year definition requires 12 months in every year, not 36 months
anywhere in the period.

**Program coverage.** California Children's Services (CCS) is assessed among
people age <21 with any Medi-Cal coverage; the Genetically Handicapped Persons
Program (GHPP) among people age >=21. GHPP becomes available once a CCS-eligible
person reaches adulthood, so no GHPP record exists before that point.

Private and other non-Medi-Cal coverage is not present in these data. CCS/GHPP
participation and Medi-Cal enrollment are the only coverage captured.

---

## Preventive screenings

| Screening | Age eligibility | Identification |
|---|---|---|
| Transcranial Doppler (TCD) | 2–16 years | CPT |
| Complete Blood Count (CBC) | ≥10 years | CPT, restricted to outpatient claim types, which excludes ED-based claims |
| Microalbumin | ≥10 years | CPT |
| Ophthalmology | ≥10 years | CPT |

Claims are deduplicated by date — multiple lines for the same screening on the
same date count once. The count of distinct screening dates over 2021–2023 is
collapsed into 0, 1, 2, or ≥3, and the categories rather than the raw count are
what is reported.

Reported once for the combined 2021–2023 period; not broken out by calendar
year. Also reported for the SCA subpopulation and for the any-coverage
population.

---

## Medications

| Medication | Age eligibility | Metrics |
|---|---|---|
| Antibiotic prophylaxis | 2 months – 5 years | Any fill; sustained fill as a 3-year average and per calendar year; average days supplied/year; median total days supplied |
| Hydroxyurea | ≥9 months | Same as above |
| Adakveo (crizanlizumab) | ≥16 years | Any fill |
| Endari (L-glutamine) | ≥5 years | Any fill |
| Oxbryta (voxelotor) | ≥4 years | Any fill |

Fills are identified by NDC. Metrics reflect prescription *fills*; adherence is
not measurable in these data. Oxbryta was withdrawn from the U.S. market in
September 2024; data reflect 2021–2023 fills only.

**Overlapping fills.** An early refill before the prior supply runs out would
overstate days on hand if each fill's supply were counted independently.
Overlapping days are counted once. The per-year metric applies the same
correction within each year, splitting a fill that spans December 31 so each
year is credited only with its own days.

**Sustained fill** is ≥300 days of supply, reported two ways:

- **3-year average** — total non-overlapping supply days ÷ 3, thresholded at 300
- **Per calendar year** — non-overlapping days within one year, thresholded at
  300 within that year

Age eligibility is derived per calendar year from date of birth; see
[Cohort and Populations](02-cohort-and-populations.md) > *Age*.

Also reported for the SCA subpopulation and the any-coverage population.

---

## Outpatient visits and provider access

**Visits** are identified by place of service, category of service, and revenue
codes. Included: offices, labs, clinics, outpatient hospitals. Excluded: ED
visits, inpatient admissions, pharmacy records. Claims are deduplicated by date
of service, so visits to different providers on the same day may be missed.

Reported: total visit count, combined and per year; any visit, combined and per
year; and a categorical count (1, 2, 3+) over 2021–2023. Reported for both
coverage populations and stratified by age category.

**Provider access.** Practitioners are identified by NPI and categorized as
hematologist or general practitioner by specialty code. **SCD-experienced** means
a practitioner who saw ≥20 unique cohort members over the three years —
practitioners in areas with few SCD patients may be missed by this definition.

Each claim carries a referring/prescribing NPI and a rendering/operating NPI;
either qualifying is enough for the visit to count. Four person-level flags:

- Any hematologist visit
- Any experienced-provider visit (hematologist or GP, regardless of SCD
  experience)
- Any SCD-experienced hematologist visit
- Any SCD-experienced general practitioner visit

---

## Emergency department

HCAI reports inpatient admissions separately from ED encounters, so an ED record
already represents a visit that did not result in admission — a
treat-and-release visit — rather than something derived from place-of-service or
revenue-code logic.

Visits are counted per calendar year and summed across 2021–2023, and collapsed
into utilization categories both per year and combined:

| Category | Visits |
|---|---|
| 0 | 0 |
| 1–3 | 1–3 |
| 4–9 | 4–9 |
| 10+ | 10 or more |

Cohort members with no ED record are counted as 0, not excluded. Visit rates are
per 1,000 using the full cohort as the denominator. Also reported by age
category.

**Complications** are identified by ICD-10-CM diagnosis code on the visit
record:

acute chest syndrome · stroke · severe infection/sepsis · splenic sequestration ·
aplastic crisis · acute anemia/hemolytic crisis · chronic kidney disease ·
vaso-occlusive episode (pain crisis) · venous thromboembolism · avascular
necrosis · pulmonary hypertension · priapism (males only)

A visit is flagged where a matching code appears in the principal diagnosis or
any secondary diagnosis field. "Any complication" is set where one or more is
present.

Two distinct quantities are reported and should not be interchanged: the **number
of people** who ever had a complication coded, and the **number of visits** with
one.

---

## Inpatient admissions

Admissions are counted per year and summed across 2021–2023, using the same four
utilization categories as the ED section, with the full cohort as denominator
regardless of whether a person has any admission. Also reported by age.

**Complications** use the same code set as the ED section. An admission is
flagged where the code appears as the principal diagnosis or any of up to 24
secondary diagnoses. A person is flagged for *any* complication where at least
one appears on at least one admission.

As with the ED section, the number of people and the number of admissions are
separate quantities.

**Length of stay** is averaged across all of a person's admissions in 2021–2023
— one value per person over the period, not per admission — and is defined only
for people with a recorded admission.

**Admissions originating in the ED** are identified by admission source code,
reported as a count per person and as a share of total admissions.

---

## Revisits

A revisit is any ED encounter or inpatient admission beginning within 1–7 or
1–30 days of discharge from a prior ED visit or inpatient stay. Four transition
types: ED to ED, ED to hospital, hospital to ED, hospital to hospital.

**The 7-day group is a subset of the 30-day group** — both are measured from the
same gap and differ only in cutoff. Do not add them.

Reported: whether a person had any revisit within 7 days, and within 30 days,
among people with at least one ED or hospital encounter in 2021–2023; plus
revisit counts by transition type for each window.

---

## ED and inpatient reliance

- **Emergency Department Reliance (EDR)** = ED visits ÷ (ED + ambulatory +
  inpatient)
- **Inpatient Reliance Ratio (IRR)** = inpatient ÷ (ED + ambulatory + inpatient)

Both describe how a person's care across the three settings breaks down over
2021–2023 combined.

**High EDR is EDR ≥ 0.33 at the individual level.** The ratio is rounded to two
decimal places before the comparison, so values landing exactly on 0.33 are
common rather than rare.

**Reliance is undefined for a person with no encounters** in any setting — not
zero. Those people carry a missing ratio and leave the denominator rather than
counting as not-high-reliance.

**Medi-Cal restriction.** Both ratios need the ambulatory count, which is
observable only for enrolled people. People with no enrollment are excluded
before calculation: their ambulatory count is unknowable, not zero.

**County assignment** is county of residence, not the county where care was
delivered. A person living in one county and treated in another is grouped under
residence. County figures therefore describe a county's resident population, not
care delivered within it.

**The individual threshold must not be applied to a county figure.** County
ratios are computed on summed visit counts, so they are weighted by visit volume
— a few high utilisers can carry a county past 0.33. A county EDR is not the
share of its residents with high reliance.
