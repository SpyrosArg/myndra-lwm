# MYNDRA-LWM

**Large World Model Security Taxonomy**

The first open practitioner framework for security 
risks in autonomous AI systems that build and act 
on internal models of reality.

## What it covers

MYNDRA-LWM defines 10 attack categories organized 
around the five cognitive components that all world 
model systems share: perception, world state, 
prediction, planning, and action.

| ID | Attack | Component | Severity |
|---|---|---|---|
| WM-01 | Perception Attack | Perception | Critical |
| WM-02 | Latent Poisoning | World state | Critical |
| WM-03 | Transition Attack | Prediction | High |
| WM-04 | Planning Attack | Planning | Critical |
| WM-05 | Reward Hijack | Action | Critical |
| WM-06 | Sim-to-Real Gap Exploitation | World state | High |
| WM-07 | Belief Corruption | Prediction | High |
| WM-08 | Surprise Bypass | Perception | Critical |
| WM-09 | Model Extraction | World state | Medium |
| WM-10 | Collapse Attack | Planning | Critical |

## Who it is for

Security engineers, red teams, and system designers 
working on autonomous vehicles, robotic systems, 
spacecraft, and AI agents with persistent world state.

## How to use it

**Threat modeling:** Walk the five-component 
architecture. Every exposed component maps to 
specific WM entries.

**Red teaming:** Use each entry's attack vector 
as a test methodology. Use the detection section 
to verify what monitoring should have fired.

**Secure design:** Consult mitigation sections 
before deployment. Many mitigations are 
architectural decisions cheapest at design time.

## Scope

Covers decision-coupled world model systems where 
the world model drives autonomous action in the 
real world. Does not cover generative video models 
used solely for human consumption.

## Live framework

[spyrosarg.github.io/myndra-lwm](https://spyrosarg.github.io/myndra-lwm)

## Cite this work
Argyrakos, S. (2026). MYNDRA-LWM: A Practitioner
Taxonomy of Security Risks in Large World Model
Systems. v1.0.
https://spyrosarg.github.io/myndra-lwm/


## License

MIT License. Free to use, cite, extend, and adapt.

---

*By Spyros Argyrakos*
