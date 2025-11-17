# Digital Twin Validation Protocol

## Introduction
No autonomous agent (L3, L4, L7) may interact with the physical hardware using a strategy that has not first been verified in the Digital Twin. This protocol implements the "Digital Model" global rule.

## Protocol Requirements ("Test Contract")
1. **Model Fidelity Check:**
   - The L2/L6-maintained Digital Twin must demonstrate it can reproduce the last 24 hours of physical experimental data with less than X% aggregate error (project-specific threshold).
   - If fidelity cannot be demonstrated, the Twin is deemed *stale* and no new strategies may enter testing until calibration/model updates resolve the mismatch.
2. **Safety Envelope Verification:**
   - Run the proposed strategy (e.g., new L3 pulse shape, new L4 measurement path) in the Digital Twin at least 1000 times.
   - Simulate expected noise, drift, and disturbances using the L0/L2 models to stress the strategy over the operational envelope.
3. **Pass Criteria:** A strategy is marked "pass" only if every simulated execution:
   - Avoids violations of all Physical and Operational Safety Envelopes.
   - Does not trigger any simulated Level 3 or Level 4 anomalies defined in `anomaly-model.md`.
   - Produces a statistically significant improvement (for L3 optimizations) or information gain (for L4 explorations) relative to the current baseline.

## Sim-to-Real Transfer Policy
- A strategy that passes the Digital Twin contract enters a **Candidate Strategy Queue**; it is not automatically deployed.
- Each candidate requires approval through a Human Checkpoint as described in `autonomy-audit-protocol.md`.
- The first hardware execution of any new strategy must occur in a supervised mode with human oversight ready to intervene.
- Subsequent unsupervised execution is permitted only after the supervised run validates that the Twin predictions match real behavior within tolerance.
