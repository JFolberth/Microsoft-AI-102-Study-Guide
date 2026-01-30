[Previous](./16-quick-reference-tables.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./18-import-export-azure-ai-language-projects.md)

# 17. [Entity Linking (Wikipedia links from text)](https://learn.microsoft.com/azure/ai-services/language-service/entity-linking/overview)

Goal: enrich extracted/ingested text with **Wikipedia-backed entity links**.

How it works
- Entity Linking disambiguates entities (for example, "Mars" the planet vs "Mars" the Roman god) and returns:
  - Entity name
  - Data source (Wikipedia)
  - URL (Wikipedia article)
  - Match spans + confidence

Important
- Entity Linking in Azure AI Language is scheduled to retire effective **September 1, 2028**.

Docs:
- Overview: https://learn.microsoft.com/azure/ai-services/language-service/entity-linking/overview
- How-to (API): https://learn.microsoft.com/azure/ai-services/language-service/entity-linking/how-to/call-api
- Quickstart (C#): https://learn.microsoft.com/azure/ai-services/language-service/entity-linking/quickstart?pivots=programming-language-csharp

C# (.NET SDK) example
```csharp
using Azure;
using Azure.AI.TextAnalytics;
using System;

// Requires env vars: LANGUAGE_KEY and LANGUAGE_ENDPOINT
string languageKey = Environment.GetEnvironmentVariable("LANGUAGE_KEY");
string languageEndpoint = Environment.GetEnvironmentVariable("LANGUAGE_ENDPOINT");

var client = new TextAnalyticsClient(
    new Uri(languageEndpoint),
    new AzureKeyCredential(languageKey));

var response = client.RecognizeLinkedEntities(
    "Microsoft was founded by Bill Gates and Paul Allen on April 4, 1975.");

foreach (var entity in response.Value)
{
    Console.WriteLine($"{entity.Name} → {entity.Url} (source: {entity.DataSource})");
}
```

---

[Previous](./16-quick-reference-tables.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./18-import-export-azure-ai-language-projects.md)

