# Google Cloud Video Intelligence API

Google Cloud API for detecting labels, tracking objects with bounding boxes, and identifying content in stored and streaming video.

**Tier:** Freemium
**Auth:** OAuth 2.0 (service account Bearer token) or API Key
**Last researched:** 2026-05-13

## Use cases

- Tracking individual objects with per-frame bounding boxes across stored surveillance footage
- Automated video cataloging via label detection and scene classification
- Real-time object annotation in live video streams via streaming annotation mode

## Pricing

- **Free tier:** 1,000 minutes/month of stored video annotation (shared across all features)
- **Paid tiers (stored video, per minute after free tier):**
  - Label Detection: $0.10/min
  - Object Tracking: $0.15/min
- **Paid tiers (streaming video, per minute):**
  - Label Detection: $0.12/min
  - Object Tracking: $0.17/min
- **Enterprise:** Volume discounts for 100,000+ minutes/month; contact Google Cloud sales
- **Notes:** Partial minutes billed as full minutes. Features billed independently — requesting both Label Detection and Object Tracking on the same video incurs both charges. Shot detection is free when requested alongside Label Detection.

## Authentication

Enable the Video Intelligence API in Google Cloud Console. Create a service account, download the JSON key, and set `GOOGLE_APPLICATION_CREDENTIALS`. Client libraries exchange the key for a short-lived OAuth 2.0 Bearer token automatically. Alternatively, pass an API Key as a `key` query parameter for quick testing.

## Endpoints

- **Base URL:** `https://videointelligence.googleapis.com/v1/`
- **Key endpoints:**
  - `POST /videos:annotate` — submit stored video (GCS URI) for async annotation (label detection, object tracking)
  - `GET /operations/{name}` — poll async job status and retrieve results
  - `POST /videos:annotate` with streaming config — submit streaming annotation request via bidirectional gRPC

## Example call

```bash
curl -X POST \
  "https://videointelligence.googleapis.com/v1/videos:annotate" \
  -H "Authorization: Bearer $(gcloud auth print-access-token)" \
  -H "Content-Type: application/json" \
  -d '{
    "inputUri": "gs://my-bucket/video.mp4",
    "features": ["OBJECT_TRACKING"]
  }'
```

```python
from google.cloud import videointelligence

client = videointelligence.VideoIntelligenceServiceClient()
op = client.annotate_video(
    request={
        "input_uri": "gs://my-bucket/video.mp4",
        "features": [videointelligence.Feature.OBJECT_TRACKING],
    }
)
result = op.result(timeout=300)
for track in result.annotation_results[0].object_annotations:
    print(track.entity.description, track.confidence)
```

## Rate limits

Not publicly documented as fixed values. Quotas are managed per Google Cloud project via the Service Quotas console and can be increased on request.

## SDKs / Libraries

- **Official:** Google Cloud Python, Node.js, Java, Go, C#, PHP, Ruby client libraries
- **Community:** REST integrations via any HTTP client

## Documentation

- Main docs: https://cloud.google.com/video-intelligence/docs
- API reference: https://cloud.google.com/video-intelligence/docs/reference/rest

## Notes

- Input video must be in Google Cloud Storage (`gs://`) for stored video; inline base64 bytes supported for files under 10 MB.
- `OBJECT_TRACKING` returns bounding boxes per frame; `LABEL_DETECTION` returns segment-level labels without spatial data.
- Streaming annotation requires a persistent bidirectional gRPC connection — not supported via REST.
- Entity descriptions are returned in English regardless of video language or region.
