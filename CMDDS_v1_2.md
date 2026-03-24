# CMDDS — EquiRisk-FoodDeserts

## Conceptual Model Design Documentation for Simulation (CMDDS)

**Version:** 1.2
**Date:** 2026-03-23
**Author:** Min Wu, PhD
**Affiliation:** Zilber College of Public Health, University of Wisconsin-Milwaukee
**GitHub:** https://github.com/Min-PH/EquiRisk-FoodDeserts

**Cite this CMDDS:**
> Wu, M. (2026). CMDDS for EquiRisk-FoodDeserts v1.2 — Integrated Simulation Framework for Equity-Aware Diabetes Care Navigation in Food Deserts. GitHub. https://github.com/Min-PH/EquiRisk-FoodDeserts

**Related Works:**
> Wu, M. (2026). *Artificial Intelligence in Public Health*. Springer Nature. ISBN 978-3032158710.
> Wu, M. (2026). EquiRisk: Operationalizing Equity-Aware Risk Stratification for Diabetes Management in Food Deserts. SSRN. https://ssrn.com/abstract=6150926
> Wu, M. (2026). PAPO: A Policy-Aware Personalized Opportunity Framework for Heatwave Public Health Interventions. SSRN. https://ssrn.com/abstract=6198260
> Wu, M. (2026). CMDDS for PAPO-Heatwaves v1.1. GitHub. https://github.com/Min-PH/PAPO-Heatwave-AI

---

## Changelog

- **v1.0** — Initial release. Integrated EquiRisk + PAPO framework. Defines three-layer EquiRisk scoring, PAPO translation logic, six boundary condition categories, multi-scale architecture, required components, equity metrics, prioritization rules, assumptions, and global adaptation guide.
- **v1.1** — Added Step 11 (Simulation Validation Checklist), Step 12 (Worked Example: Milwaukee Reference Scenario), and Step 13 (Known Limitations and Open Research Questions). Expanded composite EquiRisk score specification with sub-score normalization guidance. Added `trust_barrier` attribute to Entity 1. Added BC-7 (Trust and Engagement Boundaries). Clarified NULL output escalation protocol. Added recommended modular simulation project: trust barrier analysis. Added equity metric: Contact Success Rate. Expanded candidate cities section with readiness criteria. Minor clarifications throughout.
- **v1.2** — Added agent state transition rules with permitted transitions table and re-entry logic (Step 2). Added simulation time step and scheduling specification (Step 5). Added EquiRisk tier definitions with default score ranges (Step 2). Added opportunity ranking criteria within PAPO Step 4 for multi-opportunity selection (Step 4). Added synthetic population generation guidance (Step 14). Added default contact success probability model (Step 4). Added default HbA1c trajectory specification (Step 5). Added Equity Audit Layer specification with timing, triggers, and required outputs (Step 7). Added data privacy, ethics, and IRB considerations (Step 15). Corrected worked example arithmetic with fully reproducible EquiRisk score calculations (Step 12). Added new validation checklist items for v1.2 additions. Added two new open research questions. Minor clarifications throughout.

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
| Contact assumed successful | Contact success modeled explicitly; trust barriers assessed |

### Design Philosophy

1. **Equity is a decision rule, not a report** — equity considerations are embedded in the prioritization logic from the start
2. **Feasibility is non-negotiable** — interventions are only recommended if they are reachable by the patient given real constraints; NULL output is required when no feasible option exists
3. **Human oversight is preserved** — the framework is a decision-support system; all consequential actions require human authorization at defined handover points
4. **Global adaptability** — core logic is universal; context-specific parameters are locally defined per fork
5. **Transparency and auditability** — every decision pathway must be explainable and auditable
6. **Trust is a structural variable** — patient distrust and prior negative system experiences are modeled as a boundary condition, not an individual failing

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
              (mobility, income, literacy, trust, program availability)
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
             (see Step 7 — Equity Audit Layer Specification)
```

### Why Integration Matters

EquiRisk alone answers: *"Who should we prioritize?"*
PAPO alone answers: *"What opportunities exist and who qualifies?"*
Together they answer: *"Who needs help most, what can realistically reach them, and did the system deliver equitably?"*

Neither framework is complete without the other for operational deployment. EquiRisk without PAPO produces prioritized lists with no delivery mechanism. PAPO without EquiRisk delivers opportunities without equity-aware targeting.

---

## What This Repository Is (and Is Not)

### This repository provides:
- Complete CMDDS for EquiRisk-FoodDeserts v1.2
- Full integrated EquiRisk + PAPO logic specification
- Explicit boundary conditions for action feasibility (including trust barriers)
- Multi-scale simulation specification (individual, neighborhood, city)
- Required components for a valid simulation implementation
- Equity metrics, prioritization rules, and governance requirements
- Agent state transition rules and simulation scheduling specification *(added v1.2)*
- EquiRisk tier definitions *(added v1.2)*
- Opportunity ranking criteria for multi-opportunity selection *(added v1.2)*
- Contact success probability model specification *(added v1.2)*
- HbA1c trajectory model specification *(added v1.2)*
- Equity Audit Layer specification with timing and triggers *(added v1.2)*
- Synthetic population generation guidance (Step 14) *(added v1.2)*
- Data privacy, ethics, and IRB considerations (Step 15) *(added v1.2)*
- Simulation validation checklist (Step 11)
- Worked reference scenario: Milwaukee (Step 12) — corrected v1.2
- Known limitations and open research questions (Step 13)
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
- How does modeling trust barriers change the equity profile of intervention receipt?

**Feasibility Questions:**
- How does action feasibility scoring change which individuals receive interventions compared to need-based scoring alone?
- At what resource capacity level does the system begin producing NULL outputs for high-priority individuals?
- Which feasibility constraint (transport, distance, cost, literacy, trust, time) is most binding across the population?

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
- **Trust barrier analysis** — model how historical distrust and prior negative system experiences affect contact success rates and equity outcomes *(added v1.1)*
- **Contact success modeling** — implement the contact probability model and test sensitivity to trust barrier and demographic parameters *(added v1.2)*

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
| `trust_barrier` | Prior negative system experience or documented distrust (low/moderate/high) *(added v1.1)* | Synthetic (race, prior denial history weighted) |
| `action_feasibility_score` | Composite of above — Layer 3 output | Derived |

**Composite EquiRisk Score:**
```
EquiRisk_Score = w1 * clinical_risk_score_norm
               + w2 * contextual_vulnerability_score_norm
               + w3 * (1 - action_feasibility_score_norm)

Where w1 + w2 + w3 = 1
Default weights: w1=0.4, w2=0.35, w3=0.25
Weights are stress-test targets — simulations should compare at least two weight configurations

Sub-score normalization (v1.1 guidance):
  All sub-scores must be normalized to [0,1] before applying weights.
  Min-max normalization within the simulated population is the default method.
  Document the normalization method used; do not mix normalized and raw scores.
  Sensitivity analysis should test z-score normalization as an alternative.
```

**EquiRisk Tier Definitions** *(added v1.2)*:

Composite EquiRisk scores are classified into tiers for prioritization and reporting. Default tier boundaries are provided below. Forks may adjust boundaries with justification, but must document and apply them consistently.

| Tier | Score Range | Interpretation | Prioritization Implication |
|---|---|---|---|
| Tier 1 — Critical | ≥ 0.75 | High combined risk, high vulnerability, low feasibility | Immediate priority; escalate if no feasible opportunity within one scheduling cycle |
| Tier 2 — High | 0.50 – 0.74 | Elevated combined risk | Standard priority queue; match within two scheduling cycles |
| Tier 3 — Moderate | 0.25 – 0.49 | Moderate combined risk | Matched as resources allow |
| Tier 4 — Low | < 0.25 | Lower combined risk, higher feasibility | Monitored; matched in surplus resource conditions |

> Tier boundaries are default starting points for implementation testing, not empirically calibrated thresholds. Sensitivity analysis should test alternative cutpoints (e.g., tertiles, quintiles) and report how tier assignment shifts under different normalization methods and weight configurations.

**Agent States:**
- `unidentified` — not yet reached by the system
- `identified` — EquiRisk scored, awaiting opportunity matching
- `matched` — assigned to a feasible opportunity
- `contact_attempted` — outreach initiated; contact not yet confirmed *(added v1.1)*
- `contact_failed` — outreach attempted but patient unreachable or refused *(added v1.1)*
- `in_pathway` — actively receiving intervention
- `escalated` — NULL output received, referred to human case manager
- `lost_to_followup` — dropped out of pathway
- `stabilized` — HbA1c improved to target range

**Agent State Transition Rules** *(added v1.2)*:

The following table specifies all permitted state transitions. Any transition not listed is prohibited. Each transition has a triggering condition and, where applicable, a maximum number of permitted re-entries to prevent infinite cycling.

| From State | To State | Trigger | Max Re-entries | Notes |
|---|---|---|---|---|
| `unidentified` | `identified` | System screening or registry flag | — | Entry point; irreversible once scored |
| `identified` | `matched` | PAPO opportunity engine assigns feasible opportunity | — | |
| `identified` | `escalated` | NULL output — no feasible opportunity found | — | |
| `matched` | `contact_attempted` | Outreach initiated by staff or system | — | |
| `contact_attempted` | `in_pathway` | Patient confirms and begins intervention | — | |
| `contact_attempted` | `contact_failed` | No response after defined outreach window, or patient refuses | — | |
| `contact_failed` | `matched` | Re-matched to alternative opportunity (different resource or delivery mode) | 2 | After max re-entries → `escalated` |
| `contact_failed` | `escalated` | Max re-match attempts exhausted or human review determines escalation | — | |
| `in_pathway` | `stabilized` | HbA1c reaches target range and maintained for defined observation period | — | |
| `in_pathway` | `lost_to_followup` | No engagement for defined dropout window (default: 60 days) | — | |
| `lost_to_followup` | `identified` | Re-screening or human case manager re-activation | 1 | After max re-entry → `escalated`; re-entry resets EquiRisk score |
| `escalated` | `identified` | Human case manager resolves barrier and re-activates | 1 | Requires documented resolution; re-entry resets EquiRisk score |
| `stabilized` | `identified` | HbA1c regression above threshold during monitoring period | 1 | Re-entry triggers new EquiRisk scoring |

```
State Transition Diagram (simplified):

  unidentified → identified → matched → contact_attempted → in_pathway → stabilized
                     ↑            ↑              │                │            │
                     │            │              ▼                │            │
                     │            └── contact_failed              │            │
                     │                     │                      │            │
                     │                     ▼                      ▼            │
                     └──────────── escalated ←──────── lost_to_followup       │
                     │                                                        │
                     └────────────────────────────────────────────────────────┘
                                    (re-entry with new EquiRisk scoring)
```

> **Re-entry safeguard:** All re-entry transitions require a new EquiRisk score calculation at the time of re-entry. The prior score is archived for longitudinal tracking but does not carry forward. Maximum re-entry counts are enforced per agent per simulation run; exceeding the limit forces transition to `escalated`.

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

> **v1.1 Requirement:** All resource pools must be modeled as exhaustible, spatially located, and replenished on defined cycles. Static or unlimited resource assumptions are not permitted in valid EquiRisk-PAPO implementations. Resource pool attributes should include a `trust_alignment` flag indicating whether the provider has a known trust deficit with specific community groups, which affects the effective feasibility score for matched individuals.

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
| Trust barrier flag — high severity | Cultural liaison or trusted community organization referral *(added v1.1)* |
| Agent re-entry from `escalated` or `lost_to_followup` | Human case manager authorization with documented barrier resolution *(added v1.2)* |

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
| `historical_service_bias_map` | Census-tract-level record of historical underservice or program exclusions *(added v1.1)* |

---

## Step 3 — Action Feasibility: Boundary Conditions

> This section specifies the explicit boundary conditions that determine whether an opportunity is considered feasible for a given individual. These conditions are **non-negotiable** in valid implementations — an opportunity that violates any hard boundary condition must output NULL for that individual.

### Boundary Condition Categories

#### BC-1: Geographic Boundaries

| Condition | Hard Boundary | Soft Boundary (reducible by support) |
|---|---|---|
| Distance to opportunity | > 2 miles without transport = infeasible | 1–2 miles without transport = reduced feasibility |
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

#### BC-7: Trust and Engagement Boundaries *(added v1.1)*

> Trust is a structural barrier shaped by historical exclusion, prior negative experiences, and systemic racism in healthcare. It is modeled here as a system-level constraint, not an individual character trait.

| Condition | Hard Boundary | Soft Boundary |
|---|---|---|
| High trust barrier + no trusted community referral pathway | Infeasible for initial outreach without cultural liaison or community organization intermediary | Moderate trust barrier = reduced contact success probability; CHW with community ties preferred |
| Provider has documented trust deficit with patient's community | Direct provider referral = infeasible; community intermediary required | Known trust gap = flag for trust-aligned opportunity matching |
| Prior documented refusal due to negative system experience | Direct re-contact = infeasible without new pathway or trusted intermediary | Prior reluctance = reduced contact success probability; extended outreach window |

### NULL Output Requirements

When any hard boundary condition is violated and no alternative opportunity exists:

```
NULL Output must:
1. Be explicitly recorded — not silently dropped
2. Identify which boundary condition(s) triggered the NULL
3. Activate escalation pathway to human case manager
4. Record patient in waitlist or follow-up queue
5. Trigger tactical feedback loop for resource reallocation review
6. Be reported in equity metrics disaggregated by demographic group
7. Distinguish between "no opportunity exists" and "opportunity exists but unreachable"
   — these represent different system failures requiring different responses (added v1.1)

NULL Output must NOT:
1. Assign a default low-quality opportunity to avoid NULL
2. Override hard boundary conditions algorithmically
3. Be resolved without human review for high-EquiRisk individuals
4. Be treated identically regardless of which boundary condition triggered it (added v1.1)
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
  patient.trust_barrier

STEP 1 — Policy Trigger Check:
  Is there an active program this patient is eligible for?
  If NO → output NULL → escalate
  If YES → proceed to Step 2

STEP 2 — Opportunity Query:
  Query resource pools within feasible geographic range
  Filter by: mobility constraints, cost boundary, language,
             hours, capacity availability, trust alignment

STEP 3 — Feasibility Check:
  Apply all BC-1 through BC-7 boundary conditions
  Score remaining opportunities by feasibility

STEP 4 — Opportunity Ranking:
  Rank feasible opportunities using opportunity ranking criteria (see below)
  Select top-ranked opportunity for assignment

STEP 5 — Contact Probability Assessment (added v1.2):
  Estimate contact success probability using default model (see below)
  If P(contact) < 0.2 and no trust-aligned intermediary available:
    → Flag for extended outreach protocol
  Proceed to output

STEP 6 — Output:
  If feasible opportunities exist:
    → Assign top-ranked opportunity
    → Generate personalized pathway (resource + timing + navigation support)
    → Record assignment and reduce resource pool capacity
    → Transition agent to `matched` state

  If no feasible opportunity exists:
    → Output NULL (type-coded: no_opportunity | unreachable | trust_barrier)
    → Trigger escalation pathway
    → Record NULL reason and boundary condition(s) violated
    → Add to tactical feedback queue
    → Transition agent to `escalated` state

STEP 7 — Human Handover:
  Pathway delivered to human staff for:
    → Patient notification and consent
    → Navigation support arrangement
    → Authorization where required
    → Trust-sensitive outreach approach where BC-7 applies
```

### Opportunity Ranking Criteria *(added v1.2)*

> PAPO Step 4 ranks *opportunities* for a given patient, which is distinct from the *patient* prioritization rules in Step 8. Patient prioritization determines *who* is served first; opportunity ranking determines *which resource* a given patient receives when multiple feasible options exist.

When a patient has multiple feasible opportunities after boundary condition filtering, opportunities are ranked using a weighted composite of the following criteria:

| Criterion | Weight (default) | Definition | Rationale |
|---|---|---|---|
| Trust alignment | 0.30 | Does the provider/resource have established trust with the patient's community? (binary, converted to 0 or 1) | Trust-aligned resources improve contact success and pathway completion |
| Proximity | 0.25 | Inverse of distance from patient to resource (normalized to [0,1] within feasible set) | Closer resources reduce transport barriers and no-show risk |
| Clinical match | 0.20 | Does the resource type directly address the patient's primary clinical need? (scored 0–1) | Clinical relevance improves health outcomes per intervention |
| Cost burden | 0.15 | Inverse of patient cost as share of income (normalized to [0,1]) | Lower cost burden improves uptake and sustained engagement |
| Capacity margin | 0.10 | Remaining capacity of resource pool (normalized to [0,1]) | Resources near exhaustion carry higher risk of scheduling failure |

```
Opportunity_Rank_Score = 0.30 * trust_alignment
                       + 0.25 * proximity_norm
                       + 0.20 * clinical_match
                       + 0.15 * (1 - cost_burden_norm)
                       + 0.10 * capacity_margin_norm

Select the opportunity with the highest Opportunity_Rank_Score.
Ties are broken by proximity (closer first), then by capacity margin (higher first).
```

> Opportunity ranking weights are default starting points. Simulations should test at least one alternative configuration (e.g., equal weights, proximity-dominant). Document weights used in fork README.

### Default Contact Success Probability Model *(added v1.2)*

> Contact success is modeled explicitly because universal reachability is a false assumption, particularly for populations with high trust barriers, language barriers, or unstable housing. This model estimates the probability that an outreach attempt results in confirmed patient contact.

```
P(contact) = baseline * trust_modifier * housing_modifier * language_modifier * time_modifier

Where:
  baseline = 0.70 (default population-level contact success rate)

  trust_modifier:
    trust_barrier = low      → 1.00
    trust_barrier = moderate → 0.70
    trust_barrier = high     → 0.40

  housing_modifier:
    housing_stability = stable   → 1.00
    housing_stability = unstable → 0.75
    housing_stability = homeless → 0.40

  language_modifier:
    language_barrier = false → 1.00
    language_barrier = true  → 0.80 (if interpreter or concordant staff available)
    language_barrier = true  → 0.50 (if no language support available)

  time_modifier:
    time_availability = high   → 1.00
    time_availability = medium → 0.85
    time_availability = low    → 0.65

Contact outcome is drawn stochastically: Bernoulli(P(contact)) per attempt.
Maximum contact attempts per matching cycle: 3 (default).
If all attempts fail → agent transitions to `contact_failed`.
```

> This model is a structural default for implementation testing, not an empirically calibrated predictor. The multiplicative form assumes conditional independence among modifiers — a simplification. Sensitivity analysis should test additive and interaction-based formulations. Forks should calibrate `baseline` and modifier values to local outreach data where available.

### Two Feedback Loops (Must Be Separated)

**Tactical Loop (minutes to hours) — Real-Time Reallocation:**
- Triggered by: NULL output, resource exhaustion, patient refusal, no-show, contact failure
- Actions: Reallocate resource to next-priority patient, adjust capacity counts, flag bottlenecks
- Decision authority: Frontline staff or automated reallocation within pre-authorized rules
- Must NOT modify: prioritization rules, eligibility criteria, EquiRisk weights

**Strategic Loop (months) — Policy and Resource Update:**
- Triggered by: End of program cycle, equity audit findings, funding changes
- Actions: Update resource pool locations and capacities, adjust program eligibility rules, revise EquiRisk weights based on outcome data, add or remove opportunity types, revise trust-alignment classifications of providers
- Decision authority: Program managers and policy staff only
- Must NOT: Operate on individual patient data in real time

> ⚠️ Conflation of tactical and strategic loops is not permitted in valid implementations. They operate on different timescales, involve different decision authorities, and modify different system components.

---

## Step 5 — Multi-Scale Simulation Architecture

### Simulation Time Step and Scheduling *(added v1.2)*

> The simulation time step defines the temporal resolution at which the system processes events. This specification supports both discrete-time and discrete-event implementations; the choice should be documented in the fork README.

**Default discrete-time specification:**

| Component | Time Step | Rationale |
|---|---|---|
| Base simulation tick | 1 day | Minimum resolution for appointment scheduling and resource replenishment |
| EquiRisk scoring | On entry to `identified` state, and on any re-entry transition | Score reflects current status at time of assessment |
| PAPO opportunity matching | 1 day (within scheduling cycle) | Patients in `identified` state are matched each daily tick, ordered by prioritization rule |
| Contact attempts | 1 per 3 days (default outreach cadence) | Allows response time; adjustable per fork |
| Resource pool replenishment | Per resource type (daily, weekly, monthly — see Entity 2) | Matches real-world resource availability cycles |
| Tactical feedback loop | Triggered within same daily tick as event | Real-time reallocation simulated as within-day processing |
| Strategic feedback loop | Every 90 days (default) | Quarterly review cycle; adjustable per fork |
| Equity audit | Every 30 days and at simulation end | Monthly monitoring plus final reporting (see Step 7) |
| HbA1c trajectory update | Every 30 days for agents in `in_pathway` or `stabilized` states | Monthly clinical update cycle |

**Scheduling cycle definition:** A scheduling cycle is the period within which PAPO attempts to match all patients in the `identified` state. Default = 7 days. Patients not matched within one scheduling cycle remain in `identified` and are re-queued at the start of the next cycle with updated priority. Tier 1 patients not matched within one cycle trigger an escalation alert.

**Discrete-event alternative:** Implementations may use discrete-event scheduling where state transitions are triggered by events rather than fixed ticks. In this case, the time intervals above serve as maximum inter-event intervals (e.g., EquiRisk re-scoring must occur within 1 day of re-entry; equity audit must occur at least every 30 days). Document the scheduling approach used.

### Individual Scale
- Each agent is scored by EquiRisk and matched (or not) by PAPO
- Tracks: opportunity received, time to intervention, pathway completion, HbA1c trajectory, contact success or failure
- Key output: individual equity outcome by demographic group

### Neighborhood Scale
- Aggregates individual outcomes by census tract
- Maps opportunity deserts: high-EquiRisk density + low opportunity availability
- Tracks: NULL output rate by neighborhood, resource utilization by facility, contact failure concentration
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

### Default HbA1c Trajectory Model *(added v1.2)*

> HbA1c trajectory is tracked as a simplified clinical outcome indicator. This model provides a default functional form for implementation testing; it is not a clinical prediction model. Forks requiring greater clinical realism should consult domain-specific literature and calibrate accordingly.

```
For agents in `in_pathway` state:
  HbA1c(t+1) = HbA1c(t) - improvement_rate * intervention_intensity * adherence_factor

Where:
  improvement_rate = 0.1 percentage points per month (default)
  intervention_intensity:
    food support only         → 0.5
    clinical care only        → 0.7
    food + clinical combined  → 1.0
    food + clinical + CHW     → 1.2
  adherence_factor = medication_adherence (0–1)

  Target HbA1c for `stabilized` transition: < 7.0% maintained for ≥ 3 consecutive months

For agents in `lost_to_followup` state:
  HbA1c(t+1) = HbA1c(t) + regression_rate
  regression_rate = 0.05 percentage points per month (default)

For agents in `stabilized` state (monitoring):
  HbA1c(t+1) = HbA1c(t) + noise
  noise ~ Normal(0, 0.02) per month
  If HbA1c exceeds 8.0% during monitoring → transition to `identified` (re-entry)
```

> **Limitations:** This model assumes linear trajectories, no ceiling/floor effects, and no interaction between clinical and contextual variables on HbA1c. It is suitable for testing system logic (does the right person get the right intervention?) but should not be interpreted as a clinical projection. Sensitivity analysis should test alternative improvement rates (0.05–0.15) and non-linear decay functions.

---

## Step 6 — Required Components for a Valid Implementation

Any fork claiming to implement EquiRisk-FoodDeserts must include:

| Component | Requirement |
|---|---|
| **Three-layer EquiRisk scoring** | All three layers (clinical, contextual, feasibility) must be implemented and scored separately before combination |
| **Composite EquiRisk score** | Must use explicit, reported weights; sub-scores must be normalized before combination; default weights are a stress-test target |
| **EquiRisk tier assignment** | Composite scores must be assigned to tiers using documented cutpoints; default tiers are provided in Step 2 *(added v1.2)* |
| **Exhaustible resource pools** | All opportunity types must be capacity-constrained and spatially located |
| **Boundary condition evaluation** | At minimum BC-1 (geographic), BC-3 (mobility), and BC-7 (trust) must be implemented; all seven are recommended |
| **NULL output with escalation** | NULL output is required when no feasible opportunity exists; silent failure is not permitted; NULL must be type-coded |
| **Separated feedback loops** | Tactical and strategic loops must be distinct; conflation invalidates the implementation |
| **Prioritization rule comparison** | At minimum two rules must be compared: clinical-risk-only vs. EquiRisk-weighted |
| **Equity metric** | At minimum one equity metric must be defined before simulation and reported disaggregated by group |
| **Human handover specification** | Authorization boundaries must be explicitly defined |
| **Contact success modeling** | Contact failure rates must be modeled; outcomes must not assume universal reachability *(added v1.1)* |
| **State transition enforcement** | Agent state transitions must follow the permitted transitions table; re-entry limits must be enforced *(added v1.2)* |
| **Opportunity ranking** | When multiple feasible opportunities exist, selection must follow documented ranking criteria *(added v1.2)* |
| **Simulation time step** | The scheduling approach (discrete-time or discrete-event) and all time intervals must be documented *(added v1.2)* |

### Strongly Recommended Enhancements
- Bias injection: train opportunity ranker on historically biased data and compare with fairness-constrained version
- Sensitivity analysis: vary EquiRisk weights and boundary condition thresholds
- Scenario comparison: high-resource vs. low-resource city conditions
- Global context fork: implement in a non-US city with different food system and policy environment
- Trust barrier sensitivity: vary BC-7 thresholds and compare equity outcomes with and without trust modeling
- Opportunity ranking weight sensitivity: compare default weights against equal-weight and proximity-dominant configurations *(added v1.2)*
- Contact model calibration: if local outreach data is available, calibrate baseline and modifier values and compare against defaults *(added v1.2)*

---

## Step 7 — Equity Metrics and Equity Audit Layer

Choose at least one equity metric before simulation. Report results disaggregated by race, income quartile, and neighborhood deprivation level.

| Metric | Definition | When to Use |
|---|---|---|
| **Equal allocation** | Each group receives interventions proportional to group size | Baseline comparison |
| **Equal outcomes** | Each group achieves equivalent HbA1c improvement | Equity goal metric |
| **Prioritizing** | Higher-need groups receive disproportionately more resources | When equity gap reduction is primary goal |
| **Sufficiency** | Each group receives enough to meet a defined minimum threshold | When minimum standard of care is the policy goal |
| **Contact success rate** | Proportion of identified individuals successfully contacted, by demographic group *(added v1.1)* | When trust barriers and reachability are in scope |

**Required equity outputs:**
- Opportunity receipt rate by race, income quartile, neighborhood ADI quartile
- NULL output rate by the same demographic dimensions
- NULL output type distribution (no_opportunity vs. unreachable vs. trust_barrier) by demographic group *(added v1.1)*
- Contact success rate by demographic group *(added v1.1)*
- Time to first intervention by EquiRisk tier
- Equity gap = difference in opportunity rate between highest and lowest access groups
- Equity gap change under each prioritization rule

### Equity Audit Layer Specification *(added v1.2)*

> The Equity Audit Layer is referenced in the integrated framework architecture diagram but was not fully specified prior to v1.2. This section defines its timing, triggers, required outputs, and governance.

The Equity Audit Layer operates as a periodic review mechanism that evaluates whether the EquiRisk-PAPO system is delivering opportunities equitably across demographic groups. It is not a real-time decision component — it operates on aggregated data and feeds into the strategic feedback loop.

**Timing and Triggers:**

| Trigger | Frequency | Action |
|---|---|---|
| Scheduled periodic audit | Every 30 simulation days (default) | Generate equity audit report; flag disparities exceeding alert thresholds |
| End of simulation | Once | Generate final comprehensive equity audit report |
| Strategic feedback loop activation | Every 90 days (default) | Equity audit report is a required input to strategic review |
| Manual trigger | On demand (human-initiated) | Ad hoc audit for specific concern |

**Required Equity Audit Outputs:**

Each audit report must include:

1. **Distributional summary** — opportunity receipt rate, NULL output rate, and contact success rate disaggregated by race, income quartile, and ADI quartile
2. **NULL output analysis** — NULL type distribution (no_opportunity / unreachable / trust_barrier) by demographic group, with identification of which boundary conditions are most frequently triggered per group
3. **Tier-level performance** — mean time to first intervention by EquiRisk tier, with flag if Tier 1 mean exceeds two scheduling cycles
4. **Equity gap tracking** — equity gap metric (Q4 vs. Q1 opportunity rate) over time, with trend direction
5. **Prioritization rule comparison** — side-by-side equity outcomes under each active prioritization rule
6. **Resource utilization equity** — which resource types are consumed by which demographic groups, flagging if high-EquiRisk groups are disproportionately routed to lower-intensity resources
7. **Re-entry and cycling analysis** — rates of re-entry from `lost_to_followup`, `escalated`, and `stabilized` states by demographic group *(added v1.2)*

**Alert Thresholds (defaults):**

| Condition | Threshold | Action |
|---|---|---|
| NULL output rate disparity between highest and lowest ADI quartile | > 15 percentage points | Flag for strategic review |
| Contact success rate disparity by race | > 20 percentage points | Flag for BC-7 and outreach protocol review |
| Tier 1 agents remaining in `identified` beyond 2 scheduling cycles | > 10% of Tier 1 agents | Flag for immediate resource reallocation review |
| Equity gap widening for 3 consecutive audit periods | Any magnitude | Flag for strategic review |

> Alert thresholds are implementer-defined defaults for testing. Forks should adjust based on local equity goals and population characteristics. Thresholds must be documented before simulation begins.

**Governance:**
- Equity audit reports are reviewed by program managers and equity officers, not by the automated system
- The equity audit layer does not modify prioritization rules, EquiRisk weights, or resource allocations directly — it produces findings that inform human decisions in the strategic feedback loop
- Audit reports are archived and versioned for longitudinal comparison across simulation runs

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
| **Trust-adjusted EquiRisk** | EquiRisk_score weighted additionally by inverse trust_barrier severity | Tests whether trust-centered routing further improves equity *(added v1.1)* |

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
| Patients are reachable once identified | Contact failure, refusal, and distrust are common especially in underserved populations | Model 20%, 40% contact failure rates; stratify by trust_barrier level |
| Food desert boundaries are stable | Food access changes seasonally and with store openings/closures | Model dynamic food desert boundaries |
| EquiRisk weights are valid | Optimal weights vary by city, population, and season | Sensitivity analysis across weight configurations |
| Resources are uniformly distributed within service areas | Resources cluster in accessible areas, leaving hardest-to-reach patients underserved | Inject spatial clustering of resources |
| Trust is static | Trust evolves over time with system interactions — positive or negative | Model trust as a dynamic variable that updates based on contact and outcome history *(added v1.1)* |
| Contact modifiers are independent | Trust, housing, language, and time availability likely interact (e.g., unstable housing + high trust barrier compounds contact difficulty) | Test multiplicative vs. additive vs. interaction-based contact models *(added v1.2)* |
| HbA1c trajectory is linear | Real HbA1c response is non-linear with ceiling effects and individual variability | Test non-linear decay functions and stochastic individual trajectories *(added v1.2)* |
| Synthetic population reflects real joint distributions | Correlation structure between clinical, contextual, and feasibility attributes may be misspecified | Compare outcomes using different copula assumptions or empirical correlation matrices where available *(added v1.2)* |

> ⚠️ Failure to model these assumptions will produce optimistic, non-generalizable results.

---

## Step 10 — Global Adaptation Guide

EquiRisk-FoodDeserts is designed to be forked for any city globally. The core logic is preserved across all forks. What changes per city:

### What Stays the Same (Core Logic — Do Not Modify)
- Three-layer EquiRisk scoring architecture
- PAPO policy-to-opportunity translation mechanism
- NULL output requirement (including type-coding)
- Separated feedback loops
- Human handover requirements
- Equity metric reporting requirements
- BC-7 trust barrier category (the concept is universal; parameters are local)
- Agent state transition rules and re-entry limits *(added v1.2)*
- Equity Audit Layer structure and minimum reporting requirements *(added v1.2)*

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
| Trust barrier reference groups | Race/ethnicity, immigration status | Caste, ethnicity, gender in health-seeking | Class, immigration status, minority status |
| Contact success baseline | 0.70 (default) | Calibrate to local outreach data; may be lower in informal settings | Calibrate to local data *(added v1.2)* |
| HbA1c improvement rate | 0.1 pp/month (default) | Calibrate to local clinical data | Calibrate to local data *(added v1.2)* |

### Minimum Adaptation Requirements for Non-US Forks
1. Replace ADI/SVI with locally available deprivation index
2. Redefine food desert boundary criteria for local food system
3. Specify locally available opportunity types
4. Identify relevant policy trigger mechanisms
5. Define locally appropriate equity dimensions
6. Define locally relevant trust barrier reference groups and historical exclusion patterns
7. Calibrate contact success baseline and modifier values to local outreach data where available *(added v1.2)*
8. Document all substitutions clearly in fork README

---

## Candidate Cities for Forking

This framework is well-suited for cities with:
- Significant diabetic population with food insecurity overlap
- Neighborhood-level data availability
- Active diabetes management programs to simulate

### Readiness Criteria *(added v1.1)*

Before selecting a city for forking, assess availability of:

| Criterion | Minimum Requirement | Preferred |
|---|---|---|
| Deprivation data | Census-tract-level deprivation index | Sub-tract or block-group level |
| Food access data | City-level grocery store locations | USDA-equivalent access atlas |
| Clinical population data | Synthetic or aggregate HbA1c data by neighborhood | Linked EHR + claims data |
| Program inventory | Known diabetes management programs with eligibility rules | Real-time capacity data |
| Trust/historical context | Published documentation of historical underservice | Community organization input |
| Outreach contact data | Aggregate contact success rates by program *(added v1.2)* | Demographic-stratified contact rates |

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

## Step 11 — Simulation Validation Checklist *(added v1.1, updated v1.2)*

Before reporting results from any simulation built on this CMDDS, complete the following checklist. Document outcomes in fork README.

### Structural Validity
- [ ] All three EquiRisk layers are implemented and scored independently before combination
- [ ] Sub-scores are normalized to [0,1] before weight application
- [ ] Composite EquiRisk weights are documented and sum to 1.0
- [ ] EquiRisk tier boundaries are documented and applied consistently *(added v1.2)*
- [ ] All resource pools are exhaustible and spatially located
- [ ] At minimum BC-1, BC-3, and BC-7 are implemented
- [ ] NULL output is type-coded (no_opportunity | unreachable | trust_barrier)
- [ ] NULL output triggers escalation pathway; no silent failures exist
- [ ] Tactical and strategic feedback loops are implemented separately
- [ ] Human handover points are explicitly defined and documented
- [ ] Agent state transitions follow the permitted transitions table; no prohibited transitions occur *(added v1.2)*
- [ ] Re-entry limits are enforced; agents exceeding limits transition to `escalated` *(added v1.2)*
- [ ] Opportunity ranking criteria are documented; multi-opportunity selection is not arbitrary *(added v1.2)*
- [ ] Simulation time step and scheduling approach are documented *(added v1.2)*
- [ ] Contact success probability model is implemented with documented parameters *(added v1.2)*
- [ ] HbA1c trajectory model is implemented with documented parameters *(added v1.2)*

### Equity Validity
- [ ] At least one equity metric is defined before simulation begins
- [ ] Equity outputs are disaggregated by race, income quartile, and neighborhood deprivation
- [ ] NULL output rates are reported by demographic group
- [ ] At minimum two prioritization rules are compared (clinical-only vs. EquiRisk-weighted)
- [ ] Contact success rates are modeled and reported by demographic group
- [ ] Equity Audit Layer runs at minimum every 30 simulation days and at simulation end *(added v1.2)*
- [ ] Equity audit alert thresholds are documented before simulation begins *(added v1.2)*

### Assumption Transparency
- [ ] All assumptions from Step 9 are explicitly acknowledged
- [ ] At least three assumptions are stress-tested with documented scenarios
- [ ] Results are framed as exploratory and comparative — not predictive or prescriptive
- [ ] Limitations are documented per Step 13
- [ ] Synthetic population generation method is documented (if applicable) *(added v1.2)*

### Data Privacy and Ethics *(added v1.2)*
- [ ] Data privacy and ethics requirements from Step 15 are reviewed and addressed
- [ ] If real or linked data is used, IRB approval or ethics review is documented
- [ ] Synthetic data generation method is documented with bias acknowledgment

### Adaptation Documentation (for non-Milwaukee forks)
- [ ] All substituted parameters are listed in fork README
- [ ] Local trust barrier reference groups are defined
- [ ] Local food desert definition and deprivation index are specified
- [ ] Contact success baseline and modifier values are calibrated or defaults are justified *(added v1.2)*
- [ ] Deviations from core logic are justified and documented

---

## Step 12 — Worked Example: Milwaukee Reference Scenario *(added v1.1, corrected v1.2)*

This reference scenario illustrates minimum valid implementation logic. It is not empirically calibrated — all parameter values are illustrative defaults for testing implementation structure.

### Scenario Setup

**City:** Milwaukee, WI
**Population:** 500 synthetic diabetic agents assigned to census tracts using publicly available ADI and SVI distributions (see Step 14 for generation guidance)
**Simulation period:** 12 months
**Time step:** 1 day (discrete-time)
**Scheduling cycle:** 7 days
**Resource condition:** Moderate (70% of estimated need met by available programs)
**Prioritization rules compared:** Clinical-risk-only vs. EquiRisk-weighted

### Two Illustrative Agents

| Dimension | Agent A (Low Contextual Vulnerability) | Agent B (High Contextual Vulnerability) |
|---|---|---|
| `hba1c_level` | 9.2% | 9.1% |
| `clinical_risk_score` (normalized) | 0.78 | 0.76 |
| `food_desert_status` | No | Yes |
| `area_deprivation_index` | 32 | 87 |
| `transit_score` | 0.72 | 0.19 |
| `mobility_score` | 1 (fully mobile) | 2 (limited) |
| `trust_barrier` | Low | High |
| `contextual_vulnerability_score` (normalized) | 0.31 | 0.84 |
| `action_feasibility_score` (normalized) | 0.79 | 0.22 |

**EquiRisk Score Calculation (default weights: w1=0.4, w2=0.35, w3=0.25):** *(corrected v1.2)*

```
Agent A:
  EquiRisk = 0.4 * 0.78 + 0.35 * 0.31 + 0.25 * (1 - 0.79)
           = 0.312 + 0.1085 + 0.0525
           = 0.473
  → Tier 3 (Moderate)

Agent B:
  EquiRisk = 0.4 * 0.76 + 0.35 * 0.84 + 0.25 * (1 - 0.22)
           = 0.304 + 0.294 + 0.195
           = 0.793
  → Tier 1 (Critical)
```

**Under clinical-risk-only:** Agent A prioritized (higher clinical score: 0.78 vs. 0.76).
**Under EquiRisk-weighted:** Agent B prioritized (EquiRisk 0.793 vs. 0.473 — lower clinical score offset by high contextual vulnerability and low feasibility).

### Contact Success Probability for Agent B *(added v1.2)*

```
P(contact) = 0.70 * 0.40 * 1.00 * 0.80 * 0.85
           (baseline)(trust:high)(housing:stable)(language:true,interpreter)(time:medium)
           = 0.190

P(contact) < 0.20 → flag for extended outreach protocol
Recommended: assign trust-aligned CHW intermediary before first contact attempt
```

### PAPO Translation for Agent B

```
Policy Trigger: DPP enrollment + Medicaid eligibility → confirmed active
Opportunity Query: Resources within 1.5 miles, delivery options, CHW with BC-7 trust alignment
BC-1: Nearest FQHC = 1.8 miles → outside soft boundary without transport → transport required
BC-3: Limited mobility → in-person opportunities reduced; telehealth or delivery preferred
BC-7: High trust barrier → direct provider referral infeasible → CHW intermediary required
Feasibility Check: Medically tailored meal delivery (feasible) + CHW visit (feasible with trust-aligned CHW)

Opportunity Ranking (two feasible options):
  CHW visit:
    trust_alignment = 1.0, proximity = 0.85, clinical_match = 0.8, cost_burden = 0.0, capacity = 0.60
    Score = 0.30(1.0) + 0.25(0.85) + 0.20(0.8) + 0.15(1.0) + 0.10(0.60) = 0.8225
  Meal delivery:
    trust_alignment = 0.5, proximity = 1.0, clinical_match = 0.6, cost_burden = 0.0, capacity = 0.45
    Score = 0.30(0.5) + 0.25(1.0) + 0.20(0.6) + 0.15(1.0) + 0.10(0.45) = 0.665
  → CHW visit ranked first

Output: CHW visit scheduled (primary) + medically tailored meal delivery enrolled (secondary)
Human Handover: CHW supervisor authorizes assignment; CHW briefed on trust context
Agent B state transition: identified → matched → contact_attempted (via trust-aligned CHW)
```

### HbA1c Trajectory Projection for Agent B *(added v1.2)*

```
Assuming Agent B enters `in_pathway` at month 1 with HbA1c = 9.1%:
  Intervention: food + clinical + CHW → intensity = 1.2
  Adherence: medication_adherence = 0.6 (assumed for illustration)

  Month 1: 9.1 - (0.1 * 1.2 * 0.6) = 9.1 - 0.072 = 9.028%
  Month 3: 9.1 - 3 * 0.072 = 8.884%
  Month 6: 9.1 - 6 * 0.072 = 8.668%
  Month 12: 9.1 - 12 * 0.072 = 8.236%

  Agent B does not reach stabilization target (< 7.0%) within 12 months at this adherence level.
  → Remains in `in_pathway`; highlighted in equity audit as Tier 1 agent not yet stabilized.
```

> This trajectory illustrates the model mechanics, not a clinical prediction. Higher adherence or more intensive intervention would produce different results.

### Expected Equity Outputs

| Metric | Clinical-Only Rule | EquiRisk-Weighted Rule |
|---|---|---|
| Opportunity receipt rate — ADI quartile 4 | Lower | Higher |
| NULL output rate — ADI quartile 4 | Higher | Lower |
| Mean time to intervention — EquiRisk Tier 1 | Longer | Shorter |
| Equity gap (Q4 vs Q1 opportunity rate) | Wider | Narrower |
| Contact success rate — high trust barrier group | Not differentiated | Lower (modeled explicitly) |

> These are directional predictions based on framework logic, not empirical projections. Actual simulation outputs will vary by implementation and parameter choices.

---

## Step 13 — Known Limitations and Open Research Questions *(added v1.1, updated v1.2)*

### Known Limitations of This CMDDS

**Conceptual limitations:**
- EquiRisk weights (w1, w2, w3) have no empirically validated defaults. The 0.4/0.35/0.25 split is a reasonable stress-test starting point, not a calibrated estimate.
- The composite EquiRisk score assumes linear additivity across layers. Non-linear interactions (e.g., compounding disadvantage) are not captured in the default formulation.
- Trust is modeled as a static agent attribute in v1.2. Dynamic trust — updated through system interactions — is specified as an assumption stress-test but not as a core model component.
- The framework does not model supply-side barriers in provider systems (e.g., clinician implicit bias, organizational capacity constraints) except through resource pool capacity limits.
- Opportunity ranking weights (Step 4) are not empirically derived. The default trust-first weighting reflects framework philosophy but may not be optimal for all contexts. *(added v1.2)*
- The contact success probability model assumes conditional independence among modifiers. Interaction effects (e.g., compounding of trust barrier and unstable housing) are not captured in the default multiplicative form. *(added v1.2)*

**Simulation scope limitations:**
- HbA1c trajectory modeling is simplified (linear approximation). Clinical realism requires domain-specific calibration.
- This CMDDS does not specify a network model. Social network effects on trust, information sharing, and peer-mediated uptake are out of scope.
- Seasonal variation in food access and mobility is noted as an environmental attribute but is not fully specified for simulation.
- Synthetic population generation guidance (Step 14) provides a structural approach but does not resolve the fundamental challenge of specifying realistic joint distributions without empirical data. *(added v1.2)*

**Equity limitations:**
- The framework operationalizes equity as distributional equity (who receives what). Relational equity (how people are treated in interactions) and epistemic equity (whose knowledge shapes the system) are not modeled.
- Equity metrics in Step 7 focus on receipt and outcomes. Process equity (experience of receiving care) is not captured.
- Equity audit alert thresholds are implementer-defined and may not correspond to community-defined standards of acceptable disparity. *(added v1.2)*

### Open Research Questions

These questions are beyond the scope of this CMDDS but are important directions for downstream research:

1. What are the empirically optimal EquiRisk weights for different city contexts, and how stable are they across seasons and population subgroups?
2. How does dynamic trust modeling — where trust updates based on contact and outcome history — change long-term equity trajectories?
3. At what resource level does EquiRisk-weighted prioritization cease to outperform clinical-only prioritization in equity outcomes?
4. How do supply-side barriers (clinician behavior, organizational culture) interact with demand-side barriers (patient feasibility) in ways that EquiRisk-PAPO cannot currently capture?
5. Can the EquiRisk-PAPO logic generalize to other chronic condition contexts (e.g., hypertension, mental health) beyond diabetes, and what adaptations are required?
6. What community co-design processes are required to ensure BC-7 trust barrier definitions are legitimate, non-stigmatizing, and community-validated?
7. What is the empirical correlation structure between clinical risk, contextual vulnerability, and action feasibility in real diabetic populations, and how sensitive are simulation outcomes to misspecification of these joint distributions? *(added v1.2)*
8. How should opportunity ranking weights be calibrated — through community preference elicitation, retrospective outcome analysis, or multi-objective optimization — and do optimal weights vary by EquiRisk tier? *(added v1.2)*

---

## Step 14 — Synthetic Population Generation Guidance *(added v1.2)*

> Simulations require a synthetic population of diabetic agents with correlated attributes across the three EquiRisk layers. This section provides structural guidance for generating such populations. It does not prescribe a single method; implementers should document their approach and test sensitivity to generation assumptions.

### The Core Challenge

EquiRisk scoring depends on the joint distribution of clinical, contextual, and feasibility attributes. In real populations, these attributes are correlated — individuals in high-deprivation neighborhoods are more likely to have lower transit scores, higher trust barriers, and worse clinical indicators. Generating agents with independent attribute draws will produce unrealistic populations and misleading simulation results.

### Recommended Generation Approach

**Step 1 — Define the spatial scaffold:**
- Obtain census tract–level ADI and SVI data for the target city
- Assign each synthetic agent to a census tract, with the number of agents per tract proportional to estimated diabetic prevalence (from CDC or local health department estimates)

**Step 2 — Assign contextual vulnerability attributes (Layer 2) from tract-level data:**
- `food_desert_status`: directly from USDA Food Access Research Atlas at tract level
- `area_deprivation_index`: directly from Neighborhood Atlas at tract level
- `social_vulnerability_index`: directly from CDC SVI at tract level
- `nearest_grocery_distance`: derived from USDA data or OpenStreetMap
- `transit_score`: derived from GTFS data at tract level
- `housing_stability`: drawn from ACS estimates for tract, with stochastic assignment
- `neighborhood_clinic_density`: computed from HRSA data

**Step 3 — Assign clinical risk attributes (Layer 1) conditional on contextual vulnerability:**
- Clinical risk attributes should be drawn from distributions conditioned on neighborhood deprivation. Higher-ADI tracts should have higher mean HbA1c, lower medication adherence, and higher complication counts, reflecting well-documented health disparities.
- Default correlation approach: specify a target Spearman correlation matrix between ADI and each clinical attribute, then draw using a Gaussian copula or ranked conditional sampling.
- Example target correlations (illustrative defaults for testing — not empirically calibrated):

| Attribute pair | Target Spearman ρ |
|---|---|
| ADI ↔ hba1c_level | +0.25 |
| ADI ↔ medication_adherence | −0.20 |
| ADI ↔ complication_count | +0.15 |
| ADI ↔ comorbidity_score | +0.20 |

**Step 4 — Assign feasibility attributes (Layer 3) conditional on contextual and clinical attributes:**
- `mobility_score`: drawn from age- and disability-weighted distribution per tract
- `has_transport`: drawn from ACS car ownership rates per tract
- `income_quartile`: assigned from ACS household income distribution per tract
- `health_literacy_score`: drawn from education-level distribution per tract
- `trust_barrier`: assigned conditional on race/ethnicity and ADI, with higher trust barriers in historically underserved communities. Default: in ADI quartile 4 tracts, 40% high, 35% moderate, 25% low; in ADI quartile 1 tracts, 10% high, 25% moderate, 65% low. These are illustrative defaults — forks should calibrate to local context.
- `language_barrier`: drawn from ACS language data per tract
- `insurance_status`: drawn from ACS and Medicaid enrollment data per tract
- `time_availability`: drawn from employment and caregiving burden estimates per tract

**Step 5 — Compute composite scores and validate:**
- Compute `clinical_risk_score`, `contextual_vulnerability_score`, and `action_feasibility_score` from constituent attributes
- Normalize all sub-scores to [0,1] using min-max normalization within the simulated population
- Compute composite EquiRisk score and assign tiers
- Validate: check that the synthetic population reproduces expected patterns (e.g., Tier 1 agents are concentrated in high-ADI tracts; trust barriers are higher in historically underserved communities)

### Population Size Guidance

| Purpose | Minimum N | Rationale |
|---|---|---|
| Implementation testing | 200–500 | Sufficient to test all state transitions and boundary conditions |
| Equity comparison (two rules) | 1,000–2,000 | Sufficient for stable equity gap estimates across 4 ADI quartiles |
| Sensitivity analysis | 2,000–5,000 | Required for stable variance estimates across parameter sweeps |
| Publication-quality results | 5,000+ with multiple replications | Standard for stochastic simulation confidence intervals |

### What to Document

Every fork must document the following in its README:
- Synthetic population size and number of replications
- Spatial scaffold (city, tract-level data sources)
- Correlation structure (method, target correlations, or copula specification)
- Trust barrier assignment rules
- Any departures from the guidance above, with justification

---

## Step 15 — Data Privacy, Ethics, and IRB Considerations *(added v1.2)*

> This CMDDS is designed for use with synthetic data. However, the framework is intended to be eventually applicable to real-world settings where individual-level health, demographic, and location data may be involved. This section specifies the ethical and privacy requirements that apply to any implementation.

### Synthetic Data Implementations

Even when using fully synthetic data, implementers should be aware of the following:

1. **Synthetic data can encode real biases.** If synthetic populations are generated from summary statistics drawn from biased data sources (e.g., health registries that undercount undocumented immigrants, or insurance claims that exclude uninsured populations), the synthetic population will reproduce those biases. Document the data sources used for generation and their known limitations.

2. **Ecological inference risks.** Tract-level attribute assignment (e.g., assigning higher trust barriers in high-ADI, majority-minority tracts) can reinforce stereotypes if presented without appropriate framing. Simulation outputs must be framed as system-level patterns, not individual predictions or group characterizations.

3. **Stigmatization risk.** Trust barrier modeling (BC-7) requires particular care. Trust barriers are modeled as structural outcomes of historical exclusion, not as individual deficits. Outputs should never be framed as "[group] does not trust healthcare" but rather as "the system has historically failed [group], producing lower engagement rates."

### Real or Linked Data Implementations

If any implementation uses real patient data, linked administrative records, or identifiable community-level data:

1. **IRB or ethics board review is required** before simulation development begins — not only before publication. This includes implementations that link publicly available data sets in ways that could re-identify individuals (e.g., combining tract-level health data with tract-level demographic data at fine spatial resolution).

2. **Data minimization.** Use the minimum level of geographic and demographic detail needed to test the simulation logic. Block-group-level data is rarely necessary for CMDDS validation; tract-level is typically sufficient.

3. **De-identification verification.** If synthetic agents are generated from real data distributions, verify that individual re-identification is not possible from the combination of attributes (e.g., a unique combination of age, tract, diagnosis, and language in a small tract).

4. **Community engagement.** For implementations in specific cities, particularly those involving BC-7 trust barrier definitions, engagement with affected communities is strongly recommended before defining trust barrier reference groups and historical exclusion patterns. See Open Research Question 6 (Step 13).

5. **Data use agreements.** If using HRSA, CMS, or state Medicaid data, ensure compliance with applicable data use agreements and HIPAA requirements.

### Ethical Framing of Outputs

All simulation outputs should be framed in accordance with the following principles:

- Outputs are exploratory and comparative, not predictive or prescriptive (restated for emphasis)
- Equity gaps identified in simulation reflect system design failures, not group deficiencies
- NULL output concentration in specific populations reflects structural barriers, not individual non-compliance
- Trust barriers are outcomes of system behavior, not patient characteristics
- Simulation results should not be used to justify reducing services to groups with low contact success rates; they should be used to redesign outreach to improve success rates

---

## General & Background References

The following references provide foundational context for the EquiRisk-FoodDeserts framework, including food desert definitions and measurement, the food insecurity–diabetes nexus, simulation and agent-based modeling methodology, and health equity and community health worker evidence. These references underpin multiple simulation projects in the FORK_SIMULATION_SUGGESTIONS document.

### Food Desert Definitions & Measurement

- Jiao, J., & Azimian, A. (2021). Measuring accessibility to grocery stores using radiation model and survival analysis. *Journal of Transport Geography, 94*, 103107. https://doi.org/10.1016/j.jtrangeo.2021.103107
- Raja, S., Ma, C., & Yadav, P. (2008). Beyond food deserts: Measuring and mapping racial disparities in neighborhood food environments. *Journal of Planning Education and Research, 27*(4), 469–482. https://doi.org/10.1177/0739456X08317461
- Ver Ploeg, M., Breneman, V., Farrigan, T., Hamrick, K., Hopkins, D., Kaufman, P., ... & Tuckermanty, E. (2009). *Access to affordable and nutritious food: Measuring and understanding food deserts and their consequences* (Report to Congress, AP-036). U.S. Department of Agriculture, Economic Research Service.

### Food Insecurity–Diabetes Nexus

- Berkowitz, S. A., Karter, A. J., Corbie-Smith, G., Seligman, H. K., Ackroyd, S. A., Barnard, L. S., Atlas, S. J., & Wexler, D. J. (2018). Food insecurity, food "deserts," and glycemic control in patients with diabetes: A longitudinal analysis. *Diabetes Care, 41*(6), 1188–1195. https://doi.org/10.2337/dc17-1981
- Gucciardi, E., Vahabi, M., Norris, N., Del Monte, J. P., & Farnum, C. (2014). The intersection between food insecurity and diabetes: A review. *Current Nutrition Reports, 3*(4), 324–332. https://doi.org/10.1007/s13668-014-0104-4
- Kelli, H. M., Hammadah, M., Ahmed, H., Ko, Y.-A., Topel, M., Samman-Tahhan, A., ... & Quyyumi, A. A. (2017). Association between living in food deserts and cardiovascular risk. *Circulation: Cardiovascular Quality and Outcomes, 10*(9), e003532. https://doi.org/10.1161/CIRCOUTCOMES.116.003532
- Levi, R., Bleich, S. N., & Seligman, H. K. (2023). Food insecurity and diabetes: overview of intersections and potential dual solutions. *Diabetes care*, *46*(9), 1599-1608.

### Simulation & Agent-Based Modeling Methodology

- Auchincloss, A. H., Riolo, R. L., Brown, D. G., Cook, J., & Diez Roux, A. V. (2011). An agent-based model of income inequalities in diet in the context of residential segregation. *American Journal of Preventive Medicine, 40*(3), 303–311. https://doi.org/10.1016/j.amepre.2010.10.033
- Widener, M. J., Metcalf, S. S., & Bar-Yam, Y. (2013). Agent-based modeling of policies to improve urban food access for low-income populations. *Applied Geography, 40*, 1–10. https://doi.org/10.1016/j.apgeog.2013.01.003

### Health Equity & Community Health Workers

- Kangovi, S., Mitra, N., Grande, D., Long, J. A., & Asch, D. A. (2020). Evidence-based community health worker program addresses unmet social needs and generates positive return on investment. *Health Affairs, 39*(2), 207–213. https://doi.org/10.1377/hlthaff.2019.00981
- Palmas, W., March, D., Daber, G., Findley, S. E., Teresi, J., Carrasquillo, O., & Luchsinger, J. A. (2015). Community health worker interventions to improve glycemic control in people with diabetes: A systematic review and meta-analysis. *Journal of General Internal Medicine, 30*(7), 1004–1012. https://doi.org/10.1007/s11606-015-3247-0

---

## License and Attribution

Please cite both the EquiRisk SSRN preprint and this CMDDS when publishing derived simulations or analyses. See LICENSE for details.

## Acknowledgments

This Conceptual Model Design Documentation for Simulation (CMDDS) was developed with the assistance of Claude (Anthropic), a large language model. Building on the EquiRisk equity-aware risk stratification framework, the Policy-Aware Personalized Opportunity (PAPO) framework, and the supporting literature reviews, Claude assisted in structuring and drafting the simulation specification — including entity and state definitions, boundary condition formalization, agent state transition rules, scheduling logic, the contact success probability model, HbA1c trajectory specification, Equity Audit Layer design, synthetic population generation guidance, the validation checklist, worked examples, and cross-framework integration architecture. All components were reviewed, refined, and validated by the author to ensure scientific rigor and alignment with the EquiRisk-FoodDeserts research program.

## About

CMDDS for EquiRisk-FoodDeserts: an integrated, equity-aware simulation specification for diabetes care navigation in food desert settings. Fork to model care access equity in your city.
