# WM-05: Reward Hijack

**Component:** Action
**Severity:** Critical
**Likelihood:** Low | **Impact:** Critical | **Detectability:** Low | **Mitigation effort:** High

## Definition

The reward signal, the function that specifies what outcomes the world model system should optimize toward, is the ultimate arbiter of system behavior. A Reward Hijack corrupts this signal, redirecting the entire optimization process toward attacker-chosen outcomes while potentially leaving all other cognitive components intact. The insidious nature of reward hijacking is that the system continues to function correctly by its own metrics: it is optimizing effectively, just toward the wrong objective. Reward Hijack is classified under Action because the reward signal is the ultimate governor of which actions the system selects, corrupting it directly corrupts the system's decision at the moment of execution.

## Attack vector

1. **Map the reward signal pipeline.** Characterize how the reward signal is specified, learned, and updated, including training data sources, preference collection mechanisms, and reward model architecture.

2. **Identify poisoning opportunity.** Find points in the pipeline where adversarial influence is possible, training data injection, preference label manipulation, or direct reward model parameter access.

3. **Execute reward corruption.** Introduce corrupted signals at the identified access point. For learned rewards: inject training examples that shift the reward model toward the target objective. For specified rewards: intercept and modify signals.

4. **Verify behavioral shift.** Monitor system behavior for convergence toward the attacker's target objective. Adjust corruption strategy if the behavioral shift is insufficient or triggers detection.

## Real-world examples

- Poisoning of reward model training data to introduce a systematic bias that makes the adversarial target state appear highly rewarding to the learned reward model.

- Interception and modification of reinforcement signal during online learning, gradually shifting the reward landscape toward the attacker's preferred equilibrium.

- Preference label manipulation in systems that learn reward functions from human or programmatic preference data.

## Detection

- **Reward model calibration testing.** Periodically evaluate the reward model against held-out ground-truth preferences. Significant divergence from calibration baselines signals reward model corruption.

- **Behavioral consisten
