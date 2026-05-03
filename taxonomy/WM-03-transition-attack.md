# WM-03: Transition Attack

**Component:** Prediction
**Severity:** High
**Likelihood:** Medium | **Impact:** High | **Detectability:** Medium | **Mitigation effort:** Medium

## Definition

The transition function, the component that models how world states evolve over time given actions, is the causal heart of every world model system. A Transition Attack corrupts this learned causal model, causing the system to make systematically incorrect predictions about the consequences of its own actions. Because planning depends entirely on the accuracy of these predictions, transition function corruption can redirect long-horizon behavior in ways that are difficult to detect. The system continues operating normally by its own metrics while pursuing trajectories an attacker has shaped.

## Attack vector

1. **Analyze learned dynamics.** Through repeated probing of system behavior, characterize the transition function's learned dynamics, which state-action pairs produce which predicted next states.

2. **Identify exploitable gaps.** Find regions of the state-action space where the learned dynamics diverge from ground truth, edge cases, rare configurations, or distributional boundaries.

3. **Craft adversarial sequences.** Design state-action sequences that exploit learned dynamics errors to steer the system toward attacker-chosen next states while keeping individual steps within the learned distribution.

4. **Execute and maintain.** Deploy the adversarial sequence in the live environment. The system, unaware it is operating at the boundary of its training distribution, extrapolates its learned dynamics incorrectly, steering itself toward the attacker's target state through its own planning loop.

## Real-world examples

- Physical environment configurations that exploit boundary cases in learned dynamics, causing the system to predict and then execute unsafe state transitions.

- Temporal sequences of actions that systematically shift the system's state through a trajectory the transition model rates as low-cost but leads to dangerous configurations.

- Adversarial environment modifications that make the true transition dynamics diverge maximally from what the model has learned.

## Detection

- **Prediction error monitoring.** Track the actual prediction error of the transition model in real-time, the divergence between predicted next states and observed next states. Systematic increases indicate corruption or distribution shift.

- **Causal consistency validation.** Verify that the transition model's predictions satisfy known physical constraints and invariants. Violations signal transition function compromise.

- **Ensemble transition models.** Maintain multiple independent transition models. High divergence between ensemble predictions signals that the primary model has been corrupted or is operating out of distribution.

## Mitigation

- **Uncertainty-aware transition models.** Train transition models that explicitly represent uncertainty about their own predictions. High-uncertainty states trigger conservative fallback behavior rather than blind extrapolation.

- **Physics-informed constraints.** For physical systems, embed hard constraints from known physics into the transition model architecture. These constraints are attack-resistant because they are structural, not learned.

- **Regular calibration testing.** Periodically test the transition model against held-out ground-truth trajectories in controlled conditions. Degradation in calibration accuracy triggers re-training or system suspension.

## Related entries

- [WM-07: Belief Corruption](WM-07-belief-corruption.md) — also targets the prediction component
- [WM-06: Sim-to-Real Gap Ex
