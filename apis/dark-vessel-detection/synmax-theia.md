# SynMax Theia

Maritime intelligence platform fusing AIS with daily satellite imagery (Planet, others) to detect dark vessels, ship-to-ship transfers, AIS spoofing, and loiter/rendezvous behaviour. Documented REST API at `apidocs.theia.synmax.com`.

**Tier:** Paid (subscription)
**Auth:** API Key / token (issued via Theia workspace)
**Last researched:** 2026-05-09

## Use cases

- Dark-vessel detection in the Strait of Malacca approaches — Theia compares AIS-reported positions against satellite-derived vessel detections to flag mismatches.
- Ship-to-ship transfer monitoring — Theia detected 94.6K STS events globally in 2024.
- AIS spoofing detection — identity-switch and location-spoof flagging.
- Behavioural analytics on a target fleet (loiter, anchorage time, rendezvous).
- White-label / reseller integration via Theia Partner program.

## Pricing

- **Free tier:** None publicly available.
- **Paid tiers:** Tiered subscription pricing (not publicly listed). Reseller margins available via Partner program.
- **Enterprise:** Custom contracts; US Navy and other defense customers cited.
- **Notes:** Pricing is sales-led; expect a demo + scoping cycle.

## Authentication

API key / token issued via the Theia workspace after subscription. Specifics are documented in the Theia developer docs (apidocs.theia.synmax.com).

## Endpoints

- **Workspace login:** `https://theia.synmax.com/`
- **API docs:** `https://apidocs.theia.synmax.com/`
- **Surface areas:**
  - Vessel detections (AIS + SAR/optical fusion)
  - AIS-dark detections (vessels visible in imagery without AIS)
  - Ship-to-ship transfer events
  - Vessel attribution (data automatically attributed; user can manually alter)
  - Workspace queries / saved AOIs

## Example call

```bash
# Illustrative — actual endpoint and auth in the Theia API docs.
curl -H "Authorization: Bearer $THEIA_TOKEN" \
  "https://api.theia.synmax.com/v1/detections?bbox=-2.0,99.0,6.0,105.5&date=2026-05-08"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None broadly published; REST API.
- **Community:** None notable.

## Documentation

- Theia product page: https://www.synmax.com/theia/
- API docs: https://apidocs.theia.synmax.com/
- SynMax Maritime: https://www.synmax.com/synmax-maritime/

## Notes

- Theia's differentiator is daily 20M+ km² satellite imagery fused with AIS — strong for the Strait given heavy traffic + frequent revisit.
- SynMax was awarded a US Navy contract renewal for vessel detection and monitoring (2025).
- Often listed alongside Windward, HawkEye 360, and Pole Star in maritime fusion-platform RFPs.
