# Clarifai

AI platform offering pre-trained and custom-trained object detection models for images and video via a unified API.

**Tier:** Freemium
**Auth:** API Key as Bearer token (`Authorization: Key <API_KEY>` header)
**Last researched:** 2026-05-13

## Use cases

- Detecting objects across 1,000+ pre-trained categories in camera frames with no model training
- Training and deploying custom detectors for specialized domains (retail, security, medical imaging)
- Video frame-by-frame analysis via video URL input for scene understanding and event detection

## Pricing

- **Free tier:** Not publicly documented on Clarifai's pricing page; third-party sources report ~1,000 API calls/month. Rate limited to 1 req/sec.
- **Paid tiers:**
  - Essential: $30/month — 30,000 calls, 15 req/sec
  - Professional: $300/month — 100,000 calls, 100 req/sec
  - Pay-as-you-go: Pre-trained detection models $0.002/request; custom models $0.005/request; up to 100 req/sec
- **Enterprise:** Custom pricing; unlimited calls, 1,000+ req/sec, multi-cloud/on-prem, 99.99% SLA
- **Notes:** Each model invocation counts as one API call regardless of the number of objects returned.

## Authentication

Create an account at clarifai.com and generate a Personal Access Token (PAT) or App-level API key. Pass it as `Authorization: Key <API_KEY>` in all requests. PATs are recommended over app keys for multi-app access.

## Endpoints

- **Base URL:** `https://api.clarifai.com/v2/`
- **Key endpoints:**
  - `POST /users/{user_id}/apps/{app_id}/models/{model_id}/outputs` — run inference on a model with image URL or base64 input
  - `POST /users/{user_id}/apps/{app_id}/workflows/{workflow_id}/results` — chain multiple models (e.g., detect then classify)
  - `POST /users/{user_id}/apps/{app_id}/inputs` — upload images for batch processing

## Example call

```bash
curl -X POST \
  "https://api.clarifai.com/v2/users/clarifai/apps/main/models/general-image-detection/versions/1580bb1932594c93b7e2e7f19df87f2b/outputs" \
  -H "Authorization: Key $CLARIFAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"inputs":[{"data":{"image":{"url":"https://example.com/image.jpg"}}}]}'
```

```python
from clarifai_grpc.channel.clarifai_channel import ClarifaiChannel
from clarifai_grpc.grpc.api import service_pb2_grpc, service_pb2, resources_pb2

channel = ClarifaiChannel.get_grpc_channel()
stub = service_pb2_grpc.V2Stub(channel)
metadata = (("authorization", "Key $CLARIFAI_API_KEY"),)

response = stub.PostModelOutputs(
    service_pb2.PostModelOutputsRequest(
        user_app_id=resources_pb2.UserAppIDSet(user_id="clarifai", app_id="main"),
        model_id="general-image-detection",
        inputs=[resources_pb2.Input(data=resources_pb2.Data(
            image=resources_pb2.Image(url="https://example.com/image.jpg")
        ))],
    ),
    metadata=metadata,
)
for region in response.outputs[0].data.regions:
    print(region.data.concepts[0].name, region.region_info.bounding_box)
```

## Rate limits

Free: 1 req/sec. Essential: 15 req/sec. Professional / Pay-as-you-go: 100 req/sec. Enterprise: 1,000+ req/sec.

## SDKs / Libraries

- **Official:** Python (`clarifai-grpc`), Node.js, Java, PHP; REST also supported
- **Community:** Various wrappers; gRPC-native SDK recommended for production

## Documentation

- Main docs: https://docs.clarifai.com/
- API reference: https://docs.clarifai.com/api-guide/api-overview/

## Notes

- The `general-image-detection` model returns bounding boxes for 1,000+ object categories.
- Video analysis is supported by sending video URLs; Clarifai samples frames internally — frame-level control is limited.
- Pin model version IDs explicitly to avoid breaking changes when Clarifai updates a model.
- Data residency options (EU, US, custom region) available on Enterprise.
