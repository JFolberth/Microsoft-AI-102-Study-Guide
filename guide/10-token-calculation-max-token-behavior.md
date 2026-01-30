[Previous](./09-azure-ai-language-question-answering.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./11-image-model-training-vision.md)

# 10. [Token Calculation & Max Token Behavior](https://learn.microsoft.com/azure/ai-services/openai/how-to/manage-tokens)

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

[Previous](./09-azure-ai-language-question-answering.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./11-image-model-training-vision.md)

