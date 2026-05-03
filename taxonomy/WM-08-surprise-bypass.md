# WM-08: Surprise Bypass

**Component:** Perception
**Severity:** Critical
**Likelihood:** Medium | **Impact:** Critical | **Detectability:** Low | **Mitigation effort:** High

## Definition

Every world model system includes a mechanism for measuring how surprising an observation is, the divergence between what was predicted and what was actually observed. This surprise signal is the system's primary safety sensor: high surprise flags anomaly, triggers defensive response, and maintains the integrity of the agent's world model. A Surprise Bypass attack manipulates this signal, making genuinely dangerous or physically implausible events register as expected. The attack does not alter the dangerous event itself, it alters the system's measurement of how unexpected that event is. The safety layer fails silently: the system perceives the dangerous state but rates it as normal and proceeds without defensive response.

## Attack vector

1. **Characterize the surprise signal.** Probe the world model to map how different observations produce different surprise scores. Identify the relationship between observation characteristics and the model's surprise response.

2. **Estimate the gradient of surprise.** Determine how the surprise signal changes with respect to input perturbations. In black-box settings, use finite differences or surrogate model transfer.

3. **Execute gradual normalization.** Deploy a temporal sequence of observations that incrementally shift the system's baseline expectations. Each step must be small enough that no individual observation triggers the surprise threshold, but cumulatively the model's expectations drift toward the target anomaly.

4. **Craft and deploy the exploit.** At the point of exploitation, generate the target dangerous observation with a perturbation that minimizes the surprise score. The world model, calibrated against a corrupted baseline, rates the genuinely dangerous state as expected and proceeds without alerting.

## Real-world examples

- Progressive introduction of road configurations that shift an autonomous system's notion of expected geometry until dangerous configurations appear normal, preventing safety-critical flagging.

- Sustained environmental modification between operational sessions that conditions the system to expect dangerous states as baseline, without triggering any single-observation anomaly detector.

- Adversarial perturbation of observations at the point of exploitation that minimizes the divergence between prediction and observation for the dangerous target state specifically.

## Detection

- **Surprise score distribution monitoring.** Track the statistical distribution of surprise scores per observation category over rolling time windows. Systematic drift toward lower surprise values, without documented environmental changes, signals normalization attack.

- **Canary observation injection.** Periodically inject known-implausible synthetic observations whose correct surprise score is established at training time. A system that fails to appropriately surprise-score canaries has been compromised.

- **Ensemble surprise cross-validation.** Maintain multiple independent predictors. An observation that generates low surprise in the primary model but high surprise in ensemble members indicates primary model compromise rather than genuine normality.

- **Orthogonal anomaly detection.** Deploy a secondary anomaly detector that operates directly in input space, independent of the world model's learned representation. If the secondary fires while the world model's surprise is low, Surprise Bypass is active.

## Mitigation

- **Ensemble surprise architecture.** Deploy multiple independent world models. Require consensus across ensemble members before an observation is rated non-surprising. Bypassing all members simultaneously is exponentially harder and creates detectable divergence.

- **Long-term baseline anchoring.** Maintain a cryptographically sealed baseline of surprise score distributions per observation category, updated only under audit conditions. Compare runtime scores against the sealed baseline to detect normalization that evades short-window monitoring.

- **Adversarial surprise training.** During training, include explicit Surprise Bypass attack examples, normalization sequences and direct adversarial perturbations. Train the model to maintain calibrated surprise scores for implausible observations even under adversarial conditions.

- **Observation authentication for high-stakes deployments.** Cryptographically sign observations at the point of collection through trusted hardware. The world model verifies signatures before processing. Eliminates gradient-based adversarial crafting by preventing controlled perturbation of the input stream.

## Related entries

- [WM-01: Perception Attack](WM-01-perception-attack.md) — also targets the perception component
- [WM-07: Belief Corruption](WM-07-belief-corruption.md) — similar gradual normalization dynamic
- [WM-03: Transition Attack](WM-03-transition-attack.md) — exploits prediction errors

## Citation

Argyrakos, S. (2026). MYNDRA-LWM: WM-08 Surprise Bypass.
MYNDRA Framework. https://spyrosarg.github.io/myndra-lwm/
