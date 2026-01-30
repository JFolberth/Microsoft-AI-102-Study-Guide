# AI-102 Exam Study Guide

---

## DISCLAIMER

**This study guide was generated with assistance from GitHub Copilot.**

While this guide references official Microsoft Azure documentation, validate details against the source links included. This is a supplementary study resource—API versions, quotas, endpoints, and pricing can change. Always check the official docs.

---


> Split-page version: each numbered section is now its own page under the [guide/](guide/) folder.
>
> - Use the Table of Contents below to navigate.
> - Each page has **Previous / Next / Table of Contents** links.
> - Full single-page backup: [AI-102_Study_guide_full.md](AI-102_Study_guide_full.md)


## Table of Contents

- [AI-102 Exam Study Guide](#ai-102-exam-study-guide)
  - [DISCLAIMER](#disclaimer)
  - [Table of Contents](#table-of-contents)
  - [1. File Types and Size Limitations](guide/01-file-types-and-size-limitations.md)
    - [Document Intelligence (Form Recognizer)](guide/01-file-types-and-size-limitations.md#document-intelligence-form-recognizer)
    - [Custom Vision](guide/01-file-types-and-size-limitations.md#custom-vision)
    - [Language Services (Text Analytics)](guide/01-file-types-and-size-limitations.md#language-services-text-analytics)
    - [Speech Services](guide/01-file-types-and-size-limitations.md#speech-services)
    - [Azure AI Search](guide/01-file-types-and-size-limitations.md#azure-ai-search)
    - [Azure Storage (for AI services)](guide/01-file-types-and-size-limitations.md#azure-storage-for-ai-services)
    - [Azure Video Indexer (Video processing)](guide/01-file-types-and-size-limitations.md#azure-video-indexer-video-processing)
  - [2. Control Plane - REST API Calls](guide/02-control-plane-rest-api-calls.md)
    - [API key note](guide/02-control-plane-rest-api-calls.md#api-key-note)
    - [Common REST Endpoint structure](guide/02-control-plane-rest-api-calls.md#common-rest-endpoint-structure)
    - [Document Intelligence — Analyze (REST example)](guide/02-control-plane-rest-api-calls.md#document-intelligence--analyze-rest-example)
    - [Language Services — AnalyzeTextAsync (overview \& REST)](guide/02-control-plane-rest-api-calls.md#language-services--analyzetextasync-overview--rest)
    - [Custom Vision — Prediction (REST)](guide/02-control-plane-rest-api-calls.md#custom-vision--prediction-rest)
    - [Speech-to-Text (REST)](guide/02-control-plane-rest-api-calls.md#speech-to-text-rest)
    - [Azure OpenAI — Chat completions (REST)](guide/02-control-plane-rest-api-calls.md#azure-openai--chat-completions-rest)
  - [3. Content Filtering and Message Flagging](guide/03-content-filtering-and-message-flagging.md)
  - [4. Multi-Language Support for Audio and Video](guide/04-multi-language-support-for-audio-and-video.md)
  - [5. Model Selection Criteria (Simplified)](guide/05-model-selection-criteria-simplified.md)
  - [6. Azure Security: Key Rotation](guide/06-azure-security-key-rotation.md)
  - [7. Synonyms in Document Intelligence](guide/07-synonyms-in-document-intelligence.md)
  - [8. Confidence Scoring (Short)](guide/08-confidence-scoring-short.md)
  - [9. Azure AI Language (Question Answering)](guide/09-azure-ai-language-question-answering.md)
  - [10. Token Calculation \& Max Token Behavior](guide/10-token-calculation-max-token-behavior.md)
  - [11. Image Model Training (Vision)](guide/11-image-model-training-vision.md)
  - [12. Text / Image Processing Methods (REST)](guide/12-text-image-processing-methods-rest.md)
  - [13. Semantic Kernel — Prompt Template Formats](guide/13-semantic-kernel-prompt-template-formats.md)
  - [14. SSML for Speech — Styles \& Example](guide/14-ssml-for-speech-styles-example.md)
    - [SSML attribute quick reference (Azure Speech)](guide/14-ssml-for-speech-styles-example.md#ssml-attribute-quick-reference-azure-speech)
  - [15. AI Search Indexing (Summary)](guide/15-ai-search-indexing-summary.md)
    - [What resource types can be queried with Azure AI Search?](guide/15-ai-search-indexing-summary.md#what-resource-types-can-be-queried-with-azure-ai-search)
    - [Leverage auto tag and classification in vision search](guide/15-ai-search-indexing-summary.md#leverage-auto-tag-and-classification-in-vision-search)
  - [Video (Azure Video Indexer \& video processing)](guide/video-azure-video-indexer-video-processing.md)
    - [When to run Video Indexing (and what you get)](guide/video-azure-video-indexer-video-processing.md#when-to-run-video-indexing-and-what-you-get)
  - [16. Quick Reference Tables](guide/16-quick-reference-tables.md)
    - [API Key Quick Reference](guide/16-quick-reference-tables.md#api-key-quick-reference)
    - [File Size / Limits Summary](guide/16-quick-reference-tables.md#file-size--limits-summary)
    - [Video File Outputs (Video Indexer)](guide/16-quick-reference-tables.md#video-file-outputs-video-indexer)
    - [Model Selection (cheat sheet)](guide/16-quick-reference-tables.md#model-selection-cheat-sheet)
    - [AnalyzeTextAsync() Snapshot](guide/16-quick-reference-tables.md#analyzetextasync-snapshot)
    - [Token Behavior Summary](guide/16-quick-reference-tables.md#token-behavior-summary)
    - [Confidence Score Thresholds (guidance)](guide/16-quick-reference-tables.md#confidence-score-thresholds-guidance)
    - [JSONPath Wildcard Examples](guide/16-quick-reference-tables.md#jsonpath-wildcard-examples)
  - [17. Entity Linking (Wikipedia links from text)](guide/17-entity-linking-wikipedia-links-from-text.md)
  - [18. Import/Export Azure AI Language Projects](guide/18-import-export-azure-ai-language-projects.md)
  - [19. Foundry: Scope model access for multiple APIs](guide/19-foundry-scope-model-access-for-multiple-apis.md)
  - [Useful Links (official docs)](guide/useful-links.md)

---
