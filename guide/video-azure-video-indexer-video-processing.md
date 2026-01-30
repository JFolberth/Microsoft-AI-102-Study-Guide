[Previous](./15-ai-search-indexing-summary.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./16-quick-reference-tables.md)

# Video (Azure Video Indexer & video processing)

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

[Previous](./15-ai-search-indexing-summary.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./16-quick-reference-tables.md)

