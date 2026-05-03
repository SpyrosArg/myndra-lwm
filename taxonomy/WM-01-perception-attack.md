# WM-01: Perception Attack

**Component:** Perception
**Severity:** Critical
**Likelihood:** High | **Impact:** Critical | **Detectability:** Low | **Mitigation effort:** Medium

## Definition

Every world model begins with a perception layer that encodes raw environmental observations into compact latent representations. A Perception Attack exploits this boundary, the transition from physical reality to mathematical abstraction. By introducing carefully crafted perturbations into the input stream, an attacker systematically corrupts the world model's foundational representation of the current environment state. Since all downstream reasoning, prediction, and planning depend on this initial encoding, perception-layer corruption propagates silently through the entire system without triggering architectural defenses designed for higher layers.

## Attack vector

1. **Probe the encoding surface.** Map the relationship between raw inputs and encoded representations through systematic observation. Identify input dimensions that most strongly influence downstream state estimates.

2. **Estimate adversarial direction.** Determine the gradient of the encoding loss with respect to input perturbations. In black-box settings, use finite-difference estimation or surrogate model transfer.

3. **Craft imperceptible perturbations.** Generate perturbations that produce maximally corrupted encodings while remaining below human detection thresholds and passing basic sanity checks.

4. **Introduce and propagate.** Inject perturbations into the live input stream. Corrupted representations cascade into downstream planning and action. Verify success through behavioral observation.

## Real-world examples

- Adversarial visual patterns that cause systematic misclassification of physical objects in the environment model while appearing normal to human reviewers.

- Sensor signal manipulation that corrupts distance, velocity, or orientation estimates feeding the world model state estimator.

- Transferable attacks that exploit structural vulnerabilities common across multiple encoder architectures.

## Detection

- **Representation distribution monitoring.** Track statistical properties of encoded representations continuously. Significant drift in embedding distributions without corresponding environmental change signals attack.

- **Ensemble encoder cross-validation.** Deploy multiple independent encoders and compare outputs. Divergence between ensemble members indicates adversarial input affecting one encoder's learned manifold.

- **Cross-modal consistency checking.** For multi-sensor systems, verify consistency between independent channels. Perception attacks typically affect only one modality at a time.

## Mitigation

- **Certified robust encoders.** Use provably robust architectures with mathematical guarantees on perturbation tolerance bounds. Certifiable robustness provides bounded, auditable attack impact rather than empirical claims.

- **Multi-sensor fusion with cross-validation.** Cross-validate between independent sensor channels using different physical modalities. Simultaneous corruption of all channels without detection is exponentially harder.

- **Adversarial training.** Include perception-layer attack examples in training, both known attack patterns and generated adversarial examples specific to the deployment sensor modality and environment.

## Related entries

- [WM-08: Surprise Bypass](WM-08-surprise-bypass.md) — also targets the perception component
- [WM-02: Latent Poisoning](WM-02-latent-poisoning.md) — downstream from perception

## Citation

Argyrakos, S. (2026). MYNDRA-LWM: WM-01 Perception Attack.
MYNDRA Framework. https://spyrosarg.github.io/myndra-lwm/
