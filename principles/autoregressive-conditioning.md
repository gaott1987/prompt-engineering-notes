# Autoregressive Conditioning

## What It Is

Large language models generate text one token at a time. Each generated token
becomes part of the context for predicting the next token. This means the
model's earlier output directly conditions its later output. The underlying
architecture is the Transformer, introduced in
[Vaswani et al., 2017](https://proceedings.neurips.cc/paper/2017/hash/3f5ee243547dee91fbd053c1c4a845aa-Abstract.html).

If the model starts generating a reasoning chain, each step makes the next
step more likely. If it jumps straight to an answer, that answer conditions
everything after it. This effect is closely related to the reasoning
improvements shown in
[Wei et al., 2022](https://proceedings.neurips.cc/paper/2022/hash/9d5609613524ecf4f15af0f7b31abca4-Abstract-Conference.html).

## What It Explains

- **Chain-of-Thought**: intermediate reasoning steps provide stronger
  conditioning for the final answer
- **Output constraints**: early format tokens bias the rest of the output
  toward that format
- **Failure modes**: once a model starts down a wrong path, it tends to
  continue that path

## Why It Matters for Engineering

- If a task requires multi-step reasoning, asking for steps first is not
  just "helping the model think" — it is shaping the conditional
  distribution of the final answer.
- If output format matters, front-load the format constraint. The first
  few tokens set the pattern.
- If the model makes an early mistake, retrying from scratch is often
  better than asking it to "fix" the error, because the error is already
  conditioning the context.

## Reference

Vaswani, A., Shazeer, N., Parmar, N., et al. (2017). Attention Is All You Need. *Advances in Neural Information Processing Systems*, 30, 5998–6008.

## Related Methodology

- [Chain-of-Thought](../methodology/chain-of-thought.md)
- [Output Constraints](../methodology/output-constraints.md)