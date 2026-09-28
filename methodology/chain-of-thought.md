# Chain-of-Thought (CoT)

## Pattern

Ask the model to reason step by step before giving the final answer.

## Variants

- **Zero-shot CoT**: append "Let's think step by step" without examples.
- **Few-shot CoT**: provide one or more worked examples before the target question.
- **Structured CoT**: provide an explicit reasoning template (e.g., step 1 / step 2 / step 3).

## Logical Structure

See [structured prompting](structured-prompting.md) for the base structure.

- **Role**: who the model should act as
- **Task**: what needs to be decided
- **Steps**: the reasoning steps to follow
- **Format**: how to present the final answer
- **Input**: the actual input

## Example (Logical Structure)

This example uses **structured CoT** (explicit reasoning steps).

Role: You are a decision assistant.
Task: Decide whether a user message requires device control.
Steps:
  1. Does the message mention a device?
  2. Does it express an action to perform?
  3. Is the action a control command?
Format: Give the final answer as yes or no.
Input: "Set the air conditioner to 26 degrees."

## Example (Actual API Call)

### Zero-shot CoT

system:
You are a decision assistant.

user:
Set the air conditioner to 26 degrees.
Let's think step by step.

### Few-shot CoT

system:
You are a decision assistant.

user:
Example: "Turn on the living room light." → yes, it requires device control.
Now: "Set the air conditioner to 26 degrees."
Let's think step by step.

### Structured CoT

system:
You are a decision assistant. Think step by step:
  1. Does the message mention a device?
  2. Does it express an action to perform?
  3. Is the action a control command?
Then give the final answer as yes or no.

user:
Set the air conditioner to 26 degrees.

## Why It Works

Autoregressive conditioning: each generated token becomes a condition for the next.
Intermediate reasoning steps provide stronger conditioning for the final answer,
reducing the chance of jumping to a wrong conclusion. This effect was
demonstrated in
[Wei et al., 2022](https://proceedings.neurips.cc/paper/2022/hash/9d5609613524ecf4f15af0f7b31abca4-Abstract-Conference.html),
which showed that eliciting intermediate reasoning steps significantly improves
performance on arithmetic, commonsense, and symbolic reasoning tasks.

## When to Use

Multi-step reasoning, math, logic, or any task where the model tends to jump to conclusions.

## When Not to Use

Simple extraction or formatting tasks — CoT adds latency without improving accuracy.

## Related Principles

- [Autoregressive Conditioning](../principles/autoregressive-conditioning.md)

## Related Methodology

- [Few-Shot Design](few-shot-design.md) — few-shot CoT combines examples with step-by-step reasoning
- [ReAct](react.md) — extends CoT by interleaving reasoning with external actions