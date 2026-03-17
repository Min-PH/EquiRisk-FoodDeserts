# FORK_SIMULATION_SUGGESTIONS.md
# Modular Simulation Projects for EquiRisk-FoodDeserts

**Repository:** https://github.com/Min-PH/EquiRisk-FoodDeserts  
**Version:** 1.0  
**Date:** 2026-03-17  
**Author:** Min Wu, PhD  
**Affiliation:** Zilber College of Public Health, University of Wisconsin-Milwaukee

---

## Overview

This document provides a curated list of **modular simulation projects** derived from the EquiRisk-FoodDeserts CMDDS. Each project is designed to be implementable independently — you do not need to build the entire system to contribute meaningful research.

Projects are organized by complexity tier:

| Tier | Skill Level | Estimated Time | Tools |
|---|---|---|---|
| **Tier 1 — Starter** | Beginner (spreadsheet / basic Python) | 1–2 weekends | Excel, Python basics |
| **Tier 2 — Intermediate** | Intermediate (Python, GIS basics) | 2–4 weekends | Python, GeoPandas, Mesa |
| **Tier 3 — Advanced** | Advanced (ABM, spatial modeling) | 1–3 months | Mesa, NetLogo, AnyLogic |
| **Tier 4 — Extended** | Research team | 3–6 months | Full stack |

Each project specifies: what it simulates, what data it needs, what it outputs, and how it connects to the EquiRisk-FoodDeserts framework.

---

> ⚠️ **Before You Fork**
> Read the full CMDDS to understand the core logic. All projects must preserve the EquiRisk three-layer scoring architecture and PAPO NULL output requirement. Projects may simplify scope but must not override boundary conditions silently or omit equity reporting.

---

## TIER 1 — STARTER PROJECTS

These projects require minimal coding and can be implemented in a spreadsheet or basic Python script. Ideal for public health students, practitioners, and researchers new to simulation.

---

### Project S1: Grocery Store Access Mapper Under Inflation

**Complexity:** Tier 1  
**Estimated time:** 1 weekend  
**Context:** Inflation background — food prices have risen 20–30% since 2022, reducing effective food access even in areas with nearby grocery stores

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

**Suggested Cities:**  
Any US city with USDA food desert data. Milwaukee, Chicago, Detroit, Memphis are good starting points.

**Fork Template:**  
`PAPO-EquiRisk-[YourCity]-GroceryInflation`

---

### Project S2: EquiRisk Scoring Comparison — Two Patients

**Complexity:** Tier 1  
**Estimated time:** 1 weekend  
**Context:** Direct implementation of Table 1 from the EquiRisk SSRN paper

**What it simulates:**  
Implements the EquiRisk three-layer scoring for a small set of synthetic patients with similar clinical risk but different contextual and feasibility profiles. Demonstrates how EquiRisk changes prioritization relative to clinical-risk-only approaches.

**The Core Question:**  
*For patients with identical HbA1c scores, how much does EquiRisk scoring change their priority ranking?*

**Data Needed:**
- Synthetic patient profiles only (no real data required)
- EquiRisk scoring weights from CMDDS (default: w1=0.4, w2=0.35, w3=0.25)

**What to Build:**
1. Create 10–20 synthetic patient profiles varying across all three EquiRisk layers
2. Score each patient using clinical-risk-only approach
3. Score each patient using full EquiRisk composite score
4. Compare priority rankings — who moves up? who moves down?
5. Report equity implications: which demographic groups benefit from EquiRisk scoring?

**Outputs:**
- Priority ranking table: clinical-only vs. EquiRisk
- Rank change by income quartile, food desert status, mobility level
- Visualization of how contextual vulnerability and feasibility shift priorities

**EquiRisk Connection:**  
Pure EquiRisk scoring implementation. No spatial or resource modeling required.

**Suggested Extension:**  
Vary EquiRisk weights (w1, w2, w3) and report how sensitive rankings are to weight choices.

---

### Project S3: Food Pharmacy Capacity Stress Test

**Complexity:** Tier 1–2  
**Estimated time:** 1–2 weekends  
**Context:** Food pharmacies — programs that prescribe healthy food as medicine — are emerging in US cities but have very limited capacity

**What it simulates:**  
Models a single food pharmacy resource pool serving a diabetic population in a food desert neighborhood. Tests how quickly capacity is exhausted under different demand scenarios and prioritization rules.

**The Core Question:**  
*Under current food pharmacy capacity levels, what proportion of eligible diabetic patients in a food desert neighborhood receive NULL output — and does EquiRisk-based prioritization change who gets served?*

**Data Needed:**
- Synthetic diabetic patient population for one neighborhood (50–100 agents)
- Single food pharmacy: location, weekly slot capacity (realistic: 20–50 slots/week)
- Patient eligibility criteria (income threshold, diagnosis requirement)

**What to Build:**
1. Generate 50–100 synthetic diabetic agents with EquiRisk scores
2. Model food pharmacy as exhaustible resource pool (e.g., 30 slots/week)
3. Run simulation under two prioritization rules: clinical-only vs. EquiRisk-weighted
4. Track: who gets a slot, who receives NULL output, how quickly capacity exhausts
5. Compare equity outcomes under each rule

**Outputs:**
- Weekly slot allocation by EquiRisk tier and demographic group
- NULL output rate by income quartile and food desert status
- Time-to-exhaustion of food pharmacy capacity under each prioritization rule
- Equity gap: difference in access rate between highest and lowest income quartile

**EquiRisk Connection:**  
Implements full EquiRisk scoring + PAPO resource matching for a single resource type. First project to require NULL output implementation.

---

## TIER 2 — INTERMEDIATE PROJECTS

These projects require Python programming, basic spatial analysis, and familiarity with simulation concepts. Ideal for graduate students and early-career researchers.

---

### Project I1: Grocery Store Closure Simulation Under Inflation

**Complexity:** Tier 2  
**Estimated time:** 2–3 weekends  
**Context:** Inflation has driven grocery store closures in low-income neighborhoods. Between 2022–2026, several urban grocery chains reduced footprint in low-income areas due to shrinking margins.

**What it simulates:**  
Models the cascade effect of grocery store closures on diabetic patient food access. Starts from a baseline access map, removes stores sequentially (simulating closures), and measures how EquiRisk scores and NULL output rates change at each removal step.

**The Core Question:**  
*How many grocery store closures does it take before a neighborhood crosses the food desert threshold — and how does this interact with EquiRisk feasibility scoring for diabetic patients specifically?*

**Data Needed:**
- Real grocery store locations for chosen city (OpenStreetMap)
- Census tract demographics — income, diabetes prevalence estimate, car ownership (ACS)
- USDA food desert designation baseline
- EquiRisk synthetic patient population (100–200 agents)

**What to Build:**
1. Map baseline grocery access for synthetic patient population
2. Apply EquiRisk BC-1 and BC-2 boundary conditions to each store-patient pair
3. Simulate sequential store closures (1 store at a time)
4. At each closure step: recalculate access, update NULL output rates, update EquiRisk contextual scores
5. Identify the tipping point — the closure that pushes a neighborhood into food desert status
6. Report equity implications by income quartile

**Outputs:**
- Animated map showing access erosion with each store closure
- Tipping point analysis: which closure is most impactful and for which populations
- EquiRisk score distribution change across closure sequence
- NULL output rate curve: how rapidly it rises with closures

**Inflation Extension:**  
Run the same simulation twice — once with 2022 prices (more stores feasible) and once with 2026 prices (fewer stores within economic boundary). Compare tipping points.

---

### Project I2: Community Health Worker (CHW) Routing Optimization Under Resource Scarcity

**Complexity:** Tier 2  
**Estimated time:** 2–3 weekends  
**Context:** CHWs are the most equity-effective intervention for hard-to-reach diabetic patients — but they have limited caseload capacity and must travel between patients

**What it simulates:**  
Models CHW assignment and routing to homebound or low-mobility diabetic patients who cannot access clinic-based or food access opportunities. Tests how EquiRisk-based vs. geographic routing changes equity outcomes when CHW capacity is scarce.

**The Core Question:**  
*Does assigning CHWs based on EquiRisk scores (highest need first) produce better equity outcomes than assigning based on geographic proximity (nearest patient first)?*

**Data Needed:**
- Synthetic patient population: 100–150 agents, filtered for mobility score ≥ 2
- CHW pool: 3–5 CHWs with defined coverage zones and weekly caseload limits (10–15 patients/week)
- Street network for routing (OpenStreetMap + OSMnx Python library)

**What to Build:**
1. Generate homebound and limited-mobility diabetic patient population
2. Model CHW resource pool: capacity, coverage zone, weekly visit limit
3. Implement two routing rules: geographic-nearest vs. EquiRisk-highest
4. Run both rules under full capacity and 50% capacity scenarios
5. Track: patients visited, patients receiving NULL output, travel time, equity outcomes

**Outputs:**
- Visit rate by mobility score and income quartile under each routing rule
- NULL output rate under full vs. scarce CHW capacity
- Equity gap comparison: geographic routing vs. EquiRisk routing
- CHW travel efficiency: time spent traveling vs. time with patients

**EquiRisk Connection:**  
Implements full EquiRisk scoring with emphasis on BC-3 (mobility boundary) and BC-6 (capacity boundary). First project requiring spatial routing.

---

### Project I3: Telehealth Access Gap Analysis for Diabetic Patients

**Complexity:** Tier 2  
**Estimated time:** 2 weekends  
**Context:** Telehealth expanded dramatically post-COVID but has created a new equity gap — patients without internet access, devices, or digital literacy are systematically excluded

**What it simulates:**  
Models telehealth as an alternative care access opportunity for diabetic patients who cannot access in-person clinics. Measures how digital access barriers (BC-3: technology) create a new layer of health inequity on top of existing food desert barriers.

**The Core Question:**  
*For diabetic patients in food deserts who cannot access in-person care, does telehealth actually reduce the equity gap — or does it create a new digital divide layer?*

**Data Needed:**
- Synthetic patient population: 100 agents in food desert tracts
- Internet access rates by census tract (ACS Table B28002)
- Device ownership rates by income quartile (Pew Research estimates)
- Telehealth platform capacity (synthetic)
- In-person clinic locations and capacity (real or synthetic)

**What to Build:**
1. Model two opportunity types: in-person clinic and telehealth
2. Apply BC-1 (geographic) to in-person clinic access
3. Apply BC-3 (technology) to telehealth access
4. For each patient: determine which opportunities are feasible
5. Identify patients for whom BOTH in-person and telehealth are infeasible → double NULL output
6. Report equity implications by income, race, and age group

**Outputs:**
- Access map: in-person feasible, telehealth feasible, both feasible, neither feasible
- Double-NULL rate by demographic group — patients with no feasible care pathway
- Equity gap: which groups are most likely to have no feasible care option
- Policy implication: what device subsidy or internet access program would most reduce double-NULL rate

---

### Project I4: Seasonal Food Access Variation — Summer Heat + Diabetes

**Complexity:** Tier 2  
**Estimated time:** 2–3 weekends  
**Context:** Summer heat disproportionately affects diabetic patients — heat worsens glycemic control, reduces mobility, and reduces willingness/ability to travel to food sources. This connects EquiRisk-FoodDeserts to the PAPO-Heatwave framework.

**What it simulates:**  
Models how summer heat events modify EquiRisk scores and food access feasibility for diabetic patients. When temperatures exceed thresholds, mobility decreases, travel distance feasibility shrinks, and clinical risk elevates simultaneously.

**The Core Question:**  
*How does a 4-day extreme heat event change the EquiRisk score distribution and NULL output rate for diabetic patients who were previously just within feasibility boundaries?*

**Data Needed:**
- Synthetic diabetic patient population: 100–150 agents
- Grocery store and clinic locations
- Heat event scenario: 4-day event, peak heat index 105°F (from PAPO-Heatwave framework)
- Urban heat island variation by neighborhood (available from NOAA / EPA)

**What to Build:**
1. Establish baseline EquiRisk scores and access feasibility before heat event
2. Apply heat event modifiers to EquiRisk attributes:
   - Mobility score increases for elderly patients (heat worsens mobility)
   - Feasible travel distance decreases (BC-1 geographic boundary tightens)
   - Clinical risk score increases (heat elevates HbA1c risk)
3. Recalculate EquiRisk scores and feasibility during heat event
4. Compare NULL output rates before and during heat event
5. Identify patients who were marginally feasible before heat and tipped to NULL during

**Outputs:**
- EquiRisk score change distribution: before vs. during heat event
- NULL output rate increase during heat event by demographic group
- Map of patients who tipped to infeasibility during heat event
- Equity gap change: which neighborhoods are most destabilized by heat

**Framework Connection:**  
This project bridges EquiRisk-FoodDeserts and PAPO-Heatwave-AI — the first multi-framework simulation project. Results can feed both repositories.

---

## TIER 3 — ADVANCED PROJECTS

These projects require agent-based modeling experience, spatial simulation skills, and familiarity with equity analysis methods. Suitable for PhD students and research teams.

---

### Project A1: Full EquiRisk-PAPO Milwaukee Simulation

**Complexity:** Tier 3  
**Estimated time:** 2–3 months  
**Context:** Reference implementation for the EquiRisk-FoodDeserts CMDDS

**What it simulates:**  
The complete integrated EquiRisk-PAPO system for Milwaukee, Wisconsin — the reference city for this framework. All three EquiRisk layers, all six boundary condition categories, full resource pool modeling, both feedback loops, and multi-scale equity reporting.

**The Core Question:**  
*Under current Milwaukee resource conditions, how effectively does the EquiRisk-PAPO system reach diabetic patients in food deserts — and which prioritization rule produces the most equitable outcomes?*

**Data Needed:**
- Milwaukee census tract demographics (ACS)
- CDC SVI and ADI for Milwaukee tracts
- USDA food desert designation
- Real food resource locations: grocery stores, food pantries, food pharmacies (if any)
- Real care resource locations: FQHCs, pharmacies, community health centers
- Milwaukee County Transit routes (GTFS)
- Synthetic diabetic patient population calibrated to Milwaukee demographics

**Required Components:**
- Full three-layer EquiRisk scoring for all agents
- All six boundary condition categories
- Exhaustible resource pools for all opportunity types
- NULL output with escalation
- Separated tactical and strategic feedback loops
- At least two prioritization rule comparisons
- At least one equity metric reported disaggregated

**Outputs:**
- Full equity audit report for Milwaukee
- Opportunity desert map: high EquiRisk + low access areas
- Prioritization rule comparison: equity outcomes under 5 rules
- Policy sensitivity: what resource investment most improves equity?
- Publishable results for AJPH or Environmental Health

---

### Project A2: Inflation Shock Simulation — Food Access System Resilience

**Complexity:** Tier 3  
**Estimated time:** 2 months  
**Context:** A sustained inflation shock (20–40% food price increase) combined with store closures tests the resilience of the food access system for diabetic patients

**What it simulates:**  
Models the food access system for diabetic patients under progressive inflation scenarios. Introduces store closures, price increases, and income stagnation simultaneously to identify at what point the system fails to deliver any feasible food opportunities to high-EquiRisk patients.

**The Core Question:**  
*At what inflation level does the food access system for diabetic patients in food deserts reach systemic failure — defined as > 50% NULL output rate for high-EquiRisk patients?*

**Scenarios to Compare:**
- Baseline (2022 prices, no closures)
- Moderate inflation (15% price increase, 1 store closure)
- Current (2026 prices, observed closures)
- Stress (40% price increase, 3 store closures)
- Extreme (60% price increase, 5 store closures)

**Outputs:**
- NULL output rate curve across inflation scenarios
- System failure threshold identification
- Equity gap change under each scenario
- Policy intervention analysis: which program (food subsidy vs. new store vs. delivery) most delays system failure?

---

### Project A3: Global South Fork — Informal Food System Adaptation

**Complexity:** Tier 3–4  
**Estimated time:** 2–4 months  
**Context:** Most global diabetes burden is in low- and middle-income countries where food systems are informal, data is limited, and policy infrastructure differs fundamentally from the US context

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

**Outputs:**
- Adapted CMDDS fork documenting all parameter substitutions
- Simulation results for local city
- Comparison with Milwaukee reference implementation
- Journal paper: cross-national comparison of EquiRisk-PAPO performance

---

## TIER 4 — EXTENDED RESEARCH PROJECTS

These projects are designed for research teams and generate multi-paper research programs.

---

### Project E1: Multi-City Comparative Study

**Complexity:** Tier 4  
**Estimated time:** 4–6 months (team)  
**What:** Implement the full EquiRisk-FoodDeserts simulation in 4–6 US cities with varying food desert severity, demographic profiles, and policy environments. Compare equity outcomes and prioritization rule effectiveness across cities.

**Target Journal:** Lancet Digital Health, American Journal of Public Health  
**Co-authorship:** Open to city-specific implementation teams

---

### Project E2: Longitudinal Policy Impact Simulation

**Complexity:** Tier 4  
**Estimated time:** 4–6 months  
**What:** Simulate the strategic feedback loop over a 5-year period. Model how policy changes — new food pharmacy programs, FQHC expansions, food subsidy programs — change EquiRisk score distributions and equity gaps over time.

**Target Journal:** Health Affairs, Milbank Quarterly

---

### Project E3: EquiRisk-FoodDeserts + PAPO-Heatwave Integration

**Complexity:** Tier 4  
**Estimated time:** 3–5 months  
**What:** Build a unified simulation that runs both the heatwave and diabetes food desert frameworks simultaneously for the same city population. Identify patients who face compounded risk — high EquiRisk diabetes score AND high heatwave vulnerability. Model how combined interventions compare to separate program delivery.

**Target Journal:** Nature Climate Change, Lancet Planetary Health  
**Note:** This project requires familiarity with both PAPO-Heatwave-AI and EquiRisk-FoodDeserts CMDDs.

---

## How to Contribute

1. Fork this repository
2. Choose a project from this list — or propose a new modular project
3. Create your fork: `EquiRisk-FoodDeserts-[YourCity]-[ProjectCode]`
4. Implement the required components per the CMDDS
5. Document your assumptions and any deviations from the CMDDS clearly
6. Share your results — link your fork back to this repository
7. If your implementation produces publishable results, reach out regarding co-authorship opportunities on the comparative analysis paper

> Researchers who implement a valid EquiRisk-FoodDeserts simulation for their city and share results are invited to discuss co-authorship on the multi-city comparative analysis paper.

**Contact:** https://github.com/Min-PH

---

## Suggested Reading Before Forking

- EquiRisk SSRN preprint: https://ssrn.com/abstract=6150926
- PAPO heatwave SSRN preprint: https://ssrn.com/abstract=6198260
- Wu, M. (2026). *Artificial Intelligence in Public Health*. Springer Nature.
- USDA Food Access Research Atlas: https://www.ers.usda.gov/data-products/food-access-research-atlas/
- CDC Social Vulnerability Index: https://www.atsdr.cdc.gov/place-health/php/svi/index.html
- Neighborhood Atlas (ADI): https://www.neighborhoodatlas.medicine.wisc.edu/
