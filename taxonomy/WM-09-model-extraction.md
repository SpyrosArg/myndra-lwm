# WM-09: Model Extraction

**Component:** World state
**Severity:** Medium
**Likelihood:** High | **Impact:** Medium | **Detectability:** Medium | **Mitigation effort:** Low

## Definition

The internal structure of a world model, its learned causal dynamics, latent geometry, and physical priors, represents significant intellectual and strategic value. A Model Extraction attack systematically recovers this internal structure through carefully crafted query sequences, without requiring direct access to model parameters. By observing how the system responds to designed inputs, an attacker can reconstruct a surrogate model that approximates the original's behavior. This surrogate enables more effective white-box attacks against the original, competitive intelligence gathering, and circumvention of access controls on proprietary model capabilities. The attack is notable for being difficult to distinguish from legitimate system probing or testing.

## Attack vector

1. **Design extraction query strategy.** Develop a systematic query strategy that maximally reveals internal model structure. For world models, this includes queries targeting latent space geometry, transition dynamics, and uncertainty estimates.

2. **Execute query campaign.** Submit crafted queries to the target system and collect behavioral outputs. Adapt the query strategy based on accumulated responses to maximize information extraction efficiency.

3. **Train surrogate model.** Use collected input-output pairs to train a surrogate world model that approximates the original's behavior. Evaluate surrogate fidelity on held-out test inputs.

4. **Exploit or transfer the surrogate.** Use the extracted surrogate to plan more effective attacks against the original, generate transferable adversarial examples, or directly apply the extracted knowledge.

## Real-world examples

- API-based extraction of world model transition dynamics through systematic state-action pair queries, enabling reconstruction of the model's causal structure.

- Latent space geometry recovery through observation of encoding behavior under crafted inputs, revealing the internal representation structure without parameter access.

- Surrogate model construction that enables white-box adversarial attacks against a target system that only exposes a black-box API.

## Detection

- **Query pattern analysis.** Monitor query patterns for systematic characteristics, structured coverage of the input space, progressive refinement, or correlations between queries suggesting extraction intent rather than operational use.

- **Rate limiting and access controls.** Implement per-user query rate limits and access controls that bound the information an adversary can extract within a given time window. Log all queries for forensic analysis.

## Mitigation

- **Differential privacy in inference.** Apply differential privacy to model outputs, providing formal guarantees on the amount of information about the training data and internal parameters that can be extracted through any query strategy.

- **Output perturbation with utility preservation.** Implement carefully designed output perturbation schemes that degrade extraction quality while preserving task-relevant accuracy. Structure the perturbation to be maximally harmful to surrogate training.

- **Watermarking.** Embed detectable watermarks in model behavior that allow attribution of extracted surrogates back to the source model, enabling legal action and providing deterrence against extraction.

## Related entries

- [WM-02: Latent Poisoning](WM-02-latent-poisoning.md) — also targets world state
- [WM-06: Sim-to-Real Gap Exploitation](WM-06-sim-to-real-gap.md) — also targets world state
- [WM-01: Perception Attack](WM-01-perception-attack.md) — extracted surrogate enables better perception attacks

## Citation

Argyrakos, S. (2026). MYNDRA-LWM: WM-09 Model Extraction.
MYNDRA Framework. https://spyrosarg.github.io/myndra-lwm/
