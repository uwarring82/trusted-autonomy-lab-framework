# Literature Review: Autonomous Experimental Systems and Safety Frameworks  
_Last updated: 18 November 2025_

This document summarizes the most relevant literature related to autonomous
experimental systems, self-driving laboratories, trapped-ion automation,
digital twins, and safe control. It also identifies where existing work maps
onto the eight-layer autonomy and safety framework used in this repository,
and where important gaps remain.

This is not a full survey. It is a focused review to justify the design
choices of our architecture and to provide context for future development.

---

## 1. Purpose and Central Finding

The goal of this review is to understand:

1. Which autonomy layers (0–7) are already addressed in the literature,  
2. Where safety architectures are explicitly defined, and  
3. Which scientific communities lack structured approaches to safe autonomy.

**Central finding:**  
While autonomy exists across several domains, **no current work provides a
unified safety architecture that spans from hardware design (Layer 0) to
scientific hypothesis generation (Layer 7), including conflict-resolution
rules, safety envelopes, and human checkpoints.**  
This integration is the main contribution of our roadmap.

---

## 2. Summary Table: Domains vs. Autonomy Layers

| Domain / Community                                   | Typical autonomy coverage              | Explicit safety architecture?                         | Human-in-the-loop?                               |
|------------------------------------------------------|---------------------------------------|-------------------------------------------------------|--------------------------------------------------|
| Robotics & autonomous vehicles                      | Layers 0–3; partial 4–5               | Yes (formal safety filters, reachability analysis)    | Supervisory human operator                       |
| Self-driving labs (chemistry/materials)             | Layers 3–5; some Layer 6              | Mostly implicit (device limits, lab procedures)        | “Researcher-in-the-loop”                         |
| Trapped-ion & quantum systems                       | Layers 1–3                             | Local safety mechanisms only                           | Physicist supervises calibration                 |
| Digital twin frameworks                              | Layers 0–2 and infrastructure          | Safety via simulation-first testing                    | Human approval of plans                          |
| Physics-informed ML (safe control)                  | Layers 1–3                             | Yes (state constraints, barrier functions)             | Humans design models                             |
| SDL governance & policy                              | 2–6 (conceptual), 7 discussed          | High-level governance, no technical protocol           | Human accountability emphasised                   |

---

## 3. Layered Safety Architectures (Robotics & Autonomous Vehicles)

### Key works

- **Layered T&E for Safety-Critical Autonomous Systems**  
  Caltech Murray Lab  
  https://murray.cds.caltech.edu/Layered_T%26E_for_Safety-Critical_Autonomous_Systems  
  Demonstrates layered architectures across time scales (planning, trajectory,
  control) with formal safety filters around AI-driven components.

- **Physics-Informed ML for Safe Control**  
  Uses Hamilton–Jacobi reachability and control barrier functions to enforce
  safety constraints before controllers act.

### Mapping to our framework  
These works address **Layers 0–3**: design, device limits, calibration, and
safety-constrained optimisation.  
They do **not** address experiment orchestration (Layers 4–5) or scientific
reasoning (Layers 6–7).

---

## 4. Autonomous Self-Driving Laboratories (Chemistry & Materials)

### Closed-loop optimisation and active learning

**AlphaFlow – Autonomous multi-step chemistry**  
Volk et al., *Nature Communications* 2023  
https://doi.org/10.1038/s41467-023-36804-6  
- Reinforcement learning drives a microfluidic lab.  
- Full closed-loop exploration.

**CAMEO – On-the-fly phase mapping**  
Kusne et al., *Nature Communications* 2020  
https://doi.org/10.1038/s41467-020-19597-w  
- Bayesian active learning for materials discovery.

**SARA – Hierarchical active learning**  
Ament et al., *Science Advances* 2021  
https://doi.org/10.1126/sciadv.abg4930  
- Robotic system exploring nonequilibrium phase diagrams.

### Reviews and perspectives

**The rise of self-driving labs**  
Abolhasani & Kumacheva, *Nature Synthesis* 2023  
https://doi.org/10.1038/s44160-022-00231-0  

**Self-driving labs for chemistry & materials**  
Tom et al., *Chemical Reviews* 2024  
https://doi.org/10.1021/acs.chemrev.4c00055  

### Mapping to our framework  
SDLs implement **Layers 3–5**, and partially Layer 6.  
Safety is typically implicit; human oversight is acknowledged but not formalised.

---

## 5. Trapped-Ion and Quantum Automation

### Automated calibration and control

**Bayesian calibration of trapped-ion entangling gates**  
Gerster et al., *PRX Quantum* 2022  
https://doi.org/10.1103/PRXQuantum.3.020350  

**Automation in quantum logic with molecular ions**  
Karl et al., arXiv:2510.27582  
https://arxiv.org/abs/2510.27582  

These works demonstrate:

- Automated frequency stabilisation  
- Drift compensation  
- Bayesian multi-parameter calibration  
- Continuous monitoring and manual override

### Mapping  
Covers **Layers 1–3** strongly.  
Layers 4–7 currently have **no automation** in trapped-ion systems.

---

## 6. Digital Twins for Safety Validation

**Transforming research labs with connected digital twins**  
Rihm et al., *Nexus* 2024  
https://doi.org/10.1016/j.ynexs.2024.100004  

**Modular Digital Twin for AI-Powered Laboratory**  
E Tech Group, 2025  
https://etechgroup.com/case-studies/development-of-a-modular-digital-twin/  

These works show:

- Simulation-first protocol validation  
- Edge-case and failure-mode exploration  
- API-driven lab automation models

### Mapping  
Digital twins provide safety for **Layers 0–3** and infrastructure for  
**Layers 4–5**, but lack higher-level scientific integration (**Layers 6–7**).

---

## 7. Safe Control and Physics-Informed ML

Key concepts:

- Safety as **state constraints**  
- Performance as **separate optimisation objective**  
- Formal safety guarantees (reachability, barrier functions)

Representative tutorial:  
**Safe Physics-Informed ML for Dynamics and Control**  
Drgoňa et al., ACC 2025 tutorial  
https://mallada.ece.jhu.edu/pubs/2025-ACC-Tutorial-DNBetal.pdf

### Mapping  
Strongly relevant for **Layer 3** (safe optimisation) and  
parts of **Layer 2** (state estimation and calibration).

---

## 8. Governance, Ethics, and Human Oversight

**Autonomous ‘self-driving’ laboratories: policy implications**  
Tobias & Wahab, *Royal Society Open Science* 2025  
https://doi.org/10.1098/rsos.250646  

Key insights:

- SDLs are dual-use technologies  
- Human oversight is essential  
- Scientists must review all experimental plans and code  
- Calls for symbols, summaries, transparency

**The rise of self-driving labs** (Abolhasani & Kumacheva 2023)  
Argues that ML/robotics cannot substitute for scientific concept formation.

### Mapping  
Addresses **Layers 2–6** conceptually, but provides no actionable technical
protocols or structured checkpoints.

---

## 9. Historical Safety Lessons

Automation failures show what can go wrong:

- **Three Mile Island** – trusting processed indicators instead of physical reality  
- **Boeing 737 MAX (MCAS)** – single-sensor failure driving catastrophic automation  
- **Qubit calibration blind spots** – optimisers maximising metrics while hiding systematic errors

Our framework responds with:

- A clear **order of trust** (physical limits > calibration > data > optimiser > planner > hypothesis)  
- Redundant sensing and drift checks  
- Anomaly classification and freeze-on-failure rules  
- Human checkpoints at critical layers (3, 5, 6, 7)

---

## 10. Novel Contributions of This Roadmap

This architecture adds four major contributions missing from existing literature:

### **1. Full 0–7 autonomy integration**
No other framework spans design → control → orchestration → scientific reasoning.

### **2. Explicit conflict-resolution rules**
Calibration and physical limits override everything above them.

### **3. Three-category safety envelope**
Physical, operational, and knowledge limits defined separately.

### **4. Layer-specific human checkpoints and phased deployment**
Human approval is required where autonomy becomes epistemically dangerous.

---

## 11. Key References (with links)

**Self-driving laboratories and active learning**
- Volk et al., Nat. Commun. 2023  
  https://doi.org/10.1038/s41467-023-36804-6  
- Kusne et al., Nat. Commun. 2020  
  https://doi.org/10.1038/s41467-020-19597-w  
- Ament et al., Sci. Adv. 2021  
  https://doi.org/10.1126/sciadv.abg4930  
- Tom et al., Chem. Rev. 2024  
  https://doi.org/10.1021/acs.chemrev.4c00055  

**Quantum control and automation**
- Gerster et al., PRX Quantum 2022  
  https://doi.org/10.1103/PRXQuantum.3.020350  
- Karl et al., arXiv:2510.27582  
  https://arxiv.org/abs/2510.27582  

**Governance and policy**
- Tobias & Wahab, RSOS 2025  
  https://doi.org/10.1098/rsos.250646  
- Abolhasani & Kumacheva, Nat. Synth. 2023  
  https://doi.org/10.1038/s44160-022-00231-0  

**Digital twins**
- Rihm et al., Nexus 2024  
  https://doi.org/10.1016/j.ynexs.2024.100004  
- E Tech Group, 2025  
  https://etechgroup.com/case-studies/development-of-a-modular-digital-twin/  

**Safe ML & control**
- Drgoňa et al., ACC tutorial 2025  
  https://mallada.ece.jhu.edu/pubs/2025-ACC-Tutorial-DNBetal.pdf  

---

## 12. Conclusion

Across robotics, chemistry, materials science, and quantum systems, many
components of autonomous experimentation exist.  
But **no complete framework** ties them together with:

- Unified safety architecture  
- Layered conflict-resolution  
- Safety envelopes  
- Human checkpoints  
- Audits and anomaly handling  
- Digital twin validation  

This repository provides such a framework and aims to set a benchmark for
safe, transparent, and responsible autonomous experimentation in physics.
