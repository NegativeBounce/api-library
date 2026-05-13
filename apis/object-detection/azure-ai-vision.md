# Azure AI Vision

Microsoft Azure computer vision service for detecting objects, generating tags, and extracting visual features from images.

**Tier:** Freemium
**Auth:** API Key (`Ocp-Apim-Subscription-Key` header) or Azure Entra ID Bearer token
**Last researched:** 2026-05-13

## Use cases

- Extracting object bounding boxes and tags from surveillance camera still frames
- Generating descriptive captions for images in a content moderation or asset management pipeline
- Automated visual inspection in manufacturing or logistics workflows

## Pricing

- **Free tier:** 5,000 transactions/month (F0 tier)
- **Paid tiers:** Standard tier (S1): ~$1.50/1,000 transactions for Analyze operations; each feature selected in a single Analyze call counts as one transaction per feature
- **Enterprise:** No separate named tier; volume discounts via Microsoft agreement
- **Notes:** Verify current rates at https://azure.microsoft.com/en-us/pricing/details/computer-vision/ — pricing is subject to change. Image Analysis 4.0 (API v4.0) is deprecated and retires 2028-09-25; see Notes.

## Authentication

Create an Azure AI Vision resource in the Azure portal. Use the resource key in the `Ocp-Apim-Subscription-Key` header, or obtain a Bearer token via Azure Entra ID. The base URL is resource-specific, not a global endpoint.

## Endpoints

- **Base URL:** `https://<your-resource-name>.cognitiveservices.azure.com/vision/v3.2/`
- **Key endpoints:**
  - `POST /analyze?visualFeatures=Objects,Tags` — detect objects with bounding boxes and generate image tags
  - `POST /analyze?visualFeatures=Objects,Tags,Description` — includes auto-generated image caption
  - `POST /analyze?model-name=<custom_model>` — run a custom-trained object detection model

## Example call

```bash
curl -X POST \
  "https://myresource.cognitiveservices.azure.com/vision/v3.2/analyze?visualFeatures=Objects,Tags" \
  -H "Ocp-Apim-Subscription-Key: $AZURE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"url": "https://example.com/image.jpg"}'
```

```python
from azure.cognitiveservices.vision.computervision import ComputerVisionClient
from msrest.authentication import CognitiveServicesCredentials

client = ComputerVisionClient(
    "https://myresource.cognitiveservices.azure.com/",
    CognitiveServicesCredentials("$AZURE_API_KEY")
)
result = client.analyze_image(
    "https://example.com/image.jpg",
    visual_features=["Objects", "Tags"]
)
for obj in result.objects:
    print(obj.object_property, obj.confidence, obj.rectangle)
```

## Rate limits

Not publicly documented as fixed values for the standard tier. Free tier (F0): hard cap of 20 requests/minute. Standard tier limits are managed per resource in the Azure portal; request increases via Azure Support.

## SDKs / Libraries

- **Official:** Azure SDK for Python (`azure-cognitiveservices-vision-computervision`), .NET, Java, JavaScript, Go
- **Community:** Various REST wrappers

## Documentation

- Main docs: https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/
- API reference: https://learn.microsoft.com/en-us/rest/api/computervision/

## Notes

- **Deprecation:** Image Analysis 4.0 (API v4.0) is deprecated as of 2025 and retires 2028-09-25. Microsoft recommends migrating — see https://learn.microsoft.com/en-us/azure/ai-services/computer-vision/migration-options. API v3.2 (documented above) has no announced retirement date as of this research date.
- Supported formats: JPEG, PNG, GIF, BMP. Max file size 4 MB. Min dimensions 50×50px.
- For real-time video analysis, combine with Azure AI Video Indexer (separate product and billing).
