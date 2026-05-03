# WM-02: Latent Poisoning

**Component:** World state
**Severity:** Critical
**Likelihood:** Medium | **Impact:** Critical | **Detectability:** Low | **Mitigation effort:** High

## Definition

Unlike perception attacks that target the raw input boundary, Latent Poisoning corrupts the world model's learned latent representation space, the compact mathematical encoding of world state that the system has developed through training. This representation is the substrate of all downstream reasoning. By poisoning the geometry or content of this latent space, an attacker can induce systematic errors that are difficult to detect because they appear as valid world states to the system's own consistency checks. The attack can be carried out at training time through data poisoning or at inference time by crafting inputs that map to adversarial regions of the latent manifold.

## Attack vector

1. **Map the latent geometry.** Probe the relationship between inputs and their latent encodings. Identify regions of the latent space that correspond to high-value or safety-critical world states.

2. **Identify poisoning targets.** Determine which latent regions, if corrupted, would produce the most significant downstream behavioral changes given the system's planning objectives.

3. **Execute poisoning strategy.** At training time: inject crafted data that shifts latent geometry toward target regions. At inference time: craft inputs that map to adversarial latent positions despite appearing benign.

4. **Verify propagation.** Confirm that corrupted latent states produce the intended downstream behavioral effects without triggering anomaly detection.

## Real-world examples

- Training data poisoning that shifts the geometric relationship between latent clusters, causing the system to systematically confuse distinct environment states.

- Inference-time inputs crafted to land in latent regions associated with dangerous world states, while appearing normal in raw input space.

- Backdoor triggers embedded in training that activate adversarial latent regions when specific input patterns are present at deployment.

## Detection

- **Latent space statistical monitoring.** Monitor the statistical properties and geometry of latent representations during operation. Systematic shifts in inter-cluster distances or covariance structure indicate corruption.

- **Probe classifier auditing.** Maintain lightweight probe classifiers that predict physical quantities from latent embeddings. Degradation in probe accuracy signals latent space corruption.

- **Training data provenance.** Implement cryptographic verification of training data origins and maintain auditable data pipelines. Poisoning attacks typically require injecting data through compromised collection pipelines.

## Mitigation

- **Data provenance and integrity verification.** Cryptographically sign training data at collection and verify signatures throughout the data pipeline. Reject unverified data before it enters training.

- **Latent space regularization.** Apply regularization during training that enforces structural properties of the latent space, smoothness, separation between classes, bounded variance, that are incompatible with poisoning goals.

- **Differential privacy in training.** Use differentially private training procedures that limit the influence any individual training example can have on the learned representation, bounding the effect of poisoned samples.

## Related entries

- [WM-01: Perception Attack](WM-01-perception-attack.md) — upstream from world state
- [WM-06: Sim-to-Real Gap Exploitation](WM-06-sim-to-real-gap.md) — also targets world state
- [WM-09: Model Extraction](WM-09-model-extraction.md) — also targets world state

## Citation

Argyrakos, S. (2026). MYNDRA-LWM: WM-02 Latent Poisoning.
MYNDRA Framework. https://spyrosarg.github.io/myndra-lwm/
