# Architecture Notes

## From Messages to Model Input

When you call a Chat Completions API, you send an array of messages with `role` and `content`. But what the model actually receives is a single token sequence, assembled by the server using special markers. This assembly process is handled by a **chat template**.

```
User-authored messages array
        │
        ▼
┌─────────────────────────────────────────┐
│  Server-side processing layer            │
│  · Concatenate messages per vendor rules │
│  · Insert special markers (role/message  │
│    boundaries)                           │
│  · Apply chat template                   │
└─────────────────────────────────────────┘
        │
        ▼
Model input: a token sequence with special markers
        │
        ▼
Model internals (attention, probability prediction, ...)
```

A **chat template** is the fixed format a model was trained on. When the server receives messages, it converts each message's role and content into the format the model recognizes, then feeds it to the model for inference.

## System Handling Across Vendors

Different vendors handle system messages differently at the API level. Below is a comparison of mainstream vendors.

| Vendor | System Handling | Field Location | Reference |
| :--- | :--- | :--- | :--- |
| **OpenAI** | `role: "system"` (newer models also support `role: "developer"`) | Inside messages array | [OpenAI API Reference](https://platform.openai.com/docs/api-reference/chat) |
| **DeepSeek** | `role: "system"` | Inside messages array | [DeepSeek API Docs](https://api-docs.deepseek.com/) |
| **Zhipu GLM** | `role: "system"` | Inside messages array | [Zhipu AI API Docs](https://open.bigmodel.cn/dev/api) |
| **Alibaba Qwen** | `role: "system"` | Inside messages array | No direct reference |
| **Kimi (OpenAI-compatible)** | `role: "system"` | Inside messages array | [Moonshot AI API Docs](https://platform.moonshot.cn/docs) |
| **Kimi (Anthropic-compatible)** | Top-level `system` parameter | Outside messages array | [Moonshot AI API Docs](https://platform.moonshot.cn/docs) |
| **Anthropic** | Top-level `system` parameter | Outside messages array | [Anthropic API Docs](https://docs.anthropic.com/en/api/messages) |
| **Google Gemini** | `systemInstruction` | Separate field | [Google AI API Docs](https://ai.google.dev/api/generate-content) |

## Engineering Takeaway

Most mainstream Chinese APIs (DeepSeek, GLM, Qwen) follow OpenAI's `role: "system"` convention. This means: **if you write code using the OpenAI-compatible format, a single system-handling logic can adapt to most Chinese vendors.**

The ones that genuinely require branching are Anthropic (top-level `system`), Google (`systemInstruction`), and Kimi's Anthropic-compatible endpoint.

This is why frameworks like LangChain and Dify default to the OpenAI format as their "universal interface" — at the system-handling layer, the OpenAI convention has effectively become the industry standard.

## Relationship to Prompt Engineering

In pure text generation scenarios, prompt engineering mainly revolves around `role` and `content`. You design the system message content (role, rules, output format) and the user message content (task, examples, input), and the server assembles them into a format the model can understand.

When you use `tools` and `response_format`, these fields also participate in prompt design: `tools` defines the schema of tools the model can call, and `response_format` constrains the structure of the output. They are complementary to textual instructions in `content` — different mechanisms, same goal.

## From Logical Structure to Actual API Call

Prompt engineering methodologies often describe prompts using logical labels:
Role, Context, Task, Format, Constraints. These labels are **design tools for humans**,
not part of the actual API payload.

When you call an API, the content is written as natural language, and split across
`system` and `user` messages based on whether it configures model behavior (system)
or varies per request (user).

### Mapping

| Logical Component | Where It Goes | Why |
| :--- | :--- | :--- |
| Role | system | Configures model behavior, stable across requests |
| Format | system | Output constraint, stable across requests |
| Constraints | system | Behavioral rule, stable across requests |
| Context (static) | system | Fixed background the model must know |
| Task | user | Varies per request |
| Input | user | Varies per request |
| Context (dynamic) | user | Retrieved or per-request information |

### Example

Logical structure:
  Role: You are an intent classifier.
  Context: The user is interacting with a smart home assistant.
  Task: Classify the message.
  Format: Return only the label.
  Constraints: If unclear, return "unknown".
  Input: "帮我开灯"

Actual API call:
  system: You are an intent classifier for a smart home assistant.
          Classify the user's message into one of: control_device,
          query_info, set_reminder, unknown. Return only the label.
          If unclear, return "unknown".
  user: 帮我开灯