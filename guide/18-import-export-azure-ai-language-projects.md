[Previous](./17-entity-linking-wikipedia-links-from-text.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./19-foundry-scope-model-access-for-multiple-apis.md)

# 18. Import/Export Azure AI Language Projects

Use import/export to:
- **Back up** custom projects
- **Clone** projects across resources/regions (for failover or environment promotion)
- **Recover** projects after disaster scenarios

Commonly used for:
- Custom text classification projects
- Custom named entity recognition (Custom NER) projects

Export project assets (REST)
```http
POST {ENDPOINT}/language/authoring/analyze-text/projects/{PROJECT-NAME}/:export?stringIndexType=Utf16CodeUnit&api-version={API-VERSION}
Ocp-Apim-Subscription-Key: {RESOURCE-KEY}
Content-Type: application/json

{
  "assetsToExport": ["*"]
}
```

Import project assets (REST)
```http
POST {ENDPOINT}/language/authoring/analyze-text/projects/{PROJECT-NAME}/:import?api-version={API-VERSION}
Ocp-Apim-Subscription-Key: {RESOURCE-KEY}
Content-Type: application/json

{ /* paste the exported assets JSON here */ }
```

Notes
- These operations are **async**: capture the `operation-location` header, poll job status, then download/export results and feed them into import.

Docs:
- Custom text classification backup/restore: https://learn.microsoft.com/azure/ai-services/language-service/custom-text-classification/fail-over
- Custom NER backup/restore: https://learn.microsoft.com/azure/ai-services/language-service/custom-named-entity-recognition/fail-over

---

[Previous](./17-entity-linking-wikipedia-links-from-text.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./19-foundry-scope-model-access-for-multiple-apis.md)

