# ReAct

## Pattern

Interleave reasoning steps with external actions. The model generates a
thought, takes an action, observes the result, and continues until it
reaches a final answer.

## Logical Structure

See [structured prompting](structured-prompting.md) for the base structure.

- **Role**: who the model should act as
- **Task**: what needs to be solved
- **Format**: Thought → Action → Observation → Final Answer
- **Tools**: what actions are available
- **Input**: the actual question

## Example (Logical Structure)

Role: You are a research assistant.
Task: Answer the question using available tools.
Format:
  Thought: ...
  Action: search[...]
  Observation: ...
  Final Answer: ...
Tools: search, calculate
Input: "Who wrote the paper that introduced ReAct?"

## Example (Actual API Call)

system:
You are a research assistant. Answer the question using available tools.
Use the format:
  Thought: ...
  Action: search[...]
  Observation: ...
  Final Answer: ...
Available tools: search, calculate

user:
Who wrote the paper that introduced ReAct?

## Why It Works

ReAct combines two mechanisms:
- **Chain-of-Thought**: reasoning steps condition the next step
- **Tool use**: external actions bring in information the model does not have

The interleaving means the model can correct its reasoning based on real
observations, rather than relying solely on its internal knowledge. This
was introduced in
[Yao et al., 2022](https://arxiv.org/abs/2210.03629).

## When to Use

Tasks that require external information, multi-step tool use, or dynamic
decision-making (e.g., agents, retrieval-augmented generation).

## When Not to Use

Tasks that can be solved with the model's internal knowledge alone — ReAct
adds latency and complexity without benefit.

## Related Principles

- [Autoregressive Conditioning](../principles/autoregressive-conditioning.md)
- [In-Context Pattern Matching](../principles/in-context-pattern-matching.md)

## Related Methodology

- [Chain-of-Thought](chain-of-thought.md) — ReAct extends CoT with external actions