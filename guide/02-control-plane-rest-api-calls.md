[Previous](./01-file-types-and-size-limitations.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./03-content-filtering-and-message-flagging.md)

# 2. [Control Plane - REST API Calls](https://learn.microsoft.com/azure/ai-services/reference/rest-api-resources)

### API key note
- Header `[Ocp-Apim-Subscription-Key](https://learn.microsoft.com/azure/ai-services/authentication)` (or `api-key` for OpenAI endpoints) = your Cognitive Services resource Key1 / Key2 (Azure Portal → Resource → Keys and Endpoint). Not the Azure subscription ID.

Auth docs: https://learn.microsoft.com/azure/ai-services/authentication

### Common REST Endpoint structure
```
https://<resource-name>.cognitiveservices.azure.com/<service>/<version>/<operation>
```

### [Document Intelligence — Analyze (REST example)](https://learn.microsoft.com/azure/ai-services/document-intelligence/how-to-guides/use-sdk-rest-api)
POST prebuilt-invoice analyze:
```
POST https://<resource>.cognitiveservices.azure.com/formrecognizer/documentModels/prebuilt-invoice:analyze?api-version=2023-07-31
Headers:
  Content-Type: application/json
  Ocp-Apim-Subscription-Key: <your-resource-key>

Body:
{
  "urlSource": "https://example.com/invoice.pdf"
}
```
Response includes `analyzeResult` → `documents` → `fields` with `confidence` values.

C# (.NET SDK)
```csharp
using Azure;
using Azure.AI.FormRecognizer.DocumentAnalysis;

var client = new DocumentAnalysisClient(
    new Uri("https://<resource>.cognitiveservices.azure.com/"),
    new AzureKeyCredential("<your-resource-key>"));

var operation = await client.AnalyzeDocumentFromUriAsync(
    WaitUntil.Completed, "prebuilt-invoice", new Uri("https://example.com/invoice.pdf"));

var result = operation.Value;
foreach (var doc in result.Documents)
{
    foreach (var field in doc.Fields)
        Console.WriteLine($"{field.Key}: {field.Value.Content} (confidence: {field.Value.Confidence})");
}
```

### [Language Services — AnalyzeTextAsync (overview & REST)](https://learn.microsoft.com/azure/ai-services/language-service/sentiment-opinion-mining/how-to/call-api)
AnalyzeTextAsync runs language tasks (sentiment, entities, key phrases, PII). Options include:
- `language` (optional) — service auto-detects if omitted  
- `includeOpinionMining` — enable aspect-based sentiment  
- `modelVersion`, `showStats`, `disableServiceLogs`

Returns `AnalyzeTextResult` with results, per-sentence details, scores, warnings, and statistics (if requested).

REST sentiment example:
```
POST https://<resource>.cognitiveservices.azure.com/text/analytics/v3.1/sentiment
Headers:
  Ocp-Apim-Subscription-Key: <your-resource-key>
Body:
{
  "documents": [
    {
      "id": "1",
      "language": "en",
      "text": "I love this product!"
    }
  ],
  "opinionMining": true
}
```

C# (.NET SDK)
```csharp
using Azure;
using Azure.AI.TextAnalytics;

var client = new TextAnalyticsClient(
    new Uri("https://<resource>.cognitiveservices.azure.com/"),
    new AzureKeyCredential("<your-resource-key>"));

var response = await client.AnalyzeSentimentAsync("I love this product!", options: new AnalyzeSentimentOptions { IncludeOpinionMining = true });

Console.WriteLine($"Sentiment: {response.Value.Sentiment}, Positive: {response.Value.ConfidenceScores.Positive}");
foreach (var sentence in response.Value.Sentences)
    Console.WriteLine($"  {sentence.Text} → {sentence.Sentiment}");
```

### [Custom Vision — Prediction (REST)](https://learn.microsoft.com/azure/ai-services/custom-vision-service/use-prediction-api)
POST image URL to prediction endpoint with `Prediction-Key` header. Response lists `predictions` with `tagName` and `probability`.

C# (.NET SDK)
```csharp
using Microsoft.Azure.CognitiveServices.Vision.CustomVision.Prediction;

var client = new CustomVisionPredictionClient(
    new ApiKeyServiceClientCredentials("<prediction-key>"))
    { Endpoint = "https://<resource>.cognitiveservices.azure.com/" };

var result = await client.ClassifyImageUrlAsync(
    projectId: Guid.Parse("<project-id>"),
    publishedName: "<iteration-name>",
    new ImageUrl("https://example.com/image.jpg"));

foreach (var pred in result.Predictions)
    Console.WriteLine($"{pred.TagName}: {pred.Probability:P2}");
```

### [Speech-to-Text (REST)](https://learn.microsoft.com/azure/ai-services/speech-service/rest-speech-to-text)
Send binary audio to STT REST endpoint; response includes `DisplayText`, `RecognitionStatus`, timestamps.

C# (.NET SDK)
```csharp
using Microsoft.CognitiveServices.Speech;

var config = SpeechConfig.FromSubscription("<your-resource-key>", "<region>");
using var recognizer = new SpeechRecognizer(config);

var result = await recognizer.RecognizeOnceAsync();
if (result.Reason == ResultReason.RecognizedSpeech)
    Console.WriteLine($"Recognized: {result.Text}");
```

### [Azure OpenAI — Chat completions (REST)](https://learn.microsoft.com/azure/ai-services/openai/reference)
POST messages to:
```
https://<resource>.openai.azure.com/openai/deployments/<deployment-name>/chat/completions?api-version=<version>
Headers:
  api-key: <your-resource-key>
Body:
{
  "messages": [
    { "role": "system", "content": "..." },
    { "role": "user", "content": "..." }
  ],
  "max_tokens": 256,
  "temperature": 0.7
}
```
Response contains `choices[]` and `usage`. Check `finish_reason` for `"length"` truncation or `"content_filter"`.

C# (.NET SDK)
```csharp
using Azure;
using Azure.AI.OpenAI;

var client = new AzureOpenAIClient(
    new Uri("https://<resource>.openai.azure.com/"),
    new AzureKeyCredential("<your-resource-key>"));

var chatClient = client.GetChatClient("<deployment-name>");
var response = await chatClient.CompleteChatAsync(
    new ChatMessage[] {
        new SystemChatMessage("You are a helpful assistant."),
        new UserChatMessage("What is Azure?")
    });

Console.WriteLine($"Response: {response.Value.Content[0].Text}");
Console.WriteLine($"Finish reason: {response.Value.FinishReason}");
```

---

[Previous](./01-file-types-and-size-limitations.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./03-content-filtering-and-message-flagging.md)

