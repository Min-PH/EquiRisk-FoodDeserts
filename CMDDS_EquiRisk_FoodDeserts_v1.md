# CMDDS — EquiRisk-FoodDeserts

## Conceptual Model Design Documentation for Simulation (CMDDS)

**Version:** 1.0  
**Date:** 2026-03-17  
**Author:** Min Wu, PhD  
**Affiliation:** Zilber College of Public Health, University of Wisconsin-Milwaukee  
**GitHub:** https://github.com/Min-PH/EquiRisk-FoodDeserts

**Cite this CMDDS:**
> Wu, M. (2026). CMDDS for EquiRisk-FoodDeserts v1.0 — Integrated Simulation Framework for Equity-Aware Diabetes Care Navigation in Food Deserts. GitHub. https://github.com/Min-PH/EquiRisk-FoodDeserts

**Related Works:**
> Wu, M. (2026). *Artificial Intelligence in Public Health*. Springer Nature. ISBN 978-3032158710.  
> Wu, M. (2026). EquiRisk: Operationalizing Equity-Aware Risk Stratification for Diabetes Management in Food Deserts. SSRN. https://ssrn.com/abstract=6150926  
> Wu, M. (2026). PAPO: A Policy-Aware Personalized Opportunity Framework for Heatwave Public Health Interventions. SSRN. https://ssrn.com/abstract=6198260  
> Wu, M. (2026). CMDDS for PAPO-Heatwaves v1.1. GitHub. https://github.com/Min-PH/PAPO-Heatwave-AI

---

## Overview

This repository contains the Conceptual Model Design Documentation for Simulation (CMDDS) for **EquiRisk-FoodDeserts** — an integrated simulation framework combining:

- **EquiRisk** — equity-aware risk stratification integrating individual clinical risk, neighborhood contextual vulnerability, and action feasibility into a unified proactive decision rule
- **PAPO** — policy-aware personalized opportunity framework translating policy triggers and EquiRisk outputs into personalized, constraint-aware intervention pathways

Applied together to **diabetes management in food deserts**, this integrated framework addresses a critical failure in traditional public health practice:

> *Risk is identified, but interventions do not reach the people who need them most — because structural barriers, feasibility constraints, and equity considerations are ignored in the decision logic.*

### The Central Shift This Framework Makes

| Traditional Approach | EquiRisk-FoodDeserts Approach |
|---|---|
| "Who has the highest clinical risk?" | "Who has the highest combined risk AND the greatest barriers AND can be reached by a feasible intervention now?" |
| Equity as retrospective reporting | Equity as proactive decision rule |
| Clinical indicators only | Clinical + neighborhood + feasibility integrated |
| Intervention assumed feasible | Feasibility explicitly evaluated and bounded |
| Human effort drives coordination | AI-enabled, policy-constrained coordination with human oversight |
| Risk identification | Risk → actionable personalized pathway |

### Design Philosophy

1. **Equity is a decision rule, not a report** — equity considerations are embedded in the prioritization logic from the start
2. **Feasibility is non-negotiable** — interventions are only recommended if they are reachable by the patient given real constraints; NULL output is required when no feasible option exists
3. **Human oversight is preserved** — the framework is a decision-support system; all consequential actions require human authorization at defined handover points
4. **Global adaptability** — core logic is universal; context-specific parameters are locally defined per fork
5. **Transparency and auditability** — every decision pathway must be explainable and auditable

---

## Integrated Framework Architecture: EquiRisk + PAPO

The integration of EquiRisk and PAPO creates a two-phase decision system:

```
PHASE 1 — EquiRisk: WHO needs help most, and what are their constraints?
    │
    ├── Layer 1: Individual Clinical Risk
    │         (HbA1c, complications, medication adherence)
    │
    ├── Layer 2: Contextual Vulnerability
    │         (food desert status, ADI, SVI, transport, housing)
    │
    └── Layer 3: Action Feasibility
              (mobility, income, literacy, program availability)
                    │
                    ▼
             EquiRisk Score (composite)
             + Feasibility Profile (what constraints apply)
                    │
                    ▼
PHASE 2 — PAPO: WHAT intervention is feasible, and HOW is it delivered?
    │
    ├── Policy Trigger
    │         (program activation, eligibility confirmation)
    │
    ├── Opportunity Engine
    │         (match EquiRisk profile → available resources)
    │
    ├── Feasibility Check
    │         (can this person actually access this opportunity?)
    │
    ├── NULL Output Handler
    │         (if no feasible opportunity → escalate to human)
    │
    └── Personalized Pathway Output
              (specific intervention + delivery mode + timing)
                    │
                    ▼
             Equity Audit Layer
             (did the system reach the right people equitably?)
```

### Why Integration Matters

EquiRisk alone answers: *"Who should we prioritize?"*  
PAPO alone answers: *"What opportunities exist and who qualifies?"*  
Together they answer: *"Who needs help most, what can realistically reach them, and did the system deliver equitably?"*

Neither framework is complete without the other for operational deployment. EquiRisk without PAPO produces prioritized lists with no delivery mechanism. PAPO without EquiRisk delivers opportunities without equity-aware targeting.

---

## What This Repository Is (and Is Not)

### This repository provides:
- Complete CMDDS for EquiRisk-FoodDeserts v1.0
- Full integrated EquiRisk + PAPO logic specification
- Explicit boundary conditions for action feasibility
- Multi-scale simulation specification (individual, neighborhood, city)
- Required components for a valid simulation implementation
- Equity metrics, prioritization rules, and governance requirements
- Global adaptation guidance

### This repository does NOT provide:
- Executable simulation code
- City-specific parameter values
- Clinical prediction models or diagnostic tools
- Predictive or prescriptive outputs
- Autonomous decision-making logic

> ⚠️ Simulations built from this CMDDS are **exploratory and comparative**, not predictive or prescriptive. Outputs must not be used as clinical recommendations or policy mandates without independent validation.

---

## Step 1 — System Purpose and Simulation Questions

### System Purpose

EquiRisk-FoodDeserts simulates how a public health system identifies diabetic individuals in food desert settings, stratifies them using the three-layer EquiRisk logic, matches them with feasible care and food access opportunities via PAPO, and delivers personalized intervention pathways — measuring equity outcomes across prioritization rules and resource conditions.

### Primary Simulation Questions

**Equity Questions:**
- How does EquiRisk-based prioritization change the distribution of interventions across income, race, and neighborhood deprivation groups compared to clinical-risk-only approaches?
- Which prioritization rule minimizes the equity gap between the most and least advantaged populations?
- Where do opportunity deserts — areas with high EquiRisk scores but no feasible opportunities — concentrate geographically?
- What proportion of high-EquiRisk individuals receive a NULL output, and how does this vary by demographic group?

**Feasibility Questions:**
- How does action feasibility scoring change which individuals receive interventions compared to need-based scoring alone?
- At what resource capacity level does the system begin producing NULL outputs for high-priority individuals?
- Which feasibility constraint (transport, distance, cost, literacy, time) is most binding across the population?

**Policy Questions:**
- How does the timing of policy trigger activation affect equity outcomes?
- Which resource types — food support, CHW visits, telehealth, transportation — produce the greatest equity improvement per unit of investment?
- What happens to equity outcomes when resource pools are reduced by 20%, 40%, or 60%?

**System Performance Questions:**
- What is the mean time from EquiRisk scoring to opportunity delivery for the highest-priority individuals?
- How does the tactical feedback loop (real-time reallocation) improve outcomes compared to a static allocation model?
- How does injecting historical service bias into opportunity ranking affect equity outcomes?

### Modular Simulation Projects

Developers may implement one focused component rather than the full system:

- **EquiRisk scoring validation** — implement the three-layer scoring logic and test against hypothetical patient profiles
- **Food desert opportunity mapping** — model resource pool availability and geographic accessibility
- **NULL output analysis** — identify which populations most frequently receive NULL outputs and why
- **Prioritization rule comparison** — compare clinical-only vs. EquiRisk-weighted prioritization equity outcomes
- **Tactical vs. static allocation** — compare real-time reallocation to fixed assignment models
- **Bias injection test** — train opportunity ranker on historically biased data and compare with fairness-constrained version

---

## Step 2 — Conceptual Entities, Attributes, and States

### Entity 1: Individual Patient (Agent)

Each simulated individual is a diabetic patient living in or near a food desert.

**Clinical Risk Attributes (EquiRisk Layer 1):**
| Attribute | Description | Data Source |
|---|---|---|
| `hba1c_level` | Glycated hemoglobin — primary clinical risk indicator | HHS-HCC risk adjustment model |
| `complication_count` | Number of active diabetes complications | Clinical records (synthetic) |
| `medication_adherence` | Rate of medication adherence (0–1) | Pharmacy claims (synthetic) |
| `comorbidity_score` | Burden of co-occurring conditions | HHS-HCC model |
| `clinical_risk_score` | Composite of above — Layer 1 output | Derived |

**Contextual Vulnerability Attributes (EquiRisk Layer 2):**
| Attribute | Description | Data Source |
|---|---|---|
| `food_desert_status` | USDA food desert designation (binary) | USDA Food Access Research Atlas |
| `area_deprivation_index` | Neighborhood disadvantage score | Neighborhood Atlas, UW-Madison |
| `social_vulnerability_index` | CDC/ATSDR SVI score for census tract | CDC SVI |
| `nearest_grocery_distance` | Distance to nearest qualifying grocery store (miles) | USDA / OpenStreetMap |
| `transit_score` | Public transit accessibility index (0–1) | GTFS data / OpenStreetMap |
| `housing_stability` | Stable / unstable / homeless | American Community Survey (synthetic) |
| `neighborhood_clinic_density` | FQHCs and clinics per 10,000 residents | HRSA data |
| `contextual_vulnerability_score` | Composite of above — Layer 2 output | Derived |

**Action Feasibility Attributes (EquiRisk Layer 3):**
| Attribute | Description | Data Source |
|---|---|---|
| `mobility_score` | 1=fully mobile, 2=limited, 3=homebound | Synthetic (age/disability weighted) |
| `has_transport` | Access to personal vehicle (boolean) | ACS car ownership data |
| `income_quartile` | Household income quartile (1–4) | ACS census tract data |
| `health_literacy_score` | Ability to navigate health system (1–3) | Synthetic (education weighted) |
| `time_availability` | Availability for scheduled appointments (low/medium/high) | Synthetic |
| `insurance_status` | Insured / underinsured / uninsured | ACS / Medicaid enrollment data |
| `language_barrier` | Primary language not English (boolean) | ACS language data |
| `program_eligibility` | Current eligibility for active programs | Policy layer |
| `action_feasibility_score` | Composite of above — Layer 3 output | Derived |

**Composite EquiRisk Score:**
```
EquiRisk_Score = w1 * clinical_risk_score
               + w2 * contextual_vulnerability_score
               + w3 * (1 - action_feasibility_score)

Where w1 + w2 + w3 = 1
Default weights: w1=0.4, w2=0.35, w3=0.25
Weights are stress-test targets — simulations should compare at least two weight configurations
```

**Agent States:**
- `unidentified` — not yet reached by the system
- `identified` — EquiRisk scored, awaiting opportunity matching
- `matched` — assigned to a feasible opportunity
- `in_pathway` — actively receiving intervention
- `escalated` — NULL output received, referred to human case manager
- `lost_to_followup` — dropped out of pathway
- `stabilized` — HbA1c improved to target range

---

### Entity 2: Opportunity Resource Pool

Resources are exhaustible, spatially located, and replenished over defined time cycles.

**Food Access Opportunities:**
| Resource Type | Attributes | Replenishment Cycle |
|---|---|---|
| Grocery store slot | Location, healthy food availability score, cost level | Daily |
| Food pharmacy | Location, prescription capacity, eligibility rules | Weekly |
| Community Supported Agriculture (CSA) box | Pickup location, subscription slots, cost | Weekly |
| Food pantry | Location, capacity, operating hours, eligibility | Weekly |
| Medically tailored meal delivery | Delivery zone, weekly slot capacity, eligibility | Weekly |

**Care Access Opportunities:**
| Resource Type | Attributes | Replenishment Cycle |
|---|---|---|
| FQHC appointment slot | Location, capacity, language support, sliding scale | Daily |
| Telehealth appointment | Virtual, capacity, technology requirement | Daily |
| Community health worker visit | CHW assignment zone, caseload capacity | Weekly |
| Diabetes self-management class | Location, session capacity, language, transport req. | Monthly |
| Pharmacy consultation | Location, pharmacist availability, insurance accepted | Daily |

**Transportation Opportunities:**
| Resource Type | Attributes | Replenishment Cycle |
|---|---|---|
| Medical transport voucher | Coverage zone, trip capacity, advance booking required | Weekly |
| Volunteer driver | Coverage zone, availability schedule | Ad hoc |
| Transit pass subsidy | Coverage area, monthly capacity | Monthly |

> **v1.0 Requirement:** All resource pools must be modeled as exhaustible, spatially located, and replenished on defined cycles. Static or unlimited resource assumptions are not permitted in valid PAPO-EquiRisk implementations.

---

### Entity 3: Policy and Institutional System

**Policy Triggers** — conditions that activate intervention programs:
| Trigger Type | Example | Scope |
|---|---|---|
| Clinical threshold | HbA1c > 8.0% flagged in registry | Individual |
| Population screening | Annual diabetes prevention program enrollment | Cohort |
| Geographic activation | Food desert zip code program launch | Neighborhood |
| Emergency activation | Heat event + diabetes complication surge | City |
| Funding cycle | Grant-funded program begins | City |

**Authorization Boundaries** — points where human oversight is required:
| Decision Point | Human Role Required |
|---|---|
| EquiRisk score override | Clinician or case manager review |
| NULL output escalation | Human case manager assignment |
| High-intensity resource allocation (CHW) | Supervisor authorization |
| Patient opt-out or refusal | Human acknowledgment and documentation |
| Data privacy exception | Privacy officer review |

---

### Entity 4: Environmental Context

| Attribute | Description |
|---|---|
| `food_desert_boundary` | USDA-defined food desert census tracts |
| `neighborhood_deprivation_map` | ADI and SVI scores by census tract |
| `resource_location_map` | Spatial coordinates of all opportunity resources |
| `transit_network` | Bus routes, stops, and schedules |
| `seasonal_variation` | Summer heat effects on mobility and food access |
| `policy_environment` | Active programs, eligibility rules, funding status |

---

## Step 3 — Action Feasibility: Boundary Conditions

> This section specifies the explicit boundary conditions that determine whether an opportunity is considered feasible for a given individual. These conditions are **non-negotiable** in valid implementations — an opportunity that violates any hard boundary condition must output NULL for that individual.

### Boundary Condition Categories

#### BC-1: Geographic Boundaries

| Condition | Hard Boundary | Soft Boundary (reducible by support) |
|---|---|---|
| Distance to opportunity | > 1 mile without transport = infeasible | 0.5–1 mile = reduced feasibility score |
| Transit accessibility | No transit route within 0.25 mile = infeasible without vehicle | Limited service = reduced score |
| Delivery zone | Outside delivery zone = infeasible for delivery services | Edge of zone = flag for manual review |
| Service area | Outside program service area = infeasible | Boundary case = escalate |

#### BC-2: Economic Boundaries

| Condition | Hard Boundary | Soft Boundary |
|---|---|---|
| Cost of food opportunity | Cost > 10% of weekly food budget = infeasible | Cost 5–10% = reduced feasibility |
| Insurance requirement | Uninsured + no sliding scale = infeasible for clinical services | Underinsured = reduced score |
| Program eligibility | Income above program threshold = ineligible | Near-threshold = flag for exception review |
| Transportation cost | Cannot afford transit fare = infeasible without subsidy | Fare burden > 5% income = reduced score |

#### BC-3: Physical and Mobility Boundaries

| Condition | Hard Boundary | Soft Boundary |
|---|---|---|
| Mobility | Homebound (score=3) = infeasible for all in-person non-delivery opportunities | Limited mobility (score=2) = reduced feasibility for distant opportunities |
| Physical accessibility | Facility not ADA compliant + mobility limitation = infeasible | Partial accessibility = reduced score |
| Technology access | No internet + no device = infeasible for telehealth | Shared device = reduced score |

#### BC-4: Temporal Boundaries

| Condition | Hard Boundary | Soft Boundary |
|---|---|---|
| Appointment availability | No slots within 14 days = NULL output triggered | 7–14 days = reduced urgency match |
| Operating hours | Facility hours incompatible with patient availability = infeasible | Partial overlap = reduced score |
| Advance booking | Cannot book required days ahead = infeasible | Short booking window = reduced score |
| Program enrollment period | Enrollment closed = infeasible | Open in < 30 days = flag for waitlist |

#### BC-5: Cognitive and Communication Boundaries

| Condition | Hard Boundary | Soft Boundary |
|---|---|---|
| Language | No language-concordant service available = infeasible for complex navigation | Interpreter available = reduced score |
| Health literacy | Low literacy + no navigation support available = infeasible for self-managed programs | Low literacy + CHW available = feasible with support |
| Cognitive capacity | Documented cognitive impairment + no caregiver support = infeasible for self-managed | Mild impairment + support = reduced score |

#### BC-6: System and Policy Boundaries

| Condition | Hard Boundary | Soft Boundary |
|---|---|---|
| Program capacity | Resource pool exhausted = NULL output required | < 10% capacity remaining = reduced match priority |
| Policy eligibility | Does not meet program eligibility criteria = infeasible | Borderline eligibility = escalate to human |
| Authorization delay | Required authorization > 48 hours for urgent need = NULL output + escalation | 24–48 hour delay = reduced urgency match |
| Data availability | Insufficient data to score EquiRisk = cannot match = escalate | Partial data = score with uncertainty flag |

### NULL Output Requirements

When any hard boundary condition is violated and no alternative opportunity exists:

```
NULL Output must:
1. Be explicitly recorded — not silently dropped
2. Identify which boundary condition triggered the NULL
3. Activate escalation pathway to human case manager
4. Record patient in waitlist or follow-up queue
5. Trigger tactical feedback loop for resource reallocation review
6. Be reported in equity metrics disaggregated by demographic group

NULL Output must NOT:
1. Assign a default low-quality opportunity to avoid NULL
2. Override hard boundary conditions algorithmically
3. Be resolved without human review for high-EquiRisk individuals
```

---

## Step 4 — PAPO Integration: Policy-to-Opportunity Translation Logic

### The Core Translation Mechanism

PAPO operates as the delivery engine that receives EquiRisk outputs and translates them into actionable pathways. The translation follows this logic:

```
INPUT:
  patient.EquiRisk_score
  patient.feasibility_profile (boundary conditions assessed)
  patient.program_eligibility
  
STEP 1 — Policy Trigger Check:
  Is there an active program this patient is eligible for?
  If NO → output NULL → escalate
  If YES → proceed to Step 2

STEP 2 — Opportunity Query:
  Query resource pools within feasible geographic range
  Filter by: mobility constraints, cost boundary, language, 
             hours, capacity availability
  
STEP 3 — Feasibility Check:
  Apply all BC-1 through BC-6 boundary conditions
  Score remaining opportunities by feasibility
  
STEP 4 — Opportunity Ranking:
  Rank feasible opportunities by selected prioritization rule
  (see prioritization rules below)
  
STEP 5 — Output:
  If feasible opportunities exist:
    → Assign top-ranked opportunity
    → Generate personalized pathway (resource + timing + navigation support)
    → Record assignment and reduce resource pool capacity
  
  If no feasible opportunity exists:
    → Output NULL
    → Trigger escalation pathway
    → Record NULL reason and boundary condition violated
    → Add to tactical feedback queue

STEP 6 — Human Handover:
  Pathway delivered to human staff for:
    → Patient notification and consent
    → Navigation support arrangement
    → Authorization where required
```

### Two Feedback Loops (Must Be Separated)

**Tactical Loop (minutes to hours) — Real-Time Reallocation:**
- Triggered by: NULL output, resource exhaustion, patient refusal, no-show
- Actions: Reallocate resource to next-priority patient, adjust capacity counts, flag bottlenecks
- Decision authority: Frontline staff or automated reallocation within pre-authorized rules
- Must NOT modify: prioritization rules, eligibility criteria, EquiRisk weights

**Strategic Loop (months) — Policy and Resource Update:**
- Triggered by: End of program cycle, equity audit findings, funding changes
- Actions: Update resource pool locations and capacities, adjust program eligibility rules, revise EquiRisk weights based on outcome data, add or remove opportunity types
- Decision authority: Program managers and policy staff only
- Must NOT: Operate on individual patient data in real time

> ⚠️ Conflation of tactical and strategic loops is not permitted in valid implementations. They operate on different timescales, involve different decision authorities, and modify different system components.

---

## Step 5 — Multi-Scale Simulation Architecture

### Individual Scale
- Each agent is scored by EquiRisk and matched (or not) by PAPO
- Tracks: opportunity received, time to intervention, pathway completion, HbA1c trajectory (simplified)
- Key output: individual equity outcome by demographic group

### Neighborhood Scale
- Aggregates individual outcomes by census tract
- Maps opportunity deserts: high-EquiRisk density + low opportunity availability
- Tracks: NULL output rate by neighborhood, resource utilization by facility
- Key output: neighborhood equity gap map

### City Scale
- Aggregates across all neighborhoods
- Evaluates policy trigger timing and city-wide resource allocation efficiency
- Tracks: overall equity gap, prioritization rule comparison, resource investment vs. equity return
- Key output: city-level equity audit report

### Scale Interaction Rules
- Individual agents draw from neighborhood-level resource pools
- Neighborhood resource depletion affects city-level allocation decisions
- City-level policy changes propagate down to neighborhood and individual eligibility
- Feedback loops operate within their authorized scale — tactical at individual/neighborhood, strategic at city

---

## Step 6 — Required Components for a Valid Implementation

Any fork claiming to implement EquiRisk-FoodDeserts must include:

| Component | Requirement |
|---|---|
| **Three-layer EquiRisk scoring** | All three layers (clinical, contextual, feasibility) must be implemented and scored separately before combination |
| **Composite EquiRisk score** | Must use explicit, reported weights; default weights are a stress-test target |
| **Exhaustible resource pools** | All opportunity types must be capacity-constrained and spatially located |
| **Boundary condition evaluation** | At minimum BC-1 (geographic) and BC-3 (mobility) must be implemented; all six are recommended |
| **NULL output with escalation** | NULL output is required when no feasible opportunity exists; silent failure is not permitted |
| **Separated feedback loops** | Tactical and strategic loops must be distinct; conflation invalidates the implementation |
| **Prioritization rule comparison** | At minimum two rules must be compared: clinical-risk-only vs. EquiRisk-weighted |
| **Equity metric** | At minimum one equity metric must be defined before simulation and reported disaggregated by group |
| **Human handover specification** | Authorization boundaries must be explicitly defined |

### Strongly Recommended Enhancements
- Bias injection: train opportunity ranker on historically biased data and compare with fairness-constrained version
- Sensitivity analysis: vary EquiRisk weights and boundary condition thresholds
- Scenario comparison: high-resource vs. low-resource city conditions
- Global context fork: implement in a non-US city with different food system and policy environment

---

## Step 7 — Equity Metrics

Choose at least one equity metric before simulation. Report results disaggregated by race, income quartile, and neighborhood deprivation level.

| Metric | Definition | When to Use |
|---|---|---|
| **Equal allocation** | Each group receives interventions proportional to group size | Baseline comparison |
| **Equal outcomes** | Each group achieves equivalent HbA1c improvement | Equity goal metric |
| **Prioritizing** | Higher-need groups receive disproportionately more resources | When equity gap reduction is primary goal |
| **Sufficiency** | Each group receives enough to meet a defined minimum threshold | When minimum standard of care is the policy goal |

**Required equity outputs:**
- Opportunity receipt rate by race, income quartile, neighborhood ADI quartile
- NULL output rate by the same demographic dimensions
- Time to first intervention by EquiRisk tier
- Equity gap = difference in opportunity rate between highest and lowest access groups
- Equity gap change under each prioritization rule

---

## Step 8 — Prioritization Rules

Implement and compare at least two of the following:

| Rule | Logic | Expected Equity Effect |
|---|---|---|
| **Clinical risk only** | Rank by clinical_risk_score alone | Baseline — likely favors less disadvantaged patients |
| **EquiRisk weighted** | Rank by composite EquiRisk_score | Primary equity improvement rule |
| **Worst-off first** | Rank by contextual_vulnerability_score | Maximum equity focus |
| **Feasibility first** | Rank by action_feasibility_score (easiest to reach first) | Efficiency-oriented — likely worsens equity |
| **Random** | Random assignment within eligibility | Equity neutrality baseline |

> The comparison between clinical-risk-only and EquiRisk-weighted is the minimum required comparison. This directly operationalizes the central argument of the EquiRisk paper.

---

## Step 9 — Assumptions

These assumptions simplify real-world complexity. Simulations should stress-test them, not validate them.

| Assumption | Why It Fails in Reality | Recommended Stress Test |
|---|---|---|
| EquiRisk data is complete and accurate | Data is fragmented, incomplete, or biased toward easier-to-reach populations | Inject missing data scenarios; compare imputed vs. complete data |
| Policy is machine-readable | Policies contain discretion, ambiguity, and inter-agency conflict | Introduce policy conflict scenarios |
| A feasible opportunity always exists | Resources are frequently exhausted; geography may preclude any viable option | Run under 50%, 30%, 20% resource availability |
| Human handover is timely | Authorization delays, staff shortages, and liability concerns are common | Model 24-hour, 48-hour, and 1-week handover delays |
| Patients are reachable once identified | Contact failure, refusal, and distrust are common especially in underserved populations | Model 20%, 40% contact failure rates |
| Food desert boundaries are stable | Food access changes seasonally and with store openings/closures | Model dynamic food desert boundaries |
| EquiRisk weights are valid | Optimal weights vary by city, population, and season | Sensitivity analysis across weight configurations |
| Resources are uniformly distributed within service areas | Resources cluster in accessible areas, leaving hardest-to-reach patients underserved | Inject spatial clustering of resources |

> ⚠️ Failure to model these assumptions will produce optimistic, non-generalizable results.

---

## Step 10 — Global Adaptation Guide

EquiRisk-FoodDeserts is designed to be forked for any city globally. The core logic is preserved across all forks. What changes per city:

### What Stays the Same (Core Logic — Do Not Modify)
- Three-layer EquiRisk scoring architecture
- PAPO policy-to-opportunity translation mechanism
- NULL output requirement
- Separated feedback loops
- Human handover requirements
- Equity metric reporting requirements

### What Changes Per City (Context Parameters)

| Parameter | US Context (Milwaukee) | Global South Example | High-Income Non-US |
|---|---|---|---|
| Food desert definition | USDA LILA criteria | Informal market access, 30-min walk threshold | National food access index |
| Deprivation index | ADI / SVI | Local deprivation composite | National deprivation index |
| Clinical risk source | HHS-HCC / EHR | Community health record, CHW assessment | National health registry |
| Opportunity types | FQHC, food pharmacy, CSA | Community health post, market voucher, CHW | GP practice, food voucher scheme |
| Policy trigger | Medicaid program, DPP enrollment | National diabetes program, NGO activation | National health service protocol |
| Transport model | Bus/car ownership | Walking distance, moto-taxi, rickshaw | Public transit, cycling |
| Language dimension | English + Spanish dominant | Local language + dialect diversity | National language policy |

### Minimum Adaptation Requirements for Non-US Forks
1. Replace ADI/SVI with locally available deprivation index
2. Redefine food desert boundary criteria for local food system
3. Specify locally available opportunity types
4. Identify relevant policy trigger mechanisms
5. Define locally appropriate equity dimensions
6. Document all substitutions clearly in fork README

---

## Candidate Cities for Forking

This framework is well-suited for cities with:
- Significant diabetic population with food insecurity overlap
- Neighborhood-level data availability
- Active diabetes management programs to simulate

### US Cities
- Milwaukee, WI (reference implementation)
- Chicago, IL
- Detroit, MI
- Memphis, TN
- Houston, TX
- Philadelphia, PA

### International Cities
- Karachi, Pakistan
- Lagos, Nigeria
- Chennai, India
- São Paulo, Brazil
- Nairobi, Kenya
- Manila, Philippines

---

## Changelog

- **v1.0** — Initial release. Integrated EquiRisk + PAPO framework. Defines three-layer EquiRisk scoring, PAPO translation logic, six boundary condition categories, multi-scale architecture, required components, equity metrics, prioritization rules, assumptions, and global adaptation guide.

---

## License and Attribution

Please cite both the EquiRisk SSRN preprint and this CMDDS when publishing derived simulations or analyses. See LICENSE for details.

## About

CMDDS for EquiRisk-FoodDeserts: an integrated, equity-aware simulation specification for diabetes care navigation in food desert settings. Fork to model care access equity in your city.
