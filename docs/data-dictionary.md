# Data Dictionary

What each analytic dataset in this pipeline contains, so that a request for a
custom summary can be framed in terms of variables that actually exist.

The pipeline produces twelve analytic datasets. Every
dataset is keyed on `new_unique_id` and carries the same set of demographic and
geographic variables, so summaries can be cut by any of those without a special
request. The per-dataset sections below list only what that script adds.

Nine of the twelve have their variables itemised here. `_1_cohort`,
`_2_demographics` and `_8a_Deaths_2` are listed in
[`datasets.csv`](datasets.csv) but have no variable rows yet — a request against
those is still possible, it just cannot be scoped from this page alone.

## Before you read the tables

**These datasets are not public.** They contain person-level records derived
from restricted data sources and cannot be released. What can be produced from
them is *aggregate summaries*. This dictionary exists so that a request can name
the variables and stratifications it needs, rather than describing a table in
prose and waiting to find out whether it is possible.

**Small cells are suppressed.** Counts below 11 are not released, and neither
are percentages or totals from which a suppressed count could be recovered. A
request crossing several variables at once will often fail this test even when
each variable is available on its own the more strata, the thinner the cells.

**Check the Years column.** Some variables exist for each calendar year and for
the pooled 2021-2023 period; others exist only for the pooled period, because
the underlying flag was built once across all three years. Where a note says *no
further year stratifications available*, a per-year breakdown of that variable
cannot be produced without re-running the pipeline.

## Unit of observation
 Not every dataset is one row per person.

| Dataset | Unit of observation | Period |
|---|---|---|
| `_3_ed_access_to_care` | One row per person | 2021-2023 |
| `_4_hospital_access_to_care` | One row per person | 2021-2023 |
| `_5_ed_hospital_revisits` | One row per person | 2021-2023 |
| `_6_enrollment_access_to_care` | One row per person | 2021-2023 |
| `_7_screenings` | One row per person | 2021-2023 |
| `_8_birth_death` | **One row per county per year** | 2014-2023 |
| `_9_maternal_health` | **One row per delivery admission**; people with no delivery keep a single row | 2019-2023 |
| `_10_access_to_care_ambulatory` | One row per person | 2021-2023 |
| `_11_medications` | One row per person | 2021-2023 |


## Counts versus indicators

Several datasets carry both a count and a yes/no indicator for the same
underlying concept, and the distinction drives whether a result is a percentage
of people or a rate per visit:

- `ed_flag_<condition>` / `hosp_flag_<condition>` are **counts**  the number of
  ED visits or inpatient admissions with that condition coded.
- `ed_any_<condition>` / `hosp_any_<condition>` are **0/1 indicators** whether
  the person ever had that condition coded.

So "what share of people had a stroke coded at an ED visit" uses `ed_any_stroke`,
while "how many ED visits had a stroke coded" uses `ed_flag_stroke`. Both are
kept because both are reported.

## Stratifications available on every person-level dataset

Any of these can be crossed with the metrics below, subject to cell suppression:

- **Sex** `sex`
- **Age** `age` (continuous), `age_cat_a` (under 21 / 21 and over — a
  21-year-old falls in the older group), `age_cat_b` (10-year bands),
  `age_cat_c` (10-year bands with finer detail for children)
- **Race and ethnicity** `best_race`, `best_eth`
- **Genotype** `best_dx`; sickle cell anemia is `best_dx in ("SS","SB0")`
- **County** `main_county_nm`, or per-year `countynm2021/2022/2023`
- **Social Vulnerability Index** `SVI_main`, or per-year `SVI2021/2022/2023`
- **Medi-Cal coverage** `any_mc_elig`, `full_mc_elig`, and their per-year
  forms, from `_6_enrollment_access_to_care`

Age categories are fixed at end of 2023, or at date of death for people who
died during the period. They do not vary by year.

## Shared variables

Present on every person-level dataset.


| Variable | Definition | Years | Notes |
|---|---|---|---|
| `age` | Continuous age variable - stops at age of death if individual has passed away or at end of 2023 |  |  |
| `age_cat_a` | Binary stratification of age <= 21 years old and  >21 years  at the end of 2023 or time of death |  |  |
| `age_cat_b` | 10 year categorical age groupings at the end of 2023 or time of death |  |  |
| `age_cat_c` | 10 year categorical age groupings with further granularity in children (0-2, 3-5, 6-10) at the end of 2023 or time of death |  |  |
| `best_dx` | Best category (genotype) of SCD diagnosis based on linked administrative data |  |  |
| `best_eth` | Best ethnic category based on linked administrative data |  |  |
| `best_race` | Best racial category based on linked administrative data |  |  |
| `county_2021` | County of residence in 2021 - county numeric code | 2021 |  |
| `county_2022` | County of residence in 2022 - county numeric code | 2022 |  |
| `county_2023` | County of residence in 2023 - county numeric code | 2023 |  |
| `countynm2021` | County of residence in 2021 - county name - character | 2021 |  |
| `countynm2022` | County of residence in 2022 - county name - character | 2022 |  |
| `countynm2023` | County of residence in 2023 - county name - character | 2023 |  |
| `in_clinical` | Indicator variable of which individuals have data from SCD clinics |  |  |
| `in_nbs` | Indicator variable of which individuals have data from new born screening |  |  |
| `main_county` | The most recent county of residence - county numeric code | 2021-2023 |  |
| `main_county_nm` | The most recent county of residence - county name - character | 2021-2023 |  |
| `moved_counties` | Indicator variable of which individuals had more than one county of residence over the 3 years | 2021-2023 |  |
| `moved_zips` | Indicator variable of which individuals had more than one zip code of residence over the 3 years | 2021-2023 |  |
| `new_unique_id` | ID variable which identifies unique individuals. Use for linking across data sets |  |  |
| `prob_case` | Indicator variable of which individuals are a probable case based on admis tritave data linkage |  |  |
| `Sex` | Sex assigned at birth |  |  |
| `SVI_main` | Social Vulnerability Index quartile | 2021-2023 |  |
| `SVI2021` | Social Vulnerability Index quartile 2021 | 2021 |  |
| `SVI2022` | Social Vulnerability Index quartile 2022 | 2022 |  |
| `SVI2023` | Social Vulnerability Index quartile 2023 | 2023 |  |
| `Zip2021` | Zip code of residence in 2021 | 2021 |  |
| `Zip2022` | Zip code of residence in 2022 | 2022 |  |
| `Zip2023` | Zip code of residence in 2023 | 2023 |  |


## `_3_ed_access_to_care`

Emergency department use and SCD complications coded at ED visits. See [Emergency department](03-metric-definitions.md#emergency-department).
| Variable | Definition | Years | Notes |
|---|---|---|---|
| `ed_flag_a_anemia` | **Count** of ED visits with an ICD code for acute anemia/Hemolytic Crisis | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_a_anemia` for the person-level indicator |
| `ed_any_a_anemia` | **Indicator** (0/1) for whether the person ever had an ICD code for acute anemia/Hemolytic Crisis at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_ACS` | **Count** of ED visits with an ICD code for acute chest syndrome | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_ACS` for the person-level indicator |
| `ed_any_ACS` | **Indicator** (0/1) for whether the person ever had an ICD code for acute chest syndrome at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_any_comp` | **Count** of ED visits with an ICD code for any SCD complication | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_comp` for the person-level indicator |
| `ed_any_comp` | **Indicator** (0/1) for whether the person ever had an ICD code for any SCD complication at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_apl_crisis` | **Count** of ED visits with an ICD code for aplastic Crisis | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_apl_crisis` for the person-level indicator |
| `ed_any_apl_crisis` | **Indicator** (0/1) for whether the person ever had an ICD code for aplastic Crisis at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_Ava_nec` | **Count** of ED visits with an ICD code for avascular necrosis | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_Ava_nec` for the person-level indicator |
| `ed_any_Ava_nec` | **Indicator** (0/1) for whether the person ever had an ICD code for avascular necrosis at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_CKD` | **Count** of ED visits with an ICD code for chronic kidney disease | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_CKD` for the person-level indicator |
| `ed_any_CKD` | **Indicator** (0/1) for whether the person ever had an ICD code for chronic kidney disease at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_inf_sep` | **Count** of ED visits with an ICD code for severe infection/sepsis | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_inf_sep` for the person-level indicator |
| `ed_any_inf_sep` | **Indicator** (0/1) for whether the person ever had an ICD code for severe infection/sepsis at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_priapism` | **Count** of ED visits with an ICD code for priapism | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_priapism` for the person-level indicator |
| `ed_any_priapism` | **Indicator** (0/1) for whether the person ever had an ICD code for priapism at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_pulm_hyp` | **Count** of ED visits with an ICD code for pulmonary hypertension | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_pulm_hyp` for the person-level indicator |
| `ed_any_pulm_hyp` | **Indicator** (0/1) for whether the person ever had an ICD code for pulmonary hypertension at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_sple_seq` | **Count** of ED visits with an ICD code for splenic sequestration | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_sple_seq` for the person-level indicator |
| `ed_any_sple_seq` | **Indicator** (0/1) for whether the person ever had an ICD code for splenic sequestration at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_stroke` | **Count** of ED visits with an ICD code for stroke | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_stroke` for the person-level indicator |
| `ed_any_stroke` | **Indicator** (0/1) for whether the person ever had an ICD code for stroke at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_VOE` | **Count** of ED visits with an ICD code for Vaso-occlusive Episode or Pain Crisis | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_VOE` for the person-level indicator |
| `ed_any_VOE` | **Indicator** (0/1) for whether the person ever had an ICD code for Vaso-occlusive Episode or Pain Crisis at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_flag_VTE` | **Count** of ED visits with an ICD code for venous thromboembolism | 2021-2023 | Visit-level count, not a 0/1 flag; see `ed_any_VTE` for the person-level indicator |
| `ed_any_VTE` | **Indicator** (0/1) for whether the person ever had an ICD code for venous thromboembolism at an ED visit | 2021-2023 | Missing for people with no ED visit at all |
| `ed_use_21` | Indicator variable if individual had an ED T/R visit during 2021 | 2021 |  |
| `ed_use_22` | Indicator variable if individual had an ED T/R visit during 2022 | 2022 |  |
| `ed_use_23` | Indicator variable if individual had an ED T/R visit during 2023 | 2023 |  |
| `ed_use_total` | Indicator variable if individual had an ED T/R visit during 2021-2023 | 2021-2023 |  |
| `ed_visit_count_21` | Number of ED T/R visits and individual had during 2021 | 2021 |  |
| `ed_visit_count_22` | Number of ED T/R visits and individual had during 2022 | 2022 |  |
| `ed_visit_count_23` | Number of ED T/R visits and individual had during 2023 | 2023 |  |
| `ed_visit_count_total` | Number of ED T/R visits and individual had during 2021-2023 | 2021-2023 |  |

## `_4_hospital_access_to_care`

Inpatient admissions, length of stay, and SCD complications coded at admissions. See [Inpatient admissions](03-metric-definitions.md#inpatient-admissions).
| Variable | Definition | Years | Notes |
|---|---|---|---|
| `hosp_flag_a_anemia` | **Count** of inpatient admissions with an ICD code for acute anemia/Hemolytic Crisis | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_a_anemia` for the person-level indicator |
| `hosp_any_a_anemia` | **Indicator** (0/1) for whether the person ever had an ICD code for acute anemia/Hemolytic Crisis at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_ACS` | **Count** of inpatient admissions with an ICD code for acute chest syndrome | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_ACS` for the person-level indicator |
| `hosp_any_ACS` | **Indicator** (0/1) for whether the person ever had an ICD code for acute chest syndrome at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_any_comp` | **Count** of inpatient admissions with an ICD code for any SCD complication | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_comp` for the person-level indicator |
| `hosp_any_comp` | **Indicator** (0/1) for whether the person ever had an ICD code for any SCD complication at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_apl_crisis` | **Count** of inpatient admissions with an ICD code for aplastic Crisis | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_apl_crisis` for the person-level indicator |
| `hosp_any_apl_crisis` | **Indicator** (0/1) for whether the person ever had an ICD code for aplastic Crisis at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_Ava_nec` | **Count** of inpatient admissions with an ICD code for avascular necrosis | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_Ava_nec` for the person-level indicator |
| `hosp_any_Ava_nec` | **Indicator** (0/1) for whether the person ever had an ICD code for avascular necrosis at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_CKD` | **Count** of inpatient admissions with an ICD code for chronic kidney disease | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_CKD` for the person-level indicator |
| `hosp_any_CKD` | **Indicator** (0/1) for whether the person ever had an ICD code for chronic kidney disease at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_inf_sep` | **Count** of inpatient admissions with an ICD code for severe infection/sepsis | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_inf_sep` for the person-level indicator |
| `hosp_any_inf_sep` | **Indicator** (0/1) for whether the person ever had an ICD code for severe infection/sepsis at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_priapism` | **Count** of inpatient admissions with an ICD code for priapism | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_priapism` for the person-level indicator |
| `hosp_any_priapism` | **Indicator** (0/1) for whether the person ever had an ICD code for priapism at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_pulm_hyp` | **Count** of inpatient admissions with an ICD code for pulmonary hypertension | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_pulm_hyp` for the person-level indicator |
| `hosp_any_pulm_hyp` | **Indicator** (0/1) for whether the person ever had an ICD code for pulmonary hypertension at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_sple_seq` | **Count** of inpatient admissions with an ICD code for splenic sequestration | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_sple_seq` for the person-level indicator |
| `hosp_any_sple_seq` | **Indicator** (0/1) for whether the person ever had an ICD code for splenic sequestration at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_stroke` | **Count** of inpatient admissions with an ICD code for stroke | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_stroke` for the person-level indicator |
| `hosp_any_stroke` | **Indicator** (0/1) for whether the person ever had an ICD code for stroke at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_VOE` | **Count** of inpatient admissions with an ICD code for Vaso-occlusive Episode or Pain Crisis | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_VOE` for the person-level indicator |
| `hosp_any_VOE` | **Indicator** (0/1) for whether the person ever had an ICD code for Vaso-occlusive Episode or Pain Crisis at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_flag_VTE` | **Count** of inpatient admissions with an ICD code for venous thromboembolism | 2021-2023 | Visit-level count, not a 0/1 flag; see `hosp_any_VTE` for the person-level indicator |
| `hosp_any_VTE` | **Indicator** (0/1) for whether the person ever had an ICD code for venous thromboembolism at an inpatient admission | 2021-2023 | Missing for people with no admission at all |
| `hosp_use_21` | Indicator variable if individual had an hospital inpatient visit during 2021 | 2021 |  |
| `hosp_use_22` | Indicator variable if individual had an hospital inpatient visit during 2022 | 2022 |  |
| `hosp_use_23` | Indicator variable if individual had an hospital inpatient visit during 2023 | 2023 |  |
| `hosp_use_total` | Indicator variable if individual had an hospital inpatient visit during 2021-2023 | 2021-2023 |  |
| `hosp_visit_count_21` | Number of hospital inpatient visits and individual had during 2021 | 2021 |  |
| `hosp_visit_count_22` | Number of hospital inpatient visits and individual had during 2022 | 2022 |  |
| `hosp_visit_count_23` | Number of hospital inpatient visits and individual had during 2023 | 2023 |  |
| `hosp_visit_count_total` | Number of hospital inpatient visits and individual had during 2021-2023 | 2021-2023 |  |
| `los_avg` | Average length of hospital inpatient stay in days per individual during 2021-2023 | 2021-2023 | no further year stratifications available |
| `tot_fromED` | Number of hospital inpatient visits that started at ED visits per person during 2021-2023 | 2021-2023 | no further year stratifications available |

## `_5_ed_hospital_revisits`

Return visits within 7 and 30 days, across four transition types. See [Revisits](03-metric-definitions.md#revisits).
| Variable | Definition | Years | Notes |
|---|---|---|---|
| `ED_ED_30days` | Number of ED to ED revisits each individual had within 30 days. | 2021-2023 | no further year stratifications available |
| `ED_ED_7days` | Number of ED to ED revisits each individual had within 7 days. | 2021-2023 | no further year stratifications available |
| `ED_PD_30days` | Number of ED to hospital revisits each individual had within 30 days. | 2021-2023 | no further year stratifications available |
| `ED_PD_7days` | Number of ED to hospital revisits each individual had within 7 days. | 2021-2023 | no further year stratifications available |
| `PD_ED_30days` | Number of hospital to ED revisits each individual had within 30 days. | 2021-2023 | no further year stratifications available |
| `PD_ED_7days` | Number of hospital to ED revisits each individual had within 30 days. | 2021-2023 | no further year stratifications available |
| `PD_PD_30days` | Number of hospital to hospital revisits each individual had within 30 days. | 2021-2023 | no further year stratifications available |
| `PD_PD_7days` | Number of hospital to hospital revisits each individual had within 30 days. | 2021-2023 | no further year stratifications available |
| `revisit_30day_flag` | indicator variable if the individual had any revisits within 30 days of previous encounter | 2021-2023 | no further year stratifications available |
| `revisit_7day_flag` | indicator variable if the individual had any revisits within 7 days of previous encounter | 2021-2023 | no further year stratifications available |

## `_6_enrollment_access_to_care`

Medi-Cal enrollment continuity, plus CCS and GHPP program participation. See [Medi-Cal enrollment](03-metric-definitions.md#medi-cal-enrollment-and-program-coverage).
| Variable | Definition | Years | Notes |
|---|---|---|---|
| `any_mc_elig` | Indicator variable if the individual had MediCal coverage any month in the 3 year period | 2021-2023 |  |
| `any_mc_elig_21` | Indicator variable if the individual had MediCal coverage any month in the year 2021 | 2021 |  |
| `any_mc_elig_22` | Indicator variable if the individual had MediCal coverage any month in the year 2022 | 2022 |  |
| `any_mc_elig_23` | Indicator variable if the individual had MediCal coverage any month in the year 2023 | 2023 |  |
| `CCS_enrolled` | Indicator variable for if children (<=21) were enrolled in CCS at any point between 2021 and 2023 | 2021-2023 | no further year stratifications available |
| `full_mc_elig` | Indicator variable if the individual had MediCal coverage all 36 months of 2021-2023 | 2021-2023 |  |
| `full_mc_elig_21` | Indicator variable if the individual had MediCal coverage all 12 months of 2021 | 2021 |  |
| `full_mc_elig_22` | Indicator variable if the individual had MediCal coverage all 12 months of 2022 | 2022 |  |
| `full_mc_elig_23` | Indicator variable if the individual had MediCal coverage all 12 months of 2023 | 2023 |  |
| `GHPP_enrolled` | Indicator variable for if adults (>21) were enrolled in GHPP at any point between 2021 and 2023 | 2021-2023 | no further year stratifications available |
| `months_elig_21` | Number of months of coverage for the year 2021 | 2021 |  |
| `months_elig_22` | Number of months of coverage for the year 2022 | 2022 |  |
| `months_elig_23` | Number of months of coverage for the year 2023 | 2023 |  |

## `_7_screenings`

Preventive screening counts: transcranial Doppler, CBC, microalbumin, ophthalmology. See [Preventive screenings](03-metric-definitions.md#preventive-screenings).
| Variable | Definition | Years | Notes |
|---|---|---|---|
| `cbc_count` | Number of complete blood count blood tests in MediCal outpatient data between 2021and 2023 (>=10 y/o) | 2021-2023 | no further year stratifications available |
| `cbc_screen` | Categorical variable 0,1,2,3+ of how many complete blood count blood tests in MediCal outpatient between 2021-2023 (>=10 y/o) | 2021-2023 | no further year stratifications available |
| `microal_count` | Number of microalbumin blood tests in MediCal data between 2021and 2023 (>=10y/o) | 2021-2023 | no further year stratifications available |
| `microal_screen` | Categorical variable 0,1,2,3+ of how many microalbumin blood tests in MediCal between 2021-2023 (>=10y/o) | 2021-2023 | no further year stratifications available |
| `opth_count` | Number of ophthalmology screenings in MediCal data between 2021 and 2023 (>=10y/o) | 2021-2023 | no further year stratifications available |
| `opth_screen` | Categorical variable 0,1,2,3+ of how many ophthalmology screenings in MediCal between 2021-2023 (>=10y/o) | 2021-2023 | no further year stratifications available |
| `tcd_count` | Number of transcranial doppler scans in MediCal data between 2021and 2023 (2-16 y/o) | 2021-2023 | no further year stratifications available |
| `tcd_screen` | Categorical variable 0,1,2,3+ of how many transcranial doppler scans in MediCal between 2021-2023 (2-16 y/o) | 2021-2023 | no further year stratifications available |

## `_8_birth_death`

County-year counts of births, deaths, population, and age at death. See [Mortality](03-metric-definitions.md#mortality).
| Variable | Definition | Years | Notes |
|---|---|---|---|
| `county_name` | Name of county in California | 2014-2023 | County Level Data |
| `dt_age_cat_1` | Number of deaths aged 0-10 in county in associated year | 2014-2023 | County Level Data |
| `dt_age_cat_2` | Number of deaths aged 11-20 in county in associated year | 2014-2023 | County Level Data |
| `dt_age_cat_3` | Number of deaths aged 21-30 in county in associated year | 2014-2023 | County Level Data |
| `dt_age_cat_4` | Number of deaths aged 31-40 in county in associated year | 2014-2023 | County Level Data |
| `dt_age_cat_5` | Number of deaths aged 41-50 in county in associated year | 2014-2023 | County Level Data |
| `dt_age_cat_6` | Number of deaths aged 51-60 in county in associated year | 2014-2023 | County Level Data |
| `dt_age_cat_7` | Number of deaths aged 61+ in county in associated year | 2014-2023 | County Level Data |
| `f_med_dt_age` | Median age of death in females of county in associated year | 2014-2023 | County Level Data |
| `female_birth` | Number of females with SCD born in county in associated year | 2014-2023 | County Level Data |
| `female_death` | Number of females with SCD who died in county in associated year | 2014-2023 | County Level Data |
| `female_pop` | Total number of females with SCD in county in associated year | 2014-2023 | County Level Data |
| `m_med_dt_age` | Median age of death in males of county in associated year | 2014-2023 | County Level Data |
| `male_birth` | Number of males with SCD born in county in associated year | 2014-2023 | County Level Data |
| `male_death` | Number of males with SCD who died in county in associated year | 2014-2023 | County Level Data |
| `male_pop` | Total number of males with SCD in county in associated year | 2014-2023 | County Level Data |
| `med_dt_age` | Median age at death in SCD population in county in associated year | 2014-2023 | County Level Data |
| `total_birth` | Total number of babies with SCD born in county in associated year | 2014-2023 | County Level Data |
| `total_death` | Total number of people with SCD who died in county in associated year | 2014-2023 | County Level Data |
| `total_pop` | Total number of people with SCD in county in associated year | 2014-2023 | County Level Data |
| `year` | Associated year | 2014-2023 | County Level Data |

## `_9_maternal_health`

Delivery admissions and Severe Maternal Morbidity indicators. See [Maternal morbidity](03-metric-definitions.md#maternal-morbidity).
| Variable | Definition | Years | Notes |
|---|---|---|---|
| `any_SMM` | Indicator variable if any severe maternal morbidity was present during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `delivery_adm` | Flag to indicate if a row is associated with an admittance for delivery | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `delivery_county` | County of residence during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `delivery_order` | Order of delivery admittance (multiple admittances) | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `delivery_yr` | Year of delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `mat_age` | Maternal age at delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `mat_age_cat` | Categorical age at delivery admittance (range 12-55 y/o) | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_AFE` | Indicator variable if amniotic fluid embolism during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_AMI` | Indicator variable if acute myocardial infarction during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_aneurysm` | Indicator variable if aneurysm during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_anth` | Indicator variable if severe anesthesia complications during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_ARDS` | Indicator variable if acute respiratory distress syndrome during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_ARF` | Indicator variable if acute renal failure during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_bld_trnsf` | Indicator variable if blood transfusion during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_card_rhy` | Indicator variable if conversion of cardiac rhythm during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_DIC` | Indicator variable if disseminated intravascular coagulation during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_eclmp` | Indicator variable if eclampsia during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_emb` | Indicator variable if air and thrombotic embolism during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_ht_atk` | Indicator variable if heart failure or arrest during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_hyst` | Indicator variable if hysterectomy during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_Mat_SC` | Indicator variable if sickle cell crisis during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_PC` | Indicator variable if puerperal cerebrovascular during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_PE` | Indicator variable if pulmonary edema during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_sepsis` | Indicator variable if sepsis during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_shock` | Indicator variable if shock during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_tem_trach` | Indicator variable if temporary tracheostomy during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_vent` | Indicator variable if ventilation during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `SMM_vfib` | Indicator variable if cardiac arrest or vfib during delivery admittance | 2019-2023 | Delivery Level Data (some women have multiple rows) |
| `tot_deliv_adm` | Total number of delivery admittances a person has had | 2019-2023 | Delivery Level Data (some women have multiple rows) |

## `_10_access_to_care_ambulatory`

Outpatient visits and contact with SCD-experienced providers. See [Outpatient visits and provider access](03-metric-definitions.md#outpatient-visits-and-provider-access).
| Variable | Definition | Years | Notes |
|---|---|---|---|
| `amb_count_21` | Count of number of ambulatory visits in 2021 | 2021 |  |
| `amb_count_22` | Count of number of ambulatory visits in 2022 | 2022 |  |
| `amb_count_23` | Count of number of ambulatory visits in 2023 | 2023 |  |
| `amb_vis_cat` | Categorical variable 0,1,2,3+ of how many outpatient claims MediCal between 2021-2023 | 2021-2023 | no further year stratifications available |
| `any_amb_vis` | Indicator variable if if any ambulatory visits 2021-2023 | 2021-2023 | no further year stratifications available |
| `any_amb_vis_21` | Indicator variable if if any ambulatory visits 2021 | 2021 |  |
| `any_amb_vis_22` | Indicator variable if if any ambulatory visits 2022 | 2022 |  |
| `any_amb_vis_23` | Indicator variable if if any ambulatory visits 2023 | 2023 |  |
| `had_hema_care` | Indicator variable if person had a visit with a hematologist | 2021-2023 | no further year stratifications available |
| `had_SCD_exp_care` | Indicator variable if person had a visit with an experienced provider (any) | 2021-2023 | no further year stratifications available |
| `had_SCD_gp_care` | Indicator variable if person had a visit with an experienced GP | 2021-2023 | no further year stratifications available |
| `had_SCD_hema_care` | Indicator variable if person had a visit with an experienced hematologist | 2021-2023 | no further year stratifications available |
| `hema_visit` | Count of how many hematologist visits an individual had 2021-2023 | 2021-2023 |  |
| `SCD_exp_visit` | Count of how many SCD experienced visits an individual had 2021-2023 | 2021-2023 | no further year stratifications available |
| `scd_gp_visit` | Count of how many SCD experienced GP visits an individual had 2021-2023 | 2021-2023 | no further year stratifications available |
| `scd_hema_visit` | Count of how many SCD experienced hematologist visits an individual had 2021-2023 | 2021-2023 | no further year stratifications available |
| `total_amb_count` | Count of number of ambulatory visits 2021-2023 | 2021-2023 | no further year stratifications available |

## `_11_medications`

Prescription fills, supply days, and sustained-use flags. See [Medications](03-metric-definitions.md#medications).
| Variable | Definition | Years | Notes |
|---|---|---|---|
| `AB_300_fill` | Indicator variable if a person had an average of at least 300 fill days of antibiotic per year | 2021-2023 | no further year stratifications available |
| `AB_900_fill` | Indicator variable if a person had over 900 total fill days of antibiotic between 2021-2023 | 2021-2023 | no further year stratifications available |
| `AB_total_days` | Count of the total number of antibiotic fill days 2021-2023 | 2021-2023 | no further year stratifications available |
| `any_presc_Adakveo` | Indicator variable if person had any Adakveo fills 2021-2023 | 2021-2023 | no further year stratifications available |
| `any_presc_antibiotic` | Indicator variable if person had any antibiotic fills 2021-2023 | 2021-2023 | no further year stratifications available |
| `any_presc_Endari` | Indicator variable if person had any Endari fills 2021-2023 | 2021-2023 | no further year stratifications available |
| `any_presc_HU` | Indicator variable if person had any HU fills 2021-2023 | 2021-2023 | no further year stratifications available |
| `any_presc_Oxbryta` | Indicator variable if person had any Oxbryta fills 2021-2023 | 2021-2023 | no further year stratifications available |
| `ave_AB_fill` | Average number of antibiotic fill days per year | 2021-2023 | no further year stratifications available |
| `ave_HU_fill` | Average number of HU fill days per year | 2021-2023 | no further year stratifications available |
| `HU_300_fill` | Indicator variable if a person had an average of at least 300 fill days of HU per year | 2021-2023 | no further year stratifications available |
| `HU_900_fill` | Indicator variable if a person had over 900 total fill days of HU between 2021-2023 | 2021-2023 | no further year stratifications available |
| `HU_total_days` | Count of the total number of HU fill days 2021-2023 | 2021-2023 | no further year stratifications available |
| `presc_Adakveo_21` | Indicator variable if Adakveo was ever prescribed in | 2021 |  |
| `presc_Adakveo_22` | Indicator variable if Adakveo was ever prescribed in | 2022 |  |
| `presc_Adakveo_23` | Indicator variable if Adakveo was ever prescribed in | 2023 |  |
| `presc_antibiotic_21` | Indicator variable if antibiotics were ever prescribed in | 2021 |  |
| `presc_antibiotic_22` | Indicator variable if antibiotics were ever prescribed in | 2022 |  |
| `presc_antibiotic_23` | Indicator variable if antibiotics were ever prescribed in | 2023 |  |
| `presc_Endari_21` | Indicator variable if Endari was ever prescribed in | 2021 |  |
| `presc_Endari_22` | Indicator variable if Endari was ever prescribed in | 2022 |  |
| `presc_Endari_23` | Indicator variable if Endari was ever prescribed in | 2023 |  |
| `presc_HU_21` | Indicator variable if HU was ever prescribed in | 2021 |  |
| `presc_HU_22` | Indicator variable if HU was ever prescribed in | 2022 |  |
| `presc_HU_23` | Indicator variable if HU was ever prescribed in | 2023 |  |
| `presc_Oxbryta_21` | Indicator variable if Oxbryta was ever prescribed in | 2021 |  |
| `presc_Oxbryta_22` | Indicator variable if Oxbryta was ever prescribed in | 2022 |  |
| `presc_Oxbryta_23` | Indicator variable if Oxbryta was ever prescribed in | 2023 |  |
| `elig_ab_any` | Indicator (0/1) for whether the person fell inside the antibiotic prophylaxis age window (2 months through 5 years) at any point during 2021-2023 | 2021-2023 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_ab_21` | Indicator (0/1) for whether the person fell inside the antibiotic prophylaxis age window (2 months through 5 years) at any point during 2021 | 2021 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_ab_22` | Indicator (0/1) for whether the person fell inside the antibiotic prophylaxis age window (2 months through 5 years) at any point during 2022 | 2022 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_ab_23` | Indicator (0/1) for whether the person fell inside the antibiotic prophylaxis age window (2 months through 5 years) at any point during 2023 | 2023 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_hu_any` | Indicator (0/1) for whether the person fell inside the hydroxyurea age window (9 months and older) at any point during 2021-2023 | 2021-2023 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_hu_21` | Indicator (0/1) for whether the person fell inside the hydroxyurea age window (9 months and older) at any point during 2021 | 2021 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_hu_22` | Indicator (0/1) for whether the person fell inside the hydroxyurea age window (9 months and older) at any point during 2022 | 2022 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_hu_23` | Indicator (0/1) for whether the person fell inside the hydroxyurea age window (9 months and older) at any point during 2023 | 2023 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_endari_any` | Indicator (0/1) for whether the person fell inside the Endari (L-glutamine) age window (5 years and older) at any point during 2021-2023 | 2021-2023 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_endari_21` | Indicator (0/1) for whether the person fell inside the Endari (L-glutamine) age window (5 years and older) at any point during 2021 | 2021 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_endari_22` | Indicator (0/1) for whether the person fell inside the Endari (L-glutamine) age window (5 years and older) at any point during 2022 | 2022 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_endari_23` | Indicator (0/1) for whether the person fell inside the Endari (L-glutamine) age window (5 years and older) at any point during 2023 | 2023 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_adakveo_any` | Indicator (0/1) for whether the person fell inside the Adakveo (crizanlizumab) age window (16 years and older) at any point during 2021-2023 | 2021-2023 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_adakveo_21` | Indicator (0/1) for whether the person fell inside the Adakveo (crizanlizumab) age window (16 years and older) at any point during 2021 | 2021 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_adakveo_22` | Indicator (0/1) for whether the person fell inside the Adakveo (crizanlizumab) age window (16 years and older) at any point during 2022 | 2022 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_adakveo_23` | Indicator (0/1) for whether the person fell inside the Adakveo (crizanlizumab) age window (16 years and older) at any point during 2023 | 2023 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_oxbryta_any` | Indicator (0/1) for whether the person fell inside the Oxbryta (voxelotor) age window (4 years and older) at any point during 2021-2023 | 2021-2023 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_oxbryta_21` | Indicator (0/1) for whether the person fell inside the Oxbryta (voxelotor) age window (4 years and older) at any point during 2021 | 2021 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_oxbryta_22` | Indicator (0/1) for whether the person fell inside the Oxbryta (voxelotor) age window (4 years and older) at any point during 2022 | 2022 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |
| `elig_oxbryta_23` | Indicator (0/1) for whether the person fell inside the Oxbryta (voxelotor) age window (4 years and older) at any point during 2023 | 2023 | Derived from date of birth; excludes years after death, and people with no recorded date of birth |

