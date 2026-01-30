[Previous](./video-azure-video-indexer-video-processing.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./17-entity-linking-wikipedia-links-from-text.md)

# 16. Quick Reference Tables

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

[Previous](./video-azure-video-indexer-video-processing.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./17-entity-linking-wikipedia-links-from-text.md)

