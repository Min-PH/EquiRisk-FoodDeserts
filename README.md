# EquiRisk-FoodDeserts

## Equity-Aware Diabetes Care Navigation in Food Deserts
### An Integrated PAPO + EquiRisk Simulation Framework

**Version:** 1.2
**Date:** 2026-03-23
**Author:** Min Wu, PhD
**Affiliation:** Zilber College of Public Health, University of Wisconsin-Milwaukee
**GitHub:** https://github.com/Min-PH/EquiRisk-FoodDeserts

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19228063.svg)](https://doi.org/10.5281/zenodo.19228063)

---

## Changelog

- **v1.0** — Initial release. EquiRisk + PAPO integration, six boundary condition categories (BC-1–BC-6), 13 modular projects, global adaptation guide.
- **v1.1** — Added BC-7 (Trust and Engagement Boundaries) as a first-class boundary condition. Added `trust_barrier` as a Layer 3 attribute. Added three new modular projects (S4, I5, A4). Added Step 11 Simulation Validation Checklist, Step 12 Milwaukee Reference Scenario, and Step 13 Known Limitations and Open Research Questions to CMDDS. Added sub-score normalization guidance. Added NULL output type-coding requirement. Updated all repository files to v1.1.
- **v1.2** — Added agent state transition rules with permitted transitions table and re-entry logic. Added simulation time step and scheduling specification. Added EquiRisk tier definitions (Tier 1–4 with default score ranges). Added opportunity ranking criteria for multi-opportunity selection. Added default contact success probability model. Added default HbA1c trajectory model. Added Equity Audit Layer specification with timing, triggers, and alert thresholds. Added synthetic population generation guidance (CMDDS Step 14). Added data privacy, ethics, and IRB considerations (CMDDS Step 15). Corrected worked example arithmetic (Step 12). Added two new modular projects (S5, I6). Updated all repository files to v1.2.

---

## The Problem This Framework Addresses

Diabetes risk stratification has a critical failure mode: it identifies who is at risk but ignores whether interventions can actually reach them.

In food desert settings, a patient with high HbA1c may receive the same care recommendation as a patient with identical clinical indicators but full food access, transportation, and economic stability. Traditional approaches assume interventions are feasible. In food deserts, they frequently are not. And even when interventions are available and reachable, patients with histories of system failure, denial, or disrespect may never be successfully contacted — a barrier that is structural, not personal.

**EquiRisk-FoodDeserts addresses this by asking a different question:**

> *"Who is at highest combined risk, faces the greatest structural barriers — including trust barriers — and can be reached by a feasible intervention right now?"*

This shift — from risk identification to equity-aware action — is the central contribution of this framework.

---

## What This Repository Contains

This repository provides a **Conceptual Model Design Documentation for Simulation (CMDDS)** for EquiRisk-FoodDeserts — an integrated framework combining:

- **EquiRisk** — equity-aware risk stratification integrating individual clinical risk, neighborhood contextual vulnerability, and action feasibility (including trust barriers as of v1.1)
- **PAPO** — policy-aware personalized opportunity framework translating risk signals into personalized, constraint-aware intervention pathways

Together they operationalize equity as a **proactive decision rule**, not a retrospective reporting metric.

### Repository Files

| File | Version | Description |
|---|---|---|
| `CMDDS_EquiRisk_FoodDeserts_v1.2.md` | 1.2 | Full simulation specification — the anchor document |
| `FORK_SIMULATION_SUGGESTIONS.md` | 1.2 | 18 modular projects from beginner to advanced |
| `DESIGN_REFLECTION.md` | 1.2 | Author's reflection on the design process and human-AI collaboration |
| `CONTRIBUTING.md` | 1.2 | How to fork, implement, and contribute |
| `LICENSE.md` | 1.2 | CC BY 4.0 license with attribution requirements |
| `README.md` | 1.2 | This file |

---

## The Integrated Framework

EquiRisk-FoodDeserts operates as a two-phase decision system:

```
PHASE 1 — EquiRisk: WHO needs help, and what are their constraints?
    ├── Layer 1: Individual Clinical Risk (HbA1c, complications, adherence)
    ├── Layer 2: Contextual Vulnerability (food desert, ADI, SVI, transport)
    └── Layer 3: Action Feasibility (mobility, income, literacy, trust, time)
                        │
                        ▼
                 EquiRisk Composite Score
                 (sub-scores normalized to [0,1] before weighting)
                 → Tier Assignment (Tier 1–4) (v1.2)

PHASE 2 — PAPO: WHAT intervention is feasible, and HOW is it delivered?
    ├── Policy Trigger (program activation, eligibility)
    ├── Opportunity Matching (resource pool query + trust alignment check)
    ├── Feasibility Check (seven boundary condition categories, BC-1–BC-7)
    ├── Opportunity Ranking (multi-criteria selection when multiple options exist) (v1.2)
    ├── Contact Probability Assessment (explicit reachability modeling) (v1.2)
    ├── NULL Output (type-coded; required when no feasible option exists)
    └── Personalized Pathway (intervention + delivery + navigation)
                        │
                        ▼
                 Equity Audit Layer
                 (periodic review with defined triggers and alert thresholds) (v1.2)
```

### EquiRisk Tier Definitions *(added v1.2)*

Composite EquiRisk scores are classified into tiers for prioritization and reporting:

| Tier | Score Range | Interpretation |
|---|---|---|
| Tier 1 — Critical | ≥ 0.75 | Immediate priority; escalate if unmatched within one scheduling cycle |
| Tier 2 — High | 0.50 – 0.74 | Standard priority queue |
| Tier 3 — Moderate | 0.25 – 0.49 | Matched as resources allow |
| Tier 4 — Low | < 0.25 | Monitored; matched in surplus conditions |

### Seven Boundary Condition Categories (v1.1)

A core contribution of this CMDDS is the explicit specification of feasibility boundary conditions — the real-world constraints that determine whether an intervention can actually reach a patient:

| Category | Examples |
|---|---|
| BC-1 Geographic | Distance, transit access, delivery zone |
| BC-2 Economic | Food cost vs. budget, insurance, program eligibility |
| BC-3 Physical/Mobility | Homebound status, ADA access, technology access |
| BC-4 Temporal | Appointment availability, operating hours, enrollment periods |
| BC-5 Cognitive/Communication | Language barriers, health literacy, cognitive capacity |
| BC-6 System/Policy | Resource pool exhaustion, authorization delays, data gaps |
| **BC-7 Trust and Engagement** *(added v1.1)* | **Historical distrust, prior negative system experiences, provider trust deficits** |

When a hard boundary condition is violated and no alternative exists, the system outputs **NULL** (type-coded as `no_opportunity`, `unreachable`, or `trust_barrier`) and escalates to a human case manager. Silent failure is not permitted.

### Key v1.2 Additions

| Addition | Location | What It Specifies |
|---|---|---|
| Agent state transition rules | CMDDS Step 2 | Permitted transitions, re-entry limits, cycling safeguards |
| Simulation time step | CMDDS Step 5 | Daily base tick, scheduling cycle, event timing |
| EquiRisk tiers | CMDDS Step 2 | Four-tier classification with default score ranges |
| Opportunity ranking | CMDDS Step 4 | Five-criterion weighted composite for multi-opportunity selection |
| Contact success model | CMDDS Step 4 | Multiplicative probability model with trust, housing, language, time modifiers |
| HbA1c trajectory model | CMDDS Step 5 | Linear improvement/regression with intervention intensity and adherence |
| Equity Audit Layer | CMDDS Step 7 | Timing, triggers, seven required outputs, alert thresholds, governance |
| Synthetic population guidance | CMDDS Step 14 | Spatial scaffold, conditional attribute assignment, correlation targets |
| Data privacy and ethics | CMDDS Step 15 | IRB requirements, synthetic data bias, stigmatization safeguards |
| Corrected worked example | CMDDS Step 12 | Reproducible arithmetic, contact probability walkthrough, HbA1c projection |

---

## What This Repository Is (and Is Not)

### This repository provides:
- Complete CMDDS v1.2 specification for EquiRisk-FoodDeserts
- Integrated EquiRisk + PAPO logic with trust barriers as a first-class variable
- Seven boundary condition categories with hard and soft boundaries
- Agent state transition rules with re-entry limits and cycling safeguards *(added v1.2)*
- EquiRisk tier definitions with default score ranges *(added v1.2)*
- Opportunity ranking criteria for multi-opportunity selection *(added v1.2)*
- Default contact success probability model *(added v1.2)*
- Default HbA1c trajectory model *(added v1.2)*
- Equity Audit Layer specification with timing, triggers, and alert thresholds *(added v1.2)*
- Synthetic population generation guidance *(added v1.2)*
- Data privacy, ethics, and IRB considerations *(added v1.2)*
- Sub-score normalization guidance for the composite EquiRisk score
- NULL output type-coding specification
- Multi-scale architecture: individual, neighborhood, and city
- Simulation time step and scheduling specification *(added v1.2)*
- 18 modular simulation projects from beginner to advanced
- Step 11 Simulation Validation Checklist (updated v1.2)
- Step 12 Milwaukee Reference Scenario (corrected v1.2)
- Step 13 Known Limitations and Open Research Questions (updated v1.2)
- Global adaptation guide for non-US cities

### This repository does NOT provide:
- Executable simulation code
- City-specific parameter values
- Clinical prediction models
- Predictive or prescriptive outputs
- Autonomous decision-making logic

> ⚠️ This is a conceptual specification, not a runnable implementation. Simulations built from this CMDDS are exploratory and comparative, not predictive or prescriptive.

---

## Getting Started — Choose Your Entry Point

### If you are new to simulation:
Start with **Project S1: Grocery Store Access Mapper Under Inflation** — a spatial analysis project requiring only basic Python or spreadsheet skills. Or try **Project S4: Trust Barrier Contact Analysis** — a standalone BC-7 project requiring no spatial modeling. New in v1.2: **Project S5: State Transition Validator** lets you verify agent lifecycle logic with minimal code. See `FORK_SIMULATION_SUGGESTIONS.md`.

### If you are an intermediate Python user:
Start with **Project I1: Grocery Store Closure Simulation** or **Project I4: Seasonal Food Access — Summer Heat + Diabetes**. For trust-focused work, try **Project I5: Dynamic Trust Modeling**. New in v1.2: **Project I6: Contact Success Model Calibration** tests the contact probability model against outreach scenarios. These require GeoPandas and basic agent modeling.

### If you are an experienced ABM researcher:
Start with **Project A1: Full Milwaukee Reference Implementation** — the complete EquiRisk-PAPO system for the reference city. Or **Project A4: Trust-Adjusted Prioritization Comparative Study** to evaluate all six prioritization rules including the new trust-adjusted rule.

### If you are a Global South researcher:
See **Project A3: Global South Fork** and the Global Adaptation Guide in the CMDDS. The framework is explicitly designed for cities with informal food systems, limited data infrastructure, and locally defined trust barrier contexts.

---

## Modular Projects Overview

See `FORK_SIMULATION_SUGGESTIONS.md` for full details on all 18 projects.

| Code | Project | Tier | Key Theme |
|---|---|---|---|
| S1 | Grocery Store Access Mapper Under Inflation | Starter | Inflation + food access |
| S2 | EquiRisk Scoring Comparison | Starter | Framework validation |
| S3 | Food Pharmacy Capacity Stress Test | Starter | Resource scarcity |
| S4 | Trust Barrier Contact Analysis | Starter | BC-7 trust barriers |
| **S5** | **State Transition Validator** | **Starter** | **Agent lifecycle logic** |
| I1 | Grocery Store Closure Simulation | Intermediate | Store closures + inflation |
| I2 | CHW Routing Under Resource Scarcity | Intermediate | Care navigation equity |
| I3 | Telehealth Access Gap Analysis | Intermediate | Digital divide |
| I4 | Seasonal Food Access — Heat + Diabetes | Intermediate | Climate + food + health |
| I5 | Dynamic Trust Modeling | Intermediate | Trust as evolving variable |
| **I6** | **Contact Success Model Calibration** | **Intermediate** | **Reachability modeling** |
| A1 | Full Milwaukee Simulation | Advanced | Reference implementation |
| A2 | Inflation Shock Resilience | Advanced | System stress testing |
| A3 | Global South Fork | Advanced | International adaptation |
| A4 | Trust-Adjusted Prioritization Study | Advanced | Trust-aware routing |
| E1 | Multi-City Comparative Study | Extended | Lancet Digital Health |
| E2 | Longitudinal Policy Impact | Extended | Health Affairs |
| E3 | EquiRisk + Heatwave Integration | Extended | Nature Climate Change |

*Bold rows are new in v1.2.*

---

## How to Fork This Repository

1. Read the full CMDDS (`CMDDS_EquiRisk_FoodDeserts_v1.2.md`)
2. Choose a project from `FORK_SIMULATION_SUGGESTIONS.md`
3. Fork this repository
4. Name your fork: `EquiRisk-FoodDeserts-[YourCity]-[ProjectCode]`
5. Implement the required components per the CMDDS v1.2
6. Complete the Step 11 Simulation Validation Checklist before reporting results
7. Document your assumptions and any deviations clearly
8. Share your results and link back to this repository

See `CONTRIBUTING.md` for full guidance.

---

## Co-Authorship Invitation

Researchers who implement a valid EquiRisk-FoodDeserts simulation and share their results are invited to discuss **co-authorship** on the planned multi-city comparative analysis paper targeting *Lancet Digital Health* or *American Journal of Public Health*.

To be considered, implementations must:
- Implement all required CMDDS v1.2 components (including BC-7, contact success modeling, state transition enforcement, and opportunity ranking)
- Complete the Step 11 Simulation Validation Checklist (v1.2)
- Report at least one equity metric disaggregated by demographic group
- Compare at least two prioritization rules
- Document assumptions clearly

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

> Wu, M. (2026). CMDDS for EquiRisk-FoodDeserts v1.2 — Integrated Simulation Framework for Equity-Aware Diabetes Care Navigation in Food Deserts. GitHub. https://github.com/Min-PH/EquiRisk-FoodDeserts. DOI: https://doi.org/10.5281/zenodo.19228063

> Wu, M. (2026). EquiRisk: Operationalizing Equity-Aware Risk Stratification for Diabetes Management in Food Deserts. SSRN. https://ssrn.com/abstract=6150926

---

## About

CMDDS for EquiRisk-FoodDeserts: an integrated, equity-aware simulation specification for diabetes care navigation in food desert settings. Equity as a proactive decision rule, not a retrospective report. Trust as a structural variable, not an individual failing. Fork to model care access equity in your city.
