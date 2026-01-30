[Previous](./02-control-plane-rest-api-calls.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./04-multi-language-support-for-audio-and-video.md)

# 3. [Content Filtering and Message Flagging](https://learn.microsoft.com/azure/ai-services/openai/concepts/content-filter)

- Configure content filters via the Azure OpenAI resource (portal): set severity thresholds per category (Hate, Sexual, Violence, Self-Harm). How-to: https://learn.microsoft.com/azure/ai-services/openai/how-to/content-filters  
- Use the [Content Safety API](https://learn.microsoft.com/azure/ai-services/content-safety/quickstart-text) to pre-check or post-check text. API returns category severities and suggested actions.

Example (Content Safety REST):
```
POST https://<resource>.cognitiveservices.azure.com/contentsafety/text:analyze?api-version=2023-10-01
Headers:
  Ocp-Apim-Subscription-Key: <your-resource-key>
Body:
{
  "text": "User input text to analyze"
}
```

Handle blocked/filtered content in app logic (reject, sanitize, escalate).

---

[Previous](./02-control-plane-rest-api-calls.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./04-multi-language-support-for-audio-and-video.md)

