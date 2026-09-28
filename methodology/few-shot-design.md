# Few-Shot Design

## Pattern

Provide 2–5 examples of input → output before the actual task.

## Logical Structure

See [structured prompting](structured-prompting.md) for the base structure.

- **Role**: who the model should act as
- **Task**: what needs to be done
- **Examples**: 2–5 input → output pairs
- **Format**: expected output structure
- **Input**: the actual input to process

## Example (Logical Structure)

Role: You are an information extractor.
Task: Extract intent and target device from a user message.
Examples:
  "Turn on the living room light." → {intent: control_device, target: light}
  "What time is it now?" → {intent: query_info, target: null}
  "Remind me to take medicine tomorrow." → {intent: set_reminder, target: null}
Format: Return a JSON object.
Input: "Set the air conditioner to 26 degrees."

## Example (Actual API Call)

system:
You are an information extractor. Extract intent and target device from a user message.
Return a JSON object with fields: intent, target.

user:
Examples:
  "Turn on the living room light." → {"intent": "control_device", "target": "light"}
  "What time is it now?" → {"intent": "query_info", "target": null}
  "Remind me to take medicine tomorrow." → {"intent": "set_reminder", "target": null}

Input: "Set the air conditioner to 26 degrees."

## Why It Works

In-context pattern matching: the model identifies statistical patterns from the
examples and applies them to the new input. The examples act as anchors for
output style and structure.

## When to Use

Classification, extraction, formatting tasks where zero-shot output is inconsistent.

## Related Principles

- [In-Context Pattern Matching](../principles/in-context-pattern-matching.md)