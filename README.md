# Autonomous Experiment Architecture

A clear and safe architecture for building **human-supervised** autonomous
experimental systems. The framework consists of eight layers (numbered
0–7), starting
from design and basic stability (Layer 0) up to scientific reasoning
and hypothesis suggestions (Layer 7). Across all layers, physical safety,
scientific integrity, and human oversight remain central.

This repository aims to provide a **unified autonomy and safety model**
for experimental physics (for example trapped ions, complex laser systems,
and self-driving laboratories), which can also be adapted to other
experimental domains.

A central idea is that autonomy is only acceptable when it is:

- structured into layers with clear responsibilities,
- bounded by explicit safety envelopes,
- constrained by an order of trust that favours physical reality over
  models and optimisers, and
- continuously supervised and audited by human experts.

## Goals

- Define a transparent, multi-layer structure for autonomous experiments,
  from design (Layer 0) to scientific reasoning (Layer 7).
- Keep humans responsible for all safety-critical and scientific decisions,
  with explicit checkpoints at higher layers.
- Provide mechanisms for anomaly handling, conflict resolution, and an
  order of trust between layers (calibration and physical limits first,
  optimisers and suggestions last).
- Use digital models (digital twins) as a mandatory testing and validation
  stage before new strategies reach real hardware.
- Encourage careful, documented, and auditable development of autonomous
  systems in science, with clear safety and governance principles.

## Contents

- `docs/roadmap-table.md`  
  Complete autonomy roadmap with layers, typical methods, risks, and
  layer-specific safety measures.

- `docs/safety-envelopes.md`  
  Explanation of physical limits, operational limits, and knowledge
  limits, and how they constrain autonomous behaviour.

- `docs/policy-engine-spec.md`  
  Specification for the central policy engine (safety manager) that
  checks proposed actions against safety envelopes, human checkpoints,
  and the conflict-resolution rules.

- `docs/anomaly-model.md`  
  Four-level anomaly classification and response protocol, including
  when to pause, when to stop, and when to widen uncertainties.

- `docs/autonomy-audit-protocol.md`  
  Instructions for periodic human audits of autonomous decisions,
  including sampling strategies and reporting requirements.

- `docs/digital-twin-protocol.md`  
  Requirements for testing new control strategies and experiment plans
  in the digital twin (nominal cases, edge cases, failure modes, and
  stress tests) before hardware execution.

- `docs/literature-review.md`  
  Structured review of autonomous experimental systems, self-driving
  laboratories, digital twins, and safe control. Maps existing work
  onto the eight-layer framework and identifies the gaps this
  architecture is designed to fill.

Additional folders such as `diagrams/` and `examples/` may be added
to collect figures, case studies, and reference implementations.

## Implementation Status

This repository currently provides:
- A complete conceptual architecture
- Core safety documentation
- Initial governance and audit protocols

Reference implementations and examples will be added in later phases.

## License

This repository uses two licenses:

- **Creative Commons Attribution 4.0 International** (CC BY 4.0)  
  for all documentation, text files, diagrams, and conceptual materials.

- **MIT License**  
  for all source code or scripts contained in the repository.

You are welcome to use, modify, and share this work under these terms.
Attribution is required for documentation under the Creative Commons
Attribution 4.0 International license. The MIT terms apply to any code.
See the `LICENSE` file for details.
