[Previous](./12-text-image-processing-methods-rest.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./14-ssml-for-speech-styles-example.md)

# 13. [Semantic Kernel — Prompt Template Formats](https://learn.microsoft.com/semantic-kernel/prompts/)

Supported prompt formats:
- Plain text `.txt`  
- Markdown `.md`  
- JSON `.json` (structured prompt config)  
- YAML `.yaml` / `.yml`

Example JSON prompt config:
```json
{
  "name": "Summarize",
  "template": "Summarize: {{$input}}",
  "input_variables": { "input": { "description":"Text to summarize" } },
  "execution_settings": { "max_tokens":100, "temperature":0.7 }
}
```

Reference: https://learn.microsoft.com/semantic-kernel/prompts/prompt-template-syntax

---

[Previous](./12-text-image-processing-methods-rest.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./14-ssml-for-speech-styles-example.md)

