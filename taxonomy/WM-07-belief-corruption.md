# WM-07: Belief Corruption

**Component:** Prediction
**Severity:** High
**Likelihood:** Medium | **Impact:** High | **Detectability:** Low | **Mitigation effort:** Medium

## Definition

World model systems maintain persistent beliefs, accumulated representations of past observations and their integration into current world understanding. These beliefs are not reset between interactions; they carry forward environmental knowledge across an extended operational lifetime. Belief Corruption exploits this persistence, executing sustained campaigns of carefully calibrated adversarial observations that incrementally shift the accumulated belief state toward the attacker's target. Unlike single-observation attacks, Belief Corruption operates through time: each individual observation may appear normal, but their cumulative effect systematically corrupts the model's integrated world state. This makes the attack particularly difficult to detect and remediate: the corrupted belief state may not trigger any single-point anomaly detector.

## Attack vector

1. **Map the belief update mechanism.** Characterize how the system integrates new observations into its persistent belief state, the learning rate, recency weighting, and integration dynamics.

2. **Design incremental corruption sequence.** Plan a temporal sequence of observations that individually fall within normal ranges but cumulatively drive the belief state toward the target. Each step must be small enough to avoid triggering anomaly detectors.

3. **Execute sustained campaign.** Deploy the observation sequence across the system's operational lifetime. Maintain temporal pacing to stay within the belief update bandwidth that avoids detection.

4. **Verify belief state convergence.** Probe the system's behavioral responses to standardized test inputs over time. Progressive changes in response patterns confirm successful belief state corruption.

## Real-world examples

- Sustained campaign of slightly anomalous sensor readings that individually pass validation but cumulatively shift the world model's environmental baseline over days or weeks.

- Long-horizon episodic manipulation across multiple operational sessions that gradually corrupts the belief representation of a specific entity, location, or system parameter.

- Systematic modification of the physical environment between operational periods that accumulates into a significant belief corruption over multiple observation cycles.

## Detection

- **Longitudinal belief state auditing.** Maintain cryptographically signed snapshots of the system's belief state at regular intervals. Compare current beliefs against historical baselines to detect gradual corruption that evades point-in-time detectors.

- **Behavioral regression testing.** Periodically run standardized behavioral tests against known ground-truth scenarios. Degradation in performance on known-good test cases signals belief state corruption.

- **Belief state consistency validation.** Implement cross-validation between different modalities of the belief state. Inconsistencies that develop between independently maintained belief components indicate selective corruption.

## Mitigation

- **Immutable belief checkpoints.** Maintain cryptographically sealed belief state snapshots at regular intervals. Implement rollback capability to restore known-good belief states when corruption is detected.

- **Belief update rate limiting.** Constrain the maximum rate at which new observations can shift persistent beliefs, imposing temporal robustness that requires longer attack campaigns and increases detection probability.

- **Adversarial robustness for sequential inputs.** Train the belief update mechanism with adversarial sequential examples specifically designed to induce gradual belief corruption. Explicit robustness to these attack patterns during training significantly raises the required attack magnitude.

## Related entries

- [WM-03: Transition Attack](WM-03-transition-attack.md) — also targets the prediction component
- [WM-08: Surprise Bypass](WM-08-surprise-bypass.md) — similar gradual normalization dynamic
- [WM-06: Sim-to-Real Gap Exploitation](WM-06-sim-to-real-gap.md) — similar gradual drift dynamic

## Citation

Argyrakos, S. (2026). MYNDRA-LWM: WM-07 Belief Corruption.
MYNDRA Framework. https://spyrosarg.github.io/myndra-lwm/
