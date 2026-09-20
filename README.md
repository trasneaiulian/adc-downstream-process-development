# Data-Driven Development of an ADC Downstream Purification Process

A computational bioprocess-development case study exploring how simulated
process data can be used to support downstream purification decisions for an
antibody-drug conjugate (ADC).

The project combines protein purification and downstream-process concepts with
Python-based data analysis to investigate trade-offs between product recovery,
aggregate content, residual free drug-linker, and drug-to-antibody ratio (DAR).

> **Project status:** Work in progress. This project is being developed
> incrementally as part of ongoing training in Python and data analytics.

---

## Project objective

Following antibody-drug conjugation, downstream processing must remove
process-related impurities and undesirable product variants while maintaining
product recovery and critical quality attributes.

This project models a hypothetical post-conjugation ADC purification
development campaign and asks:

> **Which downstream process conditions provide the best balance between ADC
> recovery and product quality?**

The project currently evaluates two sequential downstream operations:

**Post-conjugation material → UF/DF → multimodal chromatography → purified ADC**

All process-response data used in this project are simulated and clearly
identified as such. They do not represent experimental measurements generated
in the laboratory.

---

## Hypothetical ADC

The case study considers a hypothetical ADC with the following characteristics:

- molecule type: IgG1 antibody-drug conjugate;
- conjugation approach: cysteine-based conjugation;
- payload: generic hydrophobic small-molecule payload;
- target mean DAR: approximately 4;
- development stage: post-conjugation downstream purification.

The post-conjugation material is assumed to contain the desired ADC together
with process-related impurities and product variants, including:

- residual free drug-linker;
- low-molecular-weight reaction components;
- aggregates;
- unconjugated or under-conjugated antibody;
- higher-DAR product species.

---

## Downstream process strategy

The simulated purification process consists of two main unit operations:

### 1. Ultrafiltration/diafiltration (UF/DF)

UF/DF is used as the initial post-conjugation cleanup operation.

Its primary objectives are to:

- remove residual free drug-linker and other low-molecular-weight components;
- perform buffer exchange;
- retain the substantially larger ADC product.

### 2. Multimodal chromatography (MMC)

Multimodal chromatography is used as a polishing operation following UF/DF.

Its primary objectives are to:

- improve product quality;
- reduce aggregates and undesirable product variants;
- maintain acceptable ADC recovery.

The project evaluates the two unit operations separately before combining
their recoveries to estimate overall downstream process performance.

---

## Multimodal chromatography screening

A full-factorial screening design was constructed to investigate three
chromatography process parameters.

| Parameter | Screening levels |
|---|---|
| pH | 5.5, 6.5, 7.5 |
| NaCl concentration | 50, 150, 300 mM |
| Load density | 10, 25 mg ADC/mL resin |

The design contains:

**3 × 3 × 2 = 18 simulated process conditions**

For each condition, three responses were evaluated:

- ADC recovery (%);
- aggregate content (%);
- mean DAR.

Residual free drug-linker is addressed separately during UF/DF development,
which represents the primary small-molecule clearance operation in the
simulated downstream process.

---

## MMC exploratory analysis

Initial analysis showed that ADC recovery was highest under moderate pH and
salt conditions and at the lower load density.

Mean recovery was highest at:

- **pH 6.5:** 91.48%;
- **150 mM NaCl:** 90.71%;
- **10 mg ADC/mL resin:** 90.84%.

Aggregate behavior showed a different trend.

Mean aggregate content decreased from:

- 3.02% at pH 5.5 to 2.35% at pH 7.5;
- 3.16% at 50 mM NaCl to 2.20% at 300 mM NaCl.

Increasing load density from 10 to 25 mg ADC/mL resin increased mean aggregate
content from 2.46% to 2.90%.

These results illustrate a simulated process-development trade-off: conditions
that maximize product recovery do not necessarily provide the strongest
aggregate clearance.

---

## Preliminary MMC process selection

To identify balanced process conditions, hypothetical project screening
criteria were applied:

- ADC recovery ≥ 90%;
- aggregate content ≤ 2.5%.

Two of the 18 screening conditions met both criteria.

The preliminary selected MMC condition was:

- **pH:** 6.5
- **NaCl concentration:** 300 mM
- **load density:** 10 mg ADC/mL resin

The simulated responses for this condition were:

| Response | Result |
|---|---:|
| ADC recovery | 92.45% |
| Aggregate content | 1.91% |
| Mean DAR | 3.96 |

This condition was selected because it provided the higher recovery and lower
aggregate content of the two conditions that met the hypothetical screening
criteria. Mean DAR remained close to the target value of approximately 4.

The alternative candidate, pH 7.5 with 150 mM NaCl and a load density of
10 mg ADC/mL resin, produced a mean DAR of 3.98 but showed slightly lower
recovery and higher aggregate content.

The selected condition should be considered a **preferred condition within
this simulated screening study**, not an experimentally demonstrated process
optimum.

It should be considered a **preferred condition within this case study**, not
an experimentally demonstrated process optimum.

---

## UF/DF development

The UF/DF study evaluated increasing diafiltration volumes from:

**0 to 6 DV**

Two primary responses were simulated:

- residual free drug-linker concentration;
- ADC recovery.

Free drug-linker clearance was represented using a simplified exponential
clearance relationship, while ADC recovery was modelled as gradually declining
with increasing processing intensity.

The simulated results demonstrated rapid initial impurity clearance followed
by diminishing returns at higher diafiltration volumes.

| DV | Free drug-linker (ppm) | Linker removal | ADC recovery |
|---:|---:|---:|---:|
| 0 | 1000.00 | 0.00% | 99.06% |
| 1 | 367.88 | 63.21% | 97.99% |
| 2 | 135.34 | 86.47% | 97.55% |
| 3 | 49.79 | 95.02% | 96.79% |
| 4 | 18.32 | 98.17% | 95.41% |
| 5 | 6.74 | 99.33% | 94.74% |
| 6 | 2.48 | 99.75% | 94.23% |

---

## Preliminary UF/DF process selection

The region between 4 and 5 DV provided an attractive balance between
small-molecule clearance and ADC recovery.

At **5 DV**:

- free drug-linker removal reached **99.33%**;
- residual free drug-linker decreased to **6.74 ppm**;
- ADC recovery remained at **94.74%**.

Increasing from 5 to 6 DV provided comparatively little additional impurity
clearance while recovery continued to decrease.

Therefore, **5 DV** was selected as the preliminary UF/DF operating condition
for this simulated process.

---

## Overall downstream process performance

The selected UF/DF condition was combined with the preferred multimodal
chromatography condition:

**Post-conjugation material → 5 DV UF/DF → MMC → purified ADC**

Because the unit operations occur sequentially, overall product recovery is
calculated multiplicatively rather than by averaging the individual recovery
values.

| Process step | Selected condition | Recovery |
|---|---|---:|
| UF/DF | 5 DV | 94.74% |
| Multimodal chromatography | pH 6.5, 300 mM NaCl, 10 mg/mL resin | 92.45% |
| Overall downstream process | UF/DF + MMC | **87.59%** |

Starting conceptually with 100 units of ADC-equivalent material, approximately
94.74 units would remain after UF/DF and approximately 87.59 units after the
subsequent chromatography operation.

This illustrates why optimization of individual purification operations must
also consider their cumulative effect on overall process yield.

---

## Data visualization

The project generates figures to support process interpretation and condition
selection.

Current visualizations include:

- recovery main effects across the MMC screening parameters;
- recovery versus aggregate trade-off and process-selection window;
- UF/DF free drug-linker clearance and ADC recovery across diafiltration
  volumes.

Figures are exported as static PNG files so that key results remain accessible
directly from the repository.

---

## Project structure

```text
adc-downstream-process-development/
├── data/
│   ├── raw/
│   └── processed/
│       ├── adc_mmc_screening_design.csv
│       ├── adc_mmc_simulated_results.csv
│       └── adc_ufdf_simulated_results.csv
├── notebooks/
│   ├── 01_process_design.ipynb
│   └── 02_ufdf_development.ipynb
├── results/
│   └── figures/
│       ├── adc_process_selection_window.png
│       ├── adc_recovery_main_effects.png
│       └── ufdf_clearance_recovery.png
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Tools and methods

The current project uses:

- Python
- Jupyter Notebook
- Pandas
- NumPy
- Matplotlib
- full-factorial experimental-design concepts
- exploratory data analysis
- rule-based process-condition screening
- data visualization
- sequential process-recovery calculations

The analysis is intentionally being developed incrementally. More advanced
statistical modelling and process optimization may be incorporated as the
project develops.

---

## Reproducibility

Processed datasets generated during the analysis are stored in
`data/processed/`.

Figures are exported to `results/figures/`.

The UF/DF analysis reads the MMC results generated by the preceding analysis
rather than manually reproducing the selected chromatography recovery value.
This helps maintain consistency between the two stages of the project.

Random variation in the simulated datasets uses fixed random seeds so that the
results can be reproduced when the notebooks are rerun.

---

## Scientific basis

The project design is informed by published literature describing
post-conjugation ADC purification and process development.

In particular, published work has demonstrated the application of multimodal
chromatography to post-conjugation ADC purification using high-throughput
screening followed by column verification and in-silico process development.

ADC downstream-processing literature also identifies attributes such as DAR,
free drug-linker, aggregates, and product variants as important considerations
during process development.

The numerical datasets in this repository were **not extracted from these
publications**. The literature provides scientific context for the hypothetical
process-development scenario, while the numerical response data are simulated.

### References

1. Matsuda Y. *Current approaches for the purification of antibody-drug
   conjugates.* Journal of Separation Science. 2022.
   DOI: 10.1002/jssc.202100575.

2. Keller WR, Wendeler M. *Using multimodal chromatography for
   post-conjugation antibody-drug conjugate purification: A methodology from
   high throughput screening to in-silico process development.*
   Journal of Chromatography A. 2021;1653:462378.
   DOI: 10.1016/j.chroma.2021.462378.

---

## Limitations

This project is a **simulated bioprocess-development case study**.

The process-response data do not represent laboratory measurements from a
specific ADC, chromatography resin, membrane, or manufacturing process.

The parameter ranges, response relationships, and screening thresholds are
project assumptions designed to create a realistic data-analysis scenario.
They should not be interpreted as universal ADC manufacturing specifications.

Because the responses are generated from predefined simulation relationships,
the exploratory analysis demonstrates whether the imposed relationships can be
identified and interpreted; it does not provide experimental evidence that
these relationships apply to real ADC purification processes.

Experimental verification would be required before applying any conclusions
to an actual downstream process.

---

## Future development

Future versions of the project may include:

- modular Python scripts for data generation and processing;
- additional process-development variables;
- formal design-of-experiments analysis;
- statistical modelling of process responses;
- multi-objective optimization;
- sensitivity analysis;
- additional product-quality attributes;
- integration of experimentally published or openly available datasets where
  appropriate.

The project will be expanded progressively as additional data-analysis methods
are learned.

## References

Matsuda, Y. (2022). Current approaches for the purification of antibody-drug
conjugates. *Journal of Separation Science*, 45(1), 74-86.
https://doi.org/10.1002/jssc.202100575

Keller, W. R., & Wendeler, M. (2021). Using multimodal chromatography for
post-conjugation antibody-drug conjugate purification: A methodology from high
throughput screening to in-silico process development.
*Journal of Chromatography A*, 1653, 462378.
https://doi.org/10.1016/j.chroma.2021.462378