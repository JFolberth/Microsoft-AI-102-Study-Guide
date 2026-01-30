[Previous](./06-azure-security-key-rotation.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./08-confidence-scoring-short.md)

# 7. [Synonyms in Document Intelligence](https://learn.microsoft.com/azure/ai-services/document-intelligence/concept-custom)

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

[Previous](./06-azure-security-key-rotation.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./08-confidence-scoring-short.md)

