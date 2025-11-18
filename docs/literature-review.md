Literature Review: Autonomous Experimental Systems and Safety Frameworks
Last updated: 18 November 2025

1. Purpose and Scope

This document provides a focused literature review to justify the design choices behind our proposed seven-layer autonomy and safety framework for experimental physics.

The goals are:
	•	To map existing work on autonomous experiments and self-driving laboratories onto our layer model.
	•	To identify which layers are already well covered and where systematic gaps remain.
	•	To show where our framework is novel, in particular regarding safety architecture, conflict resolution, and human oversight.

This is not a full survey of the field. It is a targeted overview aimed at supporting the design and publication of our roadmap.

⸻

2. Summary: Domains vs. Autonomy Layers

We use the following informal mapping of “layers”:
	•	Layers 0–3: design, hardware control, calibration, and low-level optimisation.
	•	Layers 4–5: measurement selection and experiment orchestration.
	•	Layers 6–7: data interpretation and scientific reasoning (hypotheses, models, and research goals).

Domain / Community	Typical autonomy coverage	Explicit safety architecture?	Human-in-the-loop model
Robotics and autonomous vehicles	Strong at Layers 0–3; emerging at 4–5	Yes, layered and formally analysed safety filters	Human as supervisory operator, especially for edge cases
Self-driving labs in chemistry and materials science	Strong at Layers 3–5; some at 6	Mostly implicit (equipment limits, lab practice)	“Researcher-in-the-loop”, but protocols are informal
Trapped-ion and quantum information platforms	Strong at Layers 1–3	Local safety (watchdogs, interlocks), but not global	Physicist supervises calibration and campaigns
Digital twin and connected lab architectures	Focused on Layers 0–2 and infrastructure	Safety via simulation-first testing, not full 0–7 system	Human engineers validate models and orchestration tools
Safe control / physics-informed machine learning	Layers 1–3 (control and filters)	Yes, via formal constraints and reachability	Humans design models and interpret violations
Policy / governance for self-driving labs	Conceptual coverage of 2–6; 7 discussed but not implemented	High-level safety and dual-use concerns	Human is formally responsible, but checkpoints are not layered

A central finding of this review is:

While autonomy exists at various layers across several domains, no existing work provides a unified safety architecture that spans from hardware design through scientific hypothesis generation with explicit conflict-resolution rules, human checkpoints, and audit protocols.
This integration is the primary contribution of our roadmap.

⸻

3. Layered Safety Architectures in Robotics and Autonomous Systems

Work in robotics and autonomous vehicles provides the clearest precedent for layered architectures with time-scale separation and explicit safety filters.
	•	Layered Test and Evaluation (T&E)
The Caltech “Layered T&E for Safety-Critical Autonomous Systems” project develops methods to design and verify safety-critical systems using multiple layers and time scales: slow planning, mid-level trajectory generation, and fast real-time control. Safety is enforced through formal methods and reactive tests that surround autonomous components.  ￼
	•	Data-driven safety filters
Work on Hamilton–Jacobi reachability, control barrier functions, and related “safety filter” approaches provides a toolbox to separate safety constraints from performance objectives. Safety is encoded as state constraints; performance is encoded as a cost function. The filter corrects or vetoes unsafe actions before they reach the plant.  ￼

These efforts map naturally onto our:
	•	Layers 0–2 (design, sensing/actuation, calibration), where physical limits and state constraints are defined and enforced.
	•	Layer 3 (control optimisation), where controllers or policies are optimised subject to these safety filters.

Gap relative to our framework:
This body of work concentrates on motion and control tasks, usually in robotics and vehicles. It does not address higher layers such as experiment orchestration, data interpretation, or scientific hypothesis generation, nor does it define a full order of trust across layers.

⸻

4. Self-Driving Laboratories in Chemistry and Materials Science

Self-driving laboratories (SDLs) are the most advanced examples of autonomous experimental systems in practice.

4.1 Closed-loop optimisation and active learning
	•	AlphaFlow (Volk et al., Nat. Commun. 2023)
Demonstrates a reinforcement-learning-guided, self-driven fluidic lab capable of autonomous discovery of complex multi-step chemistries. Experimental planning and execution are fully closed-loop.  ￼
	•	CAMEO (Kusne et al., Nat. Commun. 2020)
Uses Bayesian active learning for on-the-fly, closed-loop materials discovery, with X-ray diffraction at synchrotron beamlines. The system adapts measurement locations to efficiently map phase diagrams.  ￼
	•	Autonomous materials synthesis via hierarchical active learning (Ament et al., Sci. Adv. 2021)
Shows hierarchical active learning for nonequilibrium phase diagrams, combining robotic synthesis and model-based exploration strategies.  ￼

These platforms clearly implement Layers 3–5:
	•	Automatic optimisation of experimental conditions (Layer 3).
	•	Adaptive measurement selection (Layer 4).
	•	Task-level orchestration of experimental campaigns (Layer 5).

4.2 Recent reviews and perspectives
	•	“Self-Driving Laboratories for Chemistry and Materials Science” (Tom et al., Chem. Rev. 2024) provides a broad overview of architectures, optimisation strategies, and applications of SDLs.  ￼
	•	“The rise of self-driving labs in chemical and materials sciences” (Abolhasani and Kumacheva, Nat. Synth. 2023) discusses the conceptual move from automation to truly autonomous labs and highlights the central role of human researchers in concept formation.  ￼
	•	Recent perspectives and reviews such as Cooper et al., “Accelerating discovery in natural science laboratories with AI and robotics” (Sci. Robotics / arXiv:2501.06847) and Hao et al., “Autonomous Materials Synthesis Laboratories” (ChemRxiv, 2025) analyse SDLs, Materials Acceleration Platforms, and the role of AI and robotics in natural science labs.  ￼

4.3 Safety architecture and oversight

These works acknowledge safety and governance concerns (e.g. dual-use risks, environmental impact, and reproducibility), but:
	•	Safety is often implemented as implicit constraints (e.g. “do not over-pressure this reactor”, “stay within device limits”).
	•	There is no unified, layered safety architecture comparable to our 0–7 framework.
	•	Human oversight is emphasised but usually as a general principle rather than layer-specific checkpoints.

⸻

5. Autonomous Trapped-Ion and Quantum Platforms

In quantum information and precision measurement, there is substantial work on automation at the control and calibration level, especially for trapped ions and superconducting qubits.

5.1 Automated calibration and control
	•	Experimental Bayesian Calibration of Trapped-Ion Entangling Operations (Gerster et al., PRX Quantum 2022)
Presents a Bayesian calibration protocol for Mølmer–Sørensen gates that automatically estimates multi-parameter control settings, with a stopping criterion based on a target gate infidelity.  ￼
	•	Automation in quantum logic experiments with cold molecular ions (Karl et al., arXiv 2025)
Describes fully automated control of complex trapped-ion spectroscopy experiments, including hardware watchdog timers for vacuum-critical devices, continuous monitoring, and manual interrupt capabilities.  ￼
	•	Large-scale trapped-ion quantum computers (e.g. recent Quantinuum H-series systems) rely on automated calibration routines, periodic recalibration schedules, and classical control infrastructure for phase tracking and mid-circuit feedback. (Representative implementations are summarised in recent PRX and Nature papers on scalable ion-trap processors.)  ￼

These efforts align strongly with:
	•	Layer 1: hardware control and device health monitoring.
	•	Layer 2: calibration and drift compensation.
	•	Layer 3: control optimisation and gate-level performance tuning.

5.2 Gap in higher-level autonomy

There is little published work on:
	•	Layer 4: autonomous selection of measurement or experiment types for trapped-ion systems.
	•	Layer 5: full campaign-level orchestration of experimental sequences.
	•	Layers 6–7: autonomous interpretation of data (e.g. deciding whether a model is correct) or hypothesis generation in atomic physics.

Our roadmap explicitly extends autonomy for such platforms beyond control and calibration into orchestration and scientific reasoning, but with tight safety and oversight constraints.

⸻

6. Digital Twins and Connected Laboratories

Digital twins are increasingly used as a safety and validation layer in automation, including laboratory environments.
	•	“Transforming research laboratories with connected digital twins” (Rihm et al., Nexus 2024)
Proposes connected digital twins linked by dynamic knowledge graphs to represent experimental systems, enabling reasoning and goal-driven lab operation.  ￼
	•	Industrial case studies such as E Tech Group’s “Development of a Modular Digital Twin to Enable an AI-Powered Laboratory” show how digital twins can be used to validate LLM-generated protocols and orchestration plans in simulation before deploying them in a physical lab.  ￼

These works strongly support our design choice that:
	•	Every new control or experimental plan should be tested first on a digital twin.
	•	The twin should support edge-case tests, failure-mode simulation, and stress tests before hardware execution.

However, they do not yet define a full 0–7 layered safety architecture or an explicit order of trust between physical data, digital models, and autonomous planners.

⸻

7. Safe Control and Physics-Informed Machine Learning

Recent work on safe, physics-informed machine learning supplies tools for embedding safety constraints into learning-based controllers.
	•	Tutorials and surveys on safe physics-informed ML and safe reinforcement learning summarise methods using structural priors, Lyapunov functions, control barrier functions, and Hamilton–Jacobi reachability to guarantee safety for dynamical systems.  ￼

Key insights:
	•	Safety is often encoded as a separate constraint set that must hold at all times, while performance (e.g. control cost, information gain) is optimised subject to these constraints.
	•	The techniques can be adapted to enforce physical and operational limits in our Layers 1–3, and to constrain optimiser behaviour at Layer 3.

Again, these works operate mainly at the control level, not at the levels of experiment orchestration or scientific reasoning.

⸻

8. Human Oversight, Governance, and Policy for Self-Driving Labs

Several recent papers explicitly address governance, ethics, and human roles in self-driving laboratories.
	•	“Autonomous ‘self-driving’ laboratories: a review of technology and policy implications” (Tobias and Wahab, Royal Society Open Science 2025)
Reviews SDL technology and highlights dual-use concerns, security, and the need for human oversight and accountability. Recommends that humans with domain knowledge review experimental plans and code before execution.  ￼
	•	“The rise of self-driving labs in chemical and materials sciences” (Abolhasani and Kumacheva, Nat. Synth. 2023)
Emphasises the continued importance of human scientists for concept creation and problem choice, arguing that machine learning and robotics alone cannot generate scientific understanding.  ￼
	•	Broader perspectives (Cooper et al., 2025; Canty et al., Nature Communications 2025; Yoshikawa et al., 2025) discuss themes such as the role of digital twins, appropriate levels of autonomy, access to SDL infrastructure, and safe deployment pathways.  ￼

These papers converge on three points:
	1.	Human oversight is essential.
	2.	SDLs are emerging dual-use technologies that require safety and security assessments.
	3.	Governance structures are needed, but existing proposals are mostly high-level (policy and ethics) rather than layered technical protocols.

Our framework takes these insights and translates them into concrete, layer-specific human checkpoints (for example, mandatory human approval for new control strategies at Layer 3, for campaign-level changes at Layer 5, and for any scientific claims or hypotheses at Layers 6–7).

⸻

9. Lessons from Automation Failures in Safety-Critical Systems

Historical accidents in automation provide important lessons for any autonomous scientific system:
	•	Three Mile Island (nuclear, 1979):
Operators trusted processed indicators and alarms over simple physical signs (e.g. valve position), leading to misinterpretation of reactor state.
	•	Boeing 737 MAX / MCAS (aviation):
A single faulty sensor fed into an automated control law that repeatedly overrode pilot input, with insufficient cross-checks and transparency.
	•	Calibration blind spots in quantum systems:
In some early superconducting-qubit and ion-trap calibration procedures, optimisation routines maximised specific performance metrics while becoming insensitive to certain error channels, creating “blind spots” in validation.

These cases highlight failure modes where:
	•	Automation overrode or obscured physical reality.
	•	Single points of failure (sensors or models) were trusted without redundancy.
	•	Optimisation routines led to self-reinforcing measurement biases.

Our framework responds with:
	•	An explicit order of trust for conflict resolution:
	1.	Physical safety limits and calibration (Layers 0–2)
	2.	Raw and redundant hardware signals (Layer 1)
	3.	Data interpretation and models (Layer 6)
	4.	Optimisation outputs and planners (Layers 3–4)
	5.	Scientific suggestions (Layer 7)
	•	Redundancy and anomaly handling at Layers 1–2 (duplicate sensors, sanity checks, anomaly categories and responses).
	•	Autonomy audits and logging to detect drift in practice.

⸻

10. Novelty and Contribution of Our Roadmap

Based on this review, our roadmap is novel in four critical ways that directly address identified safety and governance gaps:
	1.	Integrated 7-Layer Autonomy and Safety Model
Existing work covers different subsets of layers:
	•	Robotics and safe control: mainly Layers 0–3.
	•	Self-driving chemistry and materials labs: mainly Layers 3–5, with partial Layer 6.
	•	Trapped-ion and quantum platforms: mainly Layers 1–3.
	•	Policy work: conceptual discussion of Layers 2–6 and 7, but no implementation.
Our framework is, to our knowledge, the first to offer a single, coherent model spanning Layers 0–7 for experimental physics, with consistent roles and responsibilities at each level.
	2.	Explicit Conflict-Resolution Hierarchy (“Order of Trust”)
While layered architectures are common, we did not find an explicit priority rule stating that:
Calibration and physical safety limits must overrule hardware control; hardware control must overrule data interpretation; data interpretation must overrule optimisers and planners; and no automated layer may execute scientific decisions without human approval.

This is central to preventing automation from overriding physical reality or human judgment.
	3.	Three-Category Safety Envelopes
Many works define “constraints” in a single set. We distinguish:
	•	Physical limits (what can never be exceeded without risking damage or safety).
	•	Operational limits (what is allowed in routine experiments).
	•	Knowledge limits (where our models are considered valid and where they are not).
This taxonomy allows us to reason separately about hardware safety, day-to-day experimental practice, and epistemic uncertainty.
	4.	Layer-Specific Human Checkpoints and Progressive Deployment
Policy papers call for human oversight, but do not specify where and how often. Our roadmap defines:
	•	Concrete checkpoints at Layers 3, 5, 6, and 7.
	•	An explicit phased rollout (e.g. months 1–3 for Layers 0–2 only, then gradual additions), with validation gates and autonomy audits.
This connects high-level governance principles to practical engineering steps.

⸻

11. Conclusion

The current literature provides:
	•	Strong foundations for safe control (Layers 0–3) and closed-loop experimental optimisation (Layers 3–5).
	•	Emerging frameworks for digital twins and connected labs.
	•	Increasing recognition of ethical, safety, and dual-use issues in self-driving labs.

However, there is no existing framework that:
	•	Integrates autonomy from hardware design to scientific reasoning in a single layered model.
	•	Defines a unified safety architecture with explicit conflict-resolution rules and safety envelopes.
	•	Embeds concrete, layer-specific human checkpoints and audit protocols.

Our roadmap is designed to fill this gap for experimental physics, with an emphasis on trapped ions, complex laser systems, and related quantum and precision platforms, while remaining general enough to translate to chemistry, materials, and other experimental domains.

⸻

12. Key References (with links)

Below is a non-exhaustive list of key references mentioned above:
	1.	A. A. Volk et al., “AlphaFlow: autonomous discovery and optimization of multi-step chemistry using a self-driven fluidic lab guided by reinforcement learning,” Nature Communications 14, 1263 (2023).
https://doi.org/10.1038/s41467-023-36804-6  ￼
	2.	A. G. Kusne et al., “On-the-fly closed-loop materials discovery via Bayesian active learning,” Nature Communications 11, 5966 (2020).
https://doi.org/10.1038/s41467-020-19597-w  ￼
	3.	S. Ament et al., “Autonomous materials synthesis via hierarchical active learning of nonequilibrium phase diagrams,” Science Advances 7, eabg4930 (2021).
https://doi.org/10.1126/sciadv.abg4930  ￼
	4.	M. Abolhasani and E. Kumacheva, “The rise of self-driving labs in chemical and materials sciences,” Nature Synthesis 2, 483–494 (2023).
https://doi.org/10.1038/s44160-022-00231-0  ￼
	5.	A. V. Tobias and A. Wahab, “Autonomous ‘self-driving’ laboratories: a review of technology and policy implications,” Royal Society Open Science 12, 250646 (2025).
https://doi.org/10.1098/rsos.250646  ￼
	6.	L. Gerster et al., “Experimental Bayesian Calibration of Trapped-Ion Entangling Operations,” PRX Quantum 3, 020350 (2022).
https://doi.org/10.1103/PRXQuantum.3.020350  ￼
	7.	R. Karl et al., “Automation in quantum logic experiments with cold molecular ions,” arXiv:2510.27582 (2025).
https://arxiv.org/abs/2510.27582  ￼
	8.	S. D. Rihm et al., “Transforming research laboratories with connected digital twins,” Nexus 1, 100004 (2024).
https://doi.org/10.1016/j.ynexs.2024.100004  ￼
	9.	E Tech Group, “Development of a Modular Digital Twin to Enable an AI-Powered Laboratory” (case study, 2025).
https://etechgroup.com/case-studies/development-of-a-modular-digital-twin/  ￼
	10.	R. Murray and collaborators, “Layered T&E for Safety-Critical Autonomous Systems,” Caltech Murray Wiki (project, 2023–ongoing).
https://murray.cds.caltech.edu/Layered_T%26E_for_Safety-Critical_Autonomous_Systems  ￼
	11.	J. Drgoňa et al., “Safe Physics-Informed Machine Learning for Dynamics and Control” (ACC Tutorial, 2025).
https://mallada.ece.jhu.edu/pubs/2025-ACC-Tutorial-DNBetal.pdf  ￼
	12.	A. I. Cooper et al., “Accelerating discovery in natural science laboratories with AI and robotics: perspectives and challenges,” Science Robotics (2025) and arXiv:2501.06847.
https://doi.org/10.1126/scirobotics.adv7932
https://arxiv.org/abs/2501.06847  ￼
	13.	Y. Hao et al., “Autonomous Materials Synthesis Laboratories: Integrating Artificial Intelligence with Advanced Robotics for Accelerated Discovery,” ChemRxiv (2025).
https://doi.org/10.26434/chemrxiv-2025-fk3r7  ￼
	14.	G. Tom et al., “Self-Driving Laboratories for Chemistry and Materials Science,” Chemical Reviews 124, 10727–10789 (2024).
https://doi.org/10.1021/acs.chemrev.4c00055  ￼
	15.	R. B. Canty et al., “Science acceleration and accessibility with self-driving labs,” Nature Communications 16, 59231 (2025).
https://doi.org/10.1038/s41467-025-59231-1  ￼
