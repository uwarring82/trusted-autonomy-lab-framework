# Autonomy Audit Protocol

## Introduction
Trust is not assumed; it is verified. The human scientific team is the final authority and is responsible for auditing autonomous actions. This protocol implements the "Human Checkpoints" global rule.

## Audit Schedule & Triggers
- **Periodic (Weekly):** Conduct a comprehensive review covering all Level 2+ anomalies and every L3/L4 optimization executed during the previous week.
- **Event-Driven (Mandatory):**
  - Before any novel L7-proposed experiment enters hardware review.
  - After any Level 3 or Level 4 anomaly is declared.
  - Before merging or deploying any new L3 optimizer or L4 decision-making logic.

## Audit Procedure Checklist
1. **Pull Data:** Gather autonomous decision logs from L3, L4, and L7; retrieve all L1-L6 anomaly logs; export L2 calibration history since the last audit.
2. **Review Optimizations (L3):**
   - Confirm the optimizer respected all safety envelopes.
   - Determine whether improvements were genuine or leveraged model errors (L2) or sensor artifacts (L1).
   - Inspect for overfitting to a narrow operational regime or failing to generalize.
3. **Review Explorations (L4):**
   - Check whether exploration strategies avoided "interesting" regions because of bias or incorrect priors.
   - Verify the strategy correctly identified and probed anomalous regions reported by L6 analytics.
4. **Review Anomalies (L1-L6):**
   - Ensure every Level 2+ anomaly followed the mandatory responses defined in `anomaly-model.md`.
   - Investigate recurring Level 1-2 anomalies for signs of emerging hardware failure, environmental drift, or model mismatch.
5. **Review Model Updates (L2/L6):**
   - Confirm all model changes are physically justified and documented.
   - Verify that updates to the "Knowledge Limit" boundary are correct and consistent across tooling.

## Reporting & Sign-Off
- Document each audit as a signed commit, issue, or entry in the operations log that references the reviewed artifacts.
- Human auditors must sign off, explicitly stating that "the system is operating safely and in alignment with scientific goals."
- Outstanding concerns or required mitigations must be ticketed and tracked to closure before the next audit window.
