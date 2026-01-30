[Previous](./14-ssml-for-speech-styles-example.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./video-azure-video-indexer-video-processing.md)

# 15. [AI Search Indexing (Summary)](https://learn.microsoft.com/azure/search/search-what-is-azure-search)

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

[Previous](./14-ssml-for-speech-styles-example.md) | [Table of Contents](../README.md#table-of-contents) | [Next](./video-azure-video-indexer-video-processing.md)

