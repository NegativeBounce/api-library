# Amazon Rekognition

AWS managed computer vision service for detecting objects, scenes, text, and activities in images and stored or streaming video.

**Tier:** Freemium
**Auth:** AWS IAM (Access Key + Secret); requests signed with SigV4, handled automatically by AWS SDKs
**Last researched:** 2026-05-13

## Use cases

- Labeling objects and scenes in camera frames ingested via Kinesis Video Streams
- Batch analysis of stored video for content tagging and moderation
- Detecting PPE compliance, crowd density, or vehicle types in surveillance footage

## Pricing

- **Free tier:** 1,000 images/month + 60 minutes of stored video/month for the first 12 months after AWS account creation
- **Paid tiers:**
  - Images (DetectLabels — Group 2 API): $1.00/1,000 images (first 1M), $0.80/1,000 (next 4M), $0.60/1,000 (next 30M), $0.40/1,000 (over 65M)
  - Stored video (StartLabelDetection): $0.10/min
  - Streaming video via Kinesis Video Streams: $0.00817/min
- **Enterprise:** No separate tier; high-volume pricing via AWS account team
- **Notes:** Each additional feature flag (e.g., IMAGE_PROPERTIES alongside DetectLabels) is billed as a separate API call. Stored video billed per video processed, not per object detected.

## Authentication

Use AWS IAM credentials (access key ID + secret access key) with SigV4 request signing. AWS SDKs handle signing automatically. Grant `rekognition:DetectLabels` (and equivalent) permissions via IAM policy. No separate API key — credentials flow through the standard AWS credential chain.

## Endpoints

- **Base URL:** `https://rekognition.<region>.amazonaws.com/`
- **Key endpoints:**
  - `POST /` with target `RekognitionService.DetectLabels` — detect objects/scenes in a single image
  - `POST /` with target `RekognitionService.StartLabelDetection` — async object detection on stored video (S3)
  - `POST /` with target `RekognitionService.GetLabelDetection` — poll/retrieve async video job results
  - `POST /` with target `RekognitionService.CreateStreamProcessor` — configure live Kinesis Video Streams processing

## Example call

```bash
aws rekognition detect-labels \
  --image '{"S3Object":{"Bucket":"my-bucket","Name":"frame.jpg"}}' \
  --max-labels 20 \
  --min-confidence 70 \
  --region us-east-1
```

```python
import boto3
client = boto3.client("rekognition", region_name="us-east-1")
resp = client.detect_labels(
    Image={"S3Object": {"Bucket": "my-bucket", "Name": "frame.jpg"}},
    MaxLabels=20,
    MinConfidence=70,
)
for label in resp["Labels"]:
    print(label["Name"], round(label["Confidence"], 2), label.get("Instances", []))
```

## Rate limits

Default: 50 TPS for `DetectLabels`. Each API operation has its own default TPS quota per region, adjustable via AWS Support. Stored video: max 20 concurrent jobs per account.

## SDKs / Libraries

- **Official:** AWS SDK for Python (boto3), JavaScript/Node.js, Java, .NET, Go, Ruby, PHP, C++
- **Community:** Terraform AWS provider (stream processor management)

## Documentation

- Main docs: https://docs.aws.amazon.com/rekognition/latest/dg/
- API reference: https://docs.aws.amazon.com/rekognition/latest/APIReference/

## Notes

- Supported image formats: JPEG, PNG. Raw bytes max 5 MB; S3 objects up to 15 MB.
- Stored video: H.264 codec (MPEG-4 or MOV), max 10 GB, max 6 hours.
- Streaming: input must be a Kinesis Video Stream; results delivered to a Kinesis Data Stream.
- Custom Labels (train your own detector): separate product; $1.00/training hour, $4.00/inference hour.
