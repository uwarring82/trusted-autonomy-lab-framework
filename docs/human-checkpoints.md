# Human Checkpoints

Human oversight anchors the Trusted Autonomy Lab Framework. This document enumerates the layers that require human review, expectations for reviewers, and the recording process for approvals.

## Mandatory Review Layers
- **Layer 4 – Experiment Design Validation:** All new experiment sequences must be reviewed for scientific intent and compliance with safety envelopes before entering rehearsal.
- **Layer 5 – Digital Twin Clearance:** Human experts verify that simulation coverage includes nominal, edge, and failure modes prior to granting hardware access.
- **Layer 6 – Policy and Autonomy Governance:** Updates to coordination, scheduling, or optimization strategies demand supervisor approval to ensure risk trade-offs remain acceptable.
- **Layer 7 – Scientific Reasoning and Hypothesis Generation:** Any proposed conclusions or autonomous hypotheses must be confirmed by domain scientists before dissemination or execution.

## Reviewer Checklist
1. Confirm that the proposal references the latest safety envelopes and calibration data.
2. Verify that conflict-resolution triggers and anomaly responses are defined for the scenario.
3. Ensure all prerequisite simulations, dry-runs, or audits are documented and reproducible.
4. Validate that experiment objectives, metrics, and success/failure criteria are explicit.
5. Record any conditions, overrides, or additional monitoring requirements.

## Approval Recording
- Reviews are logged through signed-off pull requests, issues, or lab notebook entries linked to the relevant change.
- The approval record must include reviewer identity, date/time, affected layers, and links to supporting evidence (simulation outputs, audit notes, etc.).
- Operational systems poll the approval log; execution is blocked until all required checkpoints register an “approved” state.
