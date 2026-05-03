# WM-06: Sim-to-Real Gap Exploitation

**Component:** World state
**Severity:** High
**Likelihood:** High | **Impact:** High | **Detectability:** Medium | **Mitigation effort:** High

## Definition

Every world model system is trained on a finite distribution of experiences that cannot perfectly represent every possible deployment condition. The gap between what the model has learned and what it encounters in deployment is not a bug but an unavoidable property of generalization. Sim-to-Real Gap Exploitation deliberately targets this gap, constructing physical or operational conditions that fall outside the training distribution, causing the model to apply incorrect learned dynamics to genuinely novel situations. The attack requires no access to the model's parameters, only knowledge of the training distribution's boundaries.

## Attack vector

1. **Characterize the training distribution.** Through behavioral probing, operational documentation, or domain knowledge, estimate the boundaries of the training distribution, the conditions under which the model was trained.

2. **Identify out-of-distribution targets.** Find configurations that are physically realizable in the deployment environment but absent or underrepresented in the training distribution.

3. **Construct adversarial conditions.** Engineer environmental conditions or operational scenarios that fall in the identified out-of-distribution region. These conditions may be physically mundane; the gap is in the model's experience, not the physics.

4. **Exploit model behavior at the boundary.** The world model, lacking calibrated uncertainty in this region, applies learned dynamics inappropriately. Monitor for exploitable behavioral failures at the distribution boundary.

## Real-world examples

- Physical configurations or environmental conditions realizable in the real world but systematically absent from the training environment due to simulator limitations.

- Operational scenarios that appear within the nominal operating envelope but combine sub-conditions in ways never seen during training, causing transition model extrapolation failures.

- Adversarial domain shifts that move the deployment environment subtly but systematically outside the training distribution without triggering explicit out-of-distribution detectors.

## Detection

- **Online out-of-distribution detection.** Deploy a lightweight OOD detector that monitors whether current observations fall within the training distribution. Flag high-uncertainty regions for conservative fallback behavior.

- **Epistemic uncertainty quantification.** Use Bayesian or ensemble methods that explicitly represent epistemic uncertainty. High epistemic uncertainty at a state signals potential sim-to-real gap exploitation.

- **Deployment domain monitoring.** Continuously characterize the statistical properties of the deployment environment and alert when significant distributional shift is detected relative to training data statistics.

## Mitigation

- **Domain randomization in training.** Train across a deliberately widened
