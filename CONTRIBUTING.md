# CONTRIBUTING.md

## How to Contribute to EquiRisk-FoodDeserts

**Version:** 1.2
**Date:** 2026-03-23

**Changelog:**
- **v1.0** — Initial release.
- **v1.1** — Updated required components table to reflect CMDDS v1.1 additions: BC-7 (trust and engagement boundaries), contact success modeling, NULL output type-coding, and sub-score normalization. Added Step 11 Validation Checklist requirement to all contribution types. Added trust barrier documentation requirement to fork README checklist. Updated project count from 13 to 16. Added open research question contributions as Type 5. Minor clarifications throughout.
- **v1.2** — Updated required components table to reflect CMDDS v1.2 additions: agent state transition enforcement, EquiRisk tier assignment, opportunity ranking criteria, simulation time step documentation, contact success probability model specification, HbA1c trajectory model, and Equity Audit Layer. Updated fork README requirements to include v1.2 components. Added synthetic population generation documentation requirement. Added data privacy and ethics checklist requirement. Updated project count from 16 to 18. Updated open research questions to reflect eight questions in CMDDS v1.2 Step 13. Updated co-authorship requirements. Minor clarifications throughout.

---

Thank you for your interest in contributing to the EquiRisk-FoodDeserts framework. This repository is a **living conceptual specification** designed to be forked, adapted, and extended by researchers worldwide.

This guide explains how to contribute at different levels — from implementing a starter project to proposing framework extensions.

---

## Before You Contribute

Please read these documents first:

1. `CMDDS_EquiRisk_FoodDeserts_v1.2.md` — the full simulation specification
2. `FORK_SIMULATION_SUGGESTIONS.md` — the 18 modular project options
3. The EquiRisk SSRN preprint: https://ssrn.com/abstract=6150926
4. The PAPO SSRN preprint: https://ssrn.com/abstract=6198260

Understanding the core framework logic before implementing ensures your simulation preserves the EquiRisk + PAPO integration and produces results that are comparable across cities.

**Key v1.2 additions to be aware of before implementing:**
- Agent state transitions must follow the permitted transitions table (CMDDS Step 2); re-entry limits are enforced
- Composite EquiRisk scores must be assigned to tiers (Tier 1–4) using documented cutpoints (CMDDS Step 2)
- When multiple feasible opportunities exist, selection must follow documented opportunity ranking criteria (CMDDS Step 4)
- The contact success probability model must be implemented with documented parameters (CMDDS Step 4)
- Simulation time step and scheduling approach must be documented (CMDDS Step 5)
- HbA1c trajectory model must be implemented with documented parameters (CMDDS Step 5)
- The Equity Audit Layer must run at minimum every 30 simulation days and at simulation end (CMDDS Step 7)
- Synthetic population generation methods must be documented per Step 14 guidance
- Data privacy and ethics requirements in Step 15 must be reviewed and addressed

**Key v1.1 additions (still required):**
- BC-7 (Trust and Engagement Boundaries) is a required boundary condition category at minimum for projects involving contact modeling
- Sub-scores must be normalized to [0,1] before applying composite EquiRisk weights
- NULL outputs must be type-coded: `no_opportunity`, `unreachable`, or `trust_barrier`
- Contact success rates must be modeled — implementations must not assume universal reachability
- The Step 11 Simulation Validation Checklist must be completed before reporting results

---

## Contribution Types

### Type 1 — City Fork (Most Welcome)

Fork this repository and implement a simulation for your own city or context. This is the primary contribution type we are looking for.

**How to fork:**

1. Fork this repository on GitHub
2. Name your fork clearly: `EquiRisk-FoodDeserts-[YourCity]-[ProjectCode]`
   - Examples: `EquiRisk-FoodDeserts-Chicago-S1`, `EquiRisk-FoodDeserts-Lagos-A3`, `EquiRisk-FoodDeserts-Chennai-TrustBarrier`
3. Choose a project from `FORK_SIMULATION_SUGGESTIONS.md`
4. Implement the required CMDDS v1.2 components for your chosen project
5. Complete the Step 11 Simulation Validation Checklist (v1.2) and include it in your fork README
6. Document your city context, data sources, and any parameter substitutions
7. Publish your results
8. Link back to this repository in your fork README

**What your fork README must include:**
- City context and why this framework is relevant there
- Which CMDDS v1.2 components you implemented
- Data sources used (with links where possible)
- Sub-score normalization method used (min-max or alternative — must be documented)
- EquiRisk tier boundaries used (default or custom with justification) *(added v1.2)*
- BC-7 trust barrier definition for your local context (reference groups, historical exclusion patterns)
- Contact success probability model parameters and their justification *(updated v1.2)*
- Opportunity ranking weights used (default or custom with justification) *(added v1.2)*
- Simulation time step and scheduling approach *(added v1.2)*
- Synthetic population generation method (spatial scaffold, correlation structure, size) *(added v1.2)*
- HbA1c trajectory model parameters *(added v1.2)*
- Any deviations from the CMDDS and why
- Completed Step 11 Simulation Validation Checklist v1.2 (or documented partial completion with justification)
- Data privacy and ethics acknowledgment per CMDDS Step 15 *(added v1.2)*
- Key findings
- Citation of this CMDDS and the EquiRisk SSRN preprint

---

### Type 2 — Framework Extension Proposal

If you identify a gap in the CMDDS — a missing boundary condition, a new equity dimension, a new opportunity type relevant to your context — you are welcome to propose an extension.

**How to propose an extension:**

1. Open a GitHub Issue in this repository
2. Title it: `[Extension Proposal] — Brief description`
3. Describe: what is missing, why it matters, how you propose to add it
4. The repository maintainer will review and respond

**Extension proposals are especially welcome for:**
- Non-US food system contexts (informal markets, voucher systems)
- New boundary condition categories not covered in BC-1 through BC-7
- Additional equity dimensions relevant to specific populations
- New opportunity types (e.g., mobile food markets, telehealth-food integration)
- Dynamic modeling of variables currently treated as static (e.g., trust, food desert boundaries)
- Connections to other public health frameworks (e.g., mental health, hypertension, maternal care)
- Non-linear EquiRisk score formulations (e.g., compounding disadvantage models) *(added v1.2)*
- Interaction-based contact success models (beyond the default multiplicative form) *(added v1.2)*
- Community co-design methods for trust barrier definitions and equity audit thresholds *(added v1.2)*

---

### Type 3 — Simulation Implementation Links

If you have built a simulation based on this framework and published results, please share a link so it can be listed in the README under Example Implementations.

**How to submit:**
- Open a GitHub Issue titled: `[Implementation Link] — YourCity`
- Include: city, project type, brief description, link to your fork or paper
- Note whether your implementation includes BC-7, contact success modeling, state transition enforcement, and opportunity ranking (v1.2 components)

---

### Type 4 — Bug Reports and Clarifications

If you find an inconsistency, ambiguity, or error in the CMDDS documentation:

1. Open a GitHub Issue titled: `[Clarification] — Brief description`
2. Describe what is unclear or inconsistent and where it appears
3. Suggest a correction if you have one

Note: Pull requests adding code implementations to this repository are not expected — this is a conceptual specification repository. Code implementations belong in your city fork.

---

### Type 5 — Open Research Question Contributions *(added v1.1, updated v1.2)*

CMDDS v1.2 Step 13 identifies eight open research questions that are beyond the scope of this specification. If your work addresses one of these questions — empirically, methodologically, or through extended simulation — we welcome a link and summary.

**Open questions currently listed in Step 13:**
1. Empirically optimal EquiRisk weights across city contexts
2. Dynamic trust modeling and long-term equity trajectories
3. Resource level at which EquiRisk-weighted prioritization ceases to outperform clinical-only
4. Supply-side barriers and their interaction with demand-side feasibility
5. Generalization of EquiRisk-PAPO to other chronic conditions
6. Community co-design processes for BC-7 trust barrier definitions
7. Empirical correlation structure between clinical risk, contextual vulnerability, and action feasibility in real diabetic populations *(added v1.2)*
8. Optimal opportunity ranking weight calibration methods *(added v1.2)*

**How to submit:**
- Open a GitHub Issue titled: `[Research Question Response] — Question number and brief description`
- Include: which open question you address, your approach, and a link to your work

---

## Required Components for a Valid Implementation (v1.2)

Any fork claiming to implement EquiRisk-FoodDeserts v1.2 must include:

| Component | Requirement |
|---|---|
| **Three-layer EquiRisk scoring** | All three layers scored separately before combination |
| **Sub-score normalization** | All sub-scores normalized to [0,1] before weight application; method documented *(added v1.1)* |
| **Composite EquiRisk score** | Explicit, reported weights — default weights are a stress-test target |
| **EquiRisk tier assignment** | Composite scores assigned to tiers using documented cutpoints *(added v1.2)* |
| **Exhaustible resource pools** | Capacity-constrained and spatially located; trust_alignment flag on resource providers *(updated v1.1)* |
| **BC-1 and BC-3 boundary conditions** | Geographic and mobility boundaries at minimum |
| **BC-7 trust and engagement boundaries** | Required for any project involving contact or outreach modeling *(added v1.1)* |
| **NULL output with type-coding** | Type-coded as no_opportunity, unreachable, or trust_barrier; escalation required *(updated v1.1)* |
| **Contact success modeling** | Contact success probability model implemented with documented parameters *(updated v1.2)* |
| **Opportunity ranking** | When multiple feasible opportunities exist, selection follows documented ranking criteria *(added v1.2)* |
| **State transition enforcement** | Agent state transitions follow permitted transitions table; re-entry limits enforced *(added v1.2)* |
| **Simulation time step** | Scheduling approach and all time intervals documented *(added v1.2)* |
| **HbA1c trajectory model** | Implemented with documented parameters for agents in pathway *(added v1.2)* |
| **Prioritization rule comparison** | At minimum: clinical-only vs. EquiRisk-weighted |
| **Equity metric** | At least one, reported disaggregated by demographic group |
| **Equity Audit Layer** | Runs at minimum every 30 simulation days and at simulation end; alert thresholds documented *(added v1.2)* |
| **Human handover specification** | Authorization boundaries explicitly defined; includes BC-7 trust escalation pathway |
| **Step 11 Validation Checklist** | Completed (v1.2) and documented in fork README *(updated v1.2)* |
| **Synthetic population documentation** | Generation method, correlation structure, and population size documented *(added v1.2)* |
| **Data privacy acknowledgment** | Step 15 requirements reviewed; IRB status documented if real data used *(added v1.2)* |

Implementations that omit these components should not claim to be valid EquiRisk-FoodDeserts v1.2 simulations. They may still be valuable exploratory analyses — just document clearly what was and was not implemented, and reference CMDDS v1.0 or v1.1 if appropriate.

---

## Co-Authorship Policy

Researchers who implement a valid EquiRisk-FoodDeserts simulation and share their results are invited to discuss **co-authorship** on the planned multi-city comparative analysis paper.

**To be considered for co-authorship:**
- Implement all required CMDDS v1.2 components listed above
- Complete the Step 11 Simulation Validation Checklist (v1.2)
- Report at least one equity metric disaggregated by race, income, and neighborhood deprivation
- Include contact success rate analysis disaggregated by demographic group *(added v1.1)*
- Include Equity Audit Layer reports with alert threshold outcomes *(added v1.2)*
- Compare at least two prioritization rules
- Document synthetic population generation method and parameters *(added v1.2)*
- Document all assumptions and deviations transparently
- Share results publicly (fork, preprint, or published paper)
- Contact the repository maintainer at https://github.com/Min-PH

Co-authorship decisions will be made based on the intellectual contribution of each implementation and standard academic co-authorship criteria. Contact early — before finalizing your analysis — to discuss fit.

---

## Conduct and Attribution

- Always cite the EquiRisk SSRN preprint and this CMDDS (v1.2) in any derived work (see LICENSE.md)
- Do not represent simulation outputs as clinical recommendations or policy mandates
- Do not remove or override human oversight requirements from the CMDDS
- Do not treat BC-7 trust barrier definitions as fixed or universal — they require local context and, where possible, community validation
- Frame trust barriers as structural outcomes of historical exclusion, not individual patient characteristics (see CMDDS Step 15)
- Document synthetic data generation methods and acknowledge potential bias encoding (see CMDDS Step 15) *(added v1.2)*
- Treat collaborators and the research community with respect
- Be transparent about your data sources, assumptions, and limitations
- When reporting trust barrier parameters, frame them as structural barriers rooted in historical exclusion — not as individual patient characteristics

---

## Questions?

Open a GitHub Issue or contact via: https://github.com/Min-PH

We particularly welcome contributions from:
- Public health researchers in Global South cities
- PhD students looking for thesis simulation projects
- City health department analysts exploring equity tools
- Computational social scientists interested in health equity ABM
- Climate and health researchers bridging to the PAPO-Heatwave-AI framework
- Community health worker program researchers interested in trust-aligned routing
- Researchers working on dynamic trust and longitudinal equity modeling *(added v1.1)*
- Methodologists working on synthetic population generation for health equity simulations *(added v1.2)*
- Ethics and community engagement researchers interested in equity audit design *(added v1.2)*
