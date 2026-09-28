# Attention and Input Structure

## What It Is

Transformer models use attention to weigh the relevance of different parts
of the input when generating each token. The structure of the input — how
it is segmented, labeled, and ordered — affects how attention is distributed.
Attention as a mechanism for weighting input relevance is introduced in
[Vaswani et al., 2017](https://proceedings.neurips.cc/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html).

Clear structure does not "add information." It makes existing information
easier for the model to locate and use. For a practical discussion of how
input structure affects long-context performance, see
[Liu et al., 2023](https://arxiv.org/abs/2307.03172).

## What It Explains

- **Structured prompting**: separating Role, Context, Task, and Format
  reduces ambiguity by making each part easier to attend to
- **Output constraints**: explicit format instructions create clear
  attention targets for format-related tokens
- **Long context degradation**: as input grows, attention spreads thinner,
  and structure becomes more important for maintaining focus

## Why It Matters for Engineering

- Structure is not decoration. It is a mechanism for controlling where
  the model directs its attention.
- In long prompts, repeating key constraints near the end can help,
  because attention to early tokens may weaken.
- Removing irrelevant content is often more effective than adding
  clarifying content, because irrelevant tokens compete for attention.

## Reference

Vaswani, A., Shazeer, N., Parmar, N., et al. (2017). Attention Is All You Need. *Advances in Neural Information Processing Systems*, 30, 5998–6008.

## Related Methodology

- [Structured Prompting](../methodology/structured-prompting.md)
- [Output Constraints](../methodology/output-constraints.md)