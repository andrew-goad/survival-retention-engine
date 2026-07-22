# Survival Strategy Framework

## Strategic Intent: From Time-to-Event Modeling to Governed Intervention Evidence

How do you move beyond asking whether an event will occur and begin estimating **when risk emerges, which groups have the shortest runway, and how controlled assumptions move the same target cohort**?

I built the Survival Strategy Framework as a reusable Python time-to-event analytical system—not a one-time Cox proportional hazards notebook. It combines governed survival-data contracts, descriptive persona discovery, regularized CoxPH modeling, five-fold validation, out-of-fold calibration, model-derived risk stratification, same-cohort scenario simulation, dependency-safe feature rebuilding, run-level evidence archives, and automated executive and technical reporting.

The reference implementation uses deterministic synthetic retention data. Its purpose is to demonstrate how survival modeling can travel from statistical development through validation, scenario governance, executive interpretation, and technical evidence without exposing PII or making production claims.

---

## Repository Navigation

For a detailed file-by-file guide, see:

[`PROJECT_ARTIFACT_MAP.md`](./PROJECT_ARTIFACT_MAP.md)

The artifact map explains the repository structure, source implementation, BRD, Validation Summary, generated stakeholder outputs, charts, run evidence, and recommended reviewer paths.

---

## Enterprise System Architecture

[![Enterprise Survival Strategy Framework Architecture](./docs/Enterprise%20Survival%20Strategy%20Framework%20Architecture.png)](./docs/Enterprise%20Survival%20Strategy%20Framework%20Architecture.png)

[Open the architecture full size](./docs/Enterprise%20Survival%20Strategy%20Framework%20Architecture.png)

The architecture is organized into five governed layers:

| Layer | Purpose | Core Question |
|---|---|---|
| **1. Survival Input Contract** | Defines run scope, duration, event/censoring, governed features, engineered terms, and scenario eligibility. | *Is the time-to-event analysis structurally valid before modeling begins?* |
| **2. Parallel Persona + CoxPH Modeling** | Separates descriptive K-Means personas from the regularized CoxPH risk model and validation evidence. | *What lifecycle groups exist, and what features are associated with modeled hazard?* |
| **3. Risk Stratification** | Scores the population, ranks partial hazard, profiles risk tiers, and selects a governed top-quartile cohort. | *Where is modeled risk concentrated?* |
| **4. Governed Same-Cohort Simulation** | Applies control, improvement, combined, and stress assumptions to identical target IDs while rebuilding engineered dependencies. | *How does modeled hazard and survival move when controlled assumptions change?* |
| **5. Multi-Audience Evidence + Run Archive** | Produces validation evidence, stakeholder artifacts, configuration snapshots, input fingerprints, manifests, and acceptance checks. | *Can the result be reviewed, challenged, reproduced, and explained?* |

### End-to-End Flow

```text
Synthetic Time-to-Event Data
→ Input Contract Validation
→ Persona Discovery
→ Regularized CoxPH Model
→ Stratified K-Fold Validation
→ Out-of-Fold Calibration
→ Proportional-Hazards Review
→ Population Partial-Hazard Scoring
→ Top-Quartile Target Cohort
→ Governed Same-Cohort Scenarios
→ Dependency Synchronization
→ Re-Scoring and Predicted Survival
→ Scenario Comparison
→ Run Registry
→ Executive PPTX + Technical PDF
```

---

## Validated Demonstration Snapshot

| Measure | Result |
|---|---:|
| Synthetic records | **7,500** |
| Observed events | **2,964** |
| Event rate | **39.52%** |
| Right-censored records | **4,536** |
| CoxPH features | **12** |
| Apparent concordance | **0.8272** |
| Five-fold mean validation concordance | **0.8272** |
| Five-fold validation standard deviation | **0.0069** |
| Integrated Brier score across configured horizons | **0.1188** |
| Maximum risk-group calibration error | **7.08%** |
| Stable descriptive personas | **3** |
| Persona stability mean adjusted Rand index | **0.9920** |
| Governed target cohort | **1,875 records** |
| Governed scenarios | **6** |
| Final acceptance posture | **`PASS_WITH_REVIEW`** |

The documented review item is a raw proportional-hazards diagnostic for `auto_renew_flag`. Multiplicity-adjusted tests pass, and the stratified sensitivity model preserves the target-cohort overlap, exact improvement-scenario ranking, and best scenario.

---

## Why Survival Analysis?

Binary classification asks:

```text
Will the event occur?
```

Survival analysis adds a second dimension:

```text
When is the event likely to occur,
and how much event-free runway remains?
```

That distinction matters because incomplete observations are not discarded. Right-censored records contribute valid time-at-risk evidence even when the event has not occurred within the observed period.

The framework therefore supports questions such as:

- Which personas have the shortest observed event-free runway?
- Which model-derived risk tiers separate most clearly over time?
- Which features are associated with higher or lower partial hazard?
- How does the same high-risk cohort move under controlled assumptions?
- Are the conclusions stable under cross-validation, calibration review, PH sensitivity, and reproducibility testing?

---

## Framework Capabilities

### 1. Governed Survival Input Contract

The framework validates the analytical contract before fitting any model.

Required controls include:

- unique governed IDs
- numeric positive duration
- binary event indicator
- explicit time-unit label
- governed model and segmentation features
- missingness and finite-value checks
- scenario feature eligibility
- protected ID, duration, and event fields
- engineered interaction and squared-term dependencies
- configured risk quantile, evaluation horizon, penalizer, and random state

This fail-fast design prevents invalid input from becoming downstream model evidence.

### 2. Parallel Persona Discovery and CoxPH Modeling

The framework deliberately separates two analytical branches:

```text
Governed Input
├── K-Means Persona Discovery
└── Regularized CoxPH Modeling
```

Personas are descriptive lifecycle segments. They are **not** inserted into the CoxPH model as hidden risk features.

The persona branch includes:

- StandardScaler
- K-Means clustering
- named segment profiles
- silhouette score
- Davies-Bouldin index
- Calinski-Harabasz index
- multi-seed adjusted Rand index stability review
- persona-level Kaplan-Meier evidence

The CoxPH branch includes:

- standardized model features
- L2-regularized Cox proportional hazards fitting
- coefficients and hazard ratios
- confidence intervals and p-values
- apparent concordance
- baseline survival and cumulative hazard
- five-fold stratified validation
- out-of-fold survival predictions
- calibration
- proportional-hazards diagnostics
- PH sensitivity analysis

### 3. Model-Derived Risk Stratification

The fitted CoxPH model generates row-level partial-hazard scores.

The framework then creates:

- high risk: top 25%
- mid risk: middle 50%
- benchmark: bottom 25%

This tiering supports:

- observed event-rate comparison
- median-duration comparison
- mean partial-hazard comparison
- characteristic profiling
- Kaplan-Meier evidence
- governed target-cohort selection

### 4. Governed Same-Cohort Scenario Simulation

The same 1,875 target IDs are held constant under every scenario.

That design isolates modeled movement from population drift:

```text
Same target population
+ controlled feature changes
+ rebuilt dependencies
= interpretable scenario movement
```

The scenario engine supports:

- neutral control scenarios
- favorable improvement scenarios
- combined scenarios
- adverse stress scenarios
- feature-level bounds
- rounding rules
- configured-versus-realized change evidence
- bound-hit rates
- same-cohort partial-hazard re-scoring
- predicted-survival comparison
- direction checks
- improvement ranking

### 5. Dependency-Safe Feature Rebuilding

Scenario edits can invalidate engineered model features unless dependencies are rebuilt.

The framework protects:

```text
_x_  → interaction terms
_sq  → squared terms
```

For example:

```text
monthly_active_days
×
product_adoption_count
=
monthly_active_days_x_product_adoption_count
```

When a base feature changes, the associated engineered fields are recalculated before scoring. `dependency_audit.csv` records the pre-rebuild discrepancy, post-rebuild discrepancy, source fields, recalculation status, and validation result.

### 6. Multi-Audience Evidence

The framework creates evidence for different review audiences:

| Audience | Artifact |
|---|---|
| Executive / business stakeholder | `Survival_Strategy_Deck.pptx` |
| Technical / validation reviewer | `Technical_Model_Evidence.pdf` |
| Governance / audit reviewer | configuration, input fingerprint, manifest, acceptance checks, validation CSVs |
| Analyst / developer | source code, row-level scores, survival curves, persona profiles, risk tiers, scenario audit |
| GitHub reviewer | architecture and browser-rendered PNG evidence |

---

## Representative Framework Outputs

### Persona Lifecycle Evidence

[![Persona Kaplan-Meier Survival Evidence](./outputs/persona_kaplan_meier.png)](./outputs/persona_kaplan_meier.png)

[Open the persona survival chart full size](./outputs/persona_kaplan_meier.png)

The three stable descriptive personas are:

| Persona | Records | Event Rate | Median Duration |
|---|---:|---:|---:|
| **Engaged & Embedded** | 3,409 | 12.94% | 14.77 months |
| **Low-Engagement Risk** | 2,442 | 60.65% | 8.92 months |
| **Service-Friction Risk** | 1,649 | 63.19% | 8.31 months |

The persona evidence is descriptive—not causal and not a substitute for model-derived risk grades. Its value is in showing that different lifecycle profiles can exhibit materially different observed runways for different operational reasons.

### Model-Derived Risk-Tier Evidence

[![Risk-Tier Kaplan-Meier Survival Evidence](./outputs/risk_tier_kaplan_meier.png)](./outputs/risk_tier_kaplan_meier.png)

[Open the risk-tier survival chart full size](./outputs/risk_tier_kaplan_meier.png)

| Risk Tier | Records | Event Rate | Median Duration | Mean Partial Hazard |
|---|---:|---:|---:|---:|
| **High Risk — Top 25%** | 1,875 | 87.57% | 3.31 months | 10.900 |
| **Mid Risk** | 3,750 | 31.92% | 12.71 months | 1.098 |
| **Benchmark — Bottom 25%** | 1,875 | 6.67% | 15.25 months | 0.200 |

The observed Kaplan-Meier ordering is monotonic:

```text
Benchmark survival
>
Mid-risk survival
>
High-risk survival
```

### Same-Cohort Predicted Survival

[![Same-Cohort Baseline and Scenario Survival](./outputs/baseline_vs_scenario_survival.png)](./outputs/baseline_vs_scenario_survival.png)

[Open the same-cohort survival chart full size](./outputs/baseline_vs_scenario_survival.png)

The chart compares CoxPH-predicted survival for the **same governed target IDs** under:

- baseline target cohort
- no-change control
- onboarding completion improvement
- support-resolution improvement
- product-adoption expansion
- combined retention strategy
- service-friction stress

The curves explicitly begin at `S(0) = 1.0`.

### Scenario Hazard Movement

[![Modeled Relative Hazard Movement by Scenario](./outputs/scenario_hazard_reduction.png)](./outputs/scenario_hazard_reduction.png)

[Open the scenario hazard chart full size](./outputs/scenario_hazard_reduction.png)

| Rank | Scenario | Modeled Hazard Movement | 12-Month Survival Movement |
|---:|---|---:|---:|
| 1 | Combined Retention Strategy | **52.86% reduction** | **+18.79 percentage points** |
| 2 | Onboarding Completion Improvement | **28.03% reduction** | **+9.51 percentage points** |
| 3 | Support Resolution Improvement | **25.72% reduction** | **+4.69 percentage points** |
| 4 | Product Adoption Expansion | **11.77% reduction** | **+3.49 percentage points** |
| 5 | No-Change Control | **0.00%** | **0.00 percentage points** |
| 6 | Service Friction Stress | **72.86% adverse increase** | **-8.22 percentage points** |

These are model-based sensitivities under configured assumptions. They are not causal treatment effects or realized retention outcomes.

### Out-of-Fold Calibration

[![Out-of-Fold Survival Calibration](./outputs/calibration_at_horizons.png)](./outputs/calibration_at_horizons.png)

[Open the calibration chart full size](./outputs/calibration_at_horizons.png)

The framework reports:

- train-only scaling inside each fold
- five stratified validation folds
- out-of-fold partial-hazard and survival predictions
- Kaplan-Meier observed survival by modeled risk group
- horizon-specific calibration error
- inverse-probability-of-censoring-weighted Brier scores
- a documented integrated Brier summary across configured horizons

Maximum absolute calibration error across the modeled risk groups was 7.08%, below the configured 10% review threshold.

### Proportional-Hazards Review

[![Scaled Schoenfeld Residual Review](./outputs/ph_assumption_diagnostics.png)](./outputs/ph_assumption_diagnostics.png)

[Open the PH diagnostic chart full size](./outputs/ph_assumption_diagnostics.png)

The raw PH test flagged `auto_renew_flag` for review:

```text
Raw p-value:        0.0278
Holm-adjusted:      0.3331
BH-adjusted:        0.3331
```

A stratified CoxPH sensitivity review preserved:

- 93.71% target-cohort overlap
- 0.8816 target-cohort Jaccard similarity
- exact favorable-scenario ranking
- the same best improvement scenario
- scenario-rank Spearman correlation of 1.000

The framework therefore retains a transparent `PASS_WITH_REVIEW` posture rather than suppressing the raw diagnostic or overstating a clean model-validation conclusion.

---

## Governed Scenario Set

| Scenario | Type | Controlled Assumption | Expected Direction |
|---|---|---|---|
| **No-Change Control** | Control | No feature movement | Neutral |
| **Onboarding Completion Improvement** | Improvement | Add 10 percentage points, bounded at 100% | Improved |
| **Support Resolution Improvement** | Improvement | Reduce resolution time by 25%, subject to the configured floor | Improved |
| **Product Adoption Expansion** | Improvement | Add one adopted product, subject to the configured cap | Improved |
| **Combined Retention Strategy** | Improvement | Apply all three improvement assumptions together | Improved |
| **Service Friction Stress** | Stress | Increase resolution time by 25% and add one service incident | Adverse |

The no-change control verifies that the simulation pipeline does not manufacture movement. The adverse stress case verifies bidirectional sensitivity rather than presenting only favorable alternatives.

---

## Validation and Acceptance Discipline

The validated run concluded:

> **`PASS_WITH_REVIEW`**

All structural, scoring, scenario, reproducibility, reporting, and archive checks passed.

The documented review posture reflects one raw proportional-hazards diagnostic. The framework retains that evidence while also reporting:

- multiplicity-adjusted PH tests
- scaled Schoenfeld residuals
- a stratified sensitivity model
- target-cohort overlap
- scenario-ranking stability
- unchanged best scenario

### Acceptance Evidence

The run confirmed:

- 7,500 unique governed IDs
- nonempty target cohort
- identical target IDs across all scenarios
- rebuilt interactions and squared terms
- complete scenario-change audit
- finite calculated scenario metrics
- survival probabilities within `[0, 1]`
- survival beginning at `S(0) = 1`
- directionally correct control, improvement, and stress scenarios
- five completed cross-validation folds
- out-of-fold calibration evidence
- persona-quality and stability evidence
- PH sensitivity review
- exact substantive reproducibility
- generated PowerPoint and PDF artifacts

---

## Technical Implementation

### Core Python Libraries

| Library | Role |
|---|---|
| `pandas` | Data contracts, profiling, scenario results, and evidence tables |
| `numpy` | Deterministic synthetic generation, numerical operations, and risk quantiles |
| `scikit-learn` | StandardScaler, K-Means, stratified folds, persona quality, and cluster stability |
| `lifelines` | CoxPH, Kaplan-Meier, concordance, predicted survival, and PH diagnostics |
| `matplotlib` | GitHub-viewable survival, calibration, PH, and scenario charts |
| `python-pptx` | Automated executive presentation |
| `reportlab` | Automated technical model-evidence PDF |

### Model Design

The primary CoxPH model uses:

```text
12 governed model features
L2 penalization = 0.10
L1 ratio = 0.00
standardized model inputs
5 stratified validation folds
risk target = top 25%
evaluation horizon = 12 months
```

The feature set includes:

- onboarding completion
- monthly active days
- product-adoption count
- support tickets
- support-resolution time
- service incidents
- starting tenure
- auto-renew status
- enterprise status
- engagement × adoption interaction
- support volume × resolution delay interaction
- onboarding squared term

---

## Run the Framework

### Install Dependencies

```bash
pip install pandas numpy matplotlib scikit-learn lifelines python-pptx reportlab
```

### Execute the Synthetic Retention Demonstration

```bash
python src/survival_strategy_framework.py \
  --demo retention \
  --records 7500 \
  --seed 42 \
  --self-test \
  --output-root outputs
```

The framework will:

1. generate deterministic synthetic retention data;
2. run internal self-tests;
3. validate the survival-data contract;
4. fit descriptive personas;
5. fit the regularized CoxPH model;
6. perform five-fold validation;
7. generate out-of-fold calibration;
8. run PH diagnostics and sensitivity analysis;
9. create the model-derived target cohort;
10. apply control, improvement, combined, and stress scenarios;
11. rebuild engineered dependencies;
12. compare modeled hazard and predicted survival;
13. generate charts;
14. archive run evidence;
15. create the executive PowerPoint and technical PDF.

---

## Anchor Artifacts

| Artifact | Location |
|---|---|
| Enterprise Architecture | [`Enterprise Survival Strategy Framework Architecture.png`](./docs/Enterprise%20Survival%20Strategy%20Framework%20Architecture.png) |
| Business Requirements Document | [`Survival_Strategy_Framework_Business_Requirements_Document.pdf`](./docs/Survival_Strategy_Framework_Business_Requirements_Document.pdf) |
| Python Source | [`survival_strategy_framework.py`](./src/survival_strategy_framework.py) |
| Validation Summary | [`Survival_Strategy_Framework_Validation_Summary.pdf`](./tests/Survival_Strategy_Framework_Validation_Summary.pdf) |
| Executive Deck | [`Survival_Strategy_Deck.pptx`](./outputs/Survival_Strategy_Deck.pptx) |
| Technical Model Evidence | [`Technical_Model_Evidence.pdf`](./outputs/Technical_Model_Evidence.pdf) |
| Run Acceptance | [`acceptance_checks.csv`](./outputs/acceptance_checks.csv) |
| Run Metadata | [`run_metadata.json`](./outputs/run_metadata.json) |
| Scenario Results | [`scenario_results.csv`](./outputs/scenario_results.csv) |
| Artifact Manifest | [`artifact_manifest.json`](./outputs/artifact_manifest.json) |

---

## Repository Map

```text
survival-strategy-framework/
│
├── README.md
├── PROJECT_ARTIFACT_MAP.md
│
├── docs/
│   ├── Enterprise Survival Strategy Framework Architecture.png
│   └── Survival_Strategy_Framework_Business_Requirements_Document.pdf
│
├── outputs/
│   ├── stakeholder outputs
│   ├── input and run controls
│   ├── model evidence
│   ├── cross-validation and calibration
│   ├── PH diagnostics and sensitivity
│   ├── persona evidence
│   ├── risk-tier evidence
│   ├── scenario evidence
│   ├── dependency audit
│   └── reproducibility evidence
│
├── src/
│   └── survival_strategy_framework.py
│
└── tests/
    └── Survival_Strategy_Framework_Validation_Summary.pdf
```

For the full file-level guide, see:

[`PROJECT_ARTIFACT_MAP.md`](./PROJECT_ARTIFACT_MAP.md)

---

## Suggested Reviewer Paths

### Fast Executive Review

1. Read this README.
2. Open the enterprise architecture.
3. Review the same-cohort predicted-survival chart.
4. Review the scenario hazard-movement chart.
5. Open the generated executive PowerPoint.
6. Review the BRD and formal Validation Summary.

### Technical / Architecture Review

1. Start with the BRD and architecture.
2. Review `src/survival_strategy_framework.py`.
3. Inspect configuration, validation, model, cross-validation, calibration, PH, persona, risk-tier, scenario, and dependency artifacts in `outputs/`.
4. Review the generated technical evidence PDF.
5. Confirm acceptance and reproducibility evidence.

### Governance / Validation Review

1. Review the formal Validation Summary.
2. Review `acceptance_checks.csv`.
3. Review `run_metadata.json`, `framework_config.json`, and `artifact_manifest.json`.
4. Confirm train-only scaling and fold-level validation.
5. Review raw and adjusted PH tests.
6. Review PH sensitivity and scenario-ranking stability.
7. Confirm same target IDs across all scenarios.
8. Review `scenario_change_audit.csv` and `dependency_audit.csv`.
9. Confirm exact substantive rerun results in `reproducibility_checks.csv`.

---

## Data, Privacy, and Interpretation Boundaries

All data in this repository is synthetic demonstration data.

This project does **not** use real customer records, PII, proprietary retention policy, production treatment rules, booked outcomes, or realized financial results.

Important interpretation boundaries:

- Partial hazard is relative modeled risk, not event probability.
- Kaplan-Meier curves are descriptive survival evidence.
- CoxPH-predicted survival requires domain validation before production use.
- The persona labels are descriptive lifecycle profiles, not causal classes.
- Risk tiers are model-derived analytical groupings, not customer treatment categories.
- Scenario movement is modeled sensitivity, not causal intervention effect.
- The improvement scenarios are illustrative assumptions, not production recommendations.
- The stress scenario demonstrates adverse sensitivity, not a forecast.
- The reported survival movement is expressed in percentage points.
- No booked revenue, realized ROI, defended LTV, or production lifetime-value estimate is claimed.
- Five-fold validation and out-of-fold calibration do not replace external or temporal validation.
- Production use would require governed domain data, calibration, monitoring, model-risk approval, implementation testing, and operational controls.

---

## Current Artifact Status

| Area | Artifact | Status | Role |
|---|---|---:|---|
| Root | README | Complete | Executive project narrative |
| Root | Project Artifact Map | Complete | Detailed navigation and reviewer paths |
| `docs/` | Enterprise Architecture | Complete | Primary README and executive system visual |
| `docs/` | BRD | Complete | Design requirements, governance, boundaries, and roadmap |
| `src/` | Python Framework | Complete | Executable implementation |
| `tests/` | Validation Summary | Complete | Independent validation synthesis and acceptance |
| `outputs/` | Executive Deck | Complete | Automated business-facing evidence |
| `outputs/` | Technical PDF | Complete | Automated technical evidence |
| `outputs/` | Run Evidence | Complete | Validation, model, scenario, audit, and reproducibility archive |

---

## Philosophy: No Cold Handoffs and No Black-Box Model Claims

A survival model should not end with a coefficient table.

This project is designed to keep the full reasoning chain connected:

```text
Input contract
→ persona context
→ CoxPH model
→ validation evidence
→ risk concentration
→ governed scenarios
→ dependency reconstruction
→ same-cohort re-scoring
→ survival movement
→ stakeholder evidence
→ run archive
```

The objective is not merely to fit a model. The objective is to preserve enough logic, controls, evidence, and interpretation for business, analytics, technical, and validation stakeholders to understand what the output means—and what it does not mean.

---

## Author

**Andrew R. Goad**

Built as a portfolio-grade governed survival-analysis, scenario-simulation, model-validation, and executive-evidence framework.
