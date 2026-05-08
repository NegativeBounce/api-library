# Capella Space

A commercial Synthetic Aperture Radar (SAR) Earth observation provider with a fully automated, self-service tasking API — sub-meter SAR imagery available 24/7, all-weather, day or night, with 15-minute scheduling cycles and tasking-to-delivery in a few hours.

**Tier:** Enterprise (sales-quoted, with self-service tasking available to authorized accounts)
**Auth:** OAuth 2.0 (username/password → JWT bearer)
**Last researched:** 2026-05-07

## Use cases

- All-weather monitoring (clouds, smoke, darkness) of ports, airfields, oil and gas infrastructure, and disaster zones where optical satellites can't see.
- Maritime domain awareness — vessel detection at any time of day.
- Defense and intelligence ISR with rapid task-to-delivery (hours, not days), with FedRAMP High / CMMC L2 security posture.
- High-frequency repeat tasking with same orbit/look geometry for change detection — Capella's "maintainSceneFraming" supports cohesive image stacks.

## Pricing

- **Free tier:** None for tasking; an Open Data Program publishes selected sample SAR scenes for evaluation and research at https://www.capellaspace.com/community/data.
- **Paid tiers:** Sales-quoted, with cost calculated per-tasking-request based on:
  - **Collect mode:** Spotlight / Spotlight Ultra (highest resolution, smallest scene), Stripmap 20/50/100 (wider swath, lower resolution).
  - **Collection tier:** affects scheduling priority and bumping policy. Higher tiers cost more but get better scheduling guarantees.
  - **Scene size:** charges are based on a nominal scene size (replaced the older per-km² model in late 2022).
  - Pricing surfaced via the API as a `costPerImageEstimate` before tasking is submitted; users review and approve costs before scheduling.
- **Enterprise:** Volume contracts and reserved capacity for defense, intelligence, and large commercial customers.
- **Notes:** Capella was acquired by IonQ in 2025 — the Capella product line continues operating but corporate ownership has changed.

## Authentication

POST username + password to `/token` to receive a JWT bearer token. Token is sent as `Authorization: Bearer <token>` on all API calls. Tokens have limited lifetime; long-running workflows should refresh as needed.

## Endpoints

- **Base URL:** `https://api.capellaspace.com`
- **Key endpoints:**
  - `POST /token` — username/password → JWT.
  - `POST /task` — submit a single tasking request (GeoJSON Feature with collection type, AOI, time window, constraints).
  - `GET /task/{id}` — tasking request status and `costPerImageEstimate`.
  - `PATCH /task/{id}/status` — approve or reject a pending cost estimate.
  - `POST /repeat-requests` — submit a repeat tasking series.
  - `GET /catalog/collections` — list available STAC collections.
  - `POST /catalog/search` — STAC catalog search of archive imagery.
  - `GET /collects/list/{id}` — order metadata and asset download links.

## Example call

```bash
# 1. Authenticate
TOKEN=$(curl -s -u "$CAPELLA_USER:$CAPELLA_PASS" \
  -X POST "https://api.capellaspace.com/token" | jq -r .accessToken)

# 2. Submit a Spotlight tasking request
curl -X POST "https://api.capellaspace.com/task" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "type": "Feature",
    "geometry": {"type": "Point", "coordinates": [-77.0369, 38.9072]},
    "properties": {
      "taskingrequestName": "DC monitoring 2026-05",
      "windowOpen": "2026-05-08T00:00:00Z",
      "windowClose": "2026-05-12T00:00:00Z",
      "collectionType": "spotlight",
      "collectionTier": "standard",
      "collectConstraints": {
        "grazingAngleMin": 25,
        "grazingAngleMax": 60,
        "lookDirection": "either"
      }
    }
  }'

# 3. Once status hits review, approve the cost
curl -X PATCH "https://api.capellaspace.com/task/$TASK_ID/status" \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"code": "submitted"}'
```

## Rate limits

Not publicly itemized. The platform supports 15-minute scheduling cycles, so tasking submissions are processed quickly. Throttling is contract-tier-dependent.

## SDKs / Libraries

- **Official:** Capella Console (web), Python sample notebooks at [`capellaspace/`](https://github.com/capellaspace) on GitHub including `capella-pysdk` examples.
- **Community:** STAC clients (e.g., `pystac-client`) work directly against the catalog endpoints.

## Documentation

- Main docs: https://docs.capellaspace.com/
- Tasking docs: https://docs.capellaspace.com/constellation-tasking/tasking-requests/
- Cost review and approval: https://docs.capellaspace.com/constellation-tasking/cost-review-and-approval/
- Support / knowledge base: https://support.capellaspace.com/
- Open Data Program: https://www.capellaspace.com/community/data

## Notes

- SAR is fundamentally different from optical: amplitude images of radar backscatter, single-polarization (HH or VV depending on collect), interpretation requires SAR-specific tooling (SNAP, GAMMA, ISCE).
- Sub-0.25m resolution on Spotlight Ultra; standard Spotlight is ~0.5m; Stripmap modes trade resolution for swath.
- "15-minute scheduling cycles" + automated cost review + Inmarsat IDRS relay means tasked imagery can be delivered in a couple of hours under good conditions — among the fastest SAR pipelines commercially available.
- Cancellation policy: cancellation costs depend on how far the task has progressed in scheduling; check the active policy before canceling at scale.
- Capella is also accessible via aggregators like UP42, which may be a lower-friction starting point for occasional users.
