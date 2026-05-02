# EquiRisk-FoodDeserts

## Equity-Aware Diabetes Care Navigation in Food Deserts
### An Integrated PAPO + EquiRisk Simulation Framework

**Version:** 1.3
**Date:** 2026-05-01
**Author:** Min Wu, PhD
**Affiliation:** Zilber College of Public Health, University of Wisconsin-Milwaukee
**GitHub:** https://github.com/Min-PH/EquiRisk-FoodDeserts

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19271682.svg)](https://doi.org/10.5281/zenodo.19271682)

---

## Changelog

- **v1.0** — Initial release. EquiRisk + PAPO integration, six boundary condition categories (BC-1–BC-6), 13 modular projects, global adaptation guide.
- **v1.1** — Added BC-7 (Trust and Engagement Boundaries) as a first-class boundary condition. Added `trust_barrier` as a Layer 3 attribute. Added three new modular projects (S4, I5, A4). Added Step 11 Simulation Validation Checklist, Step 12 Milwaukee Reference Scenario, and Step 13 Known Limitations and Open Research Questions to CMDDS. Added sub-score normalization guidance. Added NULL output type-coding requirement. Updated all repository files to v1.1.
- **v1.2** — Added agent state transition rules with permitted transitions table and re-entry logic. Added simulation time step and scheduling specification. Added EquiRisk tier definitions (Tier 1–4 with default score ranges). Added opportunity ranking criteria for multi-opportunity selection. Added default contact success probability model. Added default HbA1c trajectory model. Added Equity Audit Layer specification with timing, triggers, and alert thresholds. Added synthetic population generation guidance (CMDDS Step 14). Added data privacy, ethics, and IRB considerations (CMDDS Step 15). Corrected worked example arithmetic (Step 12). Added two new modular projects (S5, I6). Updated all repository files to v1.2.
- **v1.3** — Major structural revision driven by EquiRisk Case Report #004-M (MOKG-PH analysis). **Replaced the additive composite EquiRisk score with a multiplicative priority formulation:** `Priority = Clinical Risk × (1 + CVI) × Feasibility Weight`. Added **Contextual Vulnerability Index (CVI)** as a named composite of Layer 2 attributes. Added **Uptake Probability** as a formal Layer 3 attribute distinct from contact success. Added **BC-8 (Cultural Appropriateness Boundaries)**. Added three pre-deployment gates: **Bias Injection Protocol** (CMDDS Step 16), **Community Co-Design Requirement** (CMDDS Step 17), and **Equity Halt Threshold** (default ≥0.70 of equity-weighted expected receipt rate). Added three operational guardrails: **Bias Loop-Breaking Constraint**, **Cumulative Tactical Drift Detection**, and **Stigma Sentinel + Vulnerable Population Floor**. Updated EquiRisk tier ranges for the new [0, 2] priority scale. Updated worked example with fully reproducible multiplicative arithmetic and additive comparison. Updated CMDDS to v1.3. The companion `FORK_SIMULATION_SUGGESTIONS.md`, `CONTRIBUTING.md`, and `LICENSE.md` documents will be updated to v1.3 in subsequent commits.

> **Migration note for forks built on v1.0–v1.2:** v1.3 changes the canonical scoring formula from additive to multiplicative. Forks should re-score their populations under the new formula before publishing comparative results across CMDDS versions. The additive form is retained in the CMDDS as a deprecated alternative for backward comparison only.

---

## The Problem This Framework Addresses

Diabetes risk stratification has a critical failure mode: it identifies who is at risk but ignores whether interventions can actually reach them — and treats two patients with identical clinical scores as equivalent even when one faces structural barriers that make the recommended care effectively undeliverable.

In food desert settings, a patient with high HbA1c may receive the same care recommendation as a patient with identical clinical indicators but full food access, transportation, and economic stability. Traditional approaches assume interventions are feasible. In food deserts, they frequently are not. Even when interventions are available and reachable, patients with histories of system failure, denial, or disrespect may never be successfully contacted — a barrier that is structural, not personal. And even when contact succeeds, culturally inappropriate interventions yield low uptake.

**EquiRisk-FoodDeserts addresses this by asking a different question:**

> *"Whose effective risk is highest given their access context, faces the greatest structural and cultural barriers, and can be reached by a feasible intervention right now — and is the system actually delivering equitably?"*

The shift from additive to multiplicative scoring in v1.3 makes the central insight explicit: **contextual vulnerability does not just shift allocation; it raises the patient's effective expected health burden.** Two patients with identical clinical risk receive different priorities under EquiRisk because their *expected outcomes* differ. This is not an equity override — it is a more accurate risk assessment.

---

## What This Repository Contains

This repository provides a **Conceptual Model Design Documentation for Simulation (CMDDS)** for EquiRisk-FoodDeserts — an integrated framework combining:

- **EquiRisk** — equity-aware risk stratification integrating individual clinical risk, neighborhood contextual vulnerability, and action feasibility into a multiplicative priority score (with trust barriers, uptake probability, and cultural appropriateness as first-class variables)
- **PAPO** — policy-aware personalized opportunity framework translating risk signals into personalized, constraint-aware intervention pathways

Together they operationalize equity as a **proactive decision rule** with **community-validated halt thresholds** and **mandatory pre-deployment bias and community gates** — not a retrospective reporting metric.

### Repository Files

| File | Version | Description |
|---|---|---|
| `CMDDS_EquiRisk_FoodDeserts_v1.3.md` | 1.3 | **Full simulation specification — the anchor document (updated v1.3)** |
| `FORK_SIMULATION_SUGGESTIONS.md` | 1.2 | 18 modular projects from beginner to advanced (v1.3 update pending) |
| `CONTRIBUTING.md` | 1.2 | How to fork, implement, and contribute (v1.3 update pending) |
| `LICENSE.md` | 1.2 | CC BY 4.0 license with attribution requirements |
| `README.md` | 1.3 | This file |

> **Note on companion documents:** The CMDDS is the authoritative specification and is current at v1.3. The supporting documents above will be brought to v1.3 alignment in subsequent commits. Forks targeting v1.3 implementation should follow the CMDDS specifications even where the older companion documents differ.

---

## The Integrated Framework

EquiRisk-FoodDeserts operates as a two-phase decision system:

```
PHASE 1 — EquiRisk: WHO needs help, and what are their constraints?
    ├── Layer 1: Individual Clinical Risk (HbA1c, complications, adherence)
    │           → clinical_risk_score, normalized [0,1]
    │
    ├── Layer 2: Contextual Vulnerability (food desert, ADI, SVI, transport,
    │                                       housing, clinic density, social support)
    │           → Contextual Vulnerability Index (CVI), normalized [0,1]    (v1.3)
    │           → Contextual Vulnerability Multiplier (CVM) = (1 + CVI)     (v1.3)
    │
    └── Layer 3: Action Feasibility (mobility, income, literacy, trust,
                                      time, cultural fit, uptake probability)
                → action_feasibility_weight, normalized [0,1]
                                  │
                                  ▼
              EquiRisk Priority (multiplicative, v1.3):
                  Priority = clinical_risk_score × (1 + CVI) × feasibility_weight
                  Priority range: [0, 2]
                  → Tier Assignment (Tier 1–4, updated ranges in v1.3)

PHASE 2 — PAPO: WHAT intervention is feasible, and HOW is it delivered?
    ├── Policy Trigger (program activation, eligibility)
    ├── Opportunity Matching (resource pool query + trust + cultural fit checks)
    ├── Feasibility Check (eight boundary condition categories, BC-1–BC-8) (v1.3)
    ├── Opportunity Ranking (multi-criteria selection, includes cultural fit) (v1.3)
    ├── Contact Probability Assessment (explicit reachability modeling)
    ├── Uptake Probability Check (post-contact completion probability)        (v1.3)
    ├── NULL Output (type-coded; required when no feasible option exists)
    └── Personalized Pathway (intervention + delivery + navigation)
                                  │
                                  ▼
              Equity Audit Layer + Equity Halt Threshold              (v1.3)
              Vulnerable Population Floor + Stigma Sentinel           (v1.3)
              Bias Loop-Breaking + Cumulative Drift Detection         (v1.3)
```

### Why Multiplicative, Not Additive *(v1.3)*

The case report (#004-M, MOKG-PH analysis) found that the additive composite used in v1.0–v1.2 conflated two distinct concepts: allocation weighting (who gets resources) and effective risk adjustment (whose expected burden is higher). The multiplicative form `Clinical × (1 + CVI) × Feasibility` separates them. The CVM term `(1 + CVI)` raises the priority of contextually vulnerable patients because their probability of acting on a standard recommendation is lower — meaning their expected unmanaged disease burden is higher. The feasibility term then attenuates the priority where no feasible pathway exists, which is what triggers escalation rather than continued queueing.

This single-formula clarity is the core change in v1.3.

### EquiRisk Tier Definitions *(updated v1.3 for the [0, 2] multiplicative range)*

Composite EquiRisk priority scores are classified into tiers for prioritization and reporting:

| Tier | Priority Range | Interpretation |
|---|---|---|
| Tier 1 — Critical | ≥ 1.20 | High clinical risk amplified by high contextual vulnerability, with feasible pathway; immediate priority |
| Tier 2 — High | 0.70 – 1.19 | Elevated combined effective risk; standard priority queue |
| Tier 3 — Moderate | 0.30 – 0.69 | Moderate combined effective risk; matched as resources allow |
| Tier 4 — Low | < 0.30 | Low effective risk OR low feasibility (review whether feasibility is the binding constraint) |

> **Special case — feasibility = 0:** A priority score of 0 produced by `feasibility_weight = 0` (i.e., no feasible pathway) is *not* the same as low effective risk. These cases must produce a NULL output and trigger escalation, not be filed as Tier 4.

### Eight Boundary Condition Categories *(BC-8 added v1.3)*

A core contribution of this CMDDS is the explicit specification of feasibility boundary conditions — the real-world constraints that determine whether an intervention can actually reach a patient and be successfully completed:

| Category | Examples |
|---|---|
| BC-1 Geographic | Distance, transit access, delivery zone |
| BC-2 Economic | Food cost vs. budget, insurance, program eligibility |
| BC-3 Physical/Mobility | Homebound status, ADA access, technology access |
| BC-4 Temporal | Appointment availability, operating hours, enrollment periods |
| BC-5 Cognitive/Communication | Language barriers, health literacy, cognitive capacity |
| BC-6 System/Policy | Resource pool exhaustion, authorization delays, data gaps |
| BC-7 Trust and Engagement *(added v1.1)* | Historical distrust, prior negative system experiences, provider trust deficits |
| **BC-8 Cultural Appropriateness** *(added v1.3)* | **Culturally inappropriate interventions, dietary conflicts with cultural or religious practices, generic-not-tailored programs** |

When a hard boundary condition is violated and no alternative exists, the system outputs **NULL** (type-coded as `no_opportunity`, `unreachable`, `trust_barrier`, `cultural_mismatch`, or `low_uptake`) and escalates to a human case manager. Silent failure is not permitted.

### Key v1.3 Additions

| Addition | Location | What It Specifies |
|---|---|---|
| Multiplicative priority formula | CMDDS Step 2 | `Clinical × (1 + CVI) × Feasibility`; replaces v1.2 additive composite |
| Contextual Vulnerability Index (CVI) | CMDDS Step 2 | Eight-component weighted composite of Layer 2 attributes; community-calibrated weights |
| Uptake Probability | CMDDS Step 2, Step 4 | Post-contact intervention completion probability; default model with mobility/income/literacy/cultural-fit modifiers |
| BC-8 Cultural Appropriateness | CMDDS Step 3 | Hard and soft boundaries for cultural fit; ties to BC-7 trust |
| Bias Injection Protocol | CMDDS Step 16 | Five-step pre-deployment procedure with disparity delta thresholds (< 10% APPROVED, 10–20% CONDITIONAL, ≥ 20% BLOCKED) |
| Community Co-Design Requirement | CMDDS Step 17 | Five-question framework with named decision authority; deployment gate |
| Equity Halt Threshold | CMDDS Step 7 | Default ≥ 0.70 of equity-weighted expected receipt rate; halt and resumption logic |
| Bias Loop-Breaking Constraint | CMDDS Step 4 | Stage 2 outputs cannot re-enter Stage 1 training data without governance approval and bias re-injection |
| Cumulative Tactical Drift Detection | CMDDS Step 4 | Rolling window monitoring (N=50 quarterly / N=100 continuous); alerts on stratum-level patterns |
| Stigma Sentinel | CMDDS Step 7 | NLP scan of human-facing output text for stigmatizing language |
| Vulnerable Population Floor | CMDDS Step 7 | Minimum priority floor for doubly-vulnerable strata, applied at queue ordering |
| Updated tier ranges | CMDDS Step 2 | Tier boundaries recalibrated for the [0, 2] multiplicative priority scale |
| Updated worked example | CMDDS Step 12 | Reproducible multiplicative arithmetic; additive comparison; floor and supported-feasibility scenarios |

---

## What This Repository Is (and Is Not)

### This repository provides:
- Complete CMDDS v1.3 specification for EquiRisk-FoodDeserts
- Multiplicative priority formula `Clinical × (1 + CVI) × Feasibility` *(v1.3)*
- Integrated EquiRisk + PAPO logic with trust barriers and cultural appropriateness as first-class variables
- Eight boundary condition categories with hard and soft boundaries *(BC-8 added v1.3)*
- Contextual Vulnerability Index (CVI) and Uptake Probability specifications *(v1.3)*
- Bias Injection Protocol — required pre-deployment procedure *(v1.3)*
- Community Co-Design Requirement — required pre-deployment gate *(v1.3)*
- Equity Halt Threshold with halt and resumption logic *(v1.3)*
- Bias Loop-Breaking Constraint and Cumulative Tactical Drift Detection *(v1.3)*
- Stigma Sentinel and Vulnerable Population Floor guardrails *(v1.3)*
- Agent state transition rules with re-entry limits and cycling safeguards
- EquiRisk tier definitions with default priority ranges *(updated v1.3)*
- Opportunity ranking criteria for multi-opportunity selection *(updated v1.3)*
- Default contact success probability model
- Default uptake probability model *(added v1.3)*
- Default HbA1c trajectory model
- Equity Audit Layer specification with timing, triggers, and alert thresholds
- Synthetic population generation guidance
- Data privacy, ethics, and IRB considerations
- Sub-score normalization guidance for all composite scores
- NULL output type-coding specification (five types as of v1.3)
- Multi-scale architecture: individual, neighborhood, and city
- Simulation time step and scheduling specification
- 18 modular simulation projects from beginner to advanced (v1.3 project additions pending)
- Step 11 Simulation Validation Checklist (updated v1.3 with pre-deployment gate items)
- Step 12 Milwaukee Reference Scenario (updated v1.3 for multiplicative scoring)
- Step 13 Known Limitations and Open Research Questions (updated v1.3)
- Global adaptation guide for non-US cities (updated v1.3 with community co-design requirements)

### This repository does NOT provide:
- Executable simulation code
- City-specific parameter values
- Clinical prediction models
- Predictive or prescriptive outputs
- Autonomous decision-making logic

> ⚠️ This is a conceptual specification, not a runnable implementation. Simulations built from this CMDDS are exploratory and comparative, not predictive or prescriptive. Per v1.3, simulations intended for deployment must complete the Bias Injection Protocol (Step 16) and Community Co-Design (Step 17) before Stage 2 routing begins.

---

## Getting Started — Choose Your Entry Point

### If you are new to simulation:
Start with **Project S1: Grocery Store Access Mapper Under Inflation** — a spatial analysis project requiring only basic Python or spreadsheet skills. Or try **Project S4: Trust Barrier Contact Analysis** — a standalone BC-7 project requiring no spatial modeling. **Project S5: State Transition Validator** lets you verify agent lifecycle logic with minimal code. See `FORK_SIMULATION_SUGGESTIONS.md`.

### If you are an intermediate Python user:
Start with **Project I1: Grocery Store Closure Simulation** or **Project I4: Seasonal Food Access — Summer Heat + Diabetes**. For trust-focused work, try **Project I5: Dynamic Trust Modeling**. **Project I6: Contact Success Model Calibration** tests the contact probability model against outreach scenarios. These require GeoPandas and basic agent modeling.

### If you are an experienced ABM researcher:
Start with **Project A1: Full Milwaukee Reference Implementation** — the complete EquiRisk-PAPO system for the reference city. Or **Project A4: Trust-Adjusted Prioritization Comparative Study** to evaluate prioritization rules including the new multiplicative form.

### If you are a Global South researcher:
See **Project A3: Global South Fork** and the Global Adaptation Guide in the CMDDS. The framework is explicitly designed for cities with informal food systems, limited data infrastructure, locally defined trust barrier contexts, and locally defined cultural fit reference groups *(v1.3)*.

### If you want to test the v1.3 multiplicative formula directly:
A new starter project is recommended for v1.3 implementations: **Additive vs. Multiplicative Comparison** — re-score the same population under the v1.2 additive composite and the v1.3 multiplicative formula; report ranking divergence by demographic group. This is a recommended first project for any v1.3 fork because it builds intuition for how the formula change affects priority distributions. (To be added to `FORK_SIMULATION_SUGGESTIONS.md` in the v1.3 update.)

---

## Modular Projects Overview

See `FORK_SIMULATION_SUGGESTIONS.md` for full details on all 18 projects.

| Code | Project | Tier | Key Theme |
|---|---|---|---|
| S1 | Grocery Store Access Mapper Under Inflation | Starter | Inflation + food access |
| S2 | EquiRisk Scoring Comparison | Starter | Framework validation |
| S3 | Food Pharmacy Capacity Stress Test | Starter | Resource scarcity |
| S4 | Trust Barrier Contact Analysis | Starter | BC-7 trust barriers |
| S5 | State Transition Validator | Starter | Agent lifecycle logic |
| I1 | Grocery Store Closure Simulation | Intermediate | Store closures + inflation |
| I2 | CHW Routing Under Resource Scarcity | Intermediate | Care navigation equity |
| I3 | Telehealth Access Gap Analysis | Intermediate | Digital divide |
| I4 | Seasonal Food Access — Heat + Diabetes | Intermediate | Climate + food + health |
| I5 | Dynamic Trust Modeling | Intermediate | Trust as evolving variable |
| I6 | Contact Success Model Calibration | Intermediate | Reachability modeling |
| A1 | Full Milwaukee Simulation | Advanced | Reference implementation |
| A2 | Inflation Shock Resilience | Advanced | System stress testing |
| A3 | Global South Fork | Advanced | International adaptation |
| A4 | Trust-Adjusted Prioritization Study | Advanced | Trust-aware routing |
| E1 | Multi-City Comparative Study | Extended | Lancet Digital Health |
| E2 | Longitudinal Policy Impact | Extended | Health Affairs |
| E3 | EquiRisk + Heatwave Integration | Extended | Nature Climate Change |

> **v1.3 project additions pending:** Several v1.3 capabilities — multiplicative-vs-additive comparison, CVI weight sensitivity, Bias Injection Protocol execution, Equity Halt Threshold simulation, drift detection testing, and uptake probability calibration — are recommended as new modular projects. These will be added to `FORK_SIMULATION_SUGGESTIONS.md` in a subsequent commit. Forks may begin implementing them now using the CMDDS v1.3 specification as the source of truth.

---

## How to Fork This Repository

1. Read the full CMDDS (`CMDDS_EquiRisk_FoodDeserts_v1.3.md`)
2. Choose a project from `FORK_SIMULATION_SUGGESTIONS.md` (or propose a new v1.3-aligned project)
3. Fork this repository
4. Name your fork: `EquiRisk-FoodDeserts-[YourCity]-[ProjectCode]`
5. Implement the required components per CMDDS v1.3, including:
   - Multiplicative priority formula `Clinical × (1 + CVI) × Feasibility`
   - All eight boundary condition categories (minimum: BC-1, BC-3, BC-7, BC-8)
   - Type-coded NULL output (five types)
   - Bias loop-breaking constraint
   - Cumulative tactical drift detection
6. **For deployment-track implementations** *(v1.3)*: Complete the Bias Injection Protocol (CMDDS Step 16) and Community Co-Design (CMDDS Step 17) before activating Stage 2 routing.
7. Complete the Step 11 Simulation Validation Checklist before reporting results
8. Document your assumptions and any deviations clearly
9. Share your results and link back to this repository

See `CONTRIBUTING.md` for full guidance.

---

## Co-Authorship Invitation

Researchers who implement a valid EquiRisk-FoodDeserts simulation and share their results are invited to discuss **co-authorship** on the planned multi-city comparative analysis paper targeting *Lancet Digital Health* or *American Journal of Public Health*.

To be considered, v1.3 implementations must:
- Implement the multiplicative priority formula `Clinical × (1 + CVI) × Feasibility` *(v1.3)*
- Implement all required CMDDS v1.3 components, including BC-7, BC-8, contact success modeling, uptake probability modeling, state transition enforcement, opportunity ranking, bias loop-breaking constraint, and cumulative tactical drift detection
- Complete the Bias Injection Protocol (Step 16) and report disparity delta values *(v1.3)*
- Document Community Co-Design inputs OR explicitly justify use of default values for testing-only implementations *(v1.3)*
- Complete the Step 11 Simulation Validation Checklist (v1.3)
- Report at least one equity metric disaggregated by demographic group
- Compare at least two prioritization rules (clinical-only vs. EquiRisk-multiplicative is the minimum required comparison)
- Document assumptions clearly
- Report any halt threshold breach events and their resolutions *(v1.3)*

> **Forks built on v1.0–v1.2 are still welcome to participate** but should re-score their populations under the v1.3 multiplicative formula before submitting results for the comparative analysis. The CMDDS v1.3 includes a worked example showing both formulas applied to the same agents, which can serve as a reference.

Contact via GitHub: https://github.com/Min-PH

---

## Related Repositories

| Repository | Description |
|---|---|
| [PAPO-Heatwave-AI](https://github.com/Min-PH/PAPO-Heatwave-AI) | PAPO framework applied to heatwave response — the companion repo |

Project I4 and Project E3 in this repository explicitly bridge both frameworks.

---

## Related Publications

- **EquiRisk SSRN Preprint:** Wu, M. (2026). EquiRisk: Operationalizing Equity-Aware Risk Stratification for Diabetes Management in Food Deserts. https://ssrn.com/abstract=6150926
- **PAPO SSRN Preprint:** Wu, M. (2026). PAPO: A Policy-Aware Personalized Opportunity Framework for Heatwave Public Health Interventions. https://ssrn.com/abstract=6198260
- **Springer Textbook:** Wu, M. (2026). *Artificial Intelligence in Public Health*. Springer Nature. ISBN 978-3032158710.
- **EquiRisk Case Report (#004-M):** Wu, M. (2026). MOKG-PH Analytical Case Analysis for Diabetes in Food Deserts. Internal case report, MOKG-PH program. *(Source of v1.3 structural revisions.)*

---

## Suggested Reading Before Forking

- USDA Food Access Research Atlas: https://www.ers.usda.gov/data-products/food-access-research-atlas/
- CDC Social Vulnerability Index: https://www.atsdr.cdc.gov/place-health/php/svi/index.html
- Neighborhood Atlas (ADI): https://www.neighborhoodatlas.medicine.wisc.edu/
- HHS-HCC Risk Adjustment Model: https://www.cms.gov/medicare/payment/medicare-advantage-rates-statistics/risk-adjustment
- USDA Food Desert Locator: https://www.ers.usda.gov/data-products/food-access-research-atlas/go-to-the-atlas/

---

## Citation

Please cite the EquiRisk SSRN preprint and this repository when publishing derived work:

> Wu, M. (2026). CMDDS for EquiRisk-FoodDeserts v1.3 — Integrated Simulation Framework for Equity-Aware Diabetes Care Navigation in Food Deserts. GitHub. https://github.com/Min-PH/EquiRisk-FoodDeserts. DOI: https://doi.org/10.5281/zenodo.19271682

> Wu, M. (2026). EquiRisk: Operationalizing Equity-Aware Risk Stratification for Diabetes Management in Food Deserts. SSRN. https://ssrn.com/abstract=6150926

---

## About

CMDDS for EquiRisk-FoodDeserts: an integrated, equity-aware simulation specification for diabetes care navigation in food desert settings. Equity as a proactive decision rule, not a retrospective report. Contextual vulnerability adjusts effective risk, not just allocation (v1.3 multiplicative formulation). Trust as a structural variable, not an individual failing. Cultural fit as a community-validated boundary, not a checkbox. Bias injection and community co-design as deployment gates, not optional enhancements. Fork to model care access equity in your city.
