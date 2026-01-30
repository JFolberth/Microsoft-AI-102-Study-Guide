[Previous](../README.md#table-of-contents) | [Table of Contents](../README.md#table-of-contents) | [Next](./02-control-plane-rest-api-calls.md)

# 1. [File Types and Size Limitations](https://learn.microsoft.com/azure/ai-services/)

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

[Previous](../README.md#table-of-contents) | [Table of Contents](../README.md#table-of-contents) | [Next](./02-control-plane-rest-api-calls.md)

