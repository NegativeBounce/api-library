# Google Cloud Vision API

Google Cloud API for analyzing images to detect and localize objects, generate labels, and extract visual features.

**Tier:** Freemium
**Auth:** OAuth 2.0 (service account Bearer token) or API Key
**Last researched:** 2026-05-13

## Use cases

- Localizing objects with bounding polygons in still camera frames
- Generating whole-image label annotations for asset tagging and content classification
- Processing large batches of camera-captured images via async Cloud Storage integration

## Pricing

- **Free tier:** First 1,000 units/month free (all features share this quota)
- **Paid tiers:**
  - Object Localization: $2.25/1,000 units (units 1,001–5,000,000/month); $1.50/1,000 (5,000,001+/month)
  - Label Detection: $1.50/1,000 units (units 1,001–5,000,000/month); $1.00/1,000 (5,000,001+/month)
- **Enterprise:** No separate tier; contact Google Cloud sales for committed-use discounts
- **Notes:** Each image counts as one unit per feature requested. Requesting Object Localization and Label Detection on the same image = 2 units billed. Partial 1,000-unit blocks are prorated.

## Authentication

Enable the Cloud Vision API in Google Cloud Console. For production, create a service account, download the JSON key, and set `GOOGLE_APPLICATION_CREDENTIALS`. Client libraries handle token exchange automatically. For testing, pass an API Key as `?key=API_KEY`.

## Endpoints

- **Base URL:** `https://vision.googleapis.com/v1/`
- **Key endpoints:**
  - `POST /images:annotate` — synchronous annotation of one or more images (object localization, label detection, etc.)
  - `POST /images:asyncBatchAnnotate` — async batch annotation with results written to GCS
  - `POST /files:annotate` — annotate PDFs or multi-page TIFFs page by page

## Example call

```bash
curl -X POST \
  "https://vision.googleapis.com/v1/images:annotate?key=$GOOGLE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "requests": [{
      "image": {"source": {"imageUri": "https://example.com/image.jpg"}},
      "features": [{"type": "OBJECT_LOCALIZATION", "maxResults": 20}]
    }]
  }'
```

```python
from google.cloud import vision

client = vision.ImageAnnotatorClient()
image = vision.Image(source=vision.ImageSource(image_uri="https://example.com/image.jpg"))
response = client.object_localization(image=image)
for obj in response.localized_object_annotations:
    print(obj.name, obj.score, obj.bounding_poly)
```

## Rate limits

Not publicly documented as fixed per-minute values. Default quotas are managed per Google Cloud project via the Service Quotas console; increases available on request.

## SDKs / Libraries

- **Official:** Google Cloud Python, Node.js, Java, Go, C#, PHP, Ruby client libraries
- **Community:** Various REST wrappers

## Documentation

- Main docs: https://cloud.google.com/vision/docs
- API reference: https://cloud.google.com/vision/docs/reference/rest

## Notes

- `OBJECT_LOCALIZATION` returns bounding polygons; `LABEL_DETECTION` returns whole-image labels without spatial data — use both together for full signal.
- Max image: 20 MB via direct upload; no size limit for GCS URIs. Min dimensions: 1×1px.
- Supported formats: JPEG, PNG, GIF, BMP, WEBP, RAW, ICO, PDF, TIFF.
- This API analyzes still images only. For video object tracking, use the Video Intelligence API (see `google-cloud-video-intelligence.md`).
