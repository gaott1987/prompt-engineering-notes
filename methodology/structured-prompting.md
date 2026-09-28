# Structured Prompting

## Pattern

Break a prompt into explicit logical sections so each part has a clear role.

## Logical Structure

- **Role**: who the model should act as
- **Context**: background information
- **Task**: what needs to be done
- **Format**: expected output structure
- **Constraints**: what to avoid, edge cases

## Example (Logical Structure)

Role: You are an intent classifier.
Context: The user is interacting with a smart home assistant.
Task: Classify the message into one of: control_device, query_info, set_reminder, unknown.
Format: Return only the label.
Constraints: If unclear, return "unknown".
Input: "Turn on the living room light."

## Example (Actual API Call)

system:
You are an intent classifier for a smart home assistant.
Classify the user's message into one of: control_device, query_info, set_reminder, unknown.
Return only the label. If unclear, return "unknown".

user:
Turn on the living room light.

## Why It Works

Clear section boundaries reduce ambiguity. The model does not need the labels
themselves; it needs the semantic separation they represent. Structured prompting
makes that separation explicit during design, then natural language carries it
during execution.

## When to Use

Any task where output format matters, or where the model needs domain context.

## Related Principles

- [Attention and Input Structure](../principles/attention-and-input-structure.md)