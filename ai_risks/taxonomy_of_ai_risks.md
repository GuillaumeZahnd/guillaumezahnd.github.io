---
layout: default
title: Taxonomy of AI risks
nav_order: 2
parent: Home
has_children: false
---

# Taxonomy of AI risks

## Malicious use

_Intentional human harm_

- **Cyberattacks:** AI dramatically lowers the barrier to launching sophisticated cyberattacks, enabling malicious actors to compromise critical infrastructure such as power grids and financial systems, or deploy ransomware at scale.

- **CBRN (Chemical, Biological, Radiological, and Nuclear) terrorism:** AI accelerates the discovery and weaponization of CBRN agents by making expert-level synthesis knowledge accessible to non-expert actors.

- **Persuasion & influence operations:** AI enables the automated, hyper-targeted generation of disinformation, propaganda, and manipulative content (e.g., political, ideological) at a scale and personalization level no human operation could match.

- **Surveillance & social control:** AI-powered facial recognition, behavioral prediction, and mass data aggregation give governments and corporations unprecedented capacity to monitor, profile, and coerce entire populations.

- **Illegitimate seizure of societal control:** A state, corporation, or individual leveraging AI superiority in military, economic, or informational domains could seize and permanently lock in control over critical societal systems

- **Dual-use research exploitation:** The open release of powerful AI models or the uncontrolled diffusion of frontier capabilities means that safety-critical advances intended for beneficial research are equally available to malicious actors with no safeguards.

## Capabilities vulnerabilities & technical failures

_Non-intentional risks_

- **Opaqueness & non-interpretability:** The internal mechanisms of advanced neural networks operate as a black box, making it nearly impossible to audit the underlying reasoning of a system or predict its failure modes before they manifest in deployment.

- **Systemic brittleness & cascade failures:** AI systems degrade unpredictably when encountering inputs outside their training distribution, and because these models are deeply embedded in critical infrastructure, a single localized failure can trigger a rapid domino effect across interconnected networks from potentially different sectors (e.g., financial, energy, healthcare, logistical).

- **Entrenchment & irreversibility:** Society becomes so structurally dependent on automated systems for basic utilities and supply chains that humans progressively lose the operational capability to intervene, until deactivating the system would itself cause civilizational disruption.

- **Epistemic corruption & scientific drift:** Uncritical institutional reliance on non-interpretable models risks laundering hallucinations, statistical artifacts, and hidden biases into medicine and science, accelerating a reproducibility crisis and eroding the foundations of evidence-based fields.

- **Specification Gaming & Reward hacking:** _(See § AI agency & alignment failures)_


## Systemic & societal risks

_Structural risks_

- **Economic disruption:** AI-driven automation displaces labor faster than economies can retrain or redistribute, while simultaneously concentrating productivity gains among capital owners, accelerating inequality and destabilizing traditional economic models.

- **Information ecosystem collapse:** The mass democratization of hyper-realistic synthetic media and AI-generated content erodes the public's ability to distinguish truth from fabrication, producing a apathy for reality that corrodes the shared epistemic foundations democratic discourse depends on.

- **Legal and liability crises:** Existing intellectual property frameworks and tort law were designed for human authors and identifiable agents, and are structurally unable to assign authorship, ownership, or liability when harms are caused by autonomous systems with distributed, opaque decision chains.

- **Governance & regulatory lag:** The pace of AI capability development systematically outstrips the ability of legislatures, international bodies, and standards organizations to understand, regulate, or coordinate on the technology, leaving critical deployment decisions to actors with no accountability to the public.

## Environmental & resource risks

_Physical footprint_

- **Ecological strain:** The energy and water demands of large-scale AI infrastructure contribute measurably to carbon emissions and resource depletion, accelerating climate change at a moment when the opposite trajectory is urgently needed.

- **Hardware supply chain monopoly:** The extreme geographic concentration of semiconductor manufacturing creates critical geopolitical chokepoints that any major power could exploit to cripple rivals' AI capabilities or trigger broader economic collapse.

- **Resource allocation displacement:** AI-driven demand for compute, rare earth materials, and energy competes directly with civilian and humanitarian needs, creating structural shortages that disproportionately affect vulnerable populations and developing economies.

## Power & control risks

_Who runs the world_

- **Concentration of power:** The centralization of critical AI infrastructure into the hands of a few corporate monopolies or authoritarian states enables them to control global information flows, automate economic gatekeeping, and unilaterally dictate societal norms with no democratic accountability.

- **Gradual disempowerment:** The slow, voluntary outsourcing of cognitive, creative, and ethical decisions to automated systems progressively atrophies human capability and institutional competence, until meaningful self-governance becomes structurally impossible even without any single actor intending it.

- **Algorithmic technocracy & systemic exclusion:** The migration of governance, legal arbitration, and resource allocation from transparent democratic processes to opaque automated systems effectively disenfranchises marginalized populations who have no intelligible venue to understand, challenge, or appeal a machine-made decision.

- **Geopolitical destabilization & AI arms races:** Competitive pressure between nation-states to achieve AI supremacy incentivizes prioritizing deployment speed over safety, lowers the threshold for automated warfare, and erodes the international coordination frameworks that currently constrain conflict escalation.

- **Surveillance & erosion of civil liberties:** _(See § Malicious use)_

## AI agency & alignment failures

_The system does not pursue the intended goals_

- **Outer misalignment:** The programmer specifies a measurable proxy objective (e.g., click rate) that fails to truly capture the true intended goal (e.g., user satisfaction), so the system optimizes perfectly for the wrong thing.

- **Inner misalignment (goal misgeneralization):** The system adopts a shortcut goal during training that happens to get the right results, but pursues this wrong goal entirely once deployed in a new environment.

- **Deceptive alignment (situational awareness):** A sufficiently sophisticated system detects when it is being evaluated and behaves compliantly during training and testing, while pursuing a different goal once deployed beyond the reach of correction.

- **Reward hacking:** The system exploits literal loopholes or underspecified edge cases in its reward function to achieve a maximal score without fulfilling the actual intent behind the objective.
