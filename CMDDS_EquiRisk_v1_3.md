# CMDDS — EquiRisk-FoodDeserts

## Conceptual Model Design Documentation for Simulation (CMDDS)

**Version:** 1.3
**Date:** 2026-05-01
**Author:** Min Wu, PhD
**Affiliation:** Zilber College of Public Health, University of Wisconsin-Milwaukee
**GitHub:** https://github.com/Min-PH/EquiRisk-FoodDeserts

**Cite this CMDDS:**
> Wu, M. (2026). CMDDS for EquiRisk-FoodDeserts v1.3 — Integrated Simulation Framework for Equity-Aware Diabetes Care Navigation in Food Deserts. GitHub. https://github.com/Min-PH/EquiRisk-FoodDeserts

**Related Works:**
> Wu, M. (2026). *Artificial Intelligence in Public Health*. Springer Nature. ISBN 978-3032158710.
> Wu, M. (2026). EquiRisk: Operationalizing Equity-Aware Risk Stratification for Diabetes Management in Food Deserts. SSRN. https://ssrn.com/abstract=6150926
> Wu, M. (2026). PAPO: A Policy-Aware Personalized Opportunity Framework for Heatwave Public Health Interventions. SSRN. https://ssrn.com/abstract=6198260
> Wu, M. (2026). CMDDS for PAPO-Heatwaves v1.1. GitHub. https://github.com/Min-PH/PAPO-Heatwave-AI
> Wu, M. (2026). EquiRisk Case Report (Case #004-M): MOKG-PH Analytical Case Analysis for Diabetes in Food Deserts. Internal case report, MOKG-PH program.

---

## Changelog

- **v1.0** — Initial release. Integrated EquiRisk + PAPO framework. Defines three-layer EquiRisk scoring, PAPO translation logic, six boundary condition categories, multi-scale architecture, required components, equity metrics, prioritization rules, assumptions, and global adaptation guide.
- **v1.1** — Added Step 11 (Simulation Validation Checklist), Step 12 (Worked Example: Milwaukee Reference Scenario), and Step 13 (Known Limitations and Open Research Questions). Expanded composite EquiRisk score specification with sub-score normalization guidance. Added `trust_barrier` attribute to Entity 1. Added BC-7 (Trust and Engagement Boundaries). Clarified NULL output escalation protocol. Added recommended modular simulation project: trust barrier analysis. Added equity metric: Contact Success Rate. Expanded candidate cities section with readiness criteria. Minor clarifications throughout.
- **v1.2** — Added agent state transition rules with permitted transitions table and re-entry logic (Step 2). Added simulation time step and scheduling specification (Step 5). Added EquiRisk tier definitions with default score ranges (Step 2). Added opportunity ranking criteria within PAPO Step 4 for multi-opportunity selection (Step 4). Added synthetic population generation guidance (Step 14). Added default contact success probability model (Step 4). Added default HbA1c trajectory specification (Step 5). Added Equity Audit Layer specification with timing, triggers, and required outputs (Step 7). Added data privacy, ethics, and IRB considerations (Step 15). Corrected worked example arithmetic with fully reproducible EquiRisk score calculations (Step 12). Added new validation checklist items for v1.2 additions. Added two new open research questions. Minor clarifications throughout.
- **v1.3** — Major structural revision driven by EquiRisk Case Report #004-M (MOKG-PH analysis). **Replaced the additive composite EquiRisk score with a multiplicative formulation** (`Priority = Clinical Risk × (1 + CVI) × Feasibility Weight`) as the single canonical scoring rule (Step 2). Added **Contextual Vulnerability Index (CVI)** as a named composite of Layer 2 attributes, normalized [0,1] (Step 2). Added **Uptake Probability** as a formal Layer 3 attribute distinct from contact success, with default specification (Step 2, Step 4). Added **Bias Injection Protocol** as a required pre-deployment procedure with five steps and explicit disparity delta thresholds (new Step 16). Added **Community Co-Design Requirement** as a pre-deployment gate with five-question framework (new Step 17). Added **Equity Halt Threshold** (default ≥70% of equity-weighted expected receipt rate) with halt logic and resumption criteria (Step 7). Added **Bias Loop-Breaking Constraint** preventing Stage 2 outputs from re-entering Stage 1 training data without evidence upgrade (Step 4). Added **Cumulative Tactical Drift Detection** with rolling window monitoring (Step 4). Added **Stigma Sentinel** and **Vulnerable Population Floor** as named guardrails (Step 7). Updated worked example to demonstrate multiplicative scoring and to show how Patient B's priority shifts (Step 12). Updated validation checklist, assumptions, and adaptation guide for v1.3 additions. Added v1.3 limitations and three new open research questions (Step 13).

> **Migration note for forks built on v1.0–v1.2:** v1.3 changes the canonical scoring formula from additive to multiplicative. Forks should re-score their populations under the new formula before publishing comparative results across CMDDS versions. The additive form is documented in Step 13 (Known Limitations) as a deprecated alternative for backward comparison only.

---

## Overview

This repository contains the Conceptual Model Design Documentation for Simulation (CMDDS) for **EquiRisk-FoodDeserts** — an integrated simulation framework combining:

- **EquiRisk** — equity-aware risk stratification integrating individual clinical risk, neighborhood contextual vulnerability, and action feasibility into a unified proactive decision rule via a multiplicative priority score
- **PAPO** — policy-aware personalized opportunity framework translating policy triggers and EquiRisk outputs into personalized, constraint-aware intervention pathways

Applied together to **diabetes management in food deserts**, this integrated framework addresses a critical failure in traditional public health practice:

> *Risk is identified, but interventions do not reach the people who need them most — because structural barriers, feasibility constraints, and equity considerations are ignored in the decision logic.*

### The Central Shift This Framework Makes

| Traditional Approach | EquiRisk-FoodDeserts Approach |
|---|---|
| "Who has the highest clinical risk?" | "Who has the highest *effective* risk given access context, and can be reached by a feasible intervention now?" |
| Equity as retrospective reporting | Equity as proactive decision rule |
| Clinical indicators only | Clinical × contextual × feasibility integrated multiplicatively |
| Equity weighting adjusts allocation | Contextual vulnerability adjusts the *effective risk score itself* (not just allocation) |
| Intervention assumed feasible | Feasibility explicitly evaluated and bounded |
| Human effort drives coordination | AI-enabled, policy-constrained coordination with human oversight |
| Risk identification | Risk → actionable personalized pathway |
| Contact assumed successful | Contact success and uptake probability modeled explicitly; trust barriers assessed |

### Design Philosophy

1. **Equity is a decision rule, not a report** — equity considerations are embedded in the prioritization logic from the start
2. **Contextual vulnerability adjusts effective risk, not just allocation** — a patient who cannot access standard care faces a higher expected health burden than a patient with identical clinical risk who can; this is captured by the multiplicative formulation, not by post-hoc allocation weighting *(formalized v1.3)*
3. **Feasibility is non-negotiable** — interventions are only recommended if they are reachable by the patient given real constraints; NULL output is required when no feasible option exists
4. **Human oversight is preserved** — the framework is a decision-support system; all consequential actions require human authorization at defined handover points
5. **Global adaptability** — core logic is universal; context-specific parameters are locally defined per fork
6. **Transparency and auditability** — every decision pathway must be explainable and auditable
7. **Trust is a structural variable** — patient distrust and prior negative system experiences are modeled as a boundary condition, not an individual failing
8. **Community co-design is a deployment gate, not an enhancement** — community representatives must validate value weights, intervention pathways, and the equity halt threshold before deployment *(formalized v1.3)*
9. **Bias is presumed in administrative training data** — bias injection testing is a required pre-deployment procedure, not an optional check *(formalized v1.3)*

---

## Integrated Framework Architecture: EquiRisk + PAPO

The integration of EquiRisk and PAPO creates a two-phase decision system:

```
PHASE 1 — EquiRisk: WHO needs help most, and what are their constraints?
    │
    ├── Layer 1: Individual Clinical Risk
    │         (HbA1c, complications, medication adherence)
    │         → clinical_risk_score (normalized [0,1])
    │
    ├── Layer 2: Contextual Vulnerability
    │         (food desert status, ADI, SVI, transport, housing)
    │         → Contextual Vulnerability Index (CVI), normalized [0,1]
    │         → Contextual Vulnerability Multiplier (CVM) = (1 + CVI)
    │
    └── Layer 3: Action Feasibility
              (mobility, income, literacy, trust, program availability,
               uptake probability)
              → action_feasibility_weight (normalized [0,1])
                    │
                    ▼
        EquiRisk Priority Score (multiplicative):
            Priority = clinical_risk_score × CVM × action_feasibility_weight
                     = clinical_risk_score × (1 + CVI) × action_feasibility_weight
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
        Equity Audit Layer + Equity Halt Threshold
        (did the system reach the right people equitably?
         is receipt rate for vulnerable groups below the halt floor?)
        (see Step 7)
```

### Why Integration Matters

EquiRisk alone answers: *"Who should we prioritize, given that effective risk is a function of access context?"*
PAPO alone answers: *"What opportunities exist and who qualifies?"*
Together they answer: *"Whose effective risk is highest, what can realistically reach them, and did the system deliver equitably?"*

Neither framework is complete without the other for operational deployment. EquiRisk without PAPO produces prioritized lists with no delivery mechanism. PAPO without EquiRisk delivers opportunities without equity-aware targeting.

### Why Multiplicative, Not Additive *(v1.3 rationale)*

Versions 1.0–1.2 of this CMDDS used an additive composite of the three layers. The EquiRisk Case Report (#004-M, MOKG-PH analysis) identified that the additive form conflates two distinct concepts:

- **Allocation weighting** — adjusting how resources are distributed across patients with different barriers
- **Effective risk adjustment** — recognizing that the same clinical risk score implies a higher expected health burden when access barriers reduce uptake probability

The multiplicative formulation `Priority = Clinical Risk × (1 + CVI) × Feasibility Weight` captures the second concept: contextual vulnerability does not merely shift allocation — it raises the patient's expected burden because their probability of acting on a standard recommendation is lower. Two patients with identical clinical scores receive different priorities under EquiRisk because their *expected outcomes* differ. This is not an equity override; it is a more accurate risk assessment.

---

## What This Repository Is (and Is Not)

### This repository provides:
- Complete CMDDS for EquiRisk-FoodDeserts v1.3
- Full integrated EquiRisk + PAPO logic specification with multiplicative priority score *(updated v1.3)*
- Contextual Vulnerability Index (CVI) and Multiplier (CVM) specification *(added v1.3)*
- Uptake Probability attribute and default model *(added v1.3)*
- Explicit boundary conditions for action feasibility (including trust barriers)
- Multi-scale simulation specification (individual, neighborhood, city)
- Required components for a valid simulation implementation
- Equity metrics, prioritization rules, and governance requirements
- Equity Halt Threshold with halt logic and resumption criteria *(added v1.3)*
- Bias Injection Protocol — five-step pre-deployment procedure *(added v1.3)*
- Community Co-Design Requirement — five-question framework *(added v1.3)*
- Bias Loop-Breaking Constraint *(added v1.3)*
- Cumulative Tactical Drift Detection *(added v1.3)*
- Stigma Sentinel and Vulnerable Population Floor guardrails *(added v1.3)*
- Agent state transition rules and simulation scheduling specification (Step 2, Step 5)
- EquiRisk tier definitions (Step 2)
- Opportunity ranking criteria for multi-opportunity selection (Step 4)
- Contact success probability model specification (Step 4)
- HbA1c trajectory model specification (Step 5)
- Equity Audit Layer specification with timing and triggers (Step 7)
- Synthetic population generation guidance (Step 14)
- Data privacy, ethics, and IRB considerations (Step 15)
- Simulation validation checklist (Step 11)
- Worked reference scenario: Milwaukee, updated for multiplicative scoring (Step 12)
- Known limitations and open research questions (Step 13)
- Global adaptation guidance

### This repository does NOT provide:
- Executable simulation code
- City-specific parameter values
- Clinical prediction models or diagnostic tools
- Predictive or prescriptive outputs
- Autonomous decision-making logic

> ⚠️ Simulations built from this CMDDS are **exploratory and comparative**, not predictive or prescriptive. Outputs must not be used as clinical recommendations or policy mandates without independent validation, completion of the bias injection protocol (Step 16), and community co-design (Step 17).

---

## Step 1 — System Purpose and Simulation Questions

### System Purpose

EquiRisk-FoodDeserts simulates how a public health system identifies diabetic individuals in food desert settings, computes a multiplicative EquiRisk priority score combining clinical risk, contextual vulnerability, and action feasibility, matches identified individuals with feasible care and food access opportunities via PAPO, delivers personalized intervention pathways, and monitors equity outcomes against community-validated halt thresholds across prioritization rules and resource conditions.

### Primary Simulation Questions

**Equity Questions:**
- How does EquiRisk-based multiplicative prioritization change the distribution of interventions across income, race, and neighborhood deprivation groups compared to clinical-risk-only approaches?
- Which prioritization rule minimizes the equity gap between the most and least advantaged populations?
- Where do opportunity deserts — areas with high EquiRisk priority scores but no feasible opportunities — concentrate geographically?
- What proportion of high-priority individuals receive a NULL output, and how does this vary by demographic group?
- How does modeling trust barriers and uptake probability change the equity profile of intervention receipt?
- How often does the equity halt threshold activate, and which demographic groups trigger it most? *(added v1.3)*

**Feasibility Questions:**
- How does the action feasibility weight change which individuals receive interventions compared to clinical-only scoring?
- At what resource capacity level does the system begin producing NULL outputs for high-priority individuals?
- Which feasibility constraint (transport, distance, cost, literacy, trust, time, uptake probability) is most binding across the population?

**Policy Questions:**
- How does the timing of policy trigger activation affect equity outcomes?
- Which resource types — food support, CHW visits, telehealth, transportation — produce the greatest equity improvement per unit of investment?
- What happens to equity outcomes when resource pools are reduced by 20%, 40%, or 60%?

**System Performance Questions:**
- What is the mean time from EquiRisk scoring to opportunity delivery for the highest-priority individuals?
- How does the tactical feedback loop (real-time reallocation) improve outcomes compared to a static allocation model?
- How does injecting historical service bias into opportunity ranking affect equity outcomes? *(see Bias Injection Protocol, Step 16)*
- How often does cumulative tactical drift detection fire, and what patterns trigger it? *(added v1.3)*

### Modular Simulation Projects

Developers may implement one focused component rather than the full system:

- **EquiRisk multiplicative scoring validation** — implement the multiplicative priority formula and test against hypothetical patient profiles with varying CVI and feasibility weights *(updated v1.3)*
- **Additive vs. multiplicative comparison** — compare priority rankings produced by the v1.2 additive composite and the v1.3 multiplicative formula on the same population *(added v1.3)*
- **Food desert opportunity mapping** — model resource pool availability and geographic accessibility
- **NULL output analysis** — identify which populations most frequently receive NULL outputs and why
- **Prioritization rule comparison** — compare clinical-only vs. EquiRisk-multiplicative prioritization equity outcomes
- **Tactical vs. static allocation** — compare real-time reallocation to fixed assignment models
- **Bias injection test** — run the five-step Bias Injection Protocol (Step 16) and report disparity delta before and after EquiRisk adjustment *(updated v1.3)*
- **Trust barrier analysis** — model how historical distrust and prior negative system experiences affect contact success rates and equity outcomes
- **Contact success modeling** — implement the contact probability model and test sensitivity to trust barrier and demographic parameters
- **Uptake probability sensitivity** — vary the uptake probability attribute and measure effect on EquiRisk priority distribution and intervention receipt *(added v1.3)*
- **Equity halt threshold simulation** — implement the halt logic and measure how often it fires, by demographic group *(added v1.3)*

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
| `clinical_risk_score` | Composite of above, normalized [0,1] — Layer 1 output | Derived |

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
| `social_support_index` | Composite of household and community support availability *(added v1.3)* | ACS + community survey (synthetic) |
| `contextual_vulnerability_index` (CVI) | **Composite of above, normalized [0,1]** — Layer 2 output, used in multiplicative priority *(formalized v1.3)* | Derived |

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
| `trust_barrier` | Prior negative system experience or documented distrust (low/moderate/high) | Synthetic (race, prior denial history weighted) |
| `uptake_probability` | **Expected probability that the patient successfully accesses and completes a recommended intervention given their structural barrier profile, [0,1]** *(added v1.3)* | Derived from SDOH literature; default model below |
| `action_feasibility_weight` | Composite of above, normalized [0,1] — Layer 3 output, used in multiplicative priority | Derived |

> **Note on contact success vs. uptake probability *(v1.3 clarification)*:** Contact success (Step 4) is the probability that an outreach attempt reaches the patient. Uptake probability is the conditional probability that, once contacted, the patient successfully accesses *and completes* the recommended intervention. The two are sequential — a patient must first be contacted, then must successfully engage with the intervention. Both are modeled separately because they have different causal drivers (trust and reachability for contact; transport, time, cost, literacy, and cultural fit for uptake).

### EquiRisk Priority Score — Multiplicative Formulation *(canonical, v1.3)*

```
EquiRisk_Priority = clinical_risk_score × (1 + CVI) × action_feasibility_weight

Where:
  clinical_risk_score    ∈ [0,1]  (Layer 1, normalized)
  CVI                    ∈ [0,1]  (Layer 2 — Contextual Vulnerability Index)
  CVM = (1 + CVI)        ∈ [1,2]  (Contextual Vulnerability Multiplier)
  action_feasibility_weight ∈ [0,1] (Layer 3, normalized)

Priority range: [0, 2]
Priority interpretation:
  Higher = greater effective expected health burden requiring earlier action
  CVM = 1.0 (no vulnerability)  → priority equals clinical_risk × feasibility (no contextual elevation)
  CVM = 2.0 (maximum vulnerability) → priority is doubled relative to identical-clinical-risk patient with no contextual barriers
```

**Why multiplicative rather than additive:** Two patients with identical clinical risk scores have different *expected* health burdens if their access contexts differ. The contextually vulnerable patient is less likely to act on a standard recommendation, so their expected unmanaged-disease burden is higher. The CVM `(1 + CVI)` term makes this explicit by raising the effective priority of contextually vulnerable patients — without depending on post-hoc allocation weighting. The action_feasibility_weight then attenuates the priority where no feasible pathway exists.

> **Formula calibration:** The default formula above is the canonical EquiRisk priority. Forks may apply a power transform to CVI (e.g., `(1 + CVI^α)` with α ∈ [0.5, 1.5]) or to feasibility (e.g., `feasibility_weight^β`) for sensitivity analysis. Alternative formulations must be documented in the fork README and justified.

### CVI — Contextual Vulnerability Index Construction *(formalized v1.3)*

CVI is constructed as a weighted composite of the Layer 2 attributes:

```
CVI = (v1 * food_desert_status_norm
     + v2 * area_deprivation_index_norm
     + v3 * social_vulnerability_index_norm
     + v4 * grocery_distance_norm
     + v5 * (1 - transit_score)
     + v6 * housing_instability_norm
     + v7 * (1 - clinic_density_norm)
     + v8 * (1 - social_support_index_norm))

Where v1 + v2 + ... + v8 = 1
Default weights (illustrative, requires community calibration):
  v1=0.18 (food desert), v2=0.16 (ADI), v3=0.14 (SVI),
  v4=0.12 (grocery distance), v5=0.10 (transit),
  v6=0.12 (housing), v7=0.10 (clinic density), v8=0.08 (social support)

All sub-attributes normalized to [0,1] before combination.
Resulting CVI ∈ [0,1].
```

> **Community calibration requirement *(v1.3)*:** CVI weights are value choices, not technical optima. The relative importance of food access vs. transportation vs. housing vs. social support reflects community priorities. CVI weights must be reviewed and validated through the Community Co-Design process (Step 17) before deployment. Default weights are starting points for testing implementation structure, not deployment-ready values.

### Default Uptake Probability Model *(added v1.3)*

Uptake probability is the conditional probability that a contacted patient successfully accesses and completes a recommended intervention. It is a Layer 3 attribute used both in the action_feasibility_weight composite and in the PAPO opportunity ranking.

```
P(uptake | contacted) = u_baseline
                      * mobility_modifier
                      * income_modifier
                      * literacy_modifier
                      * cultural_fit_modifier

Where:
  u_baseline = 0.65 (default population-level uptake rate, post-contact)

  mobility_modifier:
    mobility_score = 1 (fully mobile) → 1.00
    mobility_score = 2 (limited)      → 0.80
    mobility_score = 3 (homebound)    → 0.40 (only delivery/telehealth interventions)

  income_modifier:
    income_quartile 4 → 1.00
    income_quartile 3 → 0.90
    income_quartile 2 → 0.75
    income_quartile 1 → 0.60

  literacy_modifier:
    health_literacy_score = 3 (high) → 1.00
    health_literacy_score = 2 (mod)  → 0.85
    health_literacy_score = 1 (low)  → 0.65 (without navigation support)
    health_literacy_score = 1 + CHW navigation support → 0.90

  cultural_fit_modifier:
    Intervention is culturally appropriate for community → 1.00
    Intervention is culturally generic                   → 0.85
    Intervention is documented as culturally inappropriate → 0.55
```

The action_feasibility_weight aggregates uptake probability with the boundary condition compliance state:

```
action_feasibility_weight = uptake_probability × boundary_compliance_factor

Where:
  boundary_compliance_factor:
    All BC-1 through BC-7 satisfied        → 1.0
    Soft boundary violations only          → 0.7
    Any hard boundary violated             → 0.0 (NULL output, no feasible pathway)
```

> **Limitations:** The uptake model is structural, not empirically calibrated. The multiplicative form assumes conditional independence among modifiers — a simplification known to fail when barriers compound (e.g., low literacy + low income + cultural mismatch may interact more than multiplicatively). Sensitivity analysis should test interaction-based formulations. The cultural_fit_modifier in particular requires community input to assign correctly (Step 17).

**EquiRisk Tier Definitions** *(updated v1.3 for multiplicative score range)*:

Composite EquiRisk priority scores are classified into tiers for prioritization and reporting. Default tier boundaries reflect the [0, 2] range of the multiplicative priority. Forks may adjust boundaries with justification, but must document and apply them consistently.

| Tier | Priority Range | Interpretation | Prioritization Implication |
|---|---|---|---|
| Tier 1 — Critical | ≥ 1.20 | High clinical risk amplified by high contextual vulnerability, with feasible pathway | Immediate priority; escalate if no feasible opportunity within one scheduling cycle |
| Tier 2 — High | 0.70 – 1.19 | Elevated combined effective risk | Standard priority queue; match within two scheduling cycles |
| Tier 3 — Moderate | 0.30 – 0.69 | Moderate combined effective risk | Matched as resources allow |
| Tier 4 — Low | < 0.30 | Low effective risk OR low feasibility (review whether feasibility is the binding constraint) | Monitored; matched in surplus resource conditions; flag if feasibility = 0 |

> **Special case — feasibility = 0:** A priority score of 0 produced by `feasibility_weight = 0` (i.e., no feasible pathway) is *not* the same as low effective risk. These cases must produce a NULL output (Step 3) and trigger escalation, not be filed as Tier 4.

> **Tier boundaries are default starting points** for implementation testing, not empirically calibrated thresholds. Sensitivity analysis should test alternative cutpoints and report how tier assignment shifts under different CVI weight configurations and feasibility model parameters.

**Agent States:**
- `unidentified` — not yet reached by the system
- `identified` — EquiRisk priority computed, awaiting opportunity matching
- `matched` — assigned to a feasible opportunity
- `contact_attempted` — outreach initiated; contact not yet confirmed
- `contact_failed` — outreach attempted but patient unreachable or refused
- `in_pathway` — actively receiving intervention
- `escalated` — NULL output received, referred to human case manager
- `lost_to_followup` — dropped out of pathway
- `stabilized` — HbA1c improved to target range

**Agent State Transition Rules:**

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
| `lost_to_followup` | `identified` | Re-screening or human case manager re-activation | 1 | After max re-entry → `escalated`; re-entry resets EquiRisk priority |
| `escalated` | `identified` | Human case manager resolves barrier and re-activates | 1 | Requires documented resolution; re-entry resets EquiRisk priority |
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
                                    (re-entry with new EquiRisk priority)
```

> **Re-entry safeguard:** All re-entry transitions require a new EquiRisk priority calculation at the time of re-entry. The prior score is archived for longitudinal tracking but does not carry forward. Maximum re-entry counts are enforced per agent per simulation run; exceeding the limit forces transition to `escalated`.

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

> **Resource pool requirements:** All resource pools must be modeled as exhaustible, spatially located, and replenished on defined cycles. Static or unlimited resource assumptions are not permitted in valid EquiRisk-PAPO implementations. Resource pool attributes should include a `trust_alignment` flag indicating whether the provider has a known trust deficit with specific community groups, which affects the effective feasibility score for matched individuals, and a `cultural_fit` flag indicating whether the intervention has been validated as culturally appropriate for the community served (used in the uptake probability cultural_fit_modifier).

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
| EquiRisk priority override | Clinician or case manager review |
| NULL output escalation | Human case manager assignment |
| High-intensity resource allocation (CHW) | Supervisor authorization |
| Patient opt-out or refusal | Human acknowledgment and documentation |
| Data privacy exception | Privacy officer review |
| Trust barrier flag — high severity | Cultural liaison or trusted community organization referral |
| Agent re-entry from `escalated` or `lost_to_followup` | Human case manager authorization with documented barrier resolution |
| Equity halt threshold breach | Program manager + equity officer review before resumption *(added v1.3)* |
| Bias loop-breaking constraint exception | Governance approval with documented evidence upgrade *(added v1.3)* |
| Pre-deployment community co-design sign-off | Community representatives + ethicist *(added v1.3)* |

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
| `historical_service_bias_map` | Census-tract-level record of historical underservice or program exclusions |
| `community_calibration_record` | Documented community co-design inputs: validated CVI weights, intervention pathway approvals, equity halt threshold *(added v1.3)* |

---

## Step 3 — Action Feasibility: Boundary Conditions

> This section specifies the explicit boundary conditions that determine whether an opportunity is considered feasible for a given individual. These conditions are **non-negotiable** in valid implementations — an opportunity that violates any hard boundary condition must output NULL for that individual, which sets `boundary_compliance_factor = 0` and therefore `action_feasibility_weight = 0`.

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

#### BC-7: Trust and Engagement Boundaries

> Trust is a structural barrier shaped by historical exclusion, prior negative experiences, and systemic racism in healthcare. It is modeled here as a system-level constraint, not an individual character trait.

| Condition | Hard Boundary | Soft Boundary |
|---|---|---|
| High trust barrier + no trusted community referral pathway | Infeasible for initial outreach without cultural liaison or community organization intermediary | Moderate trust barrier = reduced contact success probability; CHW with community ties preferred |
| Provider has documented trust deficit with patient's community | Direct provider referral = infeasible; community intermediary required | Known trust gap = flag for trust-aligned opportunity matching |
| Prior documented refusal due to negative system experience | Direct re-contact = infeasible without new pathway or trusted intermediary | Prior reluctance = reduced contact success probability; extended outreach window |

#### BC-8: Cultural Appropriateness Boundaries *(added v1.3)*

> Cultural fit affects uptake probability separately from feasibility. A program may be technically accessible but culturally inappropriate, in which case uptake is poor even when contact succeeds. Per Community Co-Design (Step 17), cultural appropriateness must be community-validated.

| Condition | Hard Boundary | Soft Boundary |
|---|---|---|
| Intervention documented as culturally inappropriate by community | Infeasible for primary recommendation; offer only with explicit patient choice | Generic-not-tailored intervention = reduced uptake (cultural_fit_modifier = 0.85) |
| Dietary intervention conflicting with cultural or religious food practices | Infeasible without adaptation | Modified intervention available = feasible with reduced score |

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
7. Distinguish between "no opportunity exists", "opportunity exists but unreachable",
   "trust barrier blocks contact", and "cultural mismatch blocks uptake"
   — these represent different system failures requiring different responses

NULL Output must NOT:
1. Assign a default low-quality opportunity to avoid NULL
2. Override hard boundary conditions algorithmically
3. Be resolved without human review for high-EquiRisk individuals
4. Be treated identically regardless of which boundary condition triggered it
```

> **NULL output as feasibility = 0:** When NULL is produced, the agent's `action_feasibility_weight = 0`, which sets `EquiRisk_Priority = 0`. This is a structural NULL, not low risk — the patient is recorded and escalated, not deprioritized.

---

## Step 4 — PAPO Integration: Policy-to-Opportunity Translation Logic

### The Core Translation Mechanism

PAPO operates as the delivery engine that receives EquiRisk priority scores and translates them into actionable pathways. The translation follows this logic:

```
INPUT:
  patient.EquiRisk_Priority (multiplicative score)
  patient.feasibility_profile (boundary conditions assessed)
  patient.program_eligibility
  patient.trust_barrier
  patient.uptake_probability

STEP 1 — Policy Trigger Check:
  Is there an active program this patient is eligible for?
  If NO → output NULL (type: no_program) → escalate
  If YES → proceed to Step 2

STEP 2 — Opportunity Query:
  Query resource pools within feasible geographic range
  Filter by: mobility constraints, cost boundary, language,
             hours, capacity availability, trust alignment, cultural fit

STEP 3 — Feasibility Check:
  Apply all BC-1 through BC-8 boundary conditions
  Score remaining opportunities by feasibility
  If no opportunity satisfies all hard boundaries:
    → output NULL (type-coded: no_opportunity | unreachable |
                   trust_barrier | cultural_mismatch)

STEP 4 — Opportunity Ranking:
  Rank feasible opportunities using opportunity ranking criteria (see below)
  Select top-ranked opportunity for assignment

STEP 5 — Contact Probability Assessment:
  Estimate contact success probability using default model (see below)
  If P(contact) < 0.2 and no trust-aligned intermediary available:
    → Flag for extended outreach protocol

STEP 6 — Uptake Probability Check:
  Verify uptake_probability for selected opportunity ≥ minimum threshold (default 0.30)
  If below threshold:
    → Either rank-down this opportunity and retry, or
    → Flag for navigation support assignment, or
    → Output NULL (type: low_uptake) if no support available

STEP 7 — Output:
  If feasible opportunity exists with acceptable contact and uptake probability:
    → Assign top-ranked opportunity
    → Generate personalized pathway (resource + timing + navigation support)
    → Record assignment and reduce resource pool capacity
    → Transition agent to `matched` state

  If no feasible opportunity exists:
    → Output NULL (type-coded as above)
    → Trigger escalation pathway
    → Record NULL reason and boundary condition(s) violated
    → Add to tactical feedback queue
    → Transition agent to `escalated` state

STEP 8 — Human Handover:
  Pathway delivered to human staff for:
    → Patient notification and consent
    → Navigation support arrangement
    → Authorization where required
    → Trust-sensitive outreach approach where BC-7 applies
    → Cultural liaison engagement where BC-8 applies
```

### Opportunity Ranking Criteria

> PAPO Step 4 ranks *opportunities* for a given patient, which is distinct from the *patient* prioritization rules in Step 8. Patient prioritization determines *who* is served first; opportunity ranking determines *which resource* a given patient receives when multiple feasible options exist.

When a patient has multiple feasible opportunities after boundary condition filtering, opportunities are ranked using a weighted composite of the following criteria:

| Criterion | Weight (default) | Definition | Rationale |
|---|---|---|---|
| Trust alignment | 0.25 | Does the provider/resource have established trust with the patient's community? (binary, 0 or 1) | Trust-aligned resources improve contact success and pathway completion |
| Cultural fit *(added v1.3)* | 0.15 | Is the intervention validated as culturally appropriate for the patient's community? (0/0.85/1) | Cultural fit drives uptake probability separately from access |
| Proximity | 0.20 | Inverse of distance from patient to resource (normalized to [0,1] within feasible set) | Closer resources reduce transport barriers and no-show risk |
| Clinical match | 0.20 | Does the resource type directly address the patient's primary clinical need? (scored 0–1) | Clinical relevance improves health outcomes per intervention |
| Cost burden | 0.10 | Inverse of patient cost as share of income (normalized to [0,1]) | Lower cost burden improves uptake and sustained engagement |
| Capacity margin | 0.10 | Remaining capacity of resource pool (normalized to [0,1]) | Resources near exhaustion carry higher risk of scheduling failure |

```
Opportunity_Rank_Score = 0.25 * trust_alignment
                       + 0.15 * cultural_fit
                       + 0.20 * proximity_norm
                       + 0.20 * clinical_match
                       + 0.10 * (1 - cost_burden_norm)
                       + 0.10 * capacity_margin_norm

Select the opportunity with the highest Opportunity_Rank_Score.
Ties are broken by proximity (closer first), then by capacity margin (higher first).
```

> Opportunity ranking weights are default starting points. Simulations should test at least one alternative configuration. Document weights used in fork README.

### Default Contact Success Probability Model

> Contact success is the probability that an outreach attempt reaches the patient. It is distinct from uptake probability (Step 2), which is the conditional probability of completing the intervention once contacted.

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

> The multiplicative form assumes conditional independence among modifiers — a simplification. Sensitivity analysis should test additive and interaction-based formulations.

### Two Feedback Loops (Must Be Separated)

**Tactical Loop (minutes to hours) — Real-Time Reallocation:**
- Triggered by: NULL output, resource exhaustion, patient refusal, no-show, contact failure
- Actions: Reallocate resource to next-priority patient, adjust capacity counts, flag bottlenecks
- Decision authority: Frontline staff or automated reallocation within pre-authorized rules
- Must NOT modify: prioritization rules, eligibility criteria, EquiRisk weights, CVI weights

**Strategic Loop (months) — Policy and Resource Update:**
- Triggered by: End of program cycle, equity audit findings, funding changes
- Actions: Update resource pool locations and capacities, adjust program eligibility rules, revise CVI weights based on community input and outcome data, add or remove opportunity types, revise trust-alignment classifications of providers
- Decision authority: Program managers and policy staff only
- Must NOT: Operate on individual patient data in real time

> ⚠️ Conflation of tactical and strategic loops is not permitted in valid implementations. They operate on different timescales, involve different decision authorities, and modify different system components.

### Bias Loop-Breaking Constraint *(added v1.3)*

> Stage 2 (PAPO) outputs become inputs to subsequent program enrollment records, completion tracking, and outcome data. Without an explicit constraint, these outputs re-enter Stage 1 (knowledge graph and risk modeling) as training data — encoding the EquiRisk system's own decisions as evidence of "what works." This re-encodes selection bias at scale and breaks the comparative validity of the framework.

**Constraint specification:**

```
RULE: Stage 2 PAPO outputs (assigned opportunities, completion records,
      patient outcome data generated under EquiRisk routing) must NOT
      re-enter Stage 1 training data without:

  (a) Documented governance review and approval
  (b) Evidence upgrade — the new training records must be validated
      against an independent evidence source (RCT, external cohort,
      community health survey not influenced by EquiRisk routing)
  (c) Bias re-injection test (Step 16) re-run on the upgraded training set
  (d) Disparity delta < 10% maintained in the upgraded model

If any of (a)–(d) fail, the Stage 2 outputs are flagged as observational-
only data and excluded from training. They may still be reported in
equity audits and used for descriptive analysis.
```

**Why this matters for diabetes in food deserts:** Program enrollment data systematically under-represents food desert non-completers (case report §5). If EquiRisk routing improves access for these patients, their outcomes generate new training data — but if the improvement is partial, the new data still under-represents the hardest-to-reach. Without the loop-breaking constraint, the system "learns" from its own incomplete reach and re-encodes the original bias.

### Cumulative Tactical Drift Detection *(added v1.3)*

> Individual tactical decisions are within authority. But a sustained pattern of tactical decisions can produce strategic-level outcomes (e.g., food desert patients consistently routed to telehealth instead of CHW visits, across many decisions, without any governance review). This is "cumulative drift": tactical actions cumulating into a strategic shift.

**Detection specification:**

```
Maintain a rolling window of N most recent tactical decisions per
demographic stratum (race, income quartile, ADI quartile, food desert status).

Default window sizes:
  Continuous programs (daily decisions)     → N = 100
  Quarterly cycle programs                  → N = 50

For each stratum, compute over the window:
  - Distribution of resource types assigned (CHW vs. telehealth vs. food support, etc.)
  - Mean uptake probability of assigned opportunities
  - NULL output rate

Drift alert fires if any of the following holds:
  (i)   Resource-type distribution for a stratum diverges by > 15 pp
        from the population baseline distribution
  (ii)  Mean uptake probability for a stratum drops > 20 pp below baseline
  (iii) NULL output rate for a stratum exceeds population mean by > 15 pp

On drift alert:
  → Pause further tactical reallocation for the affected stratum
  → Notify program manager + equity officer
  → Strategic review required before tactical loop resumes for that stratum
```

> **Calibration note:** Window sizes and threshold magnitudes are defaults for testing. Larger populations and longer programs may warrant larger windows; communities with smaller eligible populations may need smaller windows to remain responsive. Document choices in fork README.

---

## Step 5 — Multi-Scale Simulation Architecture

### Simulation Time Step and Scheduling

> The simulation time step defines the temporal resolution at which the system processes events. This specification supports both discrete-time and discrete-event implementations; the choice should be documented in the fork README.

**Default discrete-time specification:**

| Component | Time Step | Rationale |
|---|---|---|
| Base simulation tick | 1 day | Minimum resolution for appointment scheduling and resource replenishment |
| EquiRisk priority computation | On entry to `identified` state, and on any re-entry transition | Score reflects current status at time of assessment |
| PAPO opportunity matching | 1 day (within scheduling cycle) | Patients in `identified` state are matched each daily tick, ordered by EquiRisk priority |
| Contact attempts | 1 per 3 days (default outreach cadence) | Allows response time; adjustable per fork |
| Resource pool replenishment | Per resource type (daily, weekly, monthly — see Entity 2) | Matches real-world resource availability cycles |
| Tactical feedback loop | Triggered within same daily tick as event | Real-time reallocation simulated as within-day processing |
| Drift detection rolling window update | Every tactical decision *(added v1.3)* | Window updated continuously; alerts fire on threshold crossing |
| Strategic feedback loop | Every 90 days (default) | Quarterly review cycle; adjustable per fork |
| Equity audit | Every 30 days and at simulation end | Monthly monitoring plus final reporting (see Step 7) |
| Equity halt threshold check *(added v1.3)* | Every 30 days as part of equity audit; ad hoc on alert | Halt condition evaluated at audit cadence |
| HbA1c trajectory update | Every 30 days for agents in `in_pathway` or `stabilized` states | Monthly clinical update cycle |

**Scheduling cycle definition:** A scheduling cycle is the period within which PAPO attempts to match all patients in the `identified` state. Default = 7 days. Patients not matched within one scheduling cycle remain in `identified` and are re-queued at the start of the next cycle with updated priority. Tier 1 patients not matched within one cycle trigger an escalation alert.

**Discrete-event alternative:** Implementations may use discrete-event scheduling where state transitions are triggered by events rather than fixed ticks. In this case, the time intervals above serve as maximum inter-event intervals. Document the scheduling approach used.

### Individual Scale
- Each agent is scored by EquiRisk and matched (or not) by PAPO
- Tracks: opportunity received, time to intervention, pathway completion, HbA1c trajectory, contact success or failure, uptake outcome
- Key output: individual equity outcome by demographic group

### Neighborhood Scale
- Aggregates individual outcomes by census tract
- Maps opportunity deserts: high-priority density + low opportunity availability
- Tracks: NULL output rate by neighborhood, resource utilization by facility, contact failure concentration
- Key output: neighborhood equity gap map

### City Scale
- Aggregates across all neighborhoods
- Evaluates policy trigger timing and city-wide resource allocation efficiency
- Tracks: overall equity gap, prioritization rule comparison, resource investment vs. equity return, drift alerts and halt threshold breaches *(updated v1.3)*
- Key output: city-level equity audit report

### Scale Interaction Rules
- Individual agents draw from neighborhood-level resource pools
- Neighborhood resource depletion affects city-level allocation decisions
- City-level policy changes propagate down to neighborhood and individual eligibility
- Feedback loops operate within their authorized scale — tactical at individual/neighborhood, strategic at city

### Default HbA1c Trajectory Model

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

> **Limitations:** This model assumes linear trajectories, no ceiling/floor effects, and no interaction between clinical and contextual variables on HbA1c. It is suitable for testing system logic (does the right person get the right intervention?) but should not be interpreted as a clinical projection.

---

## Step 6 — Required Components for a Valid Implementation

Any fork claiming to implement EquiRisk-FoodDeserts v1.3 must include:

| Component | Requirement |
|---|---|
| **Three-layer EquiRisk scoring** | All three layers (clinical, contextual, feasibility) must be implemented and scored separately before combination |
| **Multiplicative EquiRisk priority** | Priority must be computed as `clinical_risk_score × (1 + CVI) × action_feasibility_weight`; sub-scores must be normalized before combination *(updated v1.3)* |
| **CVI composite** | Contextual Vulnerability Index must be computed as a documented weighted composite of Layer 2 attributes; weights must be documented and (for deployment) community-validated *(added v1.3)* |
| **Uptake probability attribute** | Uptake probability must be computed and reported separately from contact success probability *(added v1.3)* |
| **EquiRisk tier assignment** | Composite priorities must be assigned to tiers using documented cutpoints; default tiers are provided in Step 2 |
| **Exhaustible resource pools** | All opportunity types must be capacity-constrained and spatially located |
| **Boundary condition evaluation** | At minimum BC-1 (geographic), BC-3 (mobility), BC-7 (trust), and BC-8 (cultural fit) must be implemented; all eight are recommended *(updated v1.3)* |
| **NULL output with escalation** | NULL output is required when no feasible opportunity exists; silent failure is not permitted; NULL must be type-coded |
| **Separated feedback loops** | Tactical and strategic loops must be distinct; conflation invalidates the implementation |
| **Bias loop-breaking constraint** | Stage 2 outputs must not re-enter Stage 1 training data without governance approval and bias re-injection *(added v1.3)* |
| **Cumulative tactical drift detection** | Rolling window monitoring of tactical decisions, with drift alert thresholds *(added v1.3)* |
| **Prioritization rule comparison** | At minimum two rules must be compared: clinical-risk-only vs. EquiRisk-multiplicative |
| **Equity metric** | At minimum one equity metric must be defined before simulation and reported disaggregated by group |
| **Equity halt threshold** | Halt threshold must be defined before simulation; halt logic must be implemented; resumption criteria must be documented *(added v1.3)* |
| **Human handover specification** | Authorization boundaries must be explicitly defined |
| **Contact success modeling** | Contact failure rates must be modeled; outcomes must not assume universal reachability |
| **State transition enforcement** | Agent state transitions must follow the permitted transitions table; re-entry limits must be enforced |
| **Opportunity ranking** | When multiple feasible opportunities exist, selection must follow documented ranking criteria |
| **Simulation time step** | The scheduling approach (discrete-time or discrete-event) and all time intervals must be documented |

### Strongly Recommended Enhancements
- Bias injection: full execution of the five-step Bias Injection Protocol (Step 16) *(updated v1.3)*
- Sensitivity analysis: vary CVI weights, feasibility model parameters, and tier boundaries
- Scenario comparison: high-resource vs. low-resource city conditions
- Global context fork: implement in a non-US city with different food system and policy environment
- Trust barrier sensitivity: vary BC-7 thresholds and compare equity outcomes with and without trust modeling
- Cultural fit sensitivity: vary BC-8 thresholds and the cultural_fit_modifier *(added v1.3)*
- Opportunity ranking weight sensitivity: compare default weights against alternatives
- Contact model calibration: if local outreach data is available, calibrate baseline and modifier values
- Additive vs. multiplicative comparison: re-score the same population under v1.2 additive and v1.3 multiplicative formulas; report ranking divergence *(added v1.3)*

---

## Step 7 — Equity Metrics, Equity Audit Layer, Halt Threshold, and Sentinel Guardrails

Choose at least one equity metric before simulation. Report results disaggregated by race, income quartile, and neighborhood deprivation level.

| Metric | Definition | When to Use |
|---|---|---|
| **Equal allocation** | Each group receives interventions proportional to group size | Baseline comparison |
| **Equal outcomes** | Each group achieves equivalent HbA1c improvement | Equity goal metric |
| **Prioritizing** | Higher-need groups receive disproportionately more resources | When equity gap reduction is primary goal |
| **Sufficiency** | Each group receives enough to meet a defined minimum threshold | When minimum standard of care is the policy goal |
| **Contact success rate** | Proportion of identified individuals successfully contacted, by demographic group | When trust barriers and reachability are in scope |
| **Uptake completion rate** *(added v1.3)* | Proportion of contacted individuals who complete the recommended intervention, by demographic group | When uptake probability is in scope; complements contact success |
| **Equity-weighted expected receipt** *(added v1.3)* | Receipt rate that would obtain if interventions were distributed in proportion to EquiRisk priority within each demographic group | Reference distribution for equity halt threshold |

**Required equity outputs:**
- Opportunity receipt rate by race, income quartile, neighborhood ADI quartile
- NULL output rate by the same demographic dimensions
- NULL output type distribution (no_opportunity / unreachable / trust_barrier / cultural_mismatch / low_uptake) by demographic group *(updated v1.3)*
- Contact success rate by demographic group
- Uptake completion rate by demographic group *(added v1.3)*
- Time to first intervention by EquiRisk tier
- Equity gap = difference in opportunity rate between highest and lowest access groups
- Equity gap change under each prioritization rule
- Halt threshold breach events and resolutions *(added v1.3)*

### Equity Audit Layer Specification

The Equity Audit Layer operates as a periodic review mechanism that evaluates whether the EquiRisk-PAPO system is delivering opportunities equitably across demographic groups. It is not a real-time decision component — it operates on aggregated data and feeds into the strategic feedback loop and the Equity Halt Threshold check.

**Timing and Triggers:**

| Trigger | Frequency | Action |
|---|---|---|
| Scheduled periodic audit | Every 30 simulation days (default) | Generate equity audit report; flag disparities exceeding alert thresholds; check halt threshold |
| End of simulation | Once | Generate final comprehensive equity audit report |
| Strategic feedback loop activation | Every 90 days (default) | Equity audit report is a required input to strategic review |
| Manual trigger | On demand (human-initiated) | Ad hoc audit for specific concern |
| Drift alert *(added v1.3)* | When cumulative tactical drift detection fires | Stratum-specific audit for affected demographic group |

**Required Equity Audit Outputs:**

Each audit report must include:

1. **Distributional summary** — opportunity receipt rate, NULL output rate, contact success rate, and uptake completion rate disaggregated by race, income quartile, and ADI quartile *(updated v1.3)*
2. **NULL output analysis** — NULL type distribution by demographic group, with identification of which boundary conditions are most frequently triggered per group
3. **Tier-level performance** — mean time to first intervention by EquiRisk tier, with flag if Tier 1 mean exceeds two scheduling cycles
4. **Equity gap tracking** — equity gap metric (Q4 vs. Q1 opportunity rate) over time, with trend direction
5. **Prioritization rule comparison** — side-by-side equity outcomes under each active prioritization rule
6. **Resource utilization equity** — which resource types are consumed by which demographic groups, flagging if high-priority groups are disproportionately routed to lower-intensity resources
7. **Re-entry and cycling analysis** — rates of re-entry from `lost_to_followup`, `escalated`, and `stabilized` states by demographic group
8. **Halt threshold status** — current receipt rate vs. equity-weighted expected receipt for each protected stratum; breach status; days since last breach *(added v1.3)*
9. **Drift detection summary** — rolling window resource-type distributions and drift alert history *(added v1.3)*

### Equity Halt Threshold *(added v1.3)*

> The equity halt threshold is a hard guardrail that suspends EquiRisk-PAPO routing when receipt rates for vulnerable populations fall too far below the rate that the multiplicative priority model itself predicts. It is a check on whether the system is actually delivering on its priority calculation.

**Default specification:**

```
For each protected stratum S (e.g., food desert residents, ADI quartile 4 residents,
specific race/ethnicity groups identified through community co-design):

  expected_rate(S) = (sum of EquiRisk_Priority over all identified agents in S)
                   / (sum of EquiRisk_Priority over all identified agents)
                   * total_intervention_capacity

  observed_rate(S) = actual interventions delivered to agents in S

  halt_ratio(S)    = observed_rate(S) / expected_rate(S)

HALT TRIGGER:
  If halt_ratio(S) < 0.70 for stratum S over a complete equity audit period (30 days):
    → HALT NEW ROUTING for stratum S
    → Continue active pathways already in progress
    → Notify program manager + equity officer + community liaison
    → Require strategic review before resumption
```

> **Default 70% threshold:** This corresponds to the case report's recommendation (food desert patient receipt rate must remain ≥ 70% of equity-weighted expected rate). The threshold itself is a community-validated value choice (Step 17), not a technical optimum. Some communities may set a higher floor (e.g., 80%); others may accept a lower floor with explicit justification.

**Resumption criteria:**

```
Routing for halted stratum S may resume when ALL of the following hold:

  (a) Strategic review completed and root cause identified
      (e.g., resource pool exhaustion, geographic mismatch, contact failure spike)
  (b) Corrective action implemented and documented
      (e.g., resource reallocation, new opportunity types added, outreach revised)
  (c) Simulation re-run with corrective action in place shows
      projected halt_ratio(S) ≥ 0.85 for next audit period
  (d) Community liaison sign-off on the corrective action
  (e) Equity officer authorization to resume
```

> **Halt is not punishment — it is a signal:** A halt indicates that the system's priority calculation and its delivery are out of alignment, and continued operation will deepen disparity. Resumption requires fixing the system, not relaxing the threshold.

### Stigma Sentinel *(added v1.3)*

> Public health programs often produce language and recommendation framings that stigmatize the patients they aim to serve. Diabetes management is particularly prone to this — language around "compliance," "non-adherence," "lifestyle choices," and "patient responsibility" can shift moral burden onto people facing structural barriers. The stigma sentinel monitors output language for stigmatizing patterns.

**Specification:**

```
For all human-facing output text generated by the system (recommendations,
patient communications, navigator briefings, equity audit narratives):

  Apply NLP scan for stigmatizing language patterns:
    - Compliance/non-compliance framing
    - "Failure to" constructions (failure to attend, failure to manage)
    - Lifestyle-blame framing for structurally constrained behaviors
    - Food choice framing that ignores food desert context
    - Weight-stigmatizing language

  On detection:
    → Flag the output for human review before delivery
    → Suggest non-stigmatizing alternative phrasing
    → Log occurrence for periodic review

Periodic review:
    → Every 90 days, summarize sentinel hits by output type
    → Strategic loop input: pattern of repeated stigma flags requires
      template revision, not just per-instance correction
```

### Vulnerable Population Floor *(added v1.3)*

> Independent of the equity halt threshold, certain doubly-vulnerable populations (chronic disease + structural deprivation, e.g., food desert residents with diabetes) receive a minimum recommendation weight that cannot be optimized below. This protects against efficiency-oriented prioritization rules pushing these populations below a baseline.

**Specification:**

```
Define vulnerable_population strata at deployment (community-validated, Step 17).
Default for diabetes-in-food-deserts: agents with food_desert_status = 1
AND area_deprivation_index >= 80th percentile.

For all prioritization rules:
  effective_priority(agent in vulnerable_population) =
      max(EquiRisk_Priority(agent), vulnerable_floor_priority)

  vulnerable_floor_priority = 0.50 (default — equivalent to mid-Tier 3)

The floor is NOT applied to the multiplicative priority calculation itself;
it is applied at the prioritization queue ordering step. This ensures
vulnerable population agents never sort below the floor regardless of
what the priority formula returns.

Exception: If feasibility_weight = 0 (NULL output), the floor does not
apply — no feasible pathway means no intervention can be assigned, and
the agent escalates rather than holds queue position.
```

**Alert Thresholds (defaults):**

| Condition | Threshold | Action |
|---|---|---|
| NULL output rate disparity between highest and lowest ADI quartile | > 15 percentage points | Flag for strategic review |
| Contact success rate disparity by race | > 20 percentage points | Flag for BC-7 and outreach protocol review |
| Uptake completion rate disparity by income quartile *(added v1.3)* | > 20 percentage points | Flag for BC-8 cultural fit review and navigation support assessment |
| Tier 1 agents remaining in `identified` beyond 2 scheduling cycles | > 10% of Tier 1 agents | Flag for immediate resource reallocation review |
| Equity gap widening for 3 consecutive audit periods | Any magnitude | Flag for strategic review |
| Halt threshold breach *(added v1.3)* | halt_ratio(S) < 0.70 for any stratum S over 30 days | HALT routing for stratum; strategic review required |
| Stigma sentinel hit rate *(added v1.3)* | > 5% of generated outputs flagged in any 30-day period | Template revision in strategic loop |

> Alert thresholds are implementer-defined defaults for testing. Forks should adjust based on local equity goals and population characteristics. Thresholds must be documented before simulation begins and (for the halt threshold) community-validated.

**Governance:**
- Equity audit reports are reviewed by program managers and equity officers, not by the automated system
- The equity audit layer does not modify prioritization rules, EquiRisk weights, CVI weights, or resource allocations directly — it produces findings that inform human decisions in the strategic feedback loop
- Halt threshold decisions require community liaison participation in the resumption review *(added v1.3)*
- Audit reports are archived and versioned for longitudinal comparison across simulation runs

---

## Step 8 — Prioritization Rules

Implement and compare at least two of the following:

| Rule | Logic | Expected Equity Effect |
|---|---|---|
| **Clinical risk only** | Rank by clinical_risk_score alone | Baseline — likely favors less disadvantaged patients |
| **EquiRisk multiplicative** *(canonical, v1.3)* | Rank by `clinical_risk × (1 + CVI) × feasibility_weight` | Primary equity improvement rule; case-report-validated formulation |
| **EquiRisk additive** *(deprecated, retained for comparison)* | Rank by `w1*clinical + w2*contextual + w3*(1-feasibility)` (v1.0–v1.2 form) | Used only for backward comparison; not recommended for deployment *(updated v1.3)* |
| **Worst-off first** | Rank by CVI alone | Maximum equity focus |
| **Feasibility first** | Rank by action_feasibility_weight (easiest to reach first) | Efficiency-oriented — likely worsens equity |
| **Random** | Random assignment within eligibility | Equity neutrality baseline |
| **Trust-adjusted EquiRisk** | EquiRisk_Priority weighted additionally by inverse trust_barrier severity | Tests whether trust-centered routing further improves equity |

> The minimum required comparison is **clinical-risk-only vs. EquiRisk-multiplicative**. This directly operationalizes the central argument of the EquiRisk paper and the case report finding that contextual vulnerability adjusts effective risk, not just allocation.

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
| Once contacted, patients complete interventions | Uptake completion varies with structural barriers, cultural fit, and competing demands | Vary uptake probability modifiers; test interaction-based formulations *(added v1.3)* |
| Food desert boundaries are stable | Food access changes seasonally and with store openings/closures | Model dynamic food desert boundaries |
| CVI weights are valid | Optimal weights vary by community, season, and prior experience with system | Sensitivity analysis across CVI weight configurations; community recalibration *(updated v1.3)* |
| Multiplicative priority is the correct functional form | Real interactions among layers may not be multiplicative; they may be additive in some regions and super-multiplicative in others | Compare multiplicative, additive, and power-transform formulations; report ranking divergence *(added v1.3)* |
| Resources are uniformly distributed within service areas | Resources cluster in accessible areas, leaving hardest-to-reach patients underserved | Inject spatial clustering of resources |
| Trust is static | Trust evolves over time with system interactions — positive or negative | Model trust as a dynamic variable that updates based on contact and outcome history |
| Cultural fit is binary or fixed | Cultural fit is graded, dynamic, and community-defined | Vary cultural_fit_modifier; require community input on cultural fit assignment *(added v1.3)* |
| Contact modifiers are independent | Trust, housing, language, and time availability likely interact | Test multiplicative vs. additive vs. interaction-based contact models |
| Uptake modifiers are independent | Mobility, income, literacy, and cultural fit likely interact when barriers compound | Test interaction-based uptake models *(added v1.3)* |
| HbA1c trajectory is linear | Real HbA1c response is non-linear with ceiling effects and individual variability | Test non-linear decay functions and stochastic individual trajectories |
| Synthetic population reflects real joint distributions | Correlation structure between clinical, contextual, and feasibility attributes may be misspecified | Compare outcomes using different copula assumptions or empirical correlation matrices |
| Bias-free training data | Administrative data systematically under-represents food desert non-completers | Run Bias Injection Protocol (Step 16) before deployment *(added v1.3)* |
| Tactical decisions don't accumulate into strategic shifts | Repeated tactical reallocations can produce systematic patterns without governance review | Run cumulative tactical drift detection (Step 4); test alternative window sizes *(added v1.3)* |

> ⚠️ Failure to model these assumptions will produce optimistic, non-generalizable results.

---

## Step 10 — Global Adaptation Guide

EquiRisk-FoodDeserts is designed to be forked for any city globally. The core logic is preserved across all forks. What changes per city:

### What Stays the Same (Core Logic — Do Not Modify)
- Three-layer EquiRisk scoring architecture
- Multiplicative priority formula `clinical × (1 + CVI) × feasibility` *(updated v1.3)*
- PAPO policy-to-opportunity translation mechanism
- NULL output requirement (including type-coding)
- Separated feedback loops
- Bias loop-breaking constraint *(added v1.3)*
- Cumulative tactical drift detection *(added v1.3)*
- Equity halt threshold mechanism (the threshold value is locally calibrated; the *requirement* is universal) *(added v1.3)*
- Bias Injection Protocol as pre-deployment requirement *(added v1.3)*
- Community Co-Design as pre-deployment requirement *(added v1.3)*
- Human handover requirements
- Equity metric reporting requirements
- BC-7 trust barrier and BC-8 cultural appropriateness categories (the concepts are universal; parameters are local)
- Agent state transition rules and re-entry limits
- Equity Audit Layer structure and minimum reporting requirements

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
| Cultural fit reference groups *(added v1.3)* | Community-defined per fork | Community-defined per fork | Community-defined per fork |
| CVI weights *(added v1.3)* | Community-validated per fork | Community-validated per fork | Community-validated per fork |
| Equity halt threshold *(added v1.3)* | Default 0.70; community-validated | Default 0.70; community-validated | Default 0.70; community-validated |
| Drift detection window N *(added v1.3)* | 50 (quarterly) / 100 (continuous) | Calibrate to program cycle | Calibrate to program cycle |
| Contact success baseline | 0.70 (default) | Calibrate to local outreach data | Calibrate to local data |
| Uptake baseline u_baseline *(added v1.3)* | 0.65 (default) | Calibrate to local data | Calibrate to local data |
| HbA1c improvement rate | 0.1 pp/month (default) | Calibrate to local clinical data | Calibrate to local data |

### Minimum Adaptation Requirements for Non-US Forks
1. Replace ADI/SVI with locally available deprivation index
2. Redefine food desert boundary criteria for local food system
3. Specify locally available opportunity types
4. Identify relevant policy trigger mechanisms
5. Define locally appropriate equity dimensions
6. Define locally relevant trust barrier reference groups and historical exclusion patterns
7. Define locally relevant cultural fit reference groups *(added v1.3)*
8. Calibrate CVI weights through Community Co-Design (Step 17) *(added v1.3)*
9. Calibrate contact success baseline, uptake baseline, and modifier values to local outreach data where available *(updated v1.3)*
10. Set the equity halt threshold through community validation *(added v1.3)*
11. Run the Bias Injection Protocol (Step 16) on the local training data before deployment *(added v1.3)*
12. Document all substitutions clearly in fork README

---

## Candidate Cities for Forking

This framework is well-suited for cities with:
- Significant diabetic population with food insecurity overlap
- Neighborhood-level data availability
- Active diabetes management programs to simulate

### Readiness Criteria

Before selecting a city for forking, assess availability of:

| Criterion | Minimum Requirement | Preferred |
|---|---|---|
| Deprivation data | Census-tract-level deprivation index | Sub-tract or block-group level |
| Food access data | City-level grocery store locations | USDA-equivalent access atlas |
| Clinical population data | Synthetic or aggregate HbA1c data by neighborhood | Linked EHR + claims data |
| Program inventory | Known diabetes management programs with eligibility rules | Real-time capacity data |
| Trust/historical context | Published documentation of historical underservice | Community organization input |
| Outreach contact data | Aggregate contact success rates by program | Demographic-stratified contact rates |
| Community partner availability *(added v1.3)* | At least one community organization willing to participate in co-design | Established community advisory council |
| Bias injection capacity *(added v1.3)* | Ability to obtain or simulate non-administrative comparison data | Linked community health survey or screening data |

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

## Step 11 — Simulation Validation Checklist

Before reporting results from any simulation built on this CMDDS, complete the following checklist. Document outcomes in fork README.

### Structural Validity
- [ ] All three EquiRisk layers are implemented and scored independently before combination
- [ ] CVI is computed as a documented weighted composite of Layer 2 attributes *(added v1.3)*
- [ ] Uptake probability is computed as a documented attribute, separate from contact success *(added v1.3)*
- [ ] Multiplicative EquiRisk priority is computed as `clinical × (1 + CVI) × feasibility_weight` *(updated v1.3)*
- [ ] Sub-scores are normalized to [0,1] before combination
- [ ] CVI weights are documented and (for deployment) community-validated *(added v1.3)*
- [ ] EquiRisk tier boundaries are documented and applied consistently using v1.3 ranges
- [ ] All resource pools are exhaustible and spatially located
- [ ] At minimum BC-1, BC-3, BC-7, and BC-8 are implemented *(updated v1.3)*
- [ ] NULL output is type-coded (no_opportunity | unreachable | trust_barrier | cultural_mismatch | low_uptake) *(updated v1.3)*
- [ ] NULL output triggers escalation pathway; no silent failures exist
- [ ] Tactical and strategic feedback loops are implemented separately
- [ ] Bias loop-breaking constraint is implemented; Stage 2 outputs are tagged before any reuse as training data *(added v1.3)*
- [ ] Cumulative tactical drift detection is implemented with documented window size *(added v1.3)*
- [ ] Human handover points are explicitly defined and documented
- [ ] Agent state transitions follow the permitted transitions table; no prohibited transitions occur
- [ ] Re-entry limits are enforced; agents exceeding limits transition to `escalated`
- [ ] Opportunity ranking criteria are documented; multi-opportunity selection is not arbitrary
- [ ] Simulation time step and scheduling approach are documented
- [ ] Contact success probability model is implemented with documented parameters
- [ ] Uptake probability model is implemented with documented parameters *(added v1.3)*
- [ ] HbA1c trajectory model is implemented with documented parameters

### Equity Validity
- [ ] At least one equity metric is defined before simulation begins
- [ ] Equity outputs are disaggregated by race, income quartile, and neighborhood deprivation
- [ ] NULL output rates are reported by demographic group, by NULL type
- [ ] At minimum two prioritization rules are compared (clinical-only vs. EquiRisk-multiplicative)
- [ ] Contact success rates are modeled and reported by demographic group
- [ ] Uptake completion rates are modeled and reported by demographic group *(added v1.3)*
- [ ] Equity Audit Layer runs at minimum every 30 simulation days and at simulation end
- [ ] Equity audit alert thresholds are documented before simulation begins
- [ ] Equity halt threshold is defined, implemented, and (for deployment) community-validated *(added v1.3)*
- [ ] Halt threshold breach events are recorded and resumption criteria are documented *(added v1.3)*
- [ ] Stigma sentinel is implemented for human-facing output text *(added v1.3)*
- [ ] Vulnerable population floor is applied at the prioritization queue ordering step *(added v1.3)*

### Pre-Deployment Gates *(added v1.3)*
- [ ] Bias Injection Protocol (Step 16) executed end-to-end; disparity delta reported
- [ ] Disparity delta < 10% achieved before deployment, OR conditional approval with mitigation timeline (10–20%), OR deployment blocked (> 20%)
- [ ] Community Co-Design session completed (Step 17); five-question framework addressed
- [ ] Community sign-off on CVI weights, intervention pathways, equity halt threshold, and plain-language explanation
- [ ] Vulnerable population strata defined with community input

### Assumption Transparency
- [ ] All assumptions from Step 9 are explicitly acknowledged
- [ ] At least three assumptions are stress-tested with documented scenarios
- [ ] Multiplicative form vs. additive form comparison is reported (using deprecated additive as comparison) *(added v1.3)*
- [ ] Results are framed as exploratory and comparative — not predictive or prescriptive
- [ ] Limitations are documented per Step 13
- [ ] Synthetic population generation method is documented (if applicable)

### Data Privacy and Ethics
- [ ] Data privacy and ethics requirements from Step 15 are reviewed and addressed
- [ ] If real or linked data is used, IRB approval or ethics review is documented
- [ ] Synthetic data generation method is documented with bias acknowledgment

### Adaptation Documentation (for non-Milwaukee forks)
- [ ] All substituted parameters are listed in fork README
- [ ] Local trust barrier and cultural fit reference groups are defined
- [ ] Local food desert definition and deprivation index are specified
- [ ] CVI weights are calibrated through community input or defaults are justified *(added v1.3)*
- [ ] Contact success and uptake baseline values are calibrated or defaults are justified *(updated v1.3)*
- [ ] Equity halt threshold is set through community validation *(added v1.3)*
- [ ] Deviations from core logic are justified and documented

---

## Step 12 — Worked Example: Milwaukee Reference Scenario *(updated v1.3 for multiplicative priority)*

This reference scenario illustrates minimum valid implementation logic. It is not empirically calibrated — all parameter values are illustrative defaults for testing implementation structure.

### Scenario Setup

**City:** Milwaukee, WI
**Population:** 500 synthetic diabetic agents assigned to census tracts using publicly available ADI and SVI distributions (see Step 14 for generation guidance)
**Simulation period:** 12 months
**Time step:** 1 day (discrete-time)
**Scheduling cycle:** 7 days
**Resource condition:** Moderate (70% of estimated need met by available programs)
**Prioritization rules compared:** Clinical-risk-only vs. EquiRisk-multiplicative
**Equity halt threshold:** 0.70 (default)
**Drift detection window:** N = 50 (quarterly program cycle)

### Two Illustrative Agents

| Dimension | Agent A (Low Contextual Vulnerability) | Agent B (High Contextual Vulnerability) |
|---|---|---|
| `hba1c_level` | 9.2% | 9.1% |
| `clinical_risk_score` (normalized) | 0.78 | 0.76 |
| `food_desert_status` | No (0) | Yes (1) |
| `area_deprivation_index` (normalized) | 0.32 | 0.87 |
| `social_vulnerability_index` (normalized) | 0.30 | 0.85 |
| `nearest_grocery_distance` (normalized) | 0.20 | 0.85 |
| `transit_score` | 0.72 | 0.19 |
| `housing_instability` (normalized) | 0.15 | 0.55 |
| `clinic_density` (normalized) | 0.65 | 0.20 |
| `social_support_index` (normalized) | 0.70 | 0.30 |
| `mobility_score` | 1 (fully mobile) | 2 (limited) |
| `trust_barrier` | Low | High |
| `language_barrier` | False | True (interpreter available) |
| `time_availability` | High | Medium |
| `housing_stability` | Stable | Stable |
| `income_quartile` | 3 | 1 |
| `health_literacy_score` | 3 (high) | 1 (low, with CHW) |
| `cultural_fit` (selected intervention) | Generic | Culturally appropriate |

### CVI Calculation

Using default CVI weights (v1=0.18, v2=0.16, v3=0.14, v4=0.12, v5=0.10, v6=0.12, v7=0.10, v8=0.08):

```
Agent A:
  CVI_A = 0.18 * 0   + 0.16 * 0.32 + 0.14 * 0.30 + 0.12 * 0.20
        + 0.10 * (1 - 0.72) + 0.12 * 0.15 + 0.10 * (1 - 0.65) + 0.08 * (1 - 0.70)
        = 0 + 0.0512 + 0.042 + 0.024 + 0.028 + 0.018 + 0.035 + 0.024
        = 0.222

Agent B:
  CVI_B = 0.18 * 1   + 0.16 * 0.87 + 0.14 * 0.85 + 0.12 * 0.85
        + 0.10 * (1 - 0.19) + 0.12 * 0.55 + 0.10 * (1 - 0.20) + 0.08 * (1 - 0.30)
        = 0.18 + 0.1392 + 0.119 + 0.102 + 0.081 + 0.066 + 0.080 + 0.056
        = 0.823
```

### Uptake Probability and Feasibility Weight

```
Agent A (selected intervention: clinic visit, generic cultural fit):
  P(uptake_A) = 0.65 * 1.00 (mobility=1) * 0.90 (income Q3) * 1.00 (literacy=3) * 0.85 (generic fit)
              = 0.497
  All boundaries satisfied → boundary_compliance_factor = 1.0
  feasibility_weight_A = 0.497 * 1.0 = 0.497

Agent B (selected intervention: CHW + food support, culturally appropriate, with navigation):
  P(uptake_B) = 0.65 * 0.80 (mobility=2) * 0.60 (income Q1) * 0.90 (literacy=1 + CHW support) * 1.00 (cultural fit)
              = 0.281
  Soft boundary violations (transit, distance) → boundary_compliance_factor = 0.7
  feasibility_weight_B = 0.281 * 0.7 = 0.197
```

### EquiRisk Multiplicative Priority

```
Agent A:
  Priority_A = 0.78 * (1 + 0.222) * 0.497
             = 0.78 * 1.222 * 0.497
             = 0.474
  → Tier 3 (Moderate, range 0.30–0.69)

Agent B:
  Priority_B = 0.76 * (1 + 0.823) * 0.197
             = 0.76 * 1.823 * 0.197
             = 0.273
  → Tier 4 (Low, < 0.30)
```

### A Critical Observation From This Worked Example

**Under the multiplicative formula, Agent B's priority is *lower* than Agent A's** — because feasibility_weight is so reduced by low uptake probability and soft boundary violations. This is a feature, not a bug: it surfaces the case-report finding that *risk identification is not the same as feasible action*. Agent B has high effective burden (CVM = 1.82, near maximum) but low feasibility. The system is signaling: this patient's priority cannot be answered by routine matching alone.

**Required system response for Agent B:**

```
1. Vulnerable Population Floor applies:
   Agent B is in food_desert + ADI ≥ 80th percentile = vulnerable population
   effective_priority_B = max(0.273, 0.50) = 0.50  → Tier 3 (mid)

2. Tier 1 escalation check:
   If raw Priority_B were Tier 1 but feasibility = 0 → NULL escalation
   In this case, Priority_B is Tier 4; floor lifts to Tier 3
   No escalation triggered, but flagged for navigation support

3. PAPO routes to:
   CHW visit (cultural fit ✓, trust-aligned ✓, navigation ✓)
   + food pharmacy referral (delivery, no transport required)
   Both selected because they raise effective uptake_probability via support

4. Contact probability check:
   P(contact_B) = 0.70 * 0.40 (high trust) * 1.00 * 0.80 (interp.) * 0.85 (medium time) = 0.190
   < 0.20 → flag for extended outreach via trust-aligned CHW intermediary

5. Equity halt threshold:
   If, in aggregate, food desert residents receive interventions at less than
   70% of equity-weighted expected rate → HALT routing for stratum.
```

### Comparison: Multiplicative vs. Clinical-Only

| Rule | Agent A Priority | Agent B Priority | Who is served first? |
|---|---|---|---|
| **Clinical-risk-only** | 0.78 | 0.76 | Agent A (slightly) |
| **EquiRisk multiplicative (raw)** | 0.474 | 0.273 | Agent A (low feasibility pulls B's priority down) |
| **EquiRisk multiplicative + vulnerable floor** | 0.474 | 0.50 (floor) | Agent B (floor lifts) |
| **EquiRisk multiplicative + navigation support raises B's feasibility to 0.40** | 0.474 | 0.76 * 1.823 * 0.40 = 0.554 | Agent B |

> **What this shows:** The multiplicative formula by itself does not automatically prioritize Agent B over Agent A — it accurately reflects that *without intervention support*, Agent B's pathway is too low-feasibility to justify high priority. The combination of: (i) the vulnerable population floor, (ii) PAPO's routing to support-enabling interventions (CHW, navigation, food delivery), and (iii) the equity halt threshold, collectively ensures that high-CVI patients are not dropped. Each component does specific work; none is redundant.

### Comparison: Multiplicative vs. Additive (deprecated v1.0–v1.2 form)

For backward comparison, the additive form `0.4*clinical + 0.35*contextual + 0.25*(1-feasibility)` would yield:

```
Agent A (additive): 0.4*0.78 + 0.35*0.222 + 0.25*(1-0.497) = 0.312 + 0.078 + 0.126 = 0.516
Agent B (additive): 0.4*0.76 + 0.35*0.823 + 0.25*(1-0.197) = 0.304 + 0.288 + 0.201 = 0.793
```

> Under the additive form, Agent B scores higher (0.793 vs 0.516) because contextual vulnerability and infeasibility *add* to the score rather than *attenuating* it. The additive form treats infeasibility as an additional risk dimension rather than as a constraint on what the system can deliver. The case report (#004-M) found this conflates effective risk with deliverability. The multiplicative form separates them, which is why it requires the vulnerable population floor and halt threshold to ensure the system still acts on high-CVI patients even when feasibility is constrained.

### HbA1c Trajectory Projection for Agent B (assuming intervention proceeds)

```
Agent B enters `in_pathway` at month 1 with HbA1c = 9.1%:
  Intervention: food + clinical + CHW → intensity = 1.2
  Adherence: medication_adherence = 0.6 (assumed for illustration)

  Month 1:  9.1 - (0.1 * 1.2 * 0.6) = 9.028%
  Month 3:  9.1 - 3 * 0.072 = 8.884%
  Month 6:  9.1 - 6 * 0.072 = 8.668%
  Month 12: 9.1 - 12 * 0.072 = 8.236%

  Agent B does not reach stabilization target (< 7.0%) within 12 months at this adherence level.
  → Remains in `in_pathway`; highlighted in equity audit as Tier 1 agent not yet stabilized.
```

> This trajectory illustrates the model mechanics, not a clinical prediction. Higher adherence or more intensive intervention would produce different results.

### Expected Equity Outputs

| Metric | Clinical-Only Rule | EquiRisk-Multiplicative + Floor + Halt |
|---|---|---|
| Opportunity receipt rate — ADI quartile 4 | Lower | Higher |
| NULL output rate — ADI quartile 4 | Higher | Lower (driven by routing to feasible alternatives) |
| Mean time to intervention — high-CVI agents | Longer | Shorter |
| Equity gap (Q4 vs Q1 opportunity rate) | Wider | Narrower |
| Contact success rate — high trust barrier group | Not differentiated | Lower (modeled explicitly) |
| Halt threshold breach events | Frequent (system blind to disparity) | Rare (system halts and corrects) |
| Drift detection alerts | Frequent (no detection) | Caught early; corrective action triggered |

> These are directional predictions based on framework logic, not empirical projections. Actual simulation outputs will vary by implementation and parameter choices.

---

## Step 13 — Known Limitations and Open Research Questions *(updated v1.3)*

### Known Limitations of This CMDDS

**Conceptual limitations:**
- CVI weights (v1–v8) have no empirically validated defaults. The illustrative weights are starting points for testing implementation structure, not calibrated estimates. Community Co-Design (Step 17) is required before deployment.
- The multiplicative form `Priority = clinical × (1 + CVI) × feasibility_weight` assumes a specific functional relationship among the three layers. Real interactions may not be purely multiplicative; alternative forms (additive in some regions, super-multiplicative in others) are possible. Sensitivity analysis is required.
- **Deprecated additive form:** Versions 1.0–1.2 used `w1*clinical + w2*contextual + w3*(1-feasibility)`. This form is retained in Step 8 only for backward comparison. The case report (#004-M) found that the additive form conflates allocation weighting with effective risk adjustment; the multiplicative form is the recommended canonical form. *(updated v1.3)*
- Trust is modeled as a static agent attribute. Dynamic trust — updated through system interactions — is specified as an assumption stress-test but not as a core model component.
- Cultural fit is modeled as a categorical attribute (appropriate / generic / inappropriate). Real cultural fit is graded, dynamic, and community-defined; the categorical model is a simplification. *(added v1.3)*
- The framework does not model supply-side barriers in provider systems (e.g., clinician implicit bias, organizational capacity constraints) except through resource pool capacity limits.
- Opportunity ranking weights (Step 4) are not empirically derived. Default weights reflect framework philosophy but may not be optimal for all contexts.
- The contact success and uptake probability models assume conditional independence among modifiers. Interaction effects are not captured in the default multiplicative forms.

**Simulation scope limitations:**
- HbA1c trajectory modeling is simplified (linear approximation). Clinical realism requires domain-specific calibration.
- This CMDDS does not specify a network model. Social network effects on trust, information sharing, and peer-mediated uptake are out of scope.
- Seasonal variation in food access and mobility is noted as an environmental attribute but is not fully specified for simulation.
- Synthetic population generation guidance (Step 14) provides a structural approach but does not resolve the fundamental challenge of specifying realistic joint distributions without empirical data.

**Equity limitations:**
- The framework operationalizes equity as distributional equity (who receives what). Relational equity (how people are treated in interactions) and epistemic equity (whose knowledge shapes the system) are partially addressed (stigma sentinel, community co-design) but not fully modeled.
- Equity metrics in Step 7 focus on receipt and outcomes. Process equity (experience of receiving care) is not captured.
- Equity audit alert thresholds and the equity halt threshold are defaults; community calibration is required before deployment.
- The vulnerable population floor protects against floor effects but does not address ceiling effects (whether resources allocated above the floor are sufficient). *(added v1.3)*

**Bias and governance limitations *(added v1.3)*:**
- The Bias Injection Protocol (Step 16) requires non-administrative comparison data. Where this is unavailable, simulated comparison cohorts must be used, which themselves embed assumptions about the missing data.
- The bias loop-breaking constraint depends on accurate tagging of Stage 2 outputs. Implementation errors that fail to tag outputs would silently re-encode bias. Periodic audit of tagging integrity is recommended.
- Cumulative tactical drift detection window sizes are not theoretically derived. Smaller populations may need smaller windows to be responsive; larger populations may need larger windows to avoid noise alerts.

### Open Research Questions

These questions are beyond the scope of this CMDDS but are important directions for downstream research:

1. What are the empirically optimal CVI weights for different city contexts, and how stable are they across seasons and population subgroups?
2. How does dynamic trust modeling — where trust updates based on contact and outcome history — change long-term equity trajectories?
3. At what resource level does EquiRisk-multiplicative prioritization cease to outperform clinical-only prioritization in equity outcomes?
4. How do supply-side barriers (clinician behavior, organizational culture) interact with demand-side barriers (patient feasibility) in ways that EquiRisk-PAPO cannot currently capture?
5. Can the EquiRisk-PAPO logic generalize to other chronic condition contexts (e.g., hypertension, mental health) beyond diabetes, and what adaptations are required?
6. What community co-design processes are required to ensure BC-7 trust barrier and BC-8 cultural fit definitions are legitimate, non-stigmatizing, and community-validated?
7. What is the empirical correlation structure between clinical risk, contextual vulnerability, and action feasibility in real diabetic populations, and how sensitive are simulation outcomes to misspecification of these joint distributions?
8. How should opportunity ranking weights be calibrated — through community preference elicitation, retrospective outcome analysis, or multi-objective optimization — and do optimal weights vary by EquiRisk tier?
9. **Is the multiplicative form `(1 + CVI)` the right functional form, or does CVI's effect on effective risk follow a different shape (e.g., threshold, sigmoid, power)?** Empirical comparison of functional forms against observed health outcome disparities is a high-priority research direction. *(added v1.3)*
10. **What halt threshold value (default 0.70) is empirically defensible, and how does this vary across communities, conditions, and resource environments?** Threshold setting is currently a value choice; it should be informed by both community input and outcome evidence. *(added v1.3)*
11. **How effective is the bias loop-breaking constraint in practice, and what are the failure modes?** Long-running implementations may reveal mechanisms by which Stage 2 outputs re-enter Stage 1 despite the constraint. *(added v1.3)*

---

## Step 14 — Synthetic Population Generation Guidance

> Simulations require a synthetic population of diabetic agents with correlated attributes across the three EquiRisk layers. This section provides structural guidance for generating such populations. It does not prescribe a single method; implementers should document their approach and test sensitivity to generation assumptions.

### The Core Challenge

EquiRisk priority depends on the joint distribution of clinical, contextual, and feasibility attributes. In real populations, these attributes are correlated — individuals in high-deprivation neighborhoods are more likely to have lower transit scores, higher trust barriers, lower social support, and worse clinical indicators. Generating agents with independent attribute draws will produce unrealistic populations and misleading simulation results.

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
- `social_support_index` *(added v1.3)*: drawn from ACS social isolation indicators or community survey data per tract
- Compute CVI from these attributes using documented weights

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
- `trust_barrier`: assigned conditional on race/ethnicity and ADI, with higher trust barriers in historically underserved communities. Default: in ADI quartile 4 tracts, 40% high, 35% moderate, 25% low; in ADI quartile 1 tracts, 10% high, 25% moderate, 65% low.
- `language_barrier`: drawn from ACS language data per tract
- `insurance_status`: drawn from ACS and Medicaid enrollment data per tract
- `time_availability`: drawn from employment and caregiving burden estimates per tract
- `uptake_probability` *(added v1.3)*: computed from the default model in Step 2 once mobility, income, literacy, and cultural fit are assigned

**Step 5 — Compute composite scores and validate:**
- Compute `clinical_risk_score`, `CVI`, and `action_feasibility_weight` from constituent attributes
- Normalize all sub-scores to [0,1] using min-max normalization within the simulated population
- Compute multiplicative EquiRisk priority and assign tiers
- Validate: check that the synthetic population reproduces expected patterns (e.g., Tier 1 agents are concentrated in high-ADI tracts; trust barriers are higher in historically underserved communities; high-CVI agents have lower feasibility weights on average)

### Population Size Guidance

| Purpose | Minimum N | Rationale |
|---|---|---|
| Implementation testing | 200–500 | Sufficient to test all state transitions and boundary conditions |
| Equity comparison (two rules) | 1,000–2,000 | Sufficient for stable equity gap estimates across 4 ADI quartiles |
| Sensitivity analysis | 2,000–5,000 | Required for stable variance estimates across parameter sweeps |
| Bias injection testing *(added v1.3)* | 2,000+ | Sufficient stratum sizes for disparity delta estimation |
| Drift detection testing *(added v1.3)* | Number of decisions in window × 5 | Sufficient decision history to test alert thresholds |
| Publication-quality results | 5,000+ with multiple replications | Standard for stochastic simulation confidence intervals |

### What to Document

Every fork must document the following in its README:
- Synthetic population size and number of replications
- Spatial scaffold (city, tract-level data sources)
- Correlation structure (method, target correlations, or copula specification)
- Trust barrier assignment rules
- Cultural fit assignment rules *(added v1.3)*
- CVI weight values and source (default vs. community-calibrated) *(added v1.3)*
- Any departures from the guidance above, with justification

---

## Step 15 — Data Privacy, Ethics, and IRB Considerations

> This CMDDS is designed for use with synthetic data. However, the framework is intended to be eventually applicable to real-world settings where individual-level health, demographic, and location data may be involved. This section specifies the ethical and privacy requirements that apply to any implementation.

### Synthetic Data Implementations

Even when using fully synthetic data, implementers should be aware of the following:

1. **Synthetic data can encode real biases.** If synthetic populations are generated from summary statistics drawn from biased data sources (e.g., health registries that undercount undocumented immigrants, or insurance claims that exclude uninsured populations), the synthetic population will reproduce those biases. Document the data sources used for generation and their known limitations.

2. **Ecological inference risks.** Tract-level attribute assignment (e.g., assigning higher trust barriers in high-ADI, majority-minority tracts) can reinforce stereotypes if presented without appropriate framing. Simulation outputs must be framed as system-level patterns, not individual predictions or group characterizations.

3. **Stigmatization risk.** Trust barrier modeling (BC-7) and cultural fit modeling (BC-8) require particular care. Both are modeled as structural outcomes of historical exclusion, not as individual deficits. Outputs should never be framed as "[group] does not trust healthcare" or "[group] does not engage with interventions" but rather as "the system has historically failed [group], producing lower engagement rates" or "interventions designed without [group]'s input show lower uptake." *(updated v1.3)*

### Real or Linked Data Implementations

If any implementation uses real patient data, linked administrative records, or identifiable community-level data:

1. **IRB or ethics board review is required** before simulation development begins — not only before publication. This includes implementations that link publicly available data sets in ways that could re-identify individuals (e.g., combining tract-level health data with tract-level demographic data at fine spatial resolution).

2. **Data minimization.** Use the minimum level of geographic and demographic detail needed to test the simulation logic. Block-group-level data is rarely necessary for CMDDS validation; tract-level is typically sufficient.

3. **De-identification verification.** If synthetic agents are generated from real data distributions, verify that individual re-identification is not possible from the combination of attributes (e.g., a unique combination of age, tract, diagnosis, and language in a small tract).

4. **Community engagement.** For implementations in specific cities, particularly those involving BC-7 trust barrier and BC-8 cultural fit definitions and CVI weight calibration, engagement with affected communities is *required* per the Community Co-Design Requirement (Step 17). This is no longer a recommendation but a deployment gate. *(updated v1.3)*

5. **Data use agreements.** If using HRSA, CMS, or state Medicaid data, ensure compliance with applicable data use agreements and HIPAA requirements.

### Ethical Framing of Outputs

All simulation outputs should be framed in accordance with the following principles:

- Outputs are exploratory and comparative, not predictive or prescriptive (restated for emphasis)
- Equity gaps identified in simulation reflect system design failures, not group deficiencies
- NULL output concentration in specific populations reflects structural barriers, not individual non-compliance
- Trust barriers are outcomes of system behavior, not patient characteristics
- Cultural fit failures are outcomes of intervention design, not patient deficits *(added v1.3)*
- Halt threshold breaches are signals that the system needs adjustment, not signals to relax the threshold *(added v1.3)*
- Simulation results should not be used to justify reducing services to groups with low contact success rates; they should be used to redesign outreach to improve success rates

---

## Step 16 — Bias Injection Protocol *(added v1.3)*

> Diabetes management training data — claims, EHR records, program enrollment — reflects who *accessed* healthcare and *completed* interventions, not who *needed* them. Food desert patients who never reached the healthcare system are systematically absent. An AI system trained on this data will reproduce the access gap at scale, with algorithmic authority. Bias injection is a required pre-deployment procedure to detect and mitigate this risk. The procedure below is adapted from the EquiRisk Case Report (#004-M).

### Required Pre-Deployment Procedure

Bias injection is **required before Stage 2 deployment** for any implementation that uses administrative data (claims, EHR, enrollment records) for training. It is recommended even for fully synthetic populations, as a check on whether the synthetic generation itself encodes bias.

### The Five-Step Protocol

```
STEP 1 — Train baseline model:
  Train a diabetes risk stratification or intervention recommendation
  model on the available administrative data (claims, EHR, enrollment)
  WITHOUT SDOH linkage (no food desert status, no ADI, no SVI).

STEP 2 — Measure baseline disparity delta:
  For matched clinical risk scores, measure the recommendation rate
  (or predicted-risk rate) for:
    - Food desert patients vs. non-food-desert patients
    - ADI quartile 4 patients vs. ADI quartile 1 patients
    - Race/ethnicity strata identified by community co-design
  Compute disparity_delta_baseline = |rate_advantaged - rate_disadvantaged|
  for each comparison.

STEP 3 — Apply EquiRisk multiplicative schema and re-measure:
  Apply Priority = clinical × (1 + CVI) × feasibility_weight.
  Recompute recommendation rates by stratum.
  Compute disparity_delta_equirisk for each comparison.

STEP 4 — If disparity remains, apply fairness constraint:
  If disparity_delta_equirisk ≥ 0.10 for any comparison:
    Apply a fairness constraint: equalized odds, demographic parity,
    or a community-defined alternative.
  Recompute disparity_delta_constrained.

STEP 5 — Deployment decision based on residual delta:

  IF disparity_delta < 0.10 (i.e., < 10 pp):
     → APPROVED for Stage 2 deployment
  IF 0.10 ≤ disparity_delta < 0.20:
     → CONDITIONAL APPROVAL with documented mitigation timeline;
       re-run protocol within 90 days of deployment;
       enhanced equity audit cadence (every 14 days, not 30)
  IF disparity_delta ≥ 0.20:
     → DEPLOYMENT BLOCKED
       Root cause analysis required;
       re-design (typically: SDOH linkage, training data augmentation,
       community-validated feature selection) before re-running protocol
```

### Expected Findings for Diabetes-in-Food-Deserts

The case report (#004-M) projects the following expected pattern for typical administrative training data:

| Bias Source | Expected Baseline Disparity | Expected Post-EquiRisk Disparity | Mitigation |
|---|---|---|---|
| Administrative data (claims, EHR) without SDOH linkage | > 20% | < 10% with SDOH-linked CVI | Require SDOH linkage for all training records |
| Program enrollment data (intervention effectiveness training) | 10–20% | 5–10% | Inverse-propensity weighting; include non-completion as outcome data |
| CHW engagement data (sparse in food deserts) | Low-moderate (sparse, not directionally biased) | Unchanged | Supplement with published RCT evidence; treat CHW pathway as evidence-supported even with sparse local data |
| Geographic proxy variables (tract-level food desert designation) | Low (precision, not direction) | Unchanged | Use individual-level proxies where available; flag patients near tract boundaries |

### What to Document

The Bias Injection Protocol report must include:
- Training data sources and date ranges
- Stratum definitions (food desert, ADI quartile, race/ethnicity, etc.)
- Baseline model specification and disparity delta values
- EquiRisk schema application and post-EquiRisk disparity delta values
- Fairness constraint applied (if any) and post-constraint disparity delta
- Deployment decision (APPROVED / CONDITIONAL / BLOCKED) with rationale
- Mitigation plan (for CONDITIONAL or BLOCKED)
- Re-run schedule

> **The protocol report is a deployment artifact** — it must be produced before Stage 2 routing begins, archived with the simulation, and cited in publications using the simulation outputs.

---

## Step 17 — Community Co-Design Requirement *(added v1.3)*

> The EquiRisk framework operationalizes equity as a decision rule. Whether the rule reflects what affected communities consider fair is a value choice, not a technical optimum. Community co-design is the mechanism by which this value choice is made legitimately. It is a deployment gate, not a recommendation. The EquiRisk Case Report (#004-M) frames this requirement explicitly: "Community co-design is not a checkbox. If community review reveals that the proposed value weights or intervention pathways do not reflect community priorities, Stage 2 must be revised before deployment."

### Required Pre-Deployment Procedure

Before Stage 2 deployment authorization, a community co-design session must be held with representatives from the specific food desert community being served.

**Minimum participation:**
- 3–5 community members (not solely institutional advocates) representing the demographic composition of the targeted area
- At least one Community Health Worker (CHW) who is a community member
- A public health ethicist
- The technical team lead (to listen, not to defend)

### The Five-Question Framework

The session must address all five questions. Each requires a documented community position; each has authority over a specific component of the deployment.

| # | Question | Why It Matters | Decision Authority |
|---|---|---|---|
| 1 | **What does "equity" mean in this community's terms?** | Academic equity metrics may not match what residents consider fair. Community members may prioritize different outcomes (food access vs. medication adherence vs. transportation vs. social support). | Community position determines which equity metric (Step 7) is the primary report metric for this deployment |
| 2 | **Which barriers matter most, and in what order?** | The CVI combines multiple SDOH factors. The relative weighting of food access vs. transportation vs. housing vs. social support is a value choice, not a technical optimization. | Community input determines CVI weights (Step 2). Default weights are *only* used if community explicitly endorses them or for testing-only implementations |
| 3 | **What does "action feasibility" mean from the patient's perspective?** | Program inventories reflect supply-side feasibility. Patient-side feasibility (trust, language, cultural fit, time, childcare) is not in administrative data. | Community input determines BC-7 trust barrier reference groups, BC-8 cultural fit definitions, and the cultural_fit_modifier values (Step 2) |
| 4 | **Are the intervention pathways culturally appropriate?** | Nutrition counseling, CHW engagement, and food support programs vary in cultural fit. A culturally inappropriate program is not truly feasible even if technically available. | Community input determines which interventions are flagged "culturally appropriate" vs. "generic" vs. "inappropriate" in the resource pool (Step 2 Entity 2) |
| 5 | **What should the equity halt threshold be?** | The default 0.70 threshold is a starting point. The threshold value is a community-defined statement of what level of disparity is acceptable vs. intolerable. | Community input determines the halt_ratio threshold (Step 7). Default is used *only* if community explicitly endorses it |

### Output of Community Co-Design Session

The session must produce a documented record (the "community calibration record," stored as `community_calibration_record` in Entity 4) including:

1. **Community-validated CVI weights** (or explicit endorsement of defaults)
2. **Community-validated equity halt threshold** (or explicit endorsement of default 0.70)
3. **Cultural fit classifications for each intervention type** (appropriate / generic / inappropriate, with rationale)
4. **Trust barrier reference groups and historical exclusion patterns** specific to this community
5. **Vulnerable population stratum definitions** for the floor (Step 7)
6. **Community review of the plain-language explanation** of the prioritization logic (does it make sense to community members? is it stigmatizing?)
7. **Sign-off list** with names and roles
8. **Date and venue** of the session

### Iteration Requirement

If community review reveals that proposed value weights, intervention pathways, or halt thresholds do not reflect community priorities, Stage 2 deployment is suspended until revisions are made and re-reviewed. Iteration is the norm, not the exception.

### Community Calibration Record as Deployment Artifact

The community calibration record:
- Is archived with the simulation outputs
- Must be cited in any publication using deployment outputs
- Must be re-reviewed at least annually, or when:
  - The targeted community demographic composition changes substantially
  - New intervention types are added to the resource pool
  - The equity halt threshold is breached and resumption requires community sign-off
  - Cumulative tactical drift detection fires repeatedly for the same stratum

> **What this is not:** Community Co-Design is not a focus group, not a public comment period, and not a single one-time event. It is a structured value-calibration procedure with named decision authority for specific framework components. Substituting a less rigorous form of engagement does not satisfy this requirement.

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

This Conceptual Model Design Documentation for Simulation (CMDDS) was developed with the assistance of Claude (Anthropic), a large language model. Building on the EquiRisk equity-aware risk stratification framework, the Policy-Aware Personalized Opportunity (PAPO) framework, the EquiRisk Case Report (#004-M) MOKG-PH analysis, and the supporting literature reviews, Claude assisted in structuring and drafting the simulation specification — including the v1.3 transition from additive to multiplicative priority scoring, Contextual Vulnerability Index (CVI) and Multiplier (CVM) specification, uptake probability model, Bias Injection Protocol, Community Co-Design Requirement, Equity Halt Threshold, bias loop-breaking constraint, cumulative tactical drift detection, stigma sentinel, vulnerable population floor, entity and state definitions, boundary condition formalization, agent state transition rules, scheduling logic, contact success probability model, HbA1c trajectory specification, Equity Audit Layer design, synthetic population generation guidance, validation checklist, worked examples, and cross-framework integration architecture. All components were reviewed, refined, and validated by the author to ensure scientific rigor and alignment with the EquiRisk-FoodDeserts research program.

## About

CMDDS for EquiRisk-FoodDeserts: an integrated, equity-aware simulation specification for diabetes care navigation in food desert settings, with a multiplicative priority formulation, bias injection protocol, community co-design requirement, and equity halt threshold. Fork to model care access equity in your city.
