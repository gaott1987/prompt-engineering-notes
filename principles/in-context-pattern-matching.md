# In-Context Pattern Matching

## What It Is

Large language models are trained to predict the next token based on the
preceding context. When you provide examples in the prompt, the model does
not "learn" from them in the traditional sense. Instead, it identifies
statistical patterns in the examples and applies them to the new input.
This behavior was systematically demonstrated in
[Brown et al., 2020](https://proceedings.neurips.cc/paper/2020/hash/1457c0d6bfcb4967418bfb8ac142f64a-Abstract.html),
which showed that GPT-3 could perform tasks from examples alone, without
gradient updates.

This is often called **in-context learning**, but the mechanism is closer to
pattern matching than learning: the model recognizes "this looks like the
examples I was just given" and continues in the same style.

## What It Explains

- **Few-shot design**: examples anchor the output format and style
- **Structured prompting**: section labels act as patterns the model can follow
- **Consistency**: repeated patterns in the prompt lead to more consistent output

## Why It Matters for Engineering

- Examples are not "training data" — they are anchors. More examples do not
  always mean better results; the most representative examples matter more.
- Example order can affect output. The last example often has the strongest
  influence, so put the most representative one last.
- If the model's output drifts, adding or reordering examples is often more
  effective than adding more instructions.

## Reference

Brown, T., Mann, B., Ryder, N., et al. (2020). Language Models are Few-Shot Learners. *Advances in Neural Information Processing Systems*, 33, 1877–1901.

## Related Methodology

- [Few-Shot Design](../methodology/few-shot-design.md)
- [Structured Prompting](../methodology/structured-prompting.md)