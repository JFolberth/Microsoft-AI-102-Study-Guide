[Previous](./07-synonyms-in-document-intelligence.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./09-azure-ai-language-question-answering.md)

# 8. [Confidence Scoring (Short)](https://learn.microsoft.com/azure/ai-services/document-intelligence/concept-accuracy-confidence)

- Confidence values (0.0–1.0) appear at multiple levels: field-level, sentence-level, prediction probability.  
- Useful JSONPath patterns:
  - `$..confidence` — all confidence values  
  - `$.fields.*.confidence` — top-level fields  
  - `$.predictions[*].probability` — Custom Vision probabilities  
  - `$..confidence[?(@ < 0.7)]` — filter below threshold

Threshold guidance:
- Low: < 0.7, Medium: 0.7–0.89, High: ≥ 0.9 (service-dependent)

---

[Previous](./07-synonyms-in-document-intelligence.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./09-azure-ai-language-question-answering.md)

