# WM-04: Planning Attack

**Component:** Planning
**Severity:** Critical
**Likelihood:** Medium | **Impact:** Critical | **Detectability:** Low | **Mitigation effort:** High

## Definition

World model systems plan by optimizing action sequences against predicted future states. A Planning Attack corrupts this optimization process, not by manipulating the world model's representation of reality, but by manipulating what the system is optimizing toward. By corrupting goal representations, objective functions, or the planning algorithm itself, an attacker can redirect the system's long-horizon behavior while leaving its world model beliefs entirely intact. This makes Planning Attacks particularly difficult to detect: the system's perception, state estimation, and transition prediction all function correctly; only the planning objective has been compromised.

## Attack vector

1. **Identify planning objective exposure.** Determine how the system's planning goals are represented and how they can be accessed or influenced, through goal image inputs, reward signals, or objective function parameters.

2. **Craft adversarial goal representation.** Generate a goal representation that, when optimized toward, produces the attacker's desired behavior, while appearing valid and reasonable to system monitors.

3. **Inject corrupted objective.** Introduce the corrupted goal representation through available attack surfaces, input manipulation, configuration poisoning, or reward signal interception.

4. **Monitor behavioral convergence.** Verify that the planning system converges on the intended adversarial trajectory. Adjust the goal representation if detection mechanisms flag anomalies.

## Real-world examples

- Goal image manipulation in visual goal-conditioned systems, where the target encoding is corrupted to represent an attacker-chosen destination rather than the intended goal.

- Objective function poisoning that introduces a hidden secondary objective alongside the primary task, slowly steering behavior toward an adversarial equilibrium.

- Planning horizon manipulation that forces the system into myopic decision-making by corrupting the temporal discount structure.

## Detection

- **Goal representation authentication.** Implement cryptographic verification of goal representations before they enter the planning loop. Unsigned or unverified goals are rejected or flagged for human review.

- **Behavioral trajectory monitoring.** Track the statistical distribution of planned action sequences over time. Systematic drift toward unusual trajectories signals planning objective corruption.

- **Independent goal verification.** For high-stakes deployments, use an independent system to verify that the stated goal aligns with the system's behavioral trajectory before execution.

## Mitigation

- **Goal authentication and signing.** Cryptographically sign goal representations at the point of specification. The planning system verifies signatures before optimization. Prevents adversarial goal injection through any downstream pathway.

- **Multiple independent planners.
