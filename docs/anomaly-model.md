# Anomaly Model

## Introduction
System operation must halt or degrade gracefully to the safest known state in the presence of uncertainty or failure. This document defines the classification and mandatory responses that enforce that principle and uphold the "Conflict Handling" global rule.

## The Four-Level Anomaly Classification

### Level 1: Log (Warning)
- **Definition:** A minor, statistically expected deviation that keeps the system within known but non-ideal parameters.
- **Examples:** Slightly elevated sensor noise; L2 calibration drift within 1-2 sigma; sporadic telemetry dropouts that self-correct.
- **Mandatory Response:**
  1. Log the event with timestamp, affected layers, and context.
  2. Increment the appropriate monitoring counter for the component or signal.
  3. If the counter exceeds a predefined threshold within the observation window, escalate the state to Level 2.

### Level 2: Adapt (Alert)
- **Definition:** A significant deviation from the model or a failure of a non-critical component that places Operational Limits at risk.
- **Examples:** L1 lock failure; L2 calibration results outside expected bounds; L6 data interpretation fails to converge; repeated Level 1 warnings for the same subsystem.
- **Mandatory Response:**
  1. Pause L4 (Protocol Autonomy) and L3 (Optimization) activities.
  2. Trigger the relevant subsystem mitigation (e.g., initiate L1 re-lock, run L2 re-calibration, refresh L6 inference).
  3. Notify the human operator with an alert summarizing the anomaly and the autonomous action taken.

### Level 3: Safe (Hold)
- **Definition:** A critical failure, conflict between layers, or unknown state that threatens Physical Limits or Knowledge Limits.
- **Examples:** Contradictory sensor readings (L1 vs. L1); L6 data implying the L2 model is wrong per the "Conflict Handling" rule; any L3/L4 proposed action that violates an Operational Limit; disagreement between redundant controllers.
- **Mandatory Response:**
  1. Abort all active L1-L4 sequences, including queued experiments and optimizer sweeps.
  2. Place all hardware into the predefined safe-hold configuration (lasers off, fields zeroed, motion stages locked, etc.).
  3. Require mandatory human review and explicit sign-off before resuming any autonomous operation.

### Level 4: E-Stop (Hard-Stop)
- **Definition:** An immediate threat to hardware, personnel, or safety-critical boundaries.
- **Examples:** A sensor (temperature, voltage, radiation) exceeds its Physical Limit; a hardware interlock is triggered; emergency-stop input from human safety systems.
- **Mandatory Response:**
  1. Execute an immediate, non-recoverable hardware shutdown that drops all actuators to their safest passive state.
  2. Lock the system in E-Stop; clearing this state requires a full, manual human-led system restart and safety inspection.

## Implementation Responsibilities
- **Detection:**
  - Level 1 anomalies are primarily detected by L1 sensing and L2 calibration services using statistical monitors.
  - Level 2 anomalies are detected by L2/L3 supervisory logic plus the L5 Policy Engine observing counters and subsystem health.
  - Level 3 anomalies are detected by cross-layer consistency checks (L1-L4) and L6 interpretability diagnostics enforced by L5.
  - Level 4 anomalies rely on hardware interlocks, L0 safety circuits, and L5 high-priority monitors.
- **Enforcement:**
  - The L5 Orchestrator/Policy Engine enforces all state transitions, ensuring the correct mandatory response sequence is executed.
  - L5 logs state changes, notifies humans, and coordinates with L7 planning to prevent new tasks from launching until clearance is provided.
  - Human operators are responsible for clearing Level 3 safe-hold states and performing the manual restart required after Level 4.
