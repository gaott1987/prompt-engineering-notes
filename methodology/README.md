# Methodology

Prompt engineering patterns I use regularly, with rationale.

All methodology files share a common base structure (Role / Context / Task / Format / Constraints), defined in [structured-prompting.md](structured-prompting.md). Each method adds its own sections such as Examples, Steps, or Tools as needed.

| File | Pattern |
| :--- | :--- |
| [structured-prompting.md](structured-prompting.md) | Break a prompt into explicit logical sections |
| [few-shot-design.md](few-shot-design.md) | Provide input-output examples to anchor output |
| [output-constraints.md](output-constraints.md) | Constrain output format for programmatic parsing |
| [chain-of-thought.md](chain-of-thought.md) | Elicit step-by-step reasoning before the final answer |
| [react.md](react.md) | Interleave reasoning with external actions |

## Related

- [Principles](../principles/README.md) — why these patterns work
- [Experiments](../experiments/README.md) — how these patterns perform in practice