# Autonomous Experiment Architecture

A clear and safe architecture for building human-supervised autonomous
experimental systems. The framework is based on eight layers, starting
from design and basic stability (Layer 0) up to scientific reasoning
and hypothesis suggestions (Layer 7). At every layer, safety measures
and human oversight remain central.

## Goals

- Define a transparent structure for autonomous experiments
- Keep humans responsible for all scientific and safety-critical decisions
- Provide mechanisms for anomaly handling and conflict resolution
- Use digital models (“twins”) for testing and validation
- Encourage careful development of future autonomous systems in science

## Contents

- **docs/roadmap-table.md**  
  Complete autonomy roadmap with layers, risks, and safety measures.

- **docs/safety-envelopes.md**  
  Explanation of physical, operational, and knowledge limits.

- **docs/policy-engine-spec.md**  
  Specification for the central policy engine (safety manager).

- **docs/anomaly-model.md**  
  Four-level anomaly classification and response protocol.

- **docs/autonomy-audit-protocol.md**  
  Instructions for periodic human audits of autonomous decisions.

- **docs/digital-twin-protocol.md**  
  Requirements for testing new strategies in the digital model before
  hardware execution.

## License

This repository uses two licenses:

- **Creative Commons Attribution 4.0 International (CC BY 4.0)**  
  for all documentation, text files, diagrams, and conceptual materials.

- **MIT License**  
  for all source code or scripts contained in the repository.

You are welcome to use, modify, and share this work under these terms.
Attribution is required for documentation under the CC BY 4.0 license.
