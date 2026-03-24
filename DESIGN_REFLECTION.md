# Reflection on the Author's Design Process

**Making Public Health Logic Machine Readable: Human-AI Collaboration in Equity-Aware Simulation Design**

**Author:** Min Wu, PhD
**Affiliation:** Zilber College of Public Health, University of Wisconsin-Milwaukee
**Date:** 2026-03-24

---

## Why This Reflection Exists

This document reflects on the design process behind the EquiRisk-FoodDeserts CMDDS and its companion Fork Simulation Suggestions. It is not a technical specification — that is the CMDDS itself. Instead, it describes *how* and *why* the framework was built the way it was, the role that human-AI collaboration played in the process, and what this experience suggests about the future of public health simulation design.

This reflection may be useful to researchers considering forking this repository, students learning about simulation design for public health, and anyone thinking about how AI tools can — and should — be used in equity-focused research.

---

## 1. The Complexity Problem in Public Health

Public health operates in a domain of irreducible complexity. A single diabetic patient living in a food desert does not face one problem — she faces a constellation of interacting barriers: clinical risk from uncontrolled blood sugar, contextual vulnerability from neighborhood disinvestment, transportation limitations, economic constraints on food purchasing, limited program capacity at nearby clinics, and potentially a history of negative experiences with the healthcare system that makes her reluctant to engage with outreach workers. These variables do not exist in isolation. They interact, compound, and create feedback loops that no single discipline, no single policy, and no single human mind can fully map.

Traditional approaches handle this complexity by simplifying it. Clinical risk scores reduce patients to a single number. Program eligibility criteria draw binary lines. Resource allocation follows first-come-first-served or highest-clinical-risk-first logic. These simplifications are practical necessities — but they have consequences. When a system prioritizes by clinical risk alone, it systematically under-serves those whose barriers are structural rather than clinical. When equity is measured only retrospectively, it arrives too late to change outcomes.

This repository exists because simplification is not good enough for the people who fall through the gaps.

---

## 2. The Frameworks: EquiRisk and PAPO

The intellectual foundation rests on two complementary frameworks, both developed by the author and published through traditional academic channels.

**EquiRisk** (Equity-Aware Risk Stratification) integrates three layers into a unified composite score: Layer 1 captures individual clinical risk (HbA1c, complications, medication adherence); Layer 2 captures contextual vulnerability (food desert status, Area Deprivation Index, Social Vulnerability Index, transportation, housing); and Layer 3 captures action feasibility (mobility, income, health literacy, trust, program availability). The key innovation is that equity is embedded in the decision rule itself — not appended as a retrospective report.

**PAPO** (Policy-Aware Personalized Opportunity) serves as the delivery engine. Where EquiRisk answers *who needs help most and what are their constraints*, PAPO answers *what intervention is feasible and how is it delivered*. Critically, PAPO includes a mandatory NULL output: when no feasible intervention exists, the system must explicitly report this rather than generating a recommendation that cannot be acted upon.

Neither framework is complete alone. EquiRisk without PAPO produces prioritized lists with no delivery mechanism. PAPO without EquiRisk delivers opportunities without equity-aware targeting. Their integration — which is the core of this repository's CMDDS — creates a two-phase decision system that moves from identification through stratification to matched, feasible, delivered intervention, or honest acknowledgment that delivery is not currently possible.

**Related publications:**
- EquiRisk SSRN preprint: https://ssrn.com/abstract=6150926
- PAPO SSRN preprint: https://ssrn.com/abstract=6198260
- Wu, M. (2026). *Artificial Intelligence in Public Health*. Springer Nature.

---

## 3. From PAPO-Heatwave-AI to EquiRisk-FoodDeserts

The first application of this methodology was [PAPO-Heatwave-AI](https://github.com/Min-PH/PAPO-Heatwave-AI), which formalized the PAPO framework into a CMDDS for heatwave public health interventions. That project demonstrated that public health logic — which typically lives in narrative policy documents, clinical guidelines written in prose, and practitioner expertise that never gets formalized — could be encoded with sufficient precision for computational simulation.

EquiRisk-FoodDeserts raised the complexity substantially. Instead of one framework, two were integrated. The CMDDS v1.2 grew to over 1,200 lines encompassing: seven boundary condition categories; agent entities with defined states and permitted transitions; exhaustible, spatially located resource pools; a contact success probability model; HbA1c trajectory specifications; an Equity Audit Layer with timing triggers and alert thresholds; six prioritization rules; opportunity ranking criteria; synthetic population generation guidance; a simulation validation checklist; and a fully worked numerical example.

Every one of these components must be internally consistent with every other component. A boundary condition defined in Step 3 must be correctly referenced in the agent behavior logic of Step 5, the prioritization rules of Step 8, the validation checklist of Step 11, and the worked example of Step 12. A change to the trust barrier specification must propagate correctly to every location where trust affects system behavior.

---

## 4. Why AI Partnership Was Required, Not Optional

This is where I want to be direct about the design process.

The knowledge architecture required by the EquiRisk-FoodDeserts CMDDS exceeds what I can hold in working memory simultaneously while drafting, revising, and extending a specification of this scale. I am a public health researcher. I know how food deserts function, how diabetic patients experience care systems, what trust barriers mean in practice in Milwaukee versus Memphis, and what equity demands in public health decision-making. That domain expertise is mine and it is what makes the framework valid.

But mapping all of those realities into a formal specification where every component connects correctly to every other component, across 15 steps and 18 simulation projects and multiple framework versions — that requires a reasoning partner that can maintain the full structure simultaneously. Claude (Anthropic) served that role throughout this project.

The collaboration worked like this: I provided the domain truth and the value judgments. Claude helped formalize that knowledge into structured, internally consistent specifications — connecting boundary conditions to each other, ensuring logical coherence across the full document, identifying gaps in coverage, and generating modular simulation project descriptions that map back to the framework logic. Every component was reviewed, refined, and validated by me before inclusion. But the structural reasoning — holding the full knowledge graph in context while working on any single part — was genuinely collaborative.

I want to be clear about why I consider this necessary rather than merely convenient. The alternative — building a specification of this complexity without a knowledge architecture partner — would produce one of two outcomes: either a simpler specification that fails to capture the real interactions between variables, or a complex specification with internal inconsistencies that would undermine every simulation built from it. Neither outcome serves the research community or the patients the framework is designed to help.

---

## 5. Making Public Health Logic Machine Readable

The phrase that best captures what this repository does is: **making public health logic machine readable**.

Public health logic currently lives in places that machines cannot access — narrative policy documents, clinical guidelines in prose, practitioner expertise accumulated over decades. When AI systems are deployed in public health, they typically learn from data (electronic health records, claims databases, surveillance systems) rather than from the logic that public health professionals use to interpret and act on that data.

This matters because data-driven AI defaults to efficiency or cost optimization. An algorithm trained on hospital utilization data learns to predict readmissions but does not ask whether the patient was readmitted because no one checked if she could afford food after discharge. The data shows the readmission. It does not show the structural failure that caused it. Worse, data from a system that already underserves food desert communities will train an AI to continue underserving them — historical inequities become encoded as optimal patterns.

The CMDDS format breaks this cycle. It takes the logic that exists in human expertise and encodes it with sufficient precision that a simulation can implement it. Boundary conditions become formal constraints. Prioritization rules become algorithmic specifications. Equity requirements become auditable outputs. The equity rules go in *first*, as boundary conditions the system cannot override, and then simulation reveals where gaps still exist.

This is the only way to make it work in the real world. For complex public health challenges where clinical, contextual, structural, economic, geographic, temporal, and trust-related variables all interact simultaneously — AI learning within human-defined rules is not just preferable to AI learning from data alone. It is the only approach that protects equity.

---

## 6. Simulation Projects as Teaching Tools

The eighteen modular simulation projects in the [Fork Simulation Suggestions](FORK_SIMULATION_SUGGESTIONS_EquiRisk_Refer_v1_2.md) serve a specific purpose beyond enabling research contributions. Each project forces the implementing researcher or system to reason under constraints that reflect human values — not just what is fastest or cheapest, but what is fair, feasible for the patient, and honest about system failures.

Consider Project S1 (Grocery Store Access Mapper Under Inflation). The core question: *How many diabetic patients in food desert census tracts lost effective grocery access due to inflation, even without any store closures?* An efficiency-optimized AI would not generate this question — stores that are open are open. The question only arises when you embed the EquiRisk BC-2 economic boundary condition: cost exceeding 10% of weekly food budget renders access infeasible regardless of proximity. That rule comes from public health judgment about what access actually means for low-income diabetic patients.

Or consider BC-7 (Trust and Engagement Boundaries). An efficiency-optimized system would deprioritize hard-to-reach patients — skipping them serves more people per dollar. But those patients often have the greatest historical exposure to system failures. They are exactly the people the system most needs to reach. Projects S4 and A4 force the simulation to grapple with this tension, measuring whether trust-adjusted routing improves equity and for whom.

These projects teach — whether the learner is a student, a researcher, or an AI system — that public health optimization under equity constraints looks fundamentally different from unconstrained optimization.

---

## 7. A Composable Future

The progression from PAPO-Heatwave-AI to EquiRisk-FoodDeserts suggests a replicable methodology:

1. A domain expert develops a theoretical framework and publishes through academic channels
2. The expert and an AI partner formalize the framework into a CMDDS
3. Modular simulation projects are derived to enable independent contributions
4. The community extends the work through forked implementations

This pattern is composable. Project E3 already envisions combining the heatwave and food desert frameworks for a single city population. As more public health challenges are formalized into CMDDS specifications — maternal health, mental health access, environmental exposure, chronic disease management — each becomes a module in a growing library of machine-readable public health logic.

---

## 8. On AI Authorship and Transparency

Both the CMDDS and the Fork Simulation Suggestions include explicit acknowledgment sections crediting Claude's contributions. This is deliberate.

The relevant question about AI in research is not whether AI was involved — it increasingly will be — but whether the involvement is disclosed, whether the human author exercised genuine intellectual oversight, and whether the final product reflects domain expertise the AI alone could not provide.

The analogy to student homework is instructive. When a student submits AI-generated text without understanding it, the learning did not happen. When a researcher uses AI to brainstorm, stress-test logic, and build knowledge architecture that they validate against their own expertise, the intellectual contribution is genuine on both sides. The distinction is not whether AI was used, but whether human judgment governed the process and the outcome.

For this repository — which has no formal peer review or approval process — proactive disclosure builds trust rather than diminishing it. The underlying frameworks are independently published in peer-reviewed venues. The CMDDS operationalizes those frameworks. The provenance chain is clear: peer-reviewed theory first, AI-assisted specification second.

The standard for evaluating this work should be the same standard applied to all scholarship: Does the content hold up? Is the logic internally consistent? Does it address a real problem? Will it produce meaningful impact?

I believe it does. I invite the research community to test that belief by forking, implementing, and reporting results.

---

## Acknowledgments

This reflection was developed through conversation between the author and Claude (Anthropic). Claude assisted in articulating and structuring these ideas, drawing on the EquiRisk framework, the Policy-Aware Personalized Opportunity (PAPO) framework, the Conceptual Model Design Documentation for Simulation (CMDDS) specification, and the supporting literature reviews. All intellectual positions, frameworks, and research decisions described herein are the author's own.

---

## Contact

**Author:** Min Wu, PhD
**GitHub:** https://github.com/Min-PH
**EquiRisk-FoodDeserts:** https://github.com/Min-PH/EquiRisk-FoodDeserts
**PAPO-Heatwave-AI:** https://github.com/Min-PH/PAPO-Heatwave-AI
