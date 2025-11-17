# Safety Envelopes
The system does not allow every possible action.
Each command must stay inside defined safe regions called safety envelopes.
These regions are built on physical safety, valid calibration, and trusted knowledge.
They protect people, hardware, data, and the scientific record.
If one envelope is exceeded, the action stops and a human review starts.
Staying inside all envelopes keeps the autonomy stack predictable and transparent.

## Physical limits
Physical limits come from the design and hardware.
They include maximal voltages, laser power, temperatures, and mechanical ranges.
Layer 0 defines these limits and Layer 1 enforces them during every action.
Breaking them can damage hardware or create unsafe conditions.
- Defined in the design records, risk analyses, and digital model.
- Implemented by hardware switches, current limits, and controller checks.
- Changed only by humans after careful review, simulation, and documentation.

## Operational limits
Operational limits describe the range where calibrations remain valid.
Examples include trap frequencies between two values, beam positions within a zone, and temperature inside a narrow range.
Layer 2 defines and updates these limits after each calibration.
If the system moves outside these limits, it must recalibrate before running again.
Automatic routines stop and request recalibration before continuing.

## Knowledge limits
Knowledge limits describe where the current model of the system is trusted.
Layer 6 updates these limits using fresh data and anomaly reports.
Outside these regions, predictions become unreliable.
Sensitive ranges are a special case: dual-use or ethically critical parameters, or poorly understood regions where the model is weak.
Leaving the trusted region or entering sensitive ranges always requires human approval.
Automatic actions are not allowed in these areas.

## Interaction between the envelopes
Physical limits are the hardest boundaries and cannot be overridden.
Operational limits sit inside the physical bounds and ensure the calibration remains valid.
Knowledge limits sit inside the operational space and ensure the model is trustworthy.
All autonomous actions must fit inside all three envelopes at once.
If any envelope is breached, the action halts and the policy engine escalates to a human.

## Examples
A trapped ion system cannot drive electrodes beyond 200 volts (physical limit).
Within that space, it keeps trap frequencies between 0.8 and 1.1 megahertz to stay calibrated (operational limit).
It only trusts models of heating rates between 0.85 and 1.05 megahertz, and anything outside this window needs a human (knowledge limit).
A laser lab keeps pump power below 5 watts (physical), stabilises temperature within 0.1 degrees for alignment (operational), and only trusts beam quality predictions in that tight thermal range (knowledge).
