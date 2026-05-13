# Hugging Face Inference API

Hosted inference service for running open-source object detection models (DETR, YOLO, and others) via a unified REST API backed by multiple inference providers.

**Tier:** Freemium
**Auth:** Bearer token (HF User Access Token) in `Authorization` header
**Last researched:** 2026-05-13

## Use cases

- Running YOLO, DETR, or RF-DETR models without managing GPU infrastructure
- Prototyping detection pipelines against hundreds of publicly available model checkpoints
- Benchmarking architectures before committing to a dedicated deployment platform

## Pricing

- **Free tier:** $0.10/month in inference credits; Hub API rate limit: 1,000 requests per 5-minute window
- **Paid tiers:**
  - PRO: $9/month — $2.00/month in included credits; Hub API: 2,500 req/5-min
  - Team: $20/user/month — $2.00/seat/month in credits; Hub API: 3,000 req/5-min
  - Enterprise: $50+/user/month — $2.00/seat/month in credits; Hub API: 6,000 req/5-min
  - Additional credits purchasable at provider pass-through rates (no HF markup)
- **Enterprise:** Enterprise Plus tier available with up to 100,000 Hub API req/5-min
- **Notes:** Credit consumption = compute-time × hardware price. As of July 2025, the `hf-inference` native provider focuses on CPU inference; GPU-backed detection routes through third-party providers (together.ai, fireworks, etc.) at their published rates.

## Authentication

Generate a User Access Token at https://huggingface.co/settings/tokens. Pass as `Authorization: Bearer $HF_TOKEN`. To bill requests to an organization, add the `X-HF-Bill-To: <org-name>` header.

## Endpoints

- **Base URL:** `https://router.huggingface.co/hf-inference/models/` (recommended) or legacy `https://api-inference.huggingface.co/models/`
- **Key endpoints:**
  - `POST /models/{model_id}` — run inference; send image as raw bytes in the request body; task type is auto-detected from the model card

Popular object detection models:
  - `facebook/detr-resnet-50` — DETR (Detection Transformer), general-purpose
  - `hustvl/yolos-tiny` — YOLO-based transformer, lightweight
  - `Ultralytics/YOLOv8s` — YOLOv8 small
  - `roboflow/rf-detr-base` — RF-DETR (ICLR 2026), SOTA on COCO

## Example call

```bash
curl -X POST \
  "https://router.huggingface.co/hf-inference/models/facebook/detr-resnet-50" \
  -H "Authorization: Bearer $HF_TOKEN" \
  -H "Content-Type: image/jpeg" \
  --data-binary @image.jpg
```

```python
from huggingface_hub import InferenceClient

client = InferenceClient(token="$HF_TOKEN")
detections = client.object_detection("image.jpg", model="facebook/detr-resnet-50")
for d in detections:
    print(d["label"], d["score"], d["box"])
```

## Rate limits

Hub API (routing layer): Free: 1,000/5-min; PRO: 2,500/5-min; Team: 3,000/5-min; Enterprise: 6,000/5-min. Compute/inference limits are model- and provider-specific and not published as fixed values — requests consume credits until exhausted.

## SDKs / Libraries

- **Official:** Python (`huggingface_hub`, `InferenceClient`), JavaScript (`@huggingface/inference`)
- **Community:** OpenAI-compatible clients pointing to `https://router.huggingface.co/v1`

## Documentation

- Main docs: https://huggingface.co/docs/inference-providers/
- API reference: https://huggingface.co/docs/huggingface_hub/en/package_reference/inference_client

## Notes

- Model availability on `hf-inference` varies; some models are only available via third-party providers. Check each model's page for supported providers before integrating.
- Response format for `object-detection` task: `[{"label": str, "score": float, "box": {"xmin", "ymin", "xmax", "ymax"}}]`.
- Serverless inference is not suitable for latency-sensitive production workloads; use Inference Endpoints (dedicated GPU instances, $0.03–$80/hr) for SLA-backed deployments.
