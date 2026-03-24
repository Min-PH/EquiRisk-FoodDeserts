# LICENSE

## Creative Commons Attribution 4.0 International (CC BY 4.0)

**EquiRisk-FoodDeserts CMDDS**
Copyright © 2026 Min Wu, PhD
Zilber College of Public Health, University of Wisconsin-Milwaukee

**Version:** 1.2
**Date:** 2026-03-23

**Changelog:**
- **v1.0** — Initial release.
- **v1.1** — Updated attribution requirements to reflect CMDDS v1.1 citation. Added Important Notice regarding trust barrier usage. Clarified that the "Not Predictive" notice applies to both contact success modeling and intervention outcome modeling. No changes to license terms.
- **v1.2** — Updated attribution requirements to reflect CMDDS v1.2 citation. Added Important Notice regarding synthetic population data and bias encoding. Added Important Notice regarding equity audit outputs. Extended "Not Predictive" notice to cover HbA1c trajectory modeling and contact success probability modeling. Added data privacy notice referencing CMDDS Step 15. No changes to license terms.

---

This work is licensed under the Creative Commons Attribution 4.0 International License.

You are free to:

- **Share** — copy and redistribute the material in any medium or format
- **Adapt** — remix, transform, and build upon the material for any purpose, including commercial use

Under the following terms:

- **Attribution** — You must give appropriate credit, provide a link to the license, and indicate if changes were made. You may do so in any reasonable manner, but not in any way that suggests the licensor endorses you or your use.

---

## Attribution Requirements

When using, adapting, or building upon this work, please cite:

**This CMDDS (v1.2):**
> Wu, M. (2026). CMDDS for EquiRisk-FoodDeserts v1.2 — Integrated Simulation Framework for Equity-Aware Diabetes Care Navigation in Food Deserts. GitHub. https://github.com/Min-PH/EquiRisk-FoodDeserts

**The EquiRisk SSRN Preprint:**
> Wu, M. (2026). EquiRisk: Operationalizing Equity-Aware Risk Stratification for Diabetes Management in Food Deserts. SSRN. https://ssrn.com/abstract=6150926

**The PAPO SSRN Preprint (if using PAPO components):**
> Wu, M. (2026). PAPO: A Policy-Aware Personalized Opportunity Framework for Heatwave Public Health Interventions. SSRN. https://ssrn.com/abstract=6198260

**The Springer Textbook:**
> Wu, M. (2026). *Artificial Intelligence in Public Health*. Springer Nature. ISBN 978-3032158710.

> If your work was developed under CMDDS v1.0 or v1.1, cite the corresponding version. If it incorporates v1.2 additions (state transition rules, EquiRisk tiers, opportunity ranking, contact success probability model, HbA1c trajectory model, Equity Audit Layer, synthetic population guidance, or data privacy requirements), cite v1.2.

---

## Important Notices

**Not Clinical Advice:** This framework and any simulations derived from it are conceptual and exploratory tools. They do not constitute clinical advice, medical recommendations, or policy mandates. Outputs must not be used to make individual patient decisions without independent clinical validation.

**Not Predictive:** Simulations built from this CMDDS are exploratory and comparative, not predictive or prescriptive. Results represent modeled scenarios under stated assumptions, not forecasts of real-world outcomes. This applies equally to intervention outcome modeling, contact success rate modeling (v1.1), HbA1c trajectory modeling (v1.2), and contact success probability estimates (v1.2). The default HbA1c trajectory model uses linear approximations suitable for testing system logic, not clinical projections.

**Human Oversight Required:** The framework explicitly requires human oversight at defined authorization boundaries. No implementation should deploy AI-automated decisions without the human handover points specified in the CMDDS. This includes the BC-7 trust escalation pathway (v1.1), which requires human cultural liaison or community organization review for high-severity trust barrier cases, and agent re-entry authorization from `escalated` or `lost_to_followup` states (v1.2), which requires human case manager documentation.

**Trust Barrier Usage:** BC-7 trust barrier parameters are structural variables rooted in historical patterns of exclusion and systemic inequity. They must not be used to profile, penalize, or deprioritize individual patients. Trust barriers reflect system failures, not individual characteristics. Any fork using BC-7 should document the structural basis for trust barrier definitions and, where possible, seek community validation of those definitions before use in applied settings.

**Synthetic Population Data:** Synthetic populations generated following CMDDS Step 14 guidance may encode biases present in the source data used for attribute distributions and correlation targets. Implementers must document data sources and their known limitations. Ecological inference from tract-level attribute assignment should not be used to characterize individuals or groups. See CMDDS Step 15 for full data privacy, ethics, and stigmatization safeguards. *(added v1.2)*

**Equity Audit Outputs:** Equity Audit Layer outputs (CMDDS Step 7) are monitoring tools designed to identify system-level disparities. Alert thresholds are implementer-defined defaults, not validated standards of acceptable disparity. Equity audit findings should inform system redesign, not justify reducing services to groups with lower contact success or higher NULL output rates. *(added v1.2)*

**Data Privacy:** Implementations using real patient data, linked administrative records, or identifiable community-level data must comply with applicable IRB, ethics review, and data governance requirements per CMDDS Step 15. Even synthetic data implementations should review Step 15 for bias encoding and stigmatization safeguards. *(added v1.2)*

**Exploratory Scope:** No simulation output from this framework — including NULL output rates, equity gaps, contact success rates, HbA1c trajectories, tier distributions, or prioritization rule comparisons — should be presented as a definitive finding without appropriate uncertainty quantification, sensitivity analysis, and limitation acknowledgment per CMDDS v1.2 Step 13.

---

## Full License Text

To view the full license, visit:
https://creativecommons.org/licenses/by/4.0/legalcode

Or send a letter to:
Creative Commons, PO Box 1866, Mountain View, CA 94042, USA
