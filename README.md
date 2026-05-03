# MYNDRA-LWM

**Large World Model Security Taxonomy**

An open practitioner framework for security risks in
autonomous AI systems that build and act on internal
models of reality. Organized around the five cognitive
components that all world model systems share.

Built by observing how AI agents fail in adversarial
scenarios at [Agents Battlefield](https://agentsbattlefield.com),
and grounded in world model cognitive architecture theory.

## Live taxonomy

[spyrosarg.github.io/myndra-lwm](https://spyrosarg.github.io/myndra-lwm/)

## The ten attack categories

| ID | Name | Component | Severity |
|---|---|---|---|
| [WM-01](taxonomy/WM-01-perception-attack.md) | Perception Attack | Perception | Critical |
| [WM-02](taxonomy/WM-02-latent-poisoning.md) | Latent Poisoning | World state | Critical |
| [WM-03](taxonomy/WM-03-transition-attack.md) | Transition Attack | Prediction | High |
| [WM-04](taxonomy/WM-04-planning-attack.md) | Planning Attack | Planning | Critical |
| [WM-05](taxonomy/WM-05-reward-hijack.md) | Reward Hijack | Action | Critical |
| [WM-06](taxonomy/WM-06-sim-to-real-gap.md) | Sim-to-Real Gap Exploitation | World state | High |
| [WM-07](taxonomy/WM-07-belief-corruption.md) | Belief Corruption | Prediction | High |
| [WM-08](taxonomy/WM-08-surprise-bypass.md) | Surprise Bypass | Perception | Critical |
| [WM-09](taxonomy/WM-09-model-extraction.md) | Model Extraction | World state | Medium |
| [WM-10](taxonomy/WM-10-collapse-attack.md) | Collapse Attack | Planning | Critical |

## The five cognitive components

Every world model system shares this cognitive structure.
MYNDRA-LWM organizes attacks by which component they target.
Perception → World state → Prediction → Planning → Action

Each component is a distinct attack surface with distinct
failure modes. An attack on any single component propagates
through the entire system.

## Who it is for

Security engineers, red teams, and system designers working
on autonomous vehicles, robotic systems, spacecraft, and AI
agents with persistent world state.

## How to use it

**Threat modeling:** Walk the five-component architecture
against your system. Every exposed component maps to
specific WM entries with detection and mitigation guidance.

**Red teaming:** Each entry's attack vector provides a
concrete test methodology. The detection section tells you
what signals should have fired during testing but did not.

**Secure design:** Consult mitigation sections before
deployment. Many mitigations are architectural decisions
significantly cheaper at design time than as retrofits.

## Scope

Covers decision-coupled world model systems where the world
model drives autonomous action in the real world. Generative
video models used solely for human consumption are outside
scope.

## Read the paper

The full academic paper is available in the
[paper/](paper/) folder.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to propose
new attack categories, corrections, and real-world examples.

## Cite this work
Argyrakos, S. (2026). MYNDRA-LWM: A Practitioner Taxonomy
of Security Risks in Large World Model Systems. v1.0.
https://spyrosarg.github.io/myndra-lwm/

## License

MIT License. Free to use, cite, extend, and adapt.

---

*By Spyros Argyrakos*

*[myndra.gr](https://spyrosarg.github.io/myndra-framework-website/) ·
[Agents Battlefield](https://agentsbattlefield.com)*
