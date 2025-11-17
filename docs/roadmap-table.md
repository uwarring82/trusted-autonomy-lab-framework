# Roadmap Table
The autonomy stack is built from eight layers numbered 0 through 7.
Each layer has a clear purpose that supports the others.
Every layer carries known risks that must be managed.
Safety measures exist at each level to contain faults before they spread.
Human checkpoints confirm that major steps remain aligned with intent.
The combined plan keeps the digital model, hardware, and science in sync.

## Overview of the Layers
| Layer | Purpose | What this layer does | Main risks | Safety measures | Practical next steps |
| --- | --- | --- | --- | --- | --- |
| 0 | Define the system and its safe space | Build the digital model, document physical limits, and record baseline assumptions | Wrong limits or missing physics can endanger later layers | Formal design reviews, simulation stress tests, and locked baseline documents | Keep the digital twin current and publish any change log |
| 1 | Keep hardware healthy and aligned | Drive actuators, hold interlocks, monitor sensors, and compare duplicates | Hardware failure, desynchronised sensors, or alarms ignored | Redundant sensors, automatic shutdown paths, and audible alarms | Expand self-test coverage and practise emergency drills |
| 2 | Maintain calibration and learned parameters | Measure drifts, fit control curves, and update the digital model | Drift may mimic new physics and mask faults | Scheduled calibrations, rollback if confidence drops, and human sign-off | Add drift forecasting and improve data tagging |
| 3 | Optimise control actions | Create pulse shapes, waveforms, and control schedules | Unsafe pulses can damage hardware or push into unknown regions | Policy engine checks, sandbox simulations, and library of approved patterns | Build a catalogue of validated pulses and require review for new families |
| 4 | Plan measurements automatically | Choose the next measurement steps and adapt sequences | Exploration may become biased or miss safe checkpoints | Diversity guards, stop rules, and human review when bias metrics trip | Add bias monitors and expand stopping criteria |
| 5 | Manage full experiments | Orchestrate runs, coordinate subsystems, and handle long workflows | Cascading failures across subsystems | Layered rollback plans, watchdog timers, and staged automation levels | Develop runbooks for long autonomous runs and test failover scripts |
| 6 | Interpret data and update models | Analyse results, detect anomalies, and refresh model parameters | Artefacts may be accepted as true physics | Cross-check with reference data, dual analysis paths, and anomaly tagging | Increase anomaly coverage and maintain independent validation datasets |
| 7 | Provide scientific reasoning | Suggest hypotheses, plan campaigns, and summarise findings | Self-confirming loops and entry into sensitive parameter regions | Mandatory human review, hypothesis diversity checks, and limit awareness | Build transparent reasoning logs and train users to question suggestions |

## Global Rules for the System
### Order of trust
When layers disagree, the most physically grounded layer wins.
Physical limits and calibrations define the base truth.
Hardware health reports come next.
Data interpretation follows, because it combines measurements with the model.
Optimisation must honour the earlier results.
Measurement planning builds on optimisation.
Scientific reasoning is last and must obey all prior limits.

### Human checkpoints
Human review is mandatory before new pulse or waveform families reach hardware.
Long autonomous runs require a signed plan and an on-call human.
Model changes, especially those that alter safety envelopes, need approval.
Scientific conclusions or hypotheses must be reviewed before they guide actions.

### Digital model ("twin")
A digital model is built at design time to reflect the full system.
It is updated after every calibration and whenever hardware changes.
Risky strategies must prove safe in this model before touching hardware.
The policy engine compares live plans against the digital model on every run.

### Safety envelopes
Physical limits protect hardware from damage.
Operational limits show where calibrations remain valid.
Knowledge limits define where the model can be trusted.
Every action must remain inside all three envelopes at once.

### Autonomy audits
Regular human audits sample random autonomous decisions.
Auditors check for hidden drift, rule breaks, or silent overrides.
Findings are documented, shared, and feed improvements into all layers.
