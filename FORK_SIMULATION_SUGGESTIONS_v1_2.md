# FORK_SIMULATION_SUGGESTIONS.md
# Modular Simulation Projects for EquiRisk-FoodDeserts

**Repository:** https://github.com/Min-PH/EquiRisk-FoodDeserts
**Version:** 1.2
**Date:** 2026-03-23
**Author:** Min Wu, PhD
**Affiliation:** Zilber College of Public Health, University of Wisconsin-Milwaukee

**Changelog:**
- **v1.0** — Initial release. Tier 1–4 projects covering EquiRisk scoring, food access, CHW routing, telehealth, seasonal variation, trust barriers, and multi-city research programs.
- **v1.1** — Added Project S4 (Trust Barrier Contact Analysis). Added Project I5 (Dynamic Trust Modeling). Added Project A4 (Trust-Adjusted Prioritization Comparative Study). Updated all projects to reference CMDDS v1.1 boundary conditions (BC-1 through BC-7). Added v1.1 validation checklist requirements to each project. Updated tier table and overview. Minor clarifications throughout.
- **v1.2** — Added Project S5 (State Transition Validator). Added Project I6 (Contact Success Model Calibration). Updated all projects to reference CMDDS v1.2 components: state transition rules, EquiRisk tier definitions, opportunity ranking criteria, contact success probability model, HbA1c trajectory model, Equity Audit Layer, and synthetic population generation guidance (Step 14). Updated validation checklist references to v1.2. Updated tier table and overview. Minor clarifications throughout.

---

## Overview

This document provides a curated list of **modular simulation projects** derived from the EquiRisk-FoodDeserts CMDDS. Each project is designed to be implementable independently — you do not need to build the entire system to contribute meaningful research.

Projects are organized by complexity tier:

| Tier | Skill Level | Estimated Time | Tools | Projects |
|---|---|---|---|---|
| **Tier 1 — Starter** | Beginner (spreadsheet / basic Python) | 1–2 weekends | Excel, Python basics | S1, S2, S3, S4, S5 |
| **Tier 2 — Intermediate** | Intermediate (Python, GIS basics) | 2–4 weekends | Python, GeoPandas, Mesa | I1, I2, I3, I4, I5, I6 |
| **Tier 3 — Advanced** | Advanced (ABM, spatial modeling) | 1–3 months | Mesa, NetLogo, AnyLogic | A1, A2, A3, A4 |
| **Tier 4 — Extended** | Research team | 3–6 months | Full stack | E1, E2, E3 |

Each project specifies: what it simulates, what data it needs, what it outputs, and how it connects to the EquiRisk-FoodDeserts framework.

---

> ⚠️ **Before You Fork**
> Read the full CMDDS v1.2 to understand the core logic. All projects must preserve the EquiRisk three-layer scoring architecture, PAPO NULL output requirement, and — as of v1.1 — BC-7 trust barrier boundary conditions. As of v1.2, projects implementing agent state changes must follow the permitted transitions table, and projects involving multiple feasible opportunities must apply documented ranking criteria. Projects may simplify scope but must not override boundary conditions silently, omit equity reporting, or treat contact success as guaranteed.

> ✅ **Validation Requirement (v1.2)**
> Before reporting results from any project, complete the Step 11 Simulation Validation Checklist in CMDDS v1.2. At minimum, the structural validity and equity validity sections must be completed and documented in your fork README. Projects involving agent dynamics must also complete the state transition and scheduling items added in v1.2.

---

## TIER 1 — STARTER PROJECTS

These projects require minimal coding and can be implemented in a spreadsheet or basic Python script. Ideal for public health students, practitioners, and researchers new to simulation.

---

### Project S1: Grocery Store Access Mapper Under Inflation

**Complexity:** Tier 1
**Estimated time:** 1 weekend
**Context:** Inflation background — food prices have risen 20–30% since 2022, reducing effective food access even in areas with nearby grocery stores
**CMDDS v1.2 boundary conditions in scope:** BC-1 (geographic), BC-2 (economic)

**What it simulates:**
Maps the relationship between grocery store locations, food prices, and diabetic patient access in a single city. Models how inflation erodes the "feasible access" boundary — a store that was accessible at 2022 prices may no longer be accessible at 2026 prices for low-income patients.

**The Core Question:**
*How many diabetic patients in food desert census tracts lost effective grocery access due to inflation, even without any store closures?*

**Data Needed:**
- Census tract boundaries (free — Census TIGER files)
- Grocery store locations (free — OpenStreetMap or USDA Food Access Research Atlas)
- Household income by census tract (free — American Community Survey)
- Food price inflation index by category (free — BLS CPI data)
- USDA food desert designation (free — USDA Food Access Research Atlas)

**What to Build:**
1. For each census tract, calculate % of households within 0.5 and 1 mile of a grocery store
2. For each grocery store, estimate food basket cost at 2022 and 2026 prices using BLS CPI
3. Apply EquiRisk BC-2 economic boundary: cost > 10% of weekly food budget = infeasible
4. Count how many low-income diabetic households crossed the infeasibility threshold due to price increases alone
5. Map the results by neighborhood

**Outputs:**
- Map of effective food access loss due to inflation by census tract
- Count of diabetic households newly in effective food desert status post-inflation
- Equity gap: loss of access by income quartile

**EquiRisk Connection:**
Implements EquiRisk Layer 2 (Contextual Vulnerability) and BC-2 (Economic Boundary Condition) in isolation. No agent simulation required — this is a spatial analysis project.

**v1.2 Validation Note:**
This project does not require contact modeling, BC-7, state transitions, or opportunity ranking. Complete the structural validity section of the Step 11 checklist, focusing on sub-score normalization and equity metric pre-specification.

**Suggested Cities:**
Any US city with USDA food desert data. Milwaukee, Chicago, Detroit, Memphis are good starting points.

**Fork Template:**
`EquiRisk-[YourCity]-GroceryInflation`

---

### Project S2: EquiRisk Scoring Comparison — Two Patients

**Complexity:** Tier 1
**Estimated time:** 1 weekend
**Context:** Direct implementation of Table 1 from the EquiRisk SSRN paper
**CMDDS v1.2 boundary conditions in scope:** All three EquiRisk layers (scoring only; no boundary conditions required)

**What it simulates:**
Implements the EquiRisk three-layer scoring for a small set of synthetic patients with similar clinical risk but different contextual and feasibility profiles. Demonstrates how EquiRisk changes prioritization relative to clinical-risk-only approaches. As of v1.2, includes tier assignment using default score ranges.

**The Core Question:**
*For patients with identical HbA1c scores, how much does EquiRisk scoring change their priority ranking and tier assignment?*

**Data Needed:**
- Synthetic patient profiles only (no real data required)
- EquiRisk scoring weights from CMDDS v1.2 (default: w1=0.4, w2=0.35, w3=0.25)
- EquiRisk tier definitions from CMDDS v1.2 (Tier 1: ≥0.75, Tier 2: 0.50–0.74, Tier 3: 0.25–0.49, Tier 4: <0.25)

**What to Build:**
1. Create 10–20 synthetic patient profiles varying across all three EquiRisk layers
2. Include at least two profiles with varying `trust_barrier` levels to reflect v1.1 Layer 3 additions
3. Normalize all sub-scores to [0,1] before applying weights (required in CMDDS v1.2)
4. Score each patient using clinical-risk-only approach
5. Score each patient using full EquiRisk composite score
6. Assign each patient to an EquiRisk tier *(added v1.2)*
7. Compare priority rankings — who moves up? who moves down? who changes tier?
8. Report equity implications: which demographic groups benefit from EquiRisk scoring?

**Outputs:**
- Priority ranking table: clinical-only vs. EquiRisk
- Tier assignment table: which patients are Tier 1 under EquiRisk but not under clinical-only? *(added v1.2)*
- Rank change by income quartile, food desert status, mobility level, trust barrier level
- Visualization of how contextual vulnerability and feasibility shift priorities
- Sensitivity table: how rankings and tier assignments change across two weight configurations (default vs. alternative)

**EquiRisk Connection:**
Pure EquiRisk scoring implementation with tier assignment. No spatial or resource modeling required. Ideal first project for understanding the composite score logic.

**Suggested Extension:**
Vary EquiRisk weights (w1, w2, w3) and report how sensitive rankings and tier assignments are to weight choices. Include trust_barrier as a sensitivity variable. Test alternative tier boundaries (tertiles, quintiles).

---

### Project S3: Food Pharmacy Capacity Stress Test

**Complexity:** Tier 1–2
**Estimated time:** 1–2 weekends
**Context:** Food pharmacies — programs that prescribe healthy food as medicine — are emerging in US cities but have very limited capacity
**CMDDS v1.2 boundary conditions in scope:** BC-2 (economic), BC-6 (capacity)

**What it simulates:**
Models a single food pharmacy resource pool serving a diabetic population in a food desert neighborhood. Tests how quickly capacity is exhausted under different demand scenarios and prioritization rules.

**The Core Question:**
*Under current food pharmacy capacity levels, what proportion of eligible diabetic patients in a food desert neighborhood receive NULL output — and does EquiRisk-based prioritization change who gets served?*

**Data Needed:**
- Synthetic diabetic patient population for one neighborhood (50–100 agents)
- Single food pharmacy: location, weekly slot capacity (realistic: 20–50 slots/week)
- Patient eligibility criteria (income threshold, diagnosis requirement)

**What to Build:**
1. Generate 50–100 synthetic diabetic agents with full EquiRisk scores (including `trust_barrier`) and tier assignments
2. Model food pharmacy as exhaustible resource pool (e.g., 30 slots/week)
3. Run simulation under two prioritization rules: clinical-only vs. EquiRisk-weighted
4. Track: who gets a slot, who receives NULL output (type-coded), how quickly capacity exhausts
5. Report NULL output rates by EquiRisk tier *(added v1.2)*
6. Compare equity outcomes under each rule

**Outputs:**
- Weekly slot allocation by EquiRisk tier and demographic group
- NULL output rate by income quartile, food desert status, and EquiRisk tier *(updated v1.2)*
- NULL output type distribution (no_opportunity vs. capacity_exhausted) by demographic group
- Time-to-exhaustion of food pharmacy capacity under each prioritization rule
- Equity gap: difference in access rate between highest and lowest income quartile

**EquiRisk Connection:**
Implements full EquiRisk scoring + PAPO resource matching for a single resource type. First project to require NULL output implementation and type-coding.

**v1.2 Validation Note:**
NULL outputs must be type-coded. Report equity outputs disaggregated by at least income quartile and food desert status. Complete structural and equity validity sections of the Step 11 checklist. If multiple food pharmacy slots are feasible for the same patient (e.g., different days/times), apply opportunity ranking criteria.

---

### Project S4: Trust Barrier Contact Analysis *(added v1.1)*

**Complexity:** Tier 1
**Estimated time:** 1–2 weekends
**Context:** Public health outreach in food deserts often fails not because interventions are unavailable but because historical distrust of health systems prevents initial contact. BC-7 in CMDDS v1.1 formalizes trust as a structural boundary condition.
**CMDDS v1.2 boundary conditions in scope:** BC-7 (trust and engagement)

**What it simulates:**
Models the effect of trust barriers on intervention contact success rates for a synthetic diabetic patient population. Compares contact success rates across trust barrier levels (low, moderate, high) and tests whether trust-aligned outreach pathways (CHW intermediaries, community organization referrals) reduce the equity gap in contact success.

**The Core Question:**
*How much does a high trust barrier reduce the probability of first contact — and does routing outreach through trusted community intermediaries restore contact equity?*

**Data Needed:**
- Synthetic diabetic patient population: 50–100 agents with assigned `trust_barrier` levels
- Two outreach pathway types: direct provider outreach vs. CHW/community organization intermediary
- Contact success probability parameters (use CMDDS v1.2 default contact success model or project-specific defaults below)

**Suggested Default Parameters:**

| Trust Barrier Level | Direct Outreach Contact Rate | CHW/Community Intermediary Contact Rate |
|---|---|---|
| Low | 0.85 | 0.88 |
| Moderate | 0.55 | 0.78 |
| High | 0.20 | 0.65 |

> These defaults are illustrative starting points. Stress-test with ±15% variation. Real-world calibration requires community-level data. For comparison with the CMDDS v1.2 default contact success probability model (Step 4), note that these rates reflect the combined effect of all modifiers — the CMDDS model decomposes contact probability into multiplicative components.

**What to Build:**
1. Generate 50–100 synthetic agents with `trust_barrier` assigned (proportional to race/prior denial history weighting from CMDDS)
2. Assign each agent a contact success probability based on trust_barrier level and pathway type
3. Simulate two outreach scenarios: all direct outreach vs. trust-aligned routing (BC-7 applied)
4. Track: contact success rate, NULL output rate (BC-7 triggered), equity gap by trust barrier level
5. Track agent state transitions: `matched` → `contact_attempted` → `contact_failed` or `in_pathway` *(added v1.2)*
6. Calculate: how many additional patients are reached under trust-aligned routing

**Outputs:**
- Contact success rate by trust_barrier level under each outreach pathway
- NULL output rate (BC-7 type) by demographic group
- Agent state distribution at end of simulation (proportion in each state) *(added v1.2)*
- Equity gap: contact rate difference between low and high trust_barrier groups
- Equity gap change: direct outreach vs. trust-aligned routing
- Break-even analysis: how many CHW intermediary hours does it take to close the contact equity gap?

**EquiRisk Connection:**
Implements BC-7 in isolation. No spatial modeling or resource pool required. Ideal for public health practitioners who want to understand the equity implications of trust barriers without building a full simulation. Results feed directly into the `contact_success_rate` equity metric added in CMDDS v1.1.

**v1.2 Validation Note:**
This is the reference project for BC-7 implementation. Report contact success rates disaggregated by trust_barrier level and demographic group. Enforce permitted state transitions per CMDDS v1.2 Step 2. Complete the structural and equity validity sections of the Step 11 checklist. Document the contact probability parameters used and their justification.

**Suggested Extension:**
Combine with S2 (EquiRisk scoring) to model how trust barriers interact with composite EquiRisk priority rankings and tier assignments. Does a high-EquiRisk patient with a high trust barrier get deprioritized by standard outreach sequencing?

**Fork Template:**
`EquiRisk-[YourCity]-TrustBarrier`

---

### Project S5: State Transition Validator *(added v1.2)*

**Complexity:** Tier 1
**Estimated time:** 1 weekend
**Context:** CMDDS v1.2 specifies permitted agent state transitions with re-entry limits and cycling safeguards. This project validates that an implementation correctly enforces these rules before building more complex simulations.

**CMDDS v1.2 components in scope:** Agent state transition rules (Step 2), re-entry limits, EquiRisk tier assignment

**What it simulates:**
Runs a small set of synthetic agents through all possible state transition pathways — including re-entry, cycling, and prohibited transitions — to verify that the implementation correctly enforces the CMDDS v1.2 state transition table.

**The Core Question:**
*Does my implementation correctly enforce all permitted state transitions, block prohibited transitions, and respect re-entry limits?*

**Data Needed:**
- 20–30 synthetic agents with pre-assigned EquiRisk scores and tier assignments
- Scripted event sequences designed to trigger every permitted transition and every prohibited transition

**What to Build:**
1. Create a state machine implementing all 13 permitted transitions from CMDDS v1.2 Step 2
2. Script event sequences for each agent that exercise:
   - The standard pathway: `unidentified` → `identified` → `matched` → `contact_attempted` → `in_pathway` → `stabilized`
   - Contact failure and re-matching: `contact_attempted` → `contact_failed` → `matched` (up to 2 re-entries)
   - Re-entry from `contact_failed` exceeding limit → forced `escalated`
   - Re-entry from `lost_to_followup` → `identified` (1 re-entry) then → `escalated` if exceeded
   - Re-entry from `escalated` → `identified` (1 re-entry, requires documented resolution)
   - Re-entry from `stabilized` → `identified` (HbA1c regression)
   - Prohibited transitions: e.g., `unidentified` → `in_pathway`, `stabilized` → `matched`, `contact_failed` → `in_pathway`
3. Verify that re-entry transitions reset the EquiRisk score
4. Log every attempted transition, whether it succeeded or was blocked, and why

**Outputs:**
- Transition log: every attempted transition with outcome (permitted/blocked) and reason
- Coverage report: which transitions were tested, which were not
- Re-entry counter verification: agents that exceeded limits correctly forced to `escalated`
- EquiRisk score reset verification: re-entering agents received new scores

**EquiRisk Connection:**
This is a structural validation project — no spatial, resource, or equity modeling required. It verifies the agent lifecycle logic that underpins all more complex simulations. Completing this project first ensures that subsequent projects (S3, S4, I1–I5, A1–A4) have a correct state machine foundation.

**v1.2 Validation Note:**
Complete the state transition items in the structural validity section of the Step 11 checklist. This project is specifically designed to satisfy those checklist items.

**Fork Template:**
`EquiRisk-[YourCity]-StateValidator`

---

## TIER 2 — INTERMEDIATE PROJECTS

These projects require Python programming, basic spatial analysis, and familiarity with simulation concepts. Ideal for graduate students and early-career researchers.

---

### Project I1: Grocery Store Closure Simulation Under Inflation

**Complexity:** Tier 2
**Estimated time:** 2–3 weekends
**Context:** Inflation has driven grocery store closures in low-income neighborhoods. Between 2022–2026, several urban grocery chains reduced footprint in low-income areas due to shrinking margins.
**CMDDS v1.2 boundary conditions in scope:** BC-1 (geographic), BC-2 (economic)

**What it simulates:**
Models the cascade effect of grocery store closures on diabetic patient food access. Starts from a baseline access map, removes stores sequentially (simulating closures), and measures how EquiRisk scores, tier assignments, and NULL output rates change at each removal step.

**The Core Question:**
*How many grocery store closures does it take before a neighborhood crosses the food desert threshold — and how does this interact with EquiRisk feasibility scoring and tier distribution for diabetic patients specifically?*

**Data Needed:**
- Real grocery store locations for chosen city (OpenStreetMap)
- Census tract demographics — income, diabetes prevalence estimate, car ownership (ACS)
- USDA food desert designation baseline
- EquiRisk synthetic patient population (100–200 agents, generated per Step 14 guidance)

**What to Build:**
1. Map baseline grocery access for synthetic patient population
2. Apply EquiRisk BC-1 and BC-2 boundary conditions to each store-patient pair
3. Simulate sequential store closures (1 store at a time)
4. At each closure step: recalculate access, update NULL output rates, update EquiRisk contextual scores and tier assignments
5. Identify the tipping point — the closure that pushes a neighborhood into food desert status
6. Report equity implications by income quartile and EquiRisk tier

**Outputs:**
- Animated map showing access erosion with each store closure
- Tipping point analysis: which closure is most impactful and for which populations
- EquiRisk score and tier distribution change across closure sequence *(updated v1.2)*
- NULL output rate curve: how rapidly it rises with closures

**Inflation Extension:**
Run the same simulation twice — once with 2022 prices (more stores feasible) and once with 2026 prices (fewer stores within economic boundary). Compare tipping points.

**v1.2 Validation Note:**
NULL outputs must be type-coded. Sub-scores must be normalized before weight application. Report equity outputs disaggregated by income quartile, food desert status, and EquiRisk tier. Document synthetic population generation method per Step 14.

**Related Literature:**
- Allcott, H., Diamond, R., Dubé, J.-P., Handbury, J., Rahkovsky, I., & Schnell, M. (2019). Food deserts and the causes of nutritional inequality. *The Quarterly Journal of Economics, 134*(4), 1793–1844. https://doi.org/10.1093/qje/qjz015
- Wang, S., & Laefer, D. F. (2024). Modeling food-related business closure in select New York City communities using multi-scale and spatial features. *Environment and Planning B: Urban Analytics and City Science, 52*(1), 247–264. https://doi.org/10.1177/23998083241254573

---

### Project I2: Community Health Worker (CHW) Routing Optimization Under Resource Scarcity

**Complexity:** Tier 2
**Estimated time:** 2–3 weekends
**Context:** CHWs are the most equity-effective intervention for hard-to-reach diabetic patients — but they have limited caseload capacity and must travel between patients
**CMDDS v1.2 boundary conditions in scope:** BC-3 (mobility), BC-6 (capacity), BC-7 (trust — CHW trust alignment)

**What it simulates:**
Models CHW assignment and routing to homebound or low-mobility diabetic patients who cannot access clinic-based or food access opportunities. Tests how EquiRisk-based vs. geographic routing changes equity outcomes when CHW capacity is scarce.

**The Core Question:**
*Does assigning CHWs based on EquiRisk scores (highest need first) produce better equity outcomes than assigning based on geographic proximity (nearest patient first)?*

**Data Needed:**
- Synthetic patient population: 100–150 agents, filtered for mobility score ≥ 2 (generated per Step 14 guidance)
- CHW pool: 3–5 CHWs with defined coverage zones and weekly caseload limits (10–15 patients/week)
- CHW trust alignment attributes: does this CHW have trusted community relationships in the patient's neighborhood? (v1.1 addition)
- Street network for routing (OpenStreetMap + OSMnx Python library)

**What to Build:**
1. Generate homebound and limited-mobility diabetic patient population with `trust_barrier` assigned
2. Model CHW resource pool: capacity, coverage zone, weekly visit limit, trust alignment flag
3. Implement two routing rules: geographic-nearest vs. EquiRisk-highest
4. Add a third rule (v1.1): trust-aligned EquiRisk routing — prefer CHW with community trust match for high-trust-barrier patients
5. When multiple CHWs are feasible for a patient, apply opportunity ranking criteria (v1.2) to select the best-fit CHW
6. Run all rules under full capacity and 50% capacity scenarios
7. Track: patients visited, patients receiving NULL output (type-coded), travel time, equity outcomes, contact success rate
8. Track agent state transitions through the full lifecycle *(added v1.2)*

**Outputs:**
- Visit rate by mobility score and income quartile under each routing rule
- NULL output rate under full vs. scarce CHW capacity
- Contact success rate by trust_barrier level under each routing rule
- Equity gap comparison: geographic routing vs. EquiRisk routing vs. trust-aligned EquiRisk routing
- CHW travel efficiency: time spent traveling vs. time with patients
- Agent state distribution at end of simulation *(added v1.2)*

**EquiRisk Connection:**
Implements full EquiRisk scoring with emphasis on BC-3 (mobility boundary), BC-6 (capacity boundary), and BC-7 (trust boundary). First project requiring spatial routing, trust-aligned resource matching, and opportunity ranking.

**v1.2 Validation Note:**
CHW trust alignment is a BC-7 implementation. Document trust alignment assignment logic and parameters. Contact success modeling is required (use CMDDS v1.2 default model or project-specific parameters). Apply opportunity ranking criteria when multiple CHWs are feasible. Enforce state transition rules. Complete all sections of the Step 11 checklist.

**Related Literature:**
- Brunskill, E., & Lesh, N. (2010). Routing for rural health: Optimizing community health worker visit schedules. *Proceedings of the AAAI Conference on Artificial Intelligence*. https://www.cs.cmu.edu/~ebrun/brunskilllesh.pdf
- Fikar, C., & Hirsch, P. (2017). Home health care routing and scheduling: A review. *Computers & Operations Research, 77*, 86–95. https://doi.org/10.1016/j.cor.2016.07.019
- Randriamihaja, M., Ihantamalala, F. A., Rafenoarimalala, F. H., Finnegan, K. E., Rakotonirina, L., Razafinjato, B., ... & Garchitorena, A. (2024). Combining participatory mapping and route optimization algorithms to inform the delivery of community health interventions at the last mile. *medRxiv*, 2024-02.
- Mankowska, D. S., Meisel, F., & Bierwirth, C. (2014). The home health care routing and scheduling problem with interdependent services. *Health Care Management Science, 17*(1), 15–30. https://doi.org/10.1007/s10729-013-9243-1
- Spencer, M. S., Rosland, A.-M., Kieffer, E. C., Sinco, B. R., Valerio, M., Palmisano, G., ... & Heisler, M. (2011). Effectiveness of a community health worker intervention among African American and Latino adults with type 2 diabetes: A randomized controlled trial. *American Journal of Public Health, 101*(12), 2253–2260. https://doi.org/10.2105/AJPH.2010.300106

---

### Project I3: Telehealth Access Gap Analysis for Diabetic Patients

**Complexity:** Tier 2
**Estimated time:** 2 weekends
**Context:** Telehealth expanded dramatically post-COVID but has created a new equity gap — patients without internet access, devices, or digital literacy are systematically excluded
**CMDDS v1.2 boundary conditions in scope:** BC-1 (geographic), BC-3 (technology), BC-5 (health literacy)

**What it simulates:**
Models telehealth as an alternative care access opportunity for diabetic patients who cannot access in-person clinics. Measures how digital access barriers (BC-3: technology) create a new layer of health inequity on top of existing food desert barriers.

**The Core Question:**
*For diabetic patients in food deserts who cannot access in-person care, does telehealth actually reduce the equity gap — or does it create a new digital divide layer?*

**Data Needed:**
- Synthetic patient population: 100 agents in food desert tracts (generated per Step 14 guidance)
- Internet access rates by census tract (ACS Table B28002)
- Device ownership rates by income quartile (Pew Research estimates)
- Telehealth platform capacity (synthetic)
- In-person clinic locations and capacity (real or synthetic)

**What to Build:**
1. Model two opportunity types: in-person clinic and telehealth
2. Apply BC-1 (geographic) to in-person clinic access
3. Apply BC-3 (technology) to telehealth access
4. Apply BC-5 (health literacy) to telehealth navigation complexity
5. For each patient with multiple feasible options: apply opportunity ranking criteria to select best match *(added v1.2)*
6. For each patient: determine which opportunities are feasible
7. Identify patients for whom BOTH in-person and telehealth are infeasible → double NULL output (type: unreachable)
8. Report equity implications by income, race, and age group

**Outputs:**
- Access map: in-person feasible, telehealth feasible, both feasible, neither feasible
- Double-NULL rate by demographic group — patients with no feasible care pathway
- Opportunity ranking analysis: when both options are feasible, which is selected and why *(added v1.2)*
- Equity gap: which groups are most likely to have no feasible care option
- Policy implication: what device subsidy or internet access program would most reduce double-NULL rate

**v1.2 Validation Note:**
Double-NULL outputs should be type-coded as `unreachable`. Report equity outputs disaggregated by income quartile, race, and age. Apply opportunity ranking when both in-person and telehealth are feasible. Complete structural and equity validity sections of the Step 11 checklist.

**Related Literature:**
- Anderson, A., O'Connell, S. S., Thomas, C., & Chimmanamada, R. (2022). Telehealth interventions to improve diabetes management among Black and Hispanic patients: A systematic review and meta-analysis. *Journal of Racial and Ethnic Health Disparities, 9*(6), 2375–2386. https://doi.org/10.1007/s40615-021-01174-6
- Cortelyou-Ward, K., Atkins, D. N., Noblin, A., Rotarius, T., White, P., & Carey, C. (2020). Navigating the digital divide: Barriers to telehealth in rural areas. *Journal of Health Care for the Poor and Underserved, 31*(4), 1546–1556. https://doi.org/10.1353/hpu.2020.0116
- Ebekozien, O., Mungmode, A., Gianferante, D., & Odugbesan, O. (2024). Technology and health inequities in diabetes care: How do we widen access to underserved populations and utilize technology to improve outcomes for all? *Diabetes, Obesity and Metabolism, 26*(4), 1217–1230. https://doi.org/10.1111/dom.15470
- Kim, K. K., McGrath, S. P., Solorza, J. L., & Lindeman, D. (2023). The ACTIVATE digital health pilot program for diabetes and hypertension in an underserved and rural community. *Applied Clinical Informatics, 14*(4), 644–653. https://doi.org/10.1055/a-2096-0326
- Sieck, C. J., Sheon, A., Ancker, J. S., Castek, J., Callahan, B., & Siefer, A. (2021). Digital inclusion as a social determinant of health. *NPJ Digital Medicine, 4*(1), 52. https://doi.org/10.1038/s41746-021-00413-8

---

### Project I4: Seasonal Food Access Variation — Summer Heat + Diabetes

**Complexity:** Tier 2
**Estimated time:** 2–3 weekends
**Context:** Summer heat disproportionately affects diabetic patients — heat worsens glycemic control, reduces mobility, and reduces willingness/ability to travel to food sources. This connects EquiRisk-FoodDeserts to the PAPO-Heatwave framework.
**CMDDS v1.2 boundary conditions in scope:** BC-1 (geographic, heat-modified), BC-3 (mobility, heat-modified), seasonal_variation environmental attribute

**What it simulates:**
Models how summer heat events modify EquiRisk scores, tier assignments, and food access feasibility for diabetic patients. When temperatures exceed thresholds, mobility decreases, travel distance feasibility shrinks, and clinical risk elevates simultaneously.

**The Core Question:**
*How does a 4-day extreme heat event change the EquiRisk score distribution, tier assignments, and NULL output rate for diabetic patients who were previously just within feasibility boundaries?*

**Data Needed:**
- Synthetic diabetic patient population: 100–150 agents (generated per Step 14 guidance)
- Grocery store and clinic locations
- Heat event scenario: 4-day event, peak heat index 105°F (from PAPO-Heatwave framework)
- Urban heat island variation by neighborhood (available from NOAA / EPA)

**What to Build:**
1. Establish baseline EquiRisk scores, tier assignments, and access feasibility before heat event
2. Apply heat event modifiers to EquiRisk attributes:
   - Mobility score increases for elderly patients (heat worsens mobility)
   - Feasible travel distance decreases (BC-1 geographic boundary tightens)
   - Clinical risk score increases (heat elevates HbA1c risk)
3. Recalculate EquiRisk scores, tier assignments, and feasibility during heat event
4. Compare NULL output rates before and during heat event
5. Identify patients who were marginally feasible before heat and tipped to NULL during
6. Track tier migration: which patients moved from Tier 2/3 to Tier 1 during heat event *(added v1.2)*

**Outputs:**
- EquiRisk score and tier change distribution: before vs. during heat event *(updated v1.2)*
- NULL output rate increase during heat event by demographic group
- Map of patients who tipped to infeasibility during heat event
- Equity gap change: which neighborhoods are most destabilized by heat

**Framework Connection:**
This project bridges EquiRisk-FoodDeserts and PAPO-Heatwave-AI — the first multi-framework simulation project. Results can feed both repositories.

**v1.2 Validation Note:**
Re-normalize sub-scores after applying heat modifiers — do not carry over pre-event normalized values. Re-assign EquiRisk tiers after re-normalization. Report NULL output type distribution (no_opportunity vs. unreachable) separately for baseline and heat event periods.

**Related Literature:**
- Hsu, A., Sheriff, G., Chakraborty, T., & Manya, D. (2021). Disproportionate exposure to urban heat island intensity across major US cities. *Nature Communications, 12*(1), 2721. https://doi.org/10.1038/s41467-021-22799-5
- Kenny, G. P., Sigal, R. J., & McGinn, R. (2016). Body temperature regulation in diabetes. *Temperature, 3*(1), 119–145. https://doi.org/10.1080/23328940.2015.1131506
- Ratter-Rieck, J. M., Roden, M., & Herder, C. (2023). Diabetes and climate change: Current evidence and implications for people with diabetes, clinicians and policy stakeholders. *Diabetologia, 66*(6), 1003–1015. https://doi.org/10.1007/s00125-023-05901-y
- Tao, J., Zheng, H., Ho, H. C., Wang, X., Hossain, M. Z., Bai, Z., ... & Huang, C. (2023). Urban-rural disparity in heatwave effects on diabetes mortality in eastern China: A case-crossover analysis in 2016–2019. *Science of the Total Environment, 858*(Pt 2), 160026. https://doi.org/10.1016/j.scitotenv.2022.160026
- Widener, M. J., Minaker, L., Farber, S., Allen, J., Vitali, B., Coleman, P., & Cook, B. (2017). How do changes in the daily food and transportation environments affect grocery store accessibility? *Applied Geography, 83*, 46–62. https://doi.org/10.1016/j.apgeog.2017.03.018

---

### Project I5: Dynamic Trust Modeling — Trust as an Evolving Variable *(added v1.1)*

**Complexity:** Tier 2–3
**Estimated time:** 3–4 weekends
**Context:** CMDDS v1.2 identifies a key limitation: trust is modeled as a static attribute. In reality, trust evolves based on system interactions — a positive first contact experience reduces trust barriers; a failed, disrespectful, or inaccessible experience increases them. This project implements dynamic trust as a stress-test of the static assumption.
**CMDDS v1.2 boundary conditions in scope:** BC-7 (trust, dynamic variant)
**CMDDS v1.2 assumption stress-tested:** "Trust is static" (Step 9)

**What it simulates:**
Models trust barrier as a dynamic variable that updates based on each system interaction. Compares long-term equity outcomes between a static trust model (CMDDS default) and a dynamic trust model over a 12-month simulation period. As of v1.2, tracks the full agent lifecycle using state transition rules and HbA1c trajectories.

**The Core Question:**
*Does modeling trust as dynamic — updating with each system interaction — meaningfully change long-term equity outcomes compared to the static trust assumption?*

**Data Needed:**
- Synthetic diabetic patient population: 150–200 agents with initial `trust_barrier` levels (generated per Step 14 guidance)
- Interaction outcome probabilities: probability that a positive/negative interaction improves/worsens trust
- Resource pool for 12-month simulation period (simplified: single CHW program + food pharmacy)

**Trust Update Logic (suggested defaults):**
```
After successful contact and positive experience:
  trust_barrier decreases by one level (high → moderate → low)
  probability: 0.6

After failed contact or negative experience (wait time, disrespect, denial):
  trust_barrier increases by one level (low → moderate → high)
  probability: 0.7

After NULL output without explanation:
  trust_barrier increases by one level
  probability: 0.8
```
> These defaults are illustrative. Stress-test with ±20% variation. Note in fork README that these parameters require community validation before any applied use.

**What to Build:**
1. Initialize agents with static trust_barrier levels (CMDDS default)
2. Implement dynamic trust update logic: trust_barrier updates after each interaction
3. Implement full agent state transitions per CMDDS v1.2 Step 2 *(added v1.2)*
4. Implement HbA1c trajectory model for agents in `in_pathway` state *(added v1.2)*
5. Run simulation twice over 12 months: static trust model vs. dynamic trust model
6. Run Equity Audit Layer every 30 simulation days *(added v1.2)*
7. Track: trust_barrier level distribution over time, contact success rate over time, equity gap trajectory, tier migration over time
8. Identify: does the equity gap widen or narrow over time under dynamic trust? Does it differ by initial trust_barrier level?

**Outputs:**
- Trust barrier level distribution: month 0, month 6, month 12
- Contact success rate trajectory: static vs. dynamic trust model
- HbA1c trajectory comparison: static vs. dynamic trust model *(added v1.2)*
- Equity gap trajectory: does dynamic trust amplify or reduce inequity over time?
- Equity Audit Layer reports at 30-day intervals with alert threshold outcomes *(added v1.2)*
- Identification of feedback loops: conditions under which the system produces trust deterioration spirals
- Recommendation: at what interaction quality threshold does the system begin improving equity rather than worsening it?

**EquiRisk Connection:**
Implements BC-7 as a dynamic boundary condition. Directly stress-tests the static trust assumption from CMDDS Step 9. Results inform whether future CMDDS versions should promote dynamic trust to a core model component.

**v1.2 Validation Note:**
Document trust update parameters and their justification. Enforce state transition rules with re-entry limits. Implement HbA1c trajectory model. Run Equity Audit Layer at required intervals. Report contact success rate and equity gap disaggregated by initial trust_barrier level and demographic group. Complete the full Step 11 checklist — this project is a stress-test project and must explicitly document assumption deviation from the static default.

**Fork Template:**
`EquiRisk-[YourCity]-DynamicTrust`

---

### Project I6: Contact Success Model Calibration *(added v1.2)*

**Complexity:** Tier 2
**Estimated time:** 2–3 weekends
**Context:** CMDDS v1.2 introduces a default contact success probability model with multiplicative modifiers (trust, housing, language, time availability). This project tests the model's sensitivity to parameter values and compares multiplicative vs. alternative formulations.

**CMDDS v1.2 components in scope:** Contact success probability model (Step 4), agent state transitions, EquiRisk tier assignment

**What it simulates:**
Implements the CMDDS v1.2 default contact success probability model for a synthetic population and systematically varies parameters to identify which modifiers most affect equity outcomes. Compares the default multiplicative model against an additive formulation and an interaction-based formulation to test the conditional independence assumption.

**The Core Question:**
*How sensitive are equity outcomes to contact success model specification — and does the multiplicative independence assumption materially affect which populations receive NULL outputs?*

**Data Needed:**
- Synthetic diabetic patient population: 200–300 agents with full EquiRisk attributes (generated per Step 14 guidance)
- CMDDS v1.2 default contact model parameters (baseline = 0.70, modifier values per Step 4)
- Alternative parameter sets for sensitivity testing

**What to Build:**
1. Generate synthetic population with correlated attributes per Step 14 guidance
2. Implement three contact success model formulations:
   - **Multiplicative (CMDDS default):** P = baseline × trust × housing × language × time
   - **Additive:** P = baseline − trust_penalty − housing_penalty − language_penalty − time_penalty (clamped to [0,1])
   - **Interaction:** P = multiplicative model + interaction_term(trust × housing) (to test compounding disadvantage)
3. For each model: simulate 3 contact attempts per agent per matching cycle
4. Track agent state transitions: `matched` → `contact_attempted` → `contact_failed` or `in_pathway`
5. Run all three models under identical population and resource conditions
6. Compare: contact success rate, NULL output rate, and equity gap by demographic group across models

**Outputs:**
- Contact success rate by trust_barrier level, housing stability, and language barrier under each model formulation
- NULL output rate by demographic group under each model
- Equity gap comparison: which model produces the widest/narrowest equity gap?
- Sensitivity analysis: which single modifier has the largest effect on equity outcomes?
- Interaction effect estimate: does compounding trust + housing barriers produce materially different results than the multiplicative assumption?
- Recommendation: under what conditions should implementers prefer non-multiplicative models?

**EquiRisk Connection:**
Directly stress-tests the contact success probability model introduced in CMDDS v1.2 Step 4. Results inform whether the conditional independence assumption is adequate or whether future CMDDS versions should specify interaction terms. Feeds into Open Research Question 7 (Step 13).

**v1.2 Validation Note:**
Document all three model formulations and parameter values. Enforce state transition rules. Report equity outputs disaggregated by trust_barrier level, housing stability, and language barrier. Complete structural and equity validity sections of the Step 11 checklist.

**Fork Template:**
`EquiRisk-[YourCity]-ContactModel`

**Related Literature:**
- Giabbanelli, P. J., & Crutzen, R. (2017). Using agent-based models to develop public policy about food behaviours: Future directions and recommendations. *Computational and Mathematical Methods in Medicine, 2017*, 5742629. https://doi.org/10.1155/2017/5742629
- Saltelli, A., Ratto, M., Andres, T., Campolongo, F., Cariboni, J., Gatelli, D., Saisana, M., & Tarantola, S. (2008). *Global sensitivity analysis: The primer.* John Wiley & Sons. https://doi.org/10.1002/9780470725184
- Ten Broeke, G., Van Voorn, G., & Ligtenberg, A. (2016). Which sensitivity analysis method should I use for my agent-based model? *Journal of Artificial Societies and Social Simulation, 19*(1), 5. https://doi.org/10.18564/jasss.2857
- Thiele, J. C., Kurth, W., & Grimm, V. (2014). Facilitating parameter estimation and sensitivity analysis of agent-based models: A cookbook using NetLogo and R. *Journal of Artificial Societies and Social Simulation, 17*(3), 11. https://doi.org/10.18564/jasss.2503

---

## TIER 3 — ADVANCED PROJECTS

These projects require agent-based modeling experience, spatial simulation skills, and familiarity with equity analysis methods. Suitable for PhD students and research teams.

---

### Project A1: Full EquiRisk-PAPO Milwaukee Simulation

**Complexity:** Tier 3
**Estimated time:** 2–3 months
**Context:** Reference implementation for the EquiRisk-FoodDeserts CMDDS
**CMDDS v1.2 boundary conditions in scope:** BC-1 through BC-7 (all)

**What it simulates:**
The complete integrated EquiRisk-PAPO system for Milwaukee, Wisconsin — the reference city for this framework. All three EquiRisk layers, all seven boundary condition categories, full resource pool modeling, both feedback loops, and multi-scale equity reporting. As of v1.2, includes the complete agent state machine, opportunity ranking, contact success probability model, HbA1c trajectory tracking, and Equity Audit Layer.

**The Core Question:**
*Under current Milwaukee resource conditions, how effectively does the EquiRisk-PAPO system reach diabetic patients in food deserts — and which prioritization rule produces the most equitable outcomes?*

**Data Needed:**
- Milwaukee census tract demographics (ACS)
- CDC SVI and ADI for Milwaukee tracts
- USDA food desert designation
- Real food resource locations: grocery stores, food pantries, food pharmacies (if any)
- Real care resource locations: FQHCs, pharmacies, community health centers
- Milwaukee County Transit routes (GTFS)
- Synthetic diabetic patient population calibrated to Milwaukee demographics (generated per Step 14 guidance)
- Community organization map for BC-7 trust-aligned referral pathways (v1.1 addition)

**Required Components (per CMDDS v1.2 Step 6):**
- Full three-layer EquiRisk scoring for all agents with normalized sub-scores
- EquiRisk tier assignment with documented cutpoints *(added v1.2)*
- All seven boundary condition categories (BC-1 through BC-7)
- Exhaustible resource pools for all opportunity types with trust_alignment flags
- Opportunity ranking criteria for multi-opportunity selection *(added v1.2)*
- Contact success probability model with documented parameters *(added v1.2)*
- NULL output with type-coding and escalation
- Separated tactical and strategic feedback loops
- Agent state transition enforcement with re-entry limits *(added v1.2)*
- HbA1c trajectory tracking for agents in pathway *(added v1.2)*
- At least two prioritization rule comparisons (clinical-only vs. EquiRisk-weighted at minimum)
- At least one equity metric reported disaggregated
- Equity Audit Layer running every 30 simulation days with alert thresholds *(added v1.2)*
- Contact success modeling (v1.1 required component)
- Synthetic population documented per Step 14 *(added v1.2)*
- Step 11 Validation Checklist completed in full (v1.2)

**Outputs:**
- Full equity audit report for Milwaukee (Equity Audit Layer output)
- Opportunity desert map: high EquiRisk + low access areas
- Prioritization rule comparison: equity outcomes under 5+ rules including trust-adjusted EquiRisk
- Policy sensitivity: what resource investment most improves equity?
- Contact equity analysis: how does BC-7 implementation change who is reached?
- HbA1c trajectory analysis by EquiRisk tier and prioritization rule *(added v1.2)*
- Agent lifecycle analysis: state distribution over time, re-entry rates by demographic group *(added v1.2)*
- Publishable results for AJPH or Environmental Health

---

### Project A2: Inflation Shock Simulation — Food Access System Resilience

**Complexity:** Tier 3
**Estimated time:** 2 months
**Context:** A sustained inflation shock (20–40% food price increase) combined with store closures tests the resilience of the food access system for diabetic patients
**CMDDS v1.2 boundary conditions in scope:** BC-1 (geographic), BC-2 (economic), BC-6 (capacity)

**What it simulates:**
Models the food access system for diabetic patients under progressive inflation scenarios. Introduces store closures, price increases, and income stagnation simultaneously to identify at what point the system fails to deliver any feasible food opportunities to high-EquiRisk patients.

**The Core Question:**
*At what inflation level does the food access system for diabetic patients in food deserts reach systemic failure — defined as > 50% NULL output rate for Tier 1 patients?*

**Scenarios to Compare:**
- Baseline (2022 prices, no closures)
- Moderate inflation (15% price increase, 1 store closure)
- Current (2026 prices, observed closures)
- Stress (40% price increase, 3 store closures)
- Extreme (60% price increase, 5 store closures)

**Outputs:**
- NULL output rate curve across inflation scenarios by EquiRisk tier *(updated v1.2)*
- NULL output type distribution (no_opportunity vs. unreachable) per scenario
- System failure threshold identification (when Tier 1 NULL rate exceeds 50%)
- Equity gap change under each scenario
- Policy intervention analysis: which program (food subsidy vs. new store vs. delivery) most delays system failure?

**v1.2 Validation Note:**
Report NULL output type distribution (no_opportunity vs. unreachable) separately for each inflation scenario and EquiRisk tier. Sub-scores must be re-normalized at each scenario step if contextual vulnerability inputs change. Re-assign tiers after re-normalization. Document synthetic population generation per Step 14.

---

### Project A3: Global South Fork — Informal Food System Adaptation

**Complexity:** Tier 3–4
**Estimated time:** 2–4 months
**Context:** Most global diabetes burden is in low- and middle-income countries where food systems are informal, data is limited, and policy infrastructure differs fundamentally from the US context
**CMDDS v1.2 boundary conditions in scope:** BC-1 through BC-7 (all, with locally adapted parameters)

**What it simulates:**
Adapts the EquiRisk-FoodDeserts framework for a Global South city — replacing USDA food desert criteria with local food access definitions, substituting ADI/SVI with locally available deprivation indices, and redefining opportunity types for informal food markets and community health posts.

**Suggested Starter Cities:**
Karachi, Pakistan / Chennai, India / Lagos, Nigeria / Nairobi, Kenya

**Key Adaptations Required:**
- Redefine food desert boundary: walking distance to informal market (30 min threshold)
- Replace ADI with local deprivation composite
- Replace FQHC with community health post / CHW program
- Replace food pharmacy with food subsidy voucher program
- Adapt BC-2 economic boundary for local income distribution
- Define locally relevant equity dimensions (caste, gender, migrant status may be more relevant than US race categories)
- Define locally relevant trust barrier reference groups for BC-7: historical exclusions, caste dynamics, gender barriers in health-seeking
- Calibrate contact success probability model baseline and modifier values to local outreach data *(added v1.2)*
- Calibrate HbA1c trajectory improvement rate to local clinical data *(added v1.2)*
- Generate synthetic population using locally available data sources per Step 14 adaptation requirements *(added v1.2)*

**Outputs:**
- Adapted CMDDS fork documenting all parameter substitutions (including BC-7 local trust context, contact model calibration, and population generation method)
- Simulation results for local city
- Comparison with Milwaukee reference implementation
- Journal paper: cross-national comparison of EquiRisk-PAPO performance

**v1.2 Validation Note:**
BC-7 local trust barrier definitions must be documented and community-validated before use. Complete the adaptation documentation section of the Step 11 checklist. All substituted parameters must be listed in fork README. Document Step 15 data privacy considerations for your local regulatory context.

---

### Project A4: Trust-Adjusted Prioritization Comparative Study *(added v1.1)*

**Complexity:** Tier 3
**Estimated time:** 2 months
**Context:** CMDDS v1.1 adds trust-adjusted EquiRisk as a prioritization rule (Step 8). This project operationalizes and evaluates that rule against the existing five prioritization rules in a full multi-neighborhood simulation. As of v1.2, includes opportunity ranking, contact success probability model, HbA1c trajectories, and Equity Audit Layer.
**CMDDS v1.2 boundary conditions in scope:** BC-7 (trust), full EquiRisk scoring with trust-adjusted rule

**What it simulates:**
Runs a multi-neighborhood ABM comparing all six prioritization rules from CMDDS Step 8, with a focus on isolating the equity contribution of trust-adjusted routing. Measures whether trust-adjusted EquiRisk outperforms standard EquiRisk-weighted prioritization, and for which populations the difference is largest.

**The Core Question:**
*Does adding trust-barrier adjustment to the EquiRisk prioritization rule meaningfully improve equity outcomes — and is the improvement concentrated in specific demographic groups or neighborhoods?*

**What to Build:**
1. Implement full EquiRisk-PAPO system for 3–5 neighborhoods with varying trust barrier profiles
2. Generate synthetic population per Step 14 guidance *(added v1.2)*
3. Run all six prioritization rules from CMDDS Step 8
4. Apply opportunity ranking criteria when multiple resources are feasible *(added v1.2)*
5. Implement contact success probability model *(added v1.2)*
6. Track HbA1c trajectories for agents in pathway *(added v1.2)*
7. Run Equity Audit Layer every 30 simulation days *(added v1.2)*
8. For each rule: measure contact success rate, intervention receipt rate, NULL output rate, equity gap, HbA1c outcomes by tier
9. Isolate the marginal contribution of trust adjustment: compare EquiRisk-weighted vs. trust-adjusted EquiRisk
10. Identify: which neighborhoods and demographic groups benefit most from trust-adjusted routing?
11. Model resource cost: how many additional CHW trust-alignment hours are required to close the gap?

**Outputs:**
- Six-way prioritization rule comparison table
- Marginal equity contribution of trust adjustment: EquiRisk-weighted vs. trust-adjusted EquiRisk
- Contact equity map: which neighborhoods gain most from trust-aligned routing
- HbA1c trajectory comparison across prioritization rules by EquiRisk tier *(added v1.2)*
- Equity Audit Layer reports with alert threshold outcomes *(added v1.2)*
- Resource cost analysis: equity gain per CHW trust-alignment hour invested
- Policy recommendation: under what conditions is trust-adjusted routing cost-effective?

**EquiRisk Connection:**
This is the primary evaluation project for the trust-adjusted EquiRisk prioritization rule introduced in CMDDS v1.1. Results will inform whether future CMDDS versions promote trust-adjusted routing to a required rather than recommended component.

**v1.2 Validation Note:**
Complete the full Step 11 checklist (v1.2). Enforce state transition rules. Run Equity Audit Layer at required intervals. Report contact success rates and equity gaps disaggregated by trust_barrier level, race, income quartile, and neighborhood ADI quartile. Document opportunity ranking weights, contact model parameters, and synthetic population generation method. Publish trust-alignment parameter values and justify them in fork README.

**Target Journal:** American Journal of Public Health, Health Equity

**Fork Template:**
`EquiRisk-[YourCity]-TrustPrioritization`

---

## TIER 4 — EXTENDED RESEARCH PROJECTS

These projects are designed for research teams and generate multi-paper research programs.

---

### Project E1: Multi-City Comparative Study

**Complexity:** Tier 4
**Estimated time:** 4–6 months (team)
**What:** Implement the full EquiRisk-FoodDeserts simulation in 4–6 US cities with varying food desert severity, demographic profiles, and policy environments. Compare equity outcomes and prioritization rule effectiveness across cities. As of v1.2, city comparisons must include consistent use of EquiRisk tier definitions, opportunity ranking criteria, contact success model specification, Equity Audit Layer reporting, and synthetic population generation methods documented per Step 14 for cross-city comparability.

**v1.1 addition:** Compare trust barrier profiles across cities — do cities with stronger community health worker infrastructure show higher baseline contact equity?

**v1.2 addition:** Compare contact success model calibration across cities — do modifier values differ systematically by city characteristics? Compare HbA1c trajectory outcomes across cities under identical prioritization rules.

**Target Journal:** Lancet Digital Health, American Journal of Public Health
**Co-authorship:** Open to city-specific implementation teams

---

### Project E2: Longitudinal Policy Impact Simulation

**Complexity:** Tier 4
**Estimated time:** 4–6 months
**What:** Simulate the strategic feedback loop over a 5-year period. Model how policy changes — new food pharmacy programs, FQHC expansions, food subsidy programs — change EquiRisk score distributions, tier assignments, and equity gaps over time. As of v1.2, track HbA1c trajectories and Equity Audit Layer outputs over the full simulation period.

**v1.1 addition:** Include trust as a dynamic variable (see I5 methodology) in the longitudinal model. Track whether trust barrier distributions shift over time under different policy environments.

**v1.2 addition:** Track agent lifecycle patterns over 5 years — re-entry rates, cycling between states, long-term stabilization rates by EquiRisk tier. Compare Equity Audit Layer alert frequency across policy scenarios.

**Target Journal:** Health Affairs, Milbank Quarterly

---

### Project E3: EquiRisk-FoodDeserts + PAPO-Heatwave Integration

**Complexity:** Tier 4
**Estimated time:** 3–5 months
**What:** Build a unified simulation that runs both the heatwave and diabetes food desert frameworks simultaneously for the same city population. Identify patients who face compounded risk — high EquiRisk diabetes score AND high heatwave vulnerability. Model how combined interventions compare to separate program delivery.

**v1.1 addition:** Model compounded trust barriers — patients who face both food desert access failures and heatwave outreach failures due to BC-7 conditions. Are these the same patients? Does combined intervention delivery through a shared trusted intermediary improve equity for both outcomes simultaneously?

**v1.2 addition:** Use consistent contact success probability model across both frameworks. Track HbA1c trajectories for agents receiving combined vs. separate interventions. Run Equity Audit Layer across both outcome domains.

**Target Journal:** Nature Climate Change, Lancet Planetary Health
**Note:** This project requires familiarity with both PAPO-Heatwave-AI and EquiRisk-FoodDeserts CMDDs.

---

## How to Contribute

1. Fork this repository
2. Choose a project from this list — or propose a new modular project
3. Create your fork: `EquiRisk-FoodDeserts-[YourCity]-[ProjectCode]`
4. Implement the required components per the CMDDS v1.2
5. Complete the Step 11 Simulation Validation Checklist (v1.2) before reporting results
6. Document your assumptions and any deviations from the CMDDS clearly
7. Share your results — link your fork back to this repository
8. If your implementation produces publishable results, reach out regarding co-authorship opportunities on the comparative analysis paper

> Researchers who implement a valid EquiRisk-FoodDeserts simulation for their city and share results are invited to discuss co-authorship on the multi-city comparative analysis paper.

**Contact:** https://github.com/Min-PH

---

## Suggested Reading Before Forking

- EquiRisk SSRN preprint: https://ssrn.com/abstract=6150926
- PAPO heatwave SSRN preprint: https://ssrn.com/abstract=6198260
- Wu, M. (2026). *Artificial Intelligence in Public Health*. Springer Nature.
- CMDDS EquiRisk-FoodDeserts v1.2: https://github.com/Min-PH/EquiRisk-FoodDeserts
- USDA Food Access Research Atlas: https://www.ers.usda.gov/data-products/food-access-research-atlas/
- CDC Social Vulnerability Index: https://www.atsdr.cdc.gov/place-health/php/svi/index.html
- Neighborhood Atlas (ADI): https://www.neighborhoodatlas.medicine.wisc.edu/

---

## Acknowledgments

The modular simulation projects in this document were developed with the assistance of Claude (Anthropic), a large language model. Drawing on the EquiRisk equity-aware risk stratification framework, the Policy-Aware Personalized Opportunity (PAPO) framework, the Conceptual Model Design Documentation for Simulation (CMDDS) specification, and the supporting literature reviews for each framework, Claude helped conceptualize, structure, and draft these project descriptions — including scope definition, data requirements, build steps, output specifications, equity reporting guidance, and cross-project connections. All projects were reviewed, refined, and validated by the author to ensure alignment with the EquiRisk-FoodDeserts research program and the CMDDS v1.2 specification.
