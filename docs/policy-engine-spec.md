# Policy Engine Specification
The policy engine is the central safety and decision module for the lab.
It listens to every proposed action from the higher layers.
It checks them against safety envelopes and human checkpoints.
It stops unsafe ideas before they reach hardware.
No action may bypass the policy engine.
It creates a transparent record of how each decision was made.

## Role and authority
The policy engine has the final say on whether an action can reach hardware.
It may approve, reject, modify, or escalate any proposal.
If something looks dangerous, it can freeze the system in place.

## Inputs
- Action proposals from optimisation, measurement planning, and scientific reasoning (Layers 3, 4, and 7).
- Health reports from hardware control and calibration (Layers 1 and 2).
- Safety limits from design and calibration, including physical and operational limits.
- Knowledge limits and anomaly signals from data interpretation (Layer 6).
- Human approvals, overrides, and emergency stop commands.

## Outputs
The policy engine can approve an action exactly as proposed.
It can reject an action outright.
It can modify an action, such as shrinking a range to stay inside limits.
It can ask for a human decision before proceeding.
It can freeze the experiment and stop all motion.

## Decision logic
### Check physical limits
If the action breaks physical limits, the policy engine rejects it at once.
### Check operational limits
If the action is outside the calibrated region, the system must recalibrate before the action may proceed.
### Check knowledge limits
If the action leaves the trusted model region or enters a sensitive range, it is escalated to a human reviewer.
### Check human checkpoint rules
If the action type always needs human approval (new pulse family, long run, model change, or scientific claim), the engine holds it until a human decides.

## Digital model and anomaly handling
All high-risk actions are first tested in the digital model.
Only after successful digital tests will the policy engine approve hardware execution.
Hardware and calibration anomalies cause a pause or freeze until a human inspects the issue.
Model anomalies increase uncertainty and stop exploration until the model is repaired.
Epistemic anomalies halt autonomous decisions and call for human review because they signal missing knowledge.

## Logging and audits
Every policy engine decision is logged with time, source, target, outcome, and any conflict or override flags.
Logs are stored for at least one year and longer when the event is problematic.
Autonomy audits inspect random samples of these logs to confirm rule compliance.

## Failure modes and safe degradation
If the policy engine crashes or becomes unreliable, the system stops all autonomous actions.
Control falls back to simple manual commands with hardware interlocks still active.
Human intervention is required to restore the policy engine before autonomy restarts.
