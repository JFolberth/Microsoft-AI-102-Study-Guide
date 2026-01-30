[Previous](./13-semantic-kernel-prompt-template-formats.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./15-ai-search-indexing-summary.md)

# 14. [SSML for Speech — Styles & Example](https://learn.microsoft.com/azure/ai-services/speech-service/speech-synthesis-markup)

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

[Previous](./13-semantic-kernel-prompt-template-formats.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./15-ai-search-indexing-summary.md)

