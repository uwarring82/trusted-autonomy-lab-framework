# Final Integrated Roadmap for an Autonomous Experimental System

(Architect + Guardian enhancements; clear wording; no abbreviations)

## A. Roadmap Table (Layers 0–7)

| Layer | Purpose | What this layer does | Main risks | Safety measures (including Guardian additions) | Practical next steps |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **0 — Design and Basic Stability** | Build a robust experiment from the start | Use computer models to design trap shapes, optical paths, mechanical parts | Model may not match reality; over-idealization | Validate models with known reference cases; test extreme scenarios; set strict physical limits; archive all validation results | Build a digital model; define all physical limits and store them centrally |
| **1 — Hardware-Level Control** | Keep experiment in a safe working region | Automatic laser locking, beam alignment, voltage stability | “Stable but wrong”; hidden failures | Duplicate sensors; hardware switches; alarms; human override; continuous anomaly detection (Type 1) | Develop lock routines; define health indicators; test error handling |
| **2 — Calibration and System Learning** | Measure and update physical parameters | Automatic calibration of trap frequencies, beam shapes, magnetic fields | Drift mistaken for new physics; incorrect model updates | Independent calibration tests; repeated checks; cautious starting values; anomaly checks (Type 2) | Automate calibrations; synchronize digital model after each update; re-verify autonomy protocols after model changes |
| **3 — Automatic Control Optimization** | Improve pulses, waveforms, movement sequences | Machine searches for better pulses or settings | Unsafe pulses; exploitation of noise | Only allow actions inside safe physical and operational limits; new pulse families require human approval; digital twin validation before hardware | Add bounded optimizers; implement digital twin tests for each new plan |
| **4. — Automatic Choice of Measurement Steps** | Decide next measurement or scan point | Adaptive selection of time, frequency, or spatial points | Biased exploration; ignoring rare events | Exploration diversity; interrupt planning on anomalies (Type 3); knowledge-limit checks; human approval for leaving trusted regions | Introduce measurement planner; enforce exploration quotas |
| **5 — Experiment Management** | Run long experiments and respond to problems | Execute sequences; restart calibrations; pause on problems | Cascade failures; trusting outdated layers | Safety manager that checks all actions; daily or more frequent human review; freeze on Type 1–2 anomalies; logging of all inter-layer interactions | Build safety manager; dashboards; anomaly displays |
| **6 — Data Interpretation and Model Updating** | Understand data and update model | Automatic fitting, model comparison, pattern detection | Artefacts treated as physics; incorrect model switching | Forced cross-checks; uncertainty inflation; require human review for model changes; Type 3 and Type 4 anomaly signals | Implement anomaly detectors; add version control for models |
| **7 — Scientific Reasoning and Hypothesis Proposals** | Suggest new scientific ideas | Generate hypotheses or exploration goals | Reinforced errors; ethically sensitive regions | Human approval always required; forbid exploring sensitive ranges (dual-use, poorly modeled areas); autonomy audit flags | Allow suggestions but not actions; add hypothesis review process |

---

## B. Required Guardian Protocols

### 1. Anomaly Definitions and Response

A consistent, simple 4-level anomaly schema:

* **Type 1 – Hardware anomaly**
    * **Examples:** sensor disagreement, runaway temperature, lock failure
    * **Response:** Immediate pause; alert operator; block all high-level actions

* **Type 2 – Calibration anomaly**
    * **Examples:** trap frequency shifts faster than expected, beam drift
    * **Response:** Freeze all autonomous actions; require recalibration; revalidate digital model

* **Type 3 – Model anomaly**
    * **Examples:** data inconsistent with all current models
    * **Response:** Continue with larger uncertainty; flag for human review; stop adaptive exploration

* **Type 4 – Epistemic anomaly**
    * **Examples:** model uncertainty becomes too high; trusted region exceeded
    * **Response:** Halt autonomous decision-making; require human intervention

### 2. Autonomy Audit Protocol

Regular reviews of the system’s decisions:

* Monthly review for Layers 1–4
* Weekly review for Layers 5–7
* Random sampling of autonomous decisions
* Manual inspection of:
    * Safety limit compliance
    * Model consistency
    * Signs of “optimization drift”
    * Overuse of overrides
* Archive audit outcomes

### 3. Digital Twin Validation Protocol

Every new control strategy must be tested on the digital model under four scenarios:

1.  Normal conditions
2.  Boundary conditions (edges of safe region)
3.  Failure scenarios (sensor errors, partial drift)
4.  Stress test (extreme but still physically possible)

If any fail → human approval required.

Validation results must be archived before hardware execution.

### 4. Inter-Layer Logging Requirements

Every communication between layers (commands, decisions, conflicts) must be logged with:

* time
* origin and target layers
* message content
* outcome (approved, rejected, modified)
* conflict flag
* anomaly flag
* human override flag

Logs should be kept for at least one year; indefinitely for anomalies or overrides.

---

## C. Global Constitutional Rules

* **Order of trust:**
    calibration → hardware health → data interpretation → optimization → measurement planning → scientific reasoning
* **Human checkpoints:**
    * new pulse families
    * long autonomous runs
    * model changes
    * scientific hypotheses or conclusions
* **Digital model requirement:**
    all high-risk actions must pass digital model validation first.
* **Safety envelopes:**
    1.  **physical limits** (from design)
    2.  **operational limits** (from calibration)
    3.  **knowledge limits** (from data interpretation)
    All autonomous actions must remain inside these boundaries.
* **Autonomy audits:**
    regular human review of autonomous decisions.
