[Previous](./08-confidence-scoring-short.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./10-token-calculation-max-token-behavior.md)

# 9. [Azure AI Language (Question Answering)](https://learn.microsoft.com/azure/ai-services/language-service/question-answering/overview)

Query KB (REST): https://learn.microsoft.com/azure/ai-services/language-service/question-answering/how-to/query-knowledge-base
```
POST https://<resource>.cognitiveservices.azure.com/language/:query-knowledgebases?projectName=<project>&deploymentName=production&api-version=2021-10-01
Headers:
  Ocp-Apim-Subscription-Key: <your-resource-key>
Body:
{
  "question": "How do I reset my password?",
  "top": 3,
  "confidenceScoreThreshold": 0.7,
  "includeUnstructuredSources": true
}
```
Response includes answers with `confidenceScore`, `source`, and metadata.

---

[Previous](./08-confidence-scoring-short.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./10-token-calculation-max-token-behavior.md)

