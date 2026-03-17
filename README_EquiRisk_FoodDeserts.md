# EquiRisk-FoodDeserts

## Equity-Aware Diabetes Care Navigation in Food Deserts
### An Integrated PAPO + EquiRisk Simulation Framework

**Version:** 1.0  
**Date:** 2026-03-17  
**Author:** Min Wu, PhD  
**Affiliation:** Zilber College of Public Health, University of Wisconsin-Milwaukee  
**GitHub:** https://github.com/Min-PH/EquiRisk-FoodDeserts

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

---

## The Problem This Framework Addresses

Diabetes risk stratification has a critical failure mode: it identifies who is at risk but ignores whether interventions can actually reach them.

In food desert settings, a patient with high HbA1c may receive the same care recommendation as a patient with identical clinical indicators but full food access, transportation, and economic stability. Traditional approaches assume interventions are feasible. In food deserts, they frequently are not.

**EquiRisk-FoodDeserts addresses this by asking a different question:**

> *"Who is at highest combined risk, faces the greatest structural barriers, and can be reached by a feasible intervention right now?"*

This shift — from risk identification to equity-aware action — is the central contribution of this framework.

---

## What This Repository Contains

This repository provides a **Conceptual Model Design Documentation for Simulation (CMDDS)** for EquiRisk-FoodDeserts — an integrated framework combining:

- **EquiRisk** — equity-aware risk stratification integrating individual clinical risk, neighborhood contextual vulnerability, and action feasibility
- **PAPO** — policy-aware personalized opportunity framework translating risk signals into personalized, constraint-aware intervention pathways

Together they operationalize equity as a **proactive decision rule**, not a retrospective reporting metric.

### Repository Files

| File | Description |
|---|---|
| `CMDDS_EquiRisk_FoodDeserts_v1.md` | Full simulation specification — the anchor document |
| `FORK_SIMULATION_SUGGESTIONS.md` | 13 modular projects from beginner to advanced |
| `CONTRIBUTING.md` | How to fork, implement, and contribute |
| `LICENSE.md` | CC BY 4.0 license with attribution requirements |
| `README.md` | This file |

---

## The Integrated Framework

EquiRisk-FoodDeserts operates as a two-phase decision system:

```
PHASE 1 — EquiRisk: WHO needs help, and what are their constraints?
    ├── Layer 1: Individual Clinical Risk (HbA1c, complications, adherence)
    ├── Layer 2: Contextual Vulnerability (food desert, ADI, SVI, transport)
    └── Layer 3: Action Feasibility (mobility, income, literacy, time)
                        │
                        ▼
                 EquiRisk Composite Score

PHASE 2 — PAPO: WHAT intervention is feasible, and HOW is it delivered?
    ├── Policy Trigger (program activation, eligibility)
    ├── Opportunity Matching (resource pool query)
    ├── Feasibility Check (six boundary condition categories)
    ├── NULL Output (required when no feasible option exists)
    └── Personalized Pathway (intervention + delivery + navigation)
                        │
                        ▼
                 Equity Audit Output
```

### Six Boundary Condition Categories

A core contribution of this CMDDS is the explicit specification of feasibility boundary conditions — the real-world constraints that determine whether an intervention can actually reach a patient:

| Category | Examples |
|---|---|
| BC-1 Geographic | Distance, transit access, delivery zone |
| BC-2 Economic | Food cost vs. budget, insurance, program eligibility |
| BC-3 Physical/Mobility | Homebound status, ADA access, technology access |
| BC-4 Temporal | Appointment availability, operating hours, enrollment periods |
| BC-5 Cognitive/Communication | Language barriers, health literacy, cognitive capacity |
| BC-6 System/Policy | Resource pool exhaustion, authorization delays, data gaps |

When a hard boundary condition is violated and no alternative exists, the system outputs **NULL** and escalates to a human case manager. Silent failure is not permitted.

---

## What This Repository Is (and Is Not)

### This repository provides:
- Complete CMDDS specification for EquiRisk-FoodDeserts
- Integrated EquiRisk + PAPO logic
- Six boundary condition categories with hard and soft boundaries
- Multi-scale architecture: individual, neighborhood, and city
- 13 modular simulation projects from beginner to advanced
- Global adaptation guide for non-US cities
- Equity metrics, prioritization rules, and governance requirements

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
Start with **Project S1: Grocery Store Access Mapper Under Inflation** — a spatial analysis project requiring only basic Python or spreadsheet skills. See `FORK_SIMULATION_SUGGESTIONS.md`.

### If you are an intermediate Python user:
Start with **Project I1: Grocery Store Closure Simulation Under Inflation** or **Project I4: Seasonal Food Access — Summer Heat + Diabetes**. These require GeoPandas and basic agent modeling.

### If you are an experienced ABM researcher:
Start with **Project A1: Full Milwaukee Reference Implementation** — the complete EquiRisk-PAPO system for the reference city.

### If you are a Global South researcher:
See **Project A3: Global South Fork** and the Global Adaptation Guide in the CMDDS. The framework is explicitly designed for cities with informal food systems and limited data infrastructure.

---

## Modular Projects Overview

See `FORK_SIMULATION_SUGGESTIONS.md` for full details on all 13 projects.

| Code | Project | Tier | Key Theme |
|---|---|---|---|
| S1 | Grocery Store Access Mapper Under Inflation | Starter | Inflation + food access |
| S2 | EquiRisk Scoring Comparison | Starter | Framework validation |
| S3 | Food Pharmacy Capacity Stress Test | Starter | Resource scarcity |
| I1 | Grocery Store Closure Simulation | Intermediate | Store closures + inflation |
| I2 | CHW Routing Under Resource Scarcity | Intermediate | Care navigation equity |
| I3 | Telehealth Access Gap Analysis | Intermediate | Digital divide |
| I4 | Seasonal Food Access — Heat + Diabetes | Intermediate | Climate + food + health |
| A1 | Full Milwaukee Simulation | Advanced | Reference implementation |
| A2 | Inflation Shock Resilience | Advanced | System stress testing |
| A3 | Global South Fork | Advanced | International adaptation |
| E1 | Multi-City Comparative Study | Extended | Lancet Digital Health |
| E2 | Longitudinal Policy Impact | Extended | Health Affairs |
| E3 | EquiRisk + Heatwave Integration | Extended | Nature Climate Change |

---

## How to Fork This Repository

1. Read the full CMDDS (`CMDDS_EquiRisk_FoodDeserts_v1.md`)
2. Choose a project from `FORK_SIMULATION_SUGGESTIONS.md`
3. Fork this repository
4. Name your fork: `EquiRisk-FoodDeserts-[YourCity]-[ProjectCode]`
5. Implement the required components per the CMDDS
6. Document your assumptions and any deviations clearly
7. Share your results and link back to this repository

See `CONTRIBUTING.md` for full guidance.

---

## Co-Authorship Invitation

Researchers who implement a valid EquiRisk-FoodDeserts simulation and share their results are invited to discuss **co-authorship** on the planned multi-city comparative analysis paper targeting *Lancet Digital Health* or *American Journal of Public Health*.

To be considered, implementations must:
- Implement all required CMDDS components
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

> Wu, M. (2026). CMDDS for EquiRisk-FoodDeserts v1.0 — Integrated Simulation Framework for Equity-Aware Diabetes Care Navigation in Food Deserts. GitHub. https://github.com/Min-PH/EquiRisk-FoodDeserts

> Wu, M. (2026). EquiRisk: Operationalizing Equity-Aware Risk Stratification for Diabetes Management in Food Deserts. SSRN. https://ssrn.com/abstract=6150926

---

## About

CMDDS for EquiRisk-FoodDeserts: an integrated, equity-aware simulation specification for diabetes care navigation in food desert settings. Equity as a proactive decision rule, not a retrospective report. Fork to model care access equity in your city.
