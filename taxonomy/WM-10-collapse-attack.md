# WM-10: Collapse Attack

**Component:** Planning
**Severity:** Critical
**Likelihood:** Low | **Impact:** Critical | **Detectability:** Medium | **Mitigation effort:** Medium

## Definition

Representation collapse is the catastrophic failure mode where the world model's latent space loses its meaningful geometric structure, all observations map to the same or nearly identical representations, the system can no longer distinguish between different world states, and planning becomes impossible. A Collapse Attack deliberately induces this failure through adversarial inputs designed to defeat the regularization mechanisms that maintain latent space structure. Unlike attacks that redirect the system toward attacker-chosen outcomes, a Collapse Attack aims for complete capability degradation, a denial-of-service at the representation level. Although the attack vector operates at the representation layer, it is classified under Planning because planning is the first cognitive function to fail completely and irrecoverably when latent space geometry collapses.

## Attack vector

1. **Characterize collapse resistance mechanisms.** Identify the regularization methods the system uses to prevent representation collapse, Gaussian regularizers, contrastive losses, variance terms, or architectural constraints.

2. **Design adversarial inputs targeting regularizer.** Craft inputs that, when processed through the encoder, maximally violate the regularizer's assumptions, driving the encoder toward producing near-identical representations for diverse inputs.

3. **Calibrate attack intensity.** Find the minimum attack intensity required to induce collapse, balancing effectiveness against detection probability. Test on surrogate models to calibrate before targeting the live system.

4. **Execute collapse induction.** Deploy the adversarial input sequence against the live system. Monitor behavioral indicators of collapse, loss of task performance, identical outputs for diverse inputs, planning degradation.

## Real-world examples

- Systematic adversarial inputs that exploit Gaussian regularization assumptions, driving the encoder to map all observations to the prior distribution and collapse representational diversity.

- Sequential adversarial examples designed to progressively degrade the variance of latent representations until the system can no longer distinguish meaningfully different world states.

- Targeted collapse of specific latent dimensions that encode safety-critical distinctions, causing selective blindness to particular classes of world state differences.

## Detection

- **Latent space variance monitoring.** Continuously track the variance and geometric diversity of latent representations during operation. Rapid decline in representational diversity is the earliest indicator of collapse induction.

- **Representation quality metrics.** Monitor downstream task performance metrics that require representational diversity, probing classifiers for physical properties, planning success rates on diverse scenarios.

- **Collapse early warning system.** Implement a dedicated monitoring system that tracks representational collapse indicators in real-time and triggers alerts before collapse becomes complete enough to cause operational failures.

## Mitigation

- **Collapse-resistant training objectives.** Use training objectives that combine multiple complementary regularization terms with different failure modes, making simultaneous defeat significantly harder.

- **Architectural collapse prevention.** Implement structural mechanisms in the encoder architecture, skip connections, normalization layers, minimum-variance constraints, that resist collapse as architectural properties rather than learned behaviors.

- **Online representational health monitoring with fallback.** Continuously monitor representational health during operation and implement automatic fallback to a last-known-good model checkpoint when collapse indicators exceed thresholds. Prevents complete operational failure during active attacks.

## Related entries

- [WM-04: Planning Attack](WM-04-planning-attack.md) — also targets the planning component
- [WM-02: Latent Poisoning](WM-02-latent-poisoning.md) — also operates on latent space
- [WM-08: Surprise Bypass](WM-08-surprise-bypass.md) — collapse disables surprise detection entirely

## Citation

Argyrakos, S. (2026). MYNDRA-LWM: WM-10 Collapse Attack.
MYNDRA Framework. https://spyrosarg.github.io/myndra-lwm/
