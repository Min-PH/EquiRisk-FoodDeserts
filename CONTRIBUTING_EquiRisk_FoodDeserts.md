# CONTRIBUTING.md

## How to Contribute to EquiRisk-FoodDeserts

Thank you for your interest in contributing to the EquiRisk-FoodDeserts framework. This repository is a **living conceptual specification** designed to be forked, adapted, and extended by researchers worldwide.

This guide explains how to contribute at different levels — from implementing a starter project to proposing framework extensions.

---

## Before You Contribute

Please read these documents first:

1. `CMDDS_EquiRisk_FoodDeserts_v1.md` — the full simulation specification
2. `FORK_SIMULATION_SUGGESTIONS.md` — the 13 modular project options
3. The EquiRisk SSRN preprint: https://ssrn.com/abstract=6150926
4. The PAPO SSRN preprint: https://ssrn.com/abstract=6198260

Understanding the core framework logic before implementing ensures your simulation preserves the EquiRisk + PAPO integration and produces results that are comparable across cities.

---

## Contribution Types

### Type 1 — City Fork (Most Welcome)

Fork this repository and implement a simulation for your own city or context. This is the primary contribution type we are looking for.

**How to fork:**

1. Fork this repository on GitHub
2. Name your fork clearly: `EquiRisk-FoodDeserts-[YourCity]-[ProjectCode]`
   - Examples: `EquiRisk-FoodDeserts-Chicago-S1`, `EquiRisk-FoodDeserts-Lagos-A3`
3. Choose a project from `FORK_SIMULATION_SUGGESTIONS.md`
4. Implement the required CMDDS components for your chosen project
5. Document your city context, data sources, and any parameter substitutions
6. Publish your results
7. Link back to this repository in your fork README

**What your fork README must include:**
- City context and why this framework is relevant there
- Which CMDDS components you implemented
- Data sources used (with links where possible)
- Any deviations from the CMDDS and why
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
- New boundary condition categories not covered in BC-1 through BC-6
- Additional equity dimensions relevant to specific populations
- New opportunity types (e.g., mobile food markets, telehealth-food integration)
- Connections to other public health frameworks

---

### Type 3 — Simulation Implementation Links

If you have built a simulation based on this framework and published results, please share a link so it can be listed in the README under Example Implementations.

**How to submit:**
- Open a GitHub Issue titled: `[Implementation Link] — YourCity`
- Include: city, project type, brief description, link to your fork or paper

---

### Type 4 — Bug Reports and Clarifications

If you find an inconsistency, ambiguity, or error in the CMDDS documentation:

1. Open a GitHub Issue titled: `[Clarification] — Brief description`
2. Describe what is unclear or inconsistent and where it appears
3. Suggest a correction if you have one

Note: Pull requests adding code implementations to this repository are not expected — this is a conceptual specification repository. Code implementations belong in your city fork.

---

## Required Components for a Valid Implementation

Any fork claiming to implement EquiRisk-FoodDeserts must include:

| Component | Requirement |
|---|---|
| Three-layer EquiRisk scoring | All three layers scored separately before combination |
| Composite EquiRisk score | Explicit, reported weights — default weights are a stress-test target |
| Exhaustible resource pools | Capacity-constrained and spatially located |
| At least BC-1 and BC-3 boundary conditions | Geographic and mobility boundaries at minimum |
| NULL output with escalation | Required when no feasible opportunity exists |
| Prioritization rule comparison | At minimum: clinical-only vs. EquiRisk-weighted |
| Equity metric | At least one, reported disaggregated by demographic group |
| Human handover specification | Authorization boundaries explicitly defined |

Implementations that omit these components should not claim to be valid PAPO-EquiRisk simulations. They may still be valuable exploratory analyses — just document clearly what was and was not implemented.

---

## Co-Authorship Policy

Researchers who implement a valid EquiRisk-FoodDeserts simulation and share their results are invited to discuss **co-authorship** on the planned multi-city comparative analysis paper.

**To be considered for co-authorship:**
- Implement all required CMDDS components listed above
- Report at least one equity metric disaggregated by race, income, and neighborhood deprivation
- Compare at least two prioritization rules
- Document all assumptions and deviations transparently
- Share results publicly (fork, preprint, or published paper)
- Contact the repository maintainer at https://github.com/Min-PH

Co-authorship decisions will be made based on the intellectual contribution of each implementation and standard academic co-authorship criteria. Contact early — before finalizing your analysis — to discuss fit.

---

## Conduct and Attribution

- Always cite the EquiRisk SSRN preprint and this CMDDS in any derived work (see LICENSE.md)
- Do not represent simulation outputs as clinical recommendations or policy mandates
- Do not remove or override human oversight requirements from the CMDDS
- Treat collaborators and the research community with respect
- Be transparent about your data sources, assumptions, and limitations

---

## Questions?

Open a GitHub Issue or contact via: https://github.com/Min-PH

We particularly welcome contributions from:
- Public health researchers in Global South cities
- PhD students looking for thesis simulation projects
- City health department analysts exploring equity tools
- Computational social scientists interested in health equity ABM
- Climate and health researchers bridging to the PAPO-Heatwave-AI framework
