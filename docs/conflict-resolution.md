# Conflict Resolution Protocol

This document defines how the Trusted Autonomy Lab Framework manages disagreements between information sources, models, and control layers to maintain safety.

## Order of Trust Hierarchy
1. **Reality** – direct physical measurements and observed outcomes override all other data.
2. **Sensors** – calibrated sensing systems provide the next most trusted inputs when reality cannot be observed directly in real time.
3. **Low-Level Control** – deterministic control primitives, safety interlocks, and hard limits that enforce envelope compliance.
4. **Digital Twin** – simulated state estimators and predictive models that rehearse actions prior to hardware execution.
5. **High-Level Reasoning** – planners, optimizers, and scientific inference layers that propose new strategies.

## Conflict Detection
- The policy engine continuously compares sensor readings, actuator states, and digital twin predictions. Divergence thresholds are defined per layer pair (e.g., sensor vs. twin, twin vs. planner).
- When a higher-level plan violates a lower-layer safety envelope or contradicts verified observations, the discrepancy is flagged as a conflict event.
- Conflicts are categorized by severity (informational, caution, halt) and automatically logged with the originating layers and data snapshots.

## Resolution and Escalation
1. **Automatic Reconciliation** – For informational conflicts, low-level controllers attempt to revalidate data (e.g., re-run calibration) and request revised predictions from the digital twin.
2. **Layer Arbitration** – If conflict persists, control authority reverts to the most trusted consistent layer (reality → sensors → low-level control) while higher layers enter a paused state.
3. **Human Decision-Point** – Halt-level conflicts or repeated contradictions escalate to the designated human supervisor. The conflict report includes time, affected layers, proposed mitigations, and recommended safe states. Operations resume only after the human signs off on a chosen resolution or mandates further investigation.
