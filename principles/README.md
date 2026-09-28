# Principles

These notes explain **why** prompt engineering methods work, at the level of model behavior.

## Files

| Principle | Explains | Core Reference |
| :--- | :--- | :--- |
| [In-Context Pattern Matching](in-context-pattern-matching.md) | Few-shot, structured prompting | [Brown et al., 2020](https://proceedings.neurips.cc/paper/2020/hash/1457c0d6bfcb4967418bfb8ac142f64a-Abstract.html) |
| [Autoregressive Conditioning](autoregressive-conditioning.md) | Chain-of-Thought, output constraints | [Vaswani et al., 2017](https://proceedings.neurips.cc/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html) |
| [Attention and Input Structure](attention-and-input-structure.md) | Structured prompting, output constraints | [Vaswani et al., 2017](https://proceedings.neurips.cc/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html) |

## How They Relate

These principles are not mutually exclusive. They describe the same underlying process from different angles:

- **In-Context Pattern Matching** focuses on what the model *extracts* from the prompt.
- **Autoregressive Conditioning** focuses on how the model *builds* its output token by token.
- **Attention and Input Structure** focuses on how the model *distributes focus* across the input.

Together, they explain why a well-designed prompt works — and why a poorly designed one fails.