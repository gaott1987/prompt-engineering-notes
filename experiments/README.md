# Experiments

Each experiment validates one methodology, using a task as the carrier.

| # | Experiment | Methodology | Task | Variable |
| :--- | :--- | :--- | :--- | :--- |
| 01 | [01-structured-prompting.md](01-structured-prompting.md) | [structured-prompting.md](../methodology/structured-prompting.md) | Intent Classification | With vs without structured prompt |
| 02 | [02-few-shot-design.md](02-few-shot-design.md) | [few-shot-design.md](../methodology/few-shot-design.md) | Intent Classification | Number of examples: 0 / 2 / 5 |
| 03 | [03-output-constraints.md](03-output-constraints.md) | [output-constraints.md](../methodology/output-constraints.md) | Information Extraction | Constraint strength: none / natural language / JSON Schema / JSON mode |
| 04 | [04-chain-of-thought.md](04-chain-of-thought.md) | [chain-of-thought.md](../methodology/chain-of-thought.md) | GSM8K | CoT variants: direct / zero_cot / cot / react |

## Related

- [Methodology](../methodology/README.md) — the patterns being tested
- [Principles](../principles/README.md) — why these patterns work