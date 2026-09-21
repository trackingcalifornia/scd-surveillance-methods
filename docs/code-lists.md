# Code Lists

How each condition and each medication fill is identified from claims, and where
to get the codes themselves.

**The codes are in [`code-lists.csv`](code-lists.csv)** — 463 rows, one per code,
with its condition, variable stem, and code type. That is the file to use if you
want to look a code up, filter by condition or code type, or copy a list into
your own work. It renders as a sortable table in the browser and opens in any
spreadsheet tool.

This page holds what the CSV cannot: the matching rules you need in order to
reproduce a count, and notes on individual lists. The tables below summarise each
list rather than enumerating it — some lists run to 64 codes, which belongs in a
column, not a paragraph.

The lists are maintained in a reference workbook, which is imported and reshaped
into the lookup table the analysis reads.


## Where each list is used

| List | Report section | Variables produced |
|---|---|---|
| SCD complications | [Emergency department](03-metric-definitions.md#emergency-department), [Inpatient admissions](03-metric-definitions.md#inpatient-admissions) | `ed_flag_*` / `ed_any_*`, `hosp_flag_*` / `hosp_any_*` |
| Severe Maternal Morbidity | [Maternal morbidity](03-metric-definitions.md#maternal-morbidity) | `SMM_*`, `any_SMM` |
| Medications | [Medications](03-metric-definitions.md#medications) | `any_presc_*`, `presc_*_21/22/23`, supply-day totals |
| Preventive screenings | [Preventive screenings](03-metric-definitions.md#preventive-screenings) | `tcd_count`, `cbc_count`, `microal_count`, `opth_count` |

The screening CPT lists are the one exception to the lookup table: they are
maintained separately from it rather than read out of it. The codes shown below
match that separate copy exactly, so the two agree — but they are two places
holding the same list, and nothing keeps them in step.

Lists not reproduced here. **Antibiotic prophylaxis** NDCs come from a
separate internal reference table appended during lookup creation, and the list
is large.

## What each list covers

### SCD complications

| Condition | Variable stem | Codes | Examples |
|---|---|---:|---|
| Acute chest syndrome | `ACS` | 5 | `D57.01`, `D57.211`, `D57.411`, ... |
| Stroke | `stroke` | 12 | `D57.03`, `D57.213`, `D57.413`, ... |
| Severe infection / sepsis | `inf_sep` | 21 | `A02.1`, `A26.7`, `A32.7`, ... |
| Splenic sequestration | `sple_seq` | 7 | `D57.02`, `D57.212`, `D57.412`, ... |
| Aplastic crisis | `apl_crisis` | 14 | `D57.00`, `D57.09`, `D57.218`, ... |
| Priapism | `priapism` | 4 | `N48.30`, `N48.32`, `N48.33`, ... |
| Acute anemia / hemolytic crisis | `a_anemia` | 10 | `D59.3`, `D59.30`, `D59.31`, ... |
| Chronic kidney disease | `CKD` | 16 | `I12.9`, `I13.0`, `I13.10`, ... |
| Vaso-occlusive episode / pain crisis | `VOE` | 11 | `D57.00`, `D57.09`, `D57.218`, ... |
| Venous thromboembolism | `VTE` | 3 | `I26`, `I80`, `I82` |
| Avascular necrosis | `Ava_nec` | 1 | `M87` |
| Pulmonary hypertension | `pulm_hyp` | 1 | `I27` |

105 codes, all ICD-10-CM diagnosis codes. Full list: [`code-lists.csv`](code-lists.csv).

### Severe Maternal Morbidity - diagnoses

| Condition | Variable stem | Codes | Examples |
|---|---|---:|---|
| Acute myocardial infarction | `AMI` | 2 | `I21`, `I22` |
| Aneurysm | `aneurysm` | 2 | `I71`, `I79.0` |
| Acute renal failure | `ARF` | 2 | `N17`, `O90.4` |
| Acute respiratory distress syndrome | `ARDS` | 10 | `J80`, `J95.1`, `J95.2`, ... |
| Amniotic fluid embolism | `AFE` | 5 | `O88.112`, `O88.113`, `O88.119`, ... |
| Cardiac arrest / ventricular fibrillation | `vfib` | 2 | `I46`, `I49.0` |
| Disseminated intravascular coagulation | `DIC` | 29 | `D65`, `D68.8`, `D68.9`, ... |
| Eclampsia | `eclmp` | 1 | `O15` |
| Heart failure or arrest during procedure | `ht_atk` | 6 | `I97.120`, `I97.121`, `I97.130`, ... |
| Puerperal cerebrovascular disorders | `PC` | 30 | `A81.2`, `G45`, `G46`, ... |
| Pulmonary edema / acute heart failure | `PE` | 20 | `I50.1`, `I50.20`, `I50.21`, ... |
| Severe anesthesia complications | `anth` | 49 | `O29.112`, `O29.113`, `O29.114`, ... |
| Sepsis | `sepsis` | 10 | `A32.7`, `A40`, `A41`, ... |
| Shock | `shock` | 7 | `O75.1`, `R57`, `T78.2XXA`, ... |
| Sickle cell disease with crisis | `Mat_SC` | 12 | `D57.00`, `D57.01`, `D57.02`, ... |
| Air and thrombotic embolism | `emb` | 23 | `I26`, `O88.012`, `O88.013`, ... |

210 codes, all ICD-10-CM diagnosis codes. Full list: [`code-lists.csv`](code-lists.csv).

### Severe Maternal Morbidity - procedures

| Condition | Variable stem | Codes | Examples |
|---|---|---:|---|
| Conversion of cardiac rhythm | `card_rhy` | 2 | `5A12012`, `5A2204Z` |
| Blood transfusion | `bld_trnsf` | 64 | `30230H0`, `30230K0`, `30230L0`, ... |
| Hysterectomy | `hyst` | 4 | `0UT90ZL`, `0UT90ZZ`, `0UT97ZL`, ... |
| Temporary tracheostomy | `tem_trach` | 3 | `0B110F4`, `0B113F4`, `0B114F4` |
| Ventilation | `vent` | 3 | `5A1935Z`, `5A1945Z`, `5A1955Z` |

76 codes, all ICD-10-PCS procedure codes. Full list: [`code-lists.csv`](code-lists.csv).

### Preventive screenings

| Condition | Variable stem | Codes | Examples |
|---|---|---:|---|
| Transcranial Doppler | `TCD` | 5 | `93886`, `93888`, `93890`, ... |
| Complete blood count | `CBC` | 5 | `85025`, `85027`, `85007`, ... |
| Microalbumin | `microal` | 4 | `82043`, `82044`, `82570`, ... |
| Ophthalmology | `opth` | 4 | `92002`, `92004`, `92012`, ... |

18 codes, all CPT codes. Full list: [`code-lists.csv`](code-lists.csv).

### Medications

| Condition | Variable stem | Codes | Examples |
|---|---|---:|---|
| Hydroxyurea | `HU` | 44 | `000030830`, `000036335`, `000036336`, ... |
| Endari (L-glutamine) | `Endari` | 2 | `42457042001`, `42457042060` |
| Oxbryta (voxelotor) | `Oxbryta` | 5 | `72786010101`, `72786011102`, `72786011103`, ... |
| Adakveo (crizanlizumab) | `Adakveo` | 3 | `00078088361`, `J0791`, `C9053` |

54 codes, all NDC codes, except two HCPCS procedure codes for Adakveo. Full list: [`code-lists.csv`](code-lists.csv).

## Disease-modifying medication NDCs, with product names

The four disease-modifying agents, as dispensed products. Adakveo is an infusion
and is therefore identified by HCPCS procedure codes (`J0791`, `C9053`) in
addition to its NDC.

| NDC | Product |
|---|---|
| `72786010101` | voxelotor 500 MG oral tablet [Oxbryta] |
| `72786011102` | voxelotor 300 MG tablet for oral suspension [Oxbryta] |
| `72786011103` | voxelotor 300 MG tablet for oral suspension [Oxbryta] |
| `72786010202` | voxelotor 300 MG oral tablet [Oxbryta] |
| `72786010203` | voxelotor 300 MG oral tablet [Oxbryta] |
| `00078088361` | 10 ML crizanlizumab-tmca 10 MG/ML injection [Adakveo] |
| `42457042001` | glutamine 5000 MG powder for oral solution [Endari] |
| `42457042060` | glutamine 5000 MG powder for oral solution [Endari] |


## Notes on individual lists

**Antibiotic prophylaxis is not listed here.** Its NDC list is large and comes
from a separate internal reference table of antibiotic NDCs, appended when the
lookup table is built rather than maintained in this workbook.
