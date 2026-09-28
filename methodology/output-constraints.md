# Output Constraints

## Pattern

Constrain the model's output to a strict format so it can be parsed programmatically.

## Logical Structure

See [structured prompting](structured-prompting.md) for the base structure.

- **Role**: who the model should act as
- **Task**: what needs to be done
- **Format**: exact schema of the output
- **Constraints**: rules for edge cases
- **Input**: the actual input

## Example (Logical Structure)

Role: You are a structured data extractor.
Task: Extract intent, target, and value from a user message.
Format: Return a JSON object with fields: intent (string), target (string or null), value (number or null).
Constraints: Do not include any other text. If a field is not present, return null.
Input: "Set the air conditioner to 26 degrees."

## Example (Actual API Call)

system:
You are a structured data extractor. Extract intent, target, and value from a user message.
Return a JSON object with fields: intent (string), target (string or null), value (number or null).
Do not include any other text. If a field is not present, return null.

user:
Set the air conditioner to 26 degrees.

## Why It Works

Token-level format anchoring: explicit format instructions bias the model toward
generating tokens that fit the expected structure. Combined with API-level JSON mode,
this makes output reliably parseable.

## When to Use

Any time the output feeds into code, not a human reader.

## Related Principles

- [Attention and Input Structure](../principles/attention-and-input-structure.md)