# Roboflow

Computer vision platform for training, deploying, and running custom object detection models via a serverless hosted inference API.

**Tier:** Freemium
**Auth:** API Key as `api_key` query parameter
**Last researched:** 2026-05-13

## Use cases

- Deploying custom-trained YOLO or RF-DETR models for domain-specific detection (defect inspection, custom vehicle classes, security)
- Running serverless inference on camera frames without managing GPU infrastructure
- Building and versioning training datasets alongside model deployments in a single platform

## Pricing

- **Free tier:** Public plan — $60/month in included credits; all datasets and models publicly visible on Roboflow Universe
- **Paid tiers:**
  - Core: $79/month — private data and models, training analytics, downloadable weights, $60/month in credits
- **Enterprise:** Custom pricing; commercial edge deployment, RBAC, workflow versioning, model monitoring, priority GPU access
- **Notes:** Credits reset monthly (or annually on annual plans). Credit consumption rate depends on model size and inference hardware. Do not upload proprietary imagery on the free plan — all data is public.

## Authentication

Sign up at roboflow.com and retrieve your API key from Project Settings. Pass it as `?api_key=<API_KEY>` in the query string. Keys are project-scoped for custom models; Roboflow Universe models use your account key.

## Endpoints

- **Base URL:** `https://serverless.roboflow.com/`
- **Key endpoints:**
  - `POST /{project_id}/{version}?api_key={API_KEY}` — run a trained model version; post image as base64 JSON body or multipart form
  - `POST /infer/object_detection?api_key={API_KEY}` — run Roboflow's foundation detection model without custom training

## Example call

```bash
BASE64=$(base64 -w 0 image.jpg)
curl -X POST \
  "https://serverless.roboflow.com/my-project/1?api_key=$ROBOFLOW_API_KEY" \
  -H "Content-Type: application/json" \
  -d "{\"image\": \"$BASE64\"}"
```

```python
import roboflow

rf = roboflow.Roboflow(api_key="$ROBOFLOW_API_KEY")
model = rf.workspace().project("my-project").version(1).model
result = model.predict("image.jpg", confidence=40, overlap=30).json()
for pred in result["predictions"]:
    print(pred["class"], pred["confidence"], pred["x"], pred["y"])
```

## Rate limits

Not publicly documented as fixed values. Requests continue until credit balance is exhausted. Enterprise tier includes priority GPU access with SLA-backed availability.

## SDKs / Libraries

- **Official:** Python (`roboflow`), REST API
- **Community:** `inference` open-source self-hosting runtime (https://github.com/roboflow/inference); Node.js wrappers

## Documentation

- Main docs: https://docs.roboflow.com/
- API reference: https://docs.roboflow.com/deploy/hosted-api/

## Notes

- The open-source `inference` package allows self-hosting the same runtime on edge devices (Raspberry Pi, NVIDIA Jetson) with no API calls or cloud dependency.
- RF-DETR (ICLR 2026), Roboflow's SOTA detection architecture, is available for training and deployment on the platform.
- Roboflow Universe (https://universe.roboflow.com) offers thousands of pre-trained public models usable directly via the API.
- Models can be exported (ONNX, CoreML, TensorFlow Lite, etc.) for off-platform or edge deployment.
- Free plan exposes all data publicly — do not upload proprietary or sensitive imagery on the free plan.
