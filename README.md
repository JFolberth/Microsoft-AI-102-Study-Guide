# AI-102 Exam Study Guide

---

## DISCLAIMER

**This study guide was generated with assistance from GitHub Copilot.**

While this guide references official Microsoft Azure documentation, validate details against the source links included. This is a supplementary study resource—API versions, quotas, endpoints, and pricing can change. Always check the official docs.

---

## Table of Contents

- [AI-102 Exam Study Guide](#ai-102-exam-study-guide)
  - [DISCLAIMER](#disclaimer)
  - [Table of Contents](#table-of-contents)
  - [1. File Types and Size Limitations](#1-file-types-and-size-limitations)
    - [Document Intelligence (Form Recognizer)](#document-intelligence-form-recognizer)
    - [Custom Vision](#custom-vision)
    - [Language Services (Text Analytics)](#language-services-text-analytics)
    - [Speech Services](#speech-services)
    - [Azure AI Search](#azure-ai-search)
    - [Azure Storage (for AI services)](#azure-storage-for-ai-services)
    - [Azure Video Indexer (Video processing)](#azure-video-indexer-video-processing)
  - [2. Control Plane - REST API Calls](#2-control-plane---rest-api-calls)
    - [API key note](#api-key-note)
    - [Common REST Endpoint structure](#common-rest-endpoint-structure)
    - [Document Intelligence — Analyze (REST example)](#document-intelligence--analyze-rest-example)
    - [Language Services — AnalyzeTextAsync (overview \& REST)](#language-services--analyzetextasync-overview--rest)
    - [Custom Vision — Prediction (REST)](#custom-vision--prediction-rest)
    - [Speech-to-Text (REST)](#speech-to-text-rest)
    - [Azure OpenAI — Chat completions (REST)](#azure-openai--chat-completions-rest)
  - [3. Content Filtering and Message Flagging](#3-content-filtering-and-message-flagging)
  - [4. Multi-Language Support for Audio and Video](#4-multi-language-support-for-audio-and-video)
  - [5. Model Selection Criteria (Simplified)](#5-model-selection-criteria-simplified)
  - [6. Azure Security: Key Rotation](#6-azure-security-key-rotation)
  - [7. Synonyms in Document Intelligence](#7-synonyms-in-document-intelligence)
  - [8. Confidence Scoring (Short)](#8-confidence-scoring-short)
  - [9. Azure AI Language (Question Answering)](#9-azure-ai-language-question-answering)
  - [10. Token Calculation \& Max Token Behavior](#10-token-calculation--max-token-behavior)
  - [11. Image Model Training (Vision)](#11-image-model-training-vision)
  - [12. Text / Image Processing Methods (REST)](#12-text--image-processing-methods-rest)
  - [13. Semantic Kernel — Prompt Template Formats](#13-semantic-kernel--prompt-template-formats)
  - [14. SSML for Speech — Styles \& Example](#14-ssml-for-speech--styles--example)
    - [SSML attribute quick reference (Azure Speech)](#ssml-attribute-quick-reference-azure-speech)
  - [15. AI Search Indexing (Summary)](#15-ai-search-indexing-summary)
    - [What resource types can be queried with Azure AI Search?](#what-resource-types-can-be-queried-with-azure-ai-search)
    - [Leverage auto tag and classification in vision search](#leverage-auto-tag-and-classification-in-vision-search)
  - [Video (Azure Video Indexer \& video processing)](#video-azure-video-indexer--video-processing)
    - [When to run Video Indexing (and what you get)](#when-to-run-video-indexing-and-what-you-get)
  - [16. Quick Reference Tables](#16-quick-reference-tables)
    - [API Key Quick Reference](#api-key-quick-reference)
    - [File Size / Limits Summary](#file-size--limits-summary)
    - [Video File Outputs (Video Indexer)](#video-file-outputs-video-indexer)
    - [Model Selection (cheat sheet)](#model-selection-cheat-sheet)
    - [AnalyzeTextAsync() Snapshot](#analyzetextasync-snapshot)
    - [Token Behavior Summary](#token-behavior-summary)
    - [Confidence Score Thresholds (guidance)](#confidence-score-thresholds-guidance)
    - [JSONPath Wildcard Examples](#jsonpath-wildcard-examples)
  - [17. Entity Linking (Wikipedia links from text)](#17-entity-linking-wikipedia-links-from-text)
  - [18. Import/Export Azure AI Language Projects](#18-importexport-azure-ai-language-projects)
  - [19. Foundry: Scope model access for multiple APIs](#19-foundry-scope-model-access-for-multiple-apis)
  - [Useful Links (official docs)](#useful-links-official-docs)

---

## 1. [File Types and Size Limitations](https://learn.microsoft.com/azure/ai-services/)

### [Document Intelligence (Form Recognizer)](https://learn.microsoft.com/azure/ai-services/document-intelligence/)
| Operation | Max File Size | Supported Formats |
|-----------|--------------:|------------------|
| Standard Analysis | 50 MB | PDF, JPEG, PNG, TIFF, BMP |
| Batch Analysis | 50 MB per file | PDF, JPEG, PNG, TIFF, BMP |
| Large-file (Storage pipeline) | up to 500 MB (see docs) | PDF, JPEG, PNG, TIFF, BMP |
| Custom Model Training | 50 MB per file | PDF, JPEG, PNG, TIFF, BMP |

Reference: https://learn.microsoft.com/azure/ai-services/document-intelligence/service-limits

### [Custom Vision](https://learn.microsoft.com/azure/ai-services/custom-vision-service/)
| Operation | Limit | Supported Formats |
|-----------|------:|------------------|
| Batch upload | up to 64 images per request, 20 tags | JPEG, PNG, BMP, GIF |
| Single image (portal guidance) | ~6 MB | JPEG, PNG, BMP, GIF |
| Prediction payload | typically < 4 MB | JPEG, PNG, BMP, GIF |

Limits: https://learn.microsoft.com/azure/ai-services/custom-vision-service/limits-and-quotas

### [Language Services (Text Analytics)](https://learn.microsoft.com/azure/ai-services/language-service/)
| Operation | Limit | Format |
|-----------|------:|--------|
| Single document | ~5,120 characters (varies by API) | Plain text, JSON |
| Batch request | up to 1,000 documents | JSON |
| Total batch size | ~1 MB (varies) | JSON |

Data limits: https://learn.microsoft.com/azure/ai-services/language-service/concepts/data-limits

### [Speech Services](https://learn.microsoft.com/azure/ai-services/speech-service/)
| Operation | Guidance | Supported Formats |
|-----------|---------:|------------------|
| Realtime STT | seconds (service dependent) | WAV, MP3, OGG, FLAC |
| Batch recognition | larger files supported (guidance ≈ 200 MB) | WAV (PCM recommended), MP3, FLAC |
| Text-to-Speech output | up to minutes per request (see docs) | N/A |

Quotas: https://learn.microsoft.com/azure/ai-services/speech-service/speech-services-quotas-and-limits

### [Azure AI Search](https://learn.microsoft.com/azure/search/)
| Operation | Limit | Format |
|-----------|------:|--------|
| Document upload | 16 MB per document | JSON |
| Batch upload | up to 1,000 documents or 16 MB | JSON |
| Blob indexing | blob size quotas apply | Various |

Limits: https://learn.microsoft.com/azure/search/search-limits-quotas-capacity

### [Azure Storage (for AI services)](https://learn.microsoft.com/azure/storage/)
| Storage Type | Max Size | Notes |
|--------------|---------:|-------|
| Block Blob | 190.7 TB | Used for large artifacts |
| Page Blob | 8 TB | 512-byte aligned pages |
| Azure Files | 100 TB (large file share) | Standard default smaller |

Reference: https://learn.microsoft.com/azure/storage/common/scalability-targets-standard-account

### [Azure Video Indexer (Video processing)](https://learn.microsoft.com/azure/media-services/video-indexer/)
| Category | Guidance | Common Formats / Artifacts |
|----------|----------|----------------------------|
| Input video | Size/length limits vary by account/region/API; for large videos, prefer uploading to Blob Storage and submitting a `videoUrl` | MP4, MOV, AVI, WMV (verify current container/codec support in docs) |
| Captions / transcript output | Generated after processing; downloaded via API | `transcript.vtt`, `transcript.srt`, `translated_<lang>.vtt/.srt` |
| Insights output | Structured analysis with timestamps and confidence | `insights.json` |
| Visual artifacts | Thumbnails/keyframes and related metadata | `.jpg` thumbnails + metadata in insights JSON |

---

## 2. [Control Plane - REST API Calls](https://learn.microsoft.com/azure/ai-services/reference/rest-api-resources)

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

## 3. [Content Filtering and Message Flagging](https://learn.microsoft.com/azure/ai-services/openai/concepts/content-filter)

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

## 4. [Multi-Language Support for Audio and Video](https://learn.microsoft.com/azure/ai-services/speech-service/language-support)

Key concept:
- Input language: many services auto-detect or accept candidate languages.  
- Output language: must be configured for translation/synthesis.

- Language detection (Text Analytics): https://learn.microsoft.com/azure/ai-services/language-service/language-detection/how-to/call-api  
- Translator REST: https://learn.microsoft.com/azure/ai-services/translator/reference/v3-0-translate  
- Speech translation: https://learn.microsoft.com/azure/ai-services/speech-service/speech-translation

Practical tip: for audio/video, provide candidate languages to improve detection; explicitly set target locales/voice names for outputs (e.g., `es-ES`, `en-US-JennyNeural`).

---

## 5. [Model Selection Criteria (Simplified)](https://learn.microsoft.com/azure/ai-services/openai/concepts/models)

Simple mapping:
- Image generation → DALL‑E  
- Speech-to-text → Whisper (or Azure Speech STT)  
- General chat → GPT‑3.5‑Turbo (cost-effective) or GPT‑4 (higher quality)  
- Embeddings → text-embedding-ada-002 (or current best embedding per docs)

Reference: https://learn.microsoft.com/azure/ai-services/openai/concepts/models

---

## 6. [Azure Security: Key Rotation](https://learn.microsoft.com/azure/ai-services/rotate-keys)

Zero-downtime pattern (portal):
1. Copy Secondary Key (Key2) and update app to use it.  
2. Regenerate Primary Key (Key1).  
3. Update app to use new Key1.  
4. Optionally regenerate Key2.  

Best practice: rotate regularly (e.g., every 90 days).

---

## 7. [Synonyms in Document Intelligence](https://learn.microsoft.com/azure/ai-services/document-intelligence/concept-custom)

Synonym example JSON:
```json
{
  "modelId": "invoice-model-v1",
  "fields": {
    "InvoiceNumber": {
      "type": "string",
      "synonyms": [
        "Invoice #",
        "Inv No",
        "Invoice No.",
        "Bill Number"
      ]
    },
    "TotalAmount": {
      "type": "number",
      "synonyms": [
        "Total",
        "Grand Total",
        "Amount Due",
        "Total Due"
      ]
    }
  }
}
```
Synonyms improve mapping of extracted text to canonical fields.

---

## 8. [Confidence Scoring (Short)](https://learn.microsoft.com/azure/ai-services/document-intelligence/concept-accuracy-confidence)

- Confidence values (0.0–1.0) appear at multiple levels: field-level, sentence-level, prediction probability.  
- Useful JSONPath patterns:
  - `$..confidence` — all confidence values  
  - `$.fields.*.confidence` — top-level fields  
  - `$.predictions[*].probability` — Custom Vision probabilities  
  - `$..confidence[?(@ < 0.7)]` — filter below threshold

Threshold guidance:
- Low: < 0.7, Medium: 0.7–0.89, High: ≥ 0.9 (service-dependent)

---

## 9. [Azure AI Language (Question Answering)](https://learn.microsoft.com/azure/ai-services/language-service/question-answering/overview)

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

## 10. [Token Calculation & Max Token Behavior](https://learn.microsoft.com/azure/ai-services/openai/how-to/manage-tokens)

- Total tokens = prompt tokens + completion tokens.  
- Approximation: 1 token ≈ 4 characters (English) or ~0.75 words.  
- If completion hits `max_tokens`, it's truncated; `finish_reason` = `"length"`.  
- Check `usage` for `prompt_tokens`, `completion_tokens`, `total_tokens`.  
- `finish_reason` values: `"stop"`, `"length"`, `"content_filter"`.

Request configuration (.json)
```json
{
  "messages": [
    {
      "role": "system",
      "content": "You are a helpful assistant."
    },
    {
      "role": "user",
      "content": "Explain transformers in detail with references and examples."
    }
  ],
  "temperature": 0.7,
  "top_p": 1,
  "max_tokens": 256,
  "frequency_penalty": 0,
  "presence_penalty": 0
}
```

Truncated response example (.json)
```json
{
  "object": "chat.completion",
  "id": "chatcmpl-abc123",
  "created": 1738118400,
  "model": "gpt-4o",
  "choices": [
    {
      "index": 0,
      "message": {
        "role": "assistant",
        "content": "Transformers are sequence-to-sequence architectures that rely on self-attention rather than recurrence. The encoder maps inputs to contextual embeddings, while the decoder generates outputs using cross-attention over encoder states. Key components include multi-head attention, positional encodings, residual connections, and layer normalization. Compared to RNNs and LSTMs, transformers enable parallelization and improved long-range dependency modeling. Notable variants such as BERT, GPT, and T5 demonstrate pretraining objectives like masked language modeling and autoregressive generation. Practical considerations include tokenization schemes, context window limits, and fine-tuning strategies for downstream tasks such as question answering, summarization, and machine translation. Common pitfalls involve hallucinations, prompt sensitivity, and data leakage. To mitigate these, apply retrieval augmentation, constrain decoding, and implement robust evaluation with held-out sets and adversarial"
      },
      "finish_reason": "length",
      "content_filter_results": {
        "hate": {
          "filtered": false,
          "severity": "safe"
        },
        "self_harm": {
          "filtered": false,
          "severity": "safe"
        },
        "sexual": {
          "filtered": false,
          "severity": "safe"
        },
        "violence": {
          "filtered": false,
          "severity": "safe"
        }
      }
    }
  ],
  "usage": {
    "prompt_tokens": 812,
    "completion_tokens": 256,
    "total_tokens": 1068
  },
  "prompt_filter_results": [
    {
      "prompt_index": 0,
      "content_filter_results": {
        "hate": {
          "filtered": false,
          "severity": "safe"
        },
        "self_harm": {
          "filtered": false,
          "severity": "safe"
        },
        "sexual": {
          "filtered": false,
          "severity": "safe"
        },
        "violence": {
          "filtered": false,
          "severity": "safe"
        }
      }
    }
  ]
}
```

---

## 11. [Image Model Training (Vision)](https://learn.microsoft.com/azure/ai-services/custom-vision-service/getting-started-build-a-classifier)

Workflow:
1. Create project (classification/object detection)  
2. Upload & tag images (min recommended: 5 images/tag; production: 50+ per tag)  
3. Train iterations; evaluate metrics; publish iteration to prediction resource  
4. For object detection include bounding boxes/regions

Best practices: balanced tags, image variety, negative examples.

---

## 12. [Text / Image Processing Methods (REST)](https://learn.microsoft.com/azure/ai-services/)

- [Computer Vision analyze image](https://learn.microsoft.com/azure/ai-services/computer-vision/how-to/call-analyze-image) — POST with `visualFeatures` (Tags, Objects, Description).  
- [Text Analytics key phrase extraction](https://learn.microsoft.com/azure/ai-services/language-service/key-phrase-extraction/how-to/call-api) — POST documents array and parse `keyPhrases`.

Always apply confidence filtering where appropriate.

---

## 13. [Semantic Kernel — Prompt Template Formats](https://learn.microsoft.com/semantic-kernel/prompts/)

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

## 14. [SSML for Speech — Styles & Example](https://learn.microsoft.com/azure/ai-services/speech-service/speech-synthesis-markup)

### SSML attribute quick reference (Azure Speech)
| Element | Attribute | Example | What it means |
|--------|-----------|---------|---------------|
| `<speak>` | `version` | `version="1.0"` | SSML spec version for the document. |
| `<speak>` | `xmlns` | `xmlns="http://www.w3.org/2001/10/synthesis"` | Default SSML namespace (required). |
| `<speak>` | `xmlns:mstts` | `xmlns:mstts="http://www.w3.org/2001/mstts"` | Azure Speech extension namespace for `mstts:*` tags (only if you use them). |
| `<speak>` / `<voice>` / `<lang>` | `xml:lang` | `xml:lang="en-US"` | Declares language/locale context used for pronunciation and voice rendering. |
| `<voice>` | `name` | `name="en-US-JennyNeural"` | Selects the voice (locale + voice). Must match a supported voice name. |
| `<mstts:express-as>` | `style` | `style="cheerful"` | Speaking style (Azure-specific). Availability depends on the chosen voice. |
| `<mstts:express-as>` | `role` | `role="YoungAdultFemale"` | Alters speaking “role”/persona for supported voices (Azure-specific). |
| `<mstts:express-as>` | `styledegree` | `styledegree="1.2"` | Adjusts intensity of the selected style (Azure-specific; support varies). |
| `<break>` | `time` | `time="400ms"` | Inserts a pause of an explicit duration. |
| `<break>` | `strength` | `strength="medium"` | Inserts a pause with relative strength (alternative to `time`). |
| `<prosody>` | `rate` | `rate="slow"` | Controls speaking rate (relative values like `slow/fast` or percentages). |
| `<prosody>` | `pitch` | `pitch="+10%"` | Adjusts pitch up/down (relative or absolute depending on SSML support). |
| `<prosody>` | `volume` | `volume="loud"` | Adjusts loudness (relative keywords or values depending on support). |
| `<say-as>` | `interpret-as` | `interpret-as="date"` | Tells the TTS engine how to read the contained text (date, number, telephone, etc.). |
| `<say-as>` | `format` | `format="mdy"` | Provides parsing hints for `interpret-as` (commonly used with dates). |
| `<emphasis>` | `level` | `level="strong"` | Emphasizes the enclosed text (reduced/ moderate/ strong). |
| `<phoneme>` | `alphabet` | `alphabet="ipa"` | Indicates phoneme alphabet used (e.g., IPA) for pronunciation overrides. |
| `<phoneme>` | `ph` | `ph="təˈmeɪtoʊ"` | The phonetic spelling for the enclosed word/phrase. |

Example SSML:
```xml
<speak version="1.0" xmlns="http://www.w3.org/2001/10/synthesis" xmlns:mstts="http://www.w3.org/2001/mstts" xml:lang="en-US">
  <voice name="en-US-JennyNeural">
    <mstts:express-as style="cheerful">Welcome! Your order is confirmed.</mstts:express-as>
    <break time="400ms"/>
    <prosody rate="slow">Estimated delivery: <say-as interpret-as="date">03/15/2026</say-as>.</prosody>
  </voice>
</speak>
```

---

## 15. [AI Search Indexing (Summary)](https://learn.microsoft.com/azure/search/search-what-is-azure-search)

Indexing steps:
1. Data source → Blob, SQL, Cosmos DB  
2. Skillset → AI enrichment (optional)  
3. Index → fields, analyzers, vector fields  
4. Indexer → ingestion schedule

Vector/semantic search: https://learn.microsoft.com/azure/search/vector-search-overview

### What resource types can be queried with Azure AI Search?

Azure AI Search queries run against your **search index**. Your index can be populated from many Azure resource types.

Two ingestion patterns:
- **Indexer-based (pull) ingestion**: use indexers to crawl supported data sources and build an index.
- **Push-based ingestion**: push JSON documents directly to the index using REST APIs or SDK.

Common supported data sources for indexers ("resource types") include:
- Azure Blob Storage
- Azure Data Lake Storage Gen2
- Azure Table Storage
- Azure SQL Database
- Azure SQL Managed Instance
- SQL Server on Azure Virtual Machines
- Azure Cosmos DB for NoSQL
- Microsoft OneLake
- Several other preview connectors (see the data sources gallery for the current list)

Docs:
- Indexers overview + supported data sources: https://learn.microsoft.com/azure/search/search-indexer-overview#supported-data-sources
- Data sources gallery: https://learn.microsoft.com/azure/search/search-data-sources-gallery
- Push data to an index: https://learn.microsoft.com/azure/search/search-what-is-data-import#pushing-data-to-an-index

### Leverage auto tag and classification in vision search

If you want image-based content to be searchable, you typically **extract tags/categories/captions/OCR at indexing time**, store those outputs in index fields, and then query/filter/facet on those fields.

Two common patterns:

1) **AI enrichment (recommended when using indexers):**
- Enable image extraction (`imageAction`) during indexing so images become available under `/document/normalized_images/*`.
- Add the built-in **Image Analysis** skill to generate `tags` and `categories`.
- Optionally add the built-in **OCR** skill to extract embedded or standalone image text.

Skillset snippet (Image Analysis tags + categories):
```json
{
  "name": "images-skillset",
  "skills": [
    {
      "@odata.type": "#Microsoft.Skills.Vision.ImageAnalysisSkill",
      "context": "/document/normalized_images/*",
      "visualFeatures": [ "tags", "categories" ],
      "inputs": [
        { "name": "image", "source": "/document/normalized_images/*" }
      ],
      "outputs": [
        { "name": "tags", "targetName": "imageTags" },
        { "name": "categories", "targetName": "imageCategories" }
      ]
    }
  ]
}
```

Indexer configuration snippet (enable normalized images):
```json
{
  "parameters": {
    "configuration": {
      "imageAction": "generateNormalizedImages"
    }
  }
}
```

Docs:
- Image Analysis skill: https://learn.microsoft.com/azure/search/cognitive-search-skill-image-analysis
- Image extraction + normalized images: https://learn.microsoft.com/azure/search/cognitive-search-concept-image-scenarios
- Skill context basics: https://learn.microsoft.com/azure/search/cognitive-search-defining-skillset#set-skill-context
- OCR skill (optional): https://learn.microsoft.com/azure/search/cognitive-search-skill-ocr

2) **Pre-process images yourself (useful if your data source isn't covered by indexers):**
- Call Azure AI Vision Image Analysis in your app.
- Store returned tags/categories/captions in your own JSON documents.
- Push those documents into Azure AI Search.

Note:
- The built-in Image Analysis skill maps to Image Analysis API v3.2. If you require Image Analysis v4.0 features inside an enrichment pipeline, use a custom skill.

---
## Video (Azure Video Indexer & video processing)

[Azure Video Indexer / Video processing docs](https://learn.microsoft.com/azure/media-services/video-indexer/)

What it does
- Video Indexer (part of Azure Media/AI tooling) analyzes video to produce:
  - Speech transcription (captions), speaker diarization, timestamps
  - Subtitle/translation generation (multiple target languages)
  - Visual insights: faces, OCR (text in video), shot/scene segmentation, thumbnails/keyframes, objects, motion
  - Content insights: keywords, topics, named entities, sentiment per segment
  - Exportable artifacts: JSON insights, SRT/VTT captions, thumbnails, transcript files

### When to run Video Indexing (and what you get)

Run Video Indexing when you need **searchable, timestamped insights** extracted from audio/video (batch/asynchronous processing). Typical triggers:

- **After ingesting new media** into a library/asset store (so you can enable deep search across transcript/OCR/keywords).
- **Before publishing or distributing content** (to generate captions/subtitles, translations, scene/keyframe markers, and thumbnails).
- **Compliance / moderation workflows** where you need transcripts and reviewable artifacts.
- **Content editing workflows** (promos/trailers) where shot/scene segmentation and keyframes reduce manual review time.

Docs:
- Video Indexer overview: https://learn.microsoft.com/azure/azure-video-indexer/video-indexer-overview
- Insights overview: https://learn.microsoft.com/azure/azure-video-indexer/insights-overview

File types & sizing guidance
- Common input formats: MP4, MOV, AVI, WMV (check docs for current supported codecs/containers)
- Large files: recommended to upload to Azure Blob Storage and provide the video URL to the indexing API (avoids direct large binary upload)
- Exact per-service size/length limits vary — consult the Video Indexer docs for current quotas and encoding guidance.

Key behavior: input auto-detection vs output config
- Spoken language: Video Indexer can auto-detect the spoken language but detection improves if you supply a language or candidate languages.
- Output language(s) for captions/translations: you must explicitly request target language(s) when creating the indexing job (Video Indexer will produce translated caption files for those languages).

Primary outputs (examples)
- insights.json — full structured analysis with timestamps and confidence scores
- transcript.vtt / transcript.srt — native-language captions
- translated_<lang>.srt / .vtt — translated captions for requested target languages
- thumbnails (jpg), keywords, faces metadata

How to interact via .NET (pattern)
- Pattern: upload video to Blob (optional) → call Video Indexer REST to create an indexing job with videoUrl or uploaded file → poll for job status → fetch insights and artifacts (JSON, captions).
- We avoid embedding auth/portal steps here; use the service key/token as required by the service.

Minimal .NET example (submit video URL, request transcripts + translations, poll for completion)
```csharp
// NOTE: replace placeholders for resource, account, and keys per your environment.
// This shows the REST pattern via HttpClient.
using System.Net.Http;
using System.Text.Json;
using System.Text;

var http = new HttpClient();

// Example: create index job (Video Indexer REST shape varies; adjust per API version)
var requestBody = new
{
    name = "MyVideoJob",
    videoUrl = "https://mystorage.blob.core.windows.net/videos/myvideo.mp4",
    privacy = "Private",
    language = "auto",                 // or "en-US" to force
    translateTo = new[] { "es", "fr" } // request Spanish and French translated captions
};

var body = new StringContent(JsonSerializer.Serialize(requestBody), Encoding.UTF8, "application/json");
// Header name may vary by API surface (this placeholder is illustrative)
http.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", "<your-resource-key>");

var createResponse = await http.PostAsync(
    "https://api.videoindexer.ai/<location>/Accounts/<accountId>/Videos?accessToken=<accessToken>",
    body);

createResponse.EnsureSuccessStatusCode();
var createJson = await createResponse.Content.ReadAsStringAsync();
Console.WriteLine("Job created: " + createJson);

// Poll for processing status (example endpoint; check docs for exact path)
string videoId = /* extract id from createJson */;
string statusUrl = $"https://api.videoindexer.ai/<location>/Accounts/<accountId>/Videos/{videoId}/Index?accessToken=<accessToken>";

while (true)
{
    var statusResp = await http.GetAsync(statusUrl);
    var statusJson = await statusResp.Content.ReadAsStringAsync();
    using var doc = JsonDocument.Parse(statusJson);
    var state = doc.RootElement.GetProperty("state").GetString(); // property name may differ
    Console.WriteLine($"State: {state}");
    if (state == "Processed" || state == "Failed") break;
    await Task.Delay(TimeSpan.FromSeconds(10));
}

// Fetch insights (JSON)
var insightsUrl = $"https://api.videoindexer.ai/<location>/Accounts/<accountId>/Videos/{videoId}/Insights?accessToken=<accessToken>";
var insightsResp = await http.GetAsync(insightsUrl);
var insights = await insightsResp.Content.ReadAsStringAsync();
Console.WriteLine("Insights JSON length: " + insights.Length);

// Fetch captions (SRT/VTT) — sample endpoint form; check docs for exact query params
var captionsUrl = $"https://api.videoindexer.ai/<location>/Accounts/<accountId>/Videos/{videoId}/Captions?language=es&accessToken=<accessToken>";
var captionsResp = await http.GetAsync(captionsUrl);
var captions = await captionsResp.Content.ReadAsStringAsync();
Console.WriteLine("Spanish captions:\n" + captions);
```

Get Video Index — example REST response (insights JSON)
```json
{
  "insights": {
    "version": "1.0.0.0",
    "duration": "0:01:50.486",
    "sourceLanguage": "en-US",
    "sourceLanguages": [
      "es-ES",
      "en-US"
    ],
    "language": "en-US",
    "transcript": [
      {
        "id": 1,
        "text": "Hi, I'm Doug from office. We're talking about new features that office insiders will see first.",
        "confidence": 0.8879,
        "speakerId": 1,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:00:00",
            "adjustedEnd": "0:00:05.75",
            "start": "0:00:00",
            "end": "0:00:05.75"
          }
        ]
      },
      {
        "id": 2,
        "text": "Emily Tran, with office graphics.",
        "confidence": 0.8879,
        "speakerId": 1,
        "language": "en-US",
        "instances": [
          {
            "adjustedStart": "0:00:05.75",
            "adjustedEnd": "0:00:07.01",
            "start": "0:00:05.75",
            "end": "0:00:07.01"
          }
        ]
      }
    ],
    "keywords": [
      {
        "id": 1,
        "text": "office insiders",
        "confidence": 0.92,
        "instances": [
          {
            "adjustedStart": "0:00:02",
            "adjustedEnd": "0:00:04",
            "start": "0:00:02",
            "end": "0:00:04"
          }
        ]
      }
    ],
    "faces": [
      {
        "id": 1,
        "name": "Unknown #1",
        "confidence": 0.75,
        "instances": [
          {
            "adjustedStart": "0:00:00",
            "adjustedEnd": "0:00:10",
            "start": "0:00:00",
            "end": "0:00:10"
          }
        ]
      }
    ],
    "emotions": [
      {
        "id": 1,
        "type": "Joy",
        "instances": [
          {
            "confidence": 0.65,
            "adjustedStart": "0:00:00",
            "adjustedEnd": "0:00:05.75",
            "start": "0:00:00",
            "end": "0:00:05.75"
          }
        ]
      }
    ]
  }
}
```
Reference: https://learn.microsoft.com/azure/azure-video-indexer/transcription-translation-lid-insight

---

## 16. Quick Reference Tables

### API Key Quick Reference
| Header Name | Use |
|-------------|-----|
| `Ocp-Apim-Subscription-Key` | Cognitive Services resource key (Key1/Key2) — used across many REST endpoints |
| `api-key` | OpenAI endpoints — use your Azure OpenAI resource key |
| `Prediction-Key` | Custom Vision prediction key (portal/endpoint) |

### File Size / Limits Summary
| Service | Max Size / Notes |
|---------|------------------|
| Document Intelligence | 50 MB per file (500 MB via storage pipelines) |
| Custom Vision | ~6 MB single upload; 64 images per batch guidance |
| Language Services | ~5,120 chars per doc; 1,000 docs per batch; ~1 MB batch |
| Speech (batch) | Guidance ~200 MB |
| AI Search | 16 MB per document (JSON) |
| Video Indexer | Limits vary; for large videos use Blob + `videoUrl` (see docs) |

### Video File Outputs (Video Indexer)
| File / Artifact | What it’s for |
|-----------------|---------------|
| `insights.json` | Full analysis results: transcript segments, speakers, OCR, faces, topics/keywords, timestamps, confidence |
| `transcript.vtt` / `transcript.srt` | Native-language captions for the detected/specified spoken language |
| `translated_<lang>.vtt` / `translated_<lang>.srt` | Translated captions for requested target language(s) |
| Thumbnails / keyframes (`.jpg`) | Visual navigation, previews; also referenced by insights metadata |

### Model Selection (cheat sheet)
| Task | Model |
|------|-------|
| Images | DALL‑E |
| Speech → text | Whisper / Azure Speech STT |
| Chat | GPT‑3.5‑Turbo / GPT‑4 |
| Embeddings | text-embedding-ada-002 (or current recommended model) |

### AnalyzeTextAsync() Snapshot
| Aspect | Details |
|--------|---------|
| Purpose | sentiment, entities, key phrases, PII, language detection |
| Key options | `includeOpinionMining`, `modelVersion`, `showStats`, `disableServiceLogs` |
| Returns | `sentiment`, `confidenceScores`, `sentences[]`, `warnings[]`, `statistics` |

### Token Behavior Summary
| Scenario | finish_reason | Behavior |
|----------|---------------|----------|
| Completes | `stop` | Full response returned |
| Hits max_tokens | `length` | Response truncated |
| Content policy hit | `content_filter` | Blocked/filtered |

### Confidence Score Thresholds (guidance)
| Service | Low | Medium | High |
|---------|------:|-------:|-----:|
| Document Intelligence | < 0.7 | 0.7–0.89 | ≥ 0.9 |
| Language Detection | < 0.7 | 0.7–0.84 | ≥ 0.85 |
| Custom Vision | < 0.6 | 0.6–0.79 | ≥ 0.8 |

### JSONPath Wildcard Examples
| Pattern | Finds |
|---------|-------|
| `$..confidence` | All confidence values anywhere in JSON |
| `$.fields.*.confidence` | Top-level extracted field confidences |
| `$.predictions[*].probability` | Prediction probabilities (Custom Vision) |

---

## 17. [Entity Linking (Wikipedia links from text)](https://learn.microsoft.com/azure/ai-services/language-service/entity-linking/overview)

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

## 18. Import/Export Azure AI Language Projects

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

## 19. Foundry: Scope model access for multiple APIs

Scenario: multiple internal APIs/microservices call **the same deployed model** in Foundry, but you want to control access per API.

Recommended approach: **Microsoft Entra ID + RBAC**
- Give each API its own identity (managed identity, service principal, or app registration).
- Assign that identity a role that grants inference access at the **Foundry resource scope**.
- Use token-based auth in each API instead of distributing keys.

Key concept
- Azure distinguishes **administration (control plane)** actions (deployments, settings) from **developer/inference (data plane)** actions (calling inference APIs). Admin rights do *not* automatically grant inference rights.

Docs:
- Keyless auth with Microsoft Entra ID: https://learn.microsoft.com/azure/ai-foundry/foundry-models/how-to/configure-entra-id
- Foundry RBAC concepts: https://learn.microsoft.com/azure/ai-foundry/concepts/rbac-foundry

Practical scoping patterns
- **Per-API isolation:** separate identities + separate role assignments (revoke one API without impacting others).
- **Hard separation:** create separate model deployments (or separate Foundry resources/projects) when you need different policies/filters/quotas per API.
- **Gateway enforcement:** put Azure API Management in front of your internal APIs to enforce per-client subscription keys, quotas, or JWT validation, while APIM (or your API) calls Foundry using a managed identity.

---

## Useful Links (official docs)
- AI-102 exam: https://learn.microsoft.com/learn/certifications/exams/ai-102  
- Azure AI Services main: https://learn.microsoft.com/azure/ai-services/  
- Document Intelligence: https://learn.microsoft.com/azure/ai-services/document-intelligence/  
- Language Service: https://learn.microsoft.com/azure/ai-services/language-service/  
- Speech Service: https://learn.microsoft.com/azure/ai-services/speech-service/  
- Custom Vision: https://learn.microsoft.com/azure/ai-services/custom-vision-service/  
- Azure AI Search: https://learn.microsoft.com/azure/search/  
- Azure Video Indexer: https://learn.microsoft.com/azure/azure-video-indexer/  
- Azure AI Foundry: https://learn.microsoft.com/azure/ai-foundry/  
- Azure OpenAI: https://learn.microsoft.com/azure/ai-services/openai/  
- Content Safety: https://learn.microsoft.com/azure/ai-services/content-safety/  
- Semantic Kernel: https://learn.microsoft.com/semantic-kernel/  

---

Good luck with your AI-102 preparation — validate details with the official docs linked above.
```