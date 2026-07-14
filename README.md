# Mobility Limitations and Fall-Related Fracture Risk: A Matched-Cohort Analysis Using NHANES Data

## Motivation

Falls are one of the leading causes of injury and loss of independence
among older adults. I wanted to explore a specific question using
publicly available health data: are older adults with mobility
difficulties more likely to have experienced a fall-related fracture,
compared to similar peers without mobility difficulties?

This project applies a matched-cohort study design, a method commonly
used in health services and epidemiological research - to a public
dataset, as a way of practicing and demonstrating applied health data
analysis skills.

## Research Question

Among adults aged 50+, do those with self-reported mobility limitations
have a higher rate of fall-caused bone fractures than those without,
after matching on age and sex?

## Data Source

**NHANES 2017–2018 cycle** (CDC/National Center for Health Statistics)
https://wwwn.cdc.gov/nchs/nhanes/continuousnhanes/default.aspx?BeginYear=2017

| File | Component | Role in this project |
|---|---|---|
| `DEMO_J` | Demographics | Age, sex — used for cohort matching |
| `OSQ_J` | Osteoporosis | Source of the fall-fracture outcome variable |
| `PFQ_J` | Physical Functioning | Source of the mobility risk-factor variable |

Data files are not included in this repository — download them directly
from the NHANES 2017–2018 Questionnaire Data page.

## Method

1. **Data assessment** — checked each source file for missingness and
   distinguished structural (skip-pattern) missingness from random
   missingness, verifying the assumption directly against the data.
2. **Cohort assembly** — merged all three files on `SEQN` (participant
   ID), restricted to adults aged 50+.
3. **Outcome variable** — `FALL_FRACTURE`: whether the participant ever
   fractured a hip, wrist, or spine as a result of a fall.
4. **Risk-factor variable** — `MOBILITY_LIMITED`: whether the participant
   reports difficulty walking, climbing stairs, standing from a chair,
   or needs special equipment to walk.
5. **Matched-cohort construction** — 1:1 nearest-neighbour matching
   without replacement, using exact matching on sex and a 2-year age
   caliper, to control for these two known confounders.
6. **Analysis** — descriptive summary statistics and a chi-square test
   comparing fall-fracture rates between matched groups.

## Key Literature

- Co-occurrence of fall-related factors in NHANES-aged 60–85 adults
  (PMC9642892)
- Multifactorial predictors of falls, National Health and Aging Trends
  Study (PMC12645780)
- Public Health Agency of Canada, *Surveillance Report on Falls in Older
  Adults in Canada*

## Results

Matching successfully balanced age (66.2 vs 66.1 years) and sex (49.1%
female in both groups) between comparison groups. After matching,
participants with mobility limitations had a significantly higher rate
of fall-caused fractures (5.6%) than those without (2.6%), χ² = 11.731,
p = 0.0006.


## Limitations

- NHANES is cross-sectional, so this analysis shows association, not
  causation or temporal order.
- No direct "did you fall" question exists in this NHANES cycle; the
  fall-fracture outcome is a literature-informed proxy and likely
  understates true fall frequency.
- Matching used two confounders (age, sex) via exact/caliper matching
  rather than Propensity Score Matching, appropriate given the limited
  number of confounders controlled for here.
- Fall risk factors are known to cluster in older adults; this analysis
  examines mobility limitation in isolation rather than jointly with
  other risk factors.

## Author

Megha Radhakrishnan Sanitha
github.com/meggie2002 | linkedin.com/in/megha-rs
