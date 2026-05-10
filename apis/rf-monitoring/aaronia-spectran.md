# Aaronia SPECTRAN / RTSA-Suite PRO

German-engineered real-time spectrum analyzer hardware (SPECTRAN V3/V4/V5/V6 series, NF-series, plus AARTOS drone-detection systems) paired with RTSA-Suite PRO software that exposes blocks for HTTP server/client, scripting, IQ streaming, and pulse classification.

**Tier:** Paid (hardware + free base software; paid software blocks for advanced features)
**Auth:** Local — software runs against connected SPECTRAN device; no cloud auth (HTTP server has optional auth)
**Last researched:** 2026-05-09

## Use cases

- Real-time RF spectrum monitoring up to 245 MHz RTBW (single V6) / ~20 GHz (multi-coupled)
- IQ/Spectra recording for forensic radio analysis (24/7 long-duration to SSD)
- Drone detection (AARTOS) with integrated camera and jammer control
- Automated pulse classification (decodes WiFi, BT, GSM, DECT, QPSK, QAM)
- Scripted / programmatic SDR workflows via HTTP server block + Python or MATLAB

## Pricing

- **Free tier:** Base RTSA-Suite PRO is included free with SPECTRAN V6 hardware purchase. Free blocks: HTTP server (1×), HTTP client (1×), AM/FM demod, file writer/reader, IQ processing, triggers, scripts.
- **Paid tiers:** Hardware sold per unit (V6 starts low-thousands USD; AARTOS systems much more). Additional RTSA-Suite PRO blocks purchasable à la carte.
- **Enterprise:** AARTOS drone-defense bundles, multi-V6 coupling for wider RTBW, custom integration via Aaronia distributors.
- **Notes:** AARTOS systems should not be auto-updated to latest RTSA — Aaronia warns it can break the system.

## Authentication

Local USB/network connection between PC and SPECTRAN device — no API key. RTSA-Suite PRO exposes an HTTP Stream Server (default `http://localhost:54664/stream`) that can be called from external scripts; auth is optional and configured per-deployment.

## Endpoints

- **Base URL (local):** `http://localhost:54664` (RTSA HTTP server, port configurable)
- **Key endpoints / interfaces:**
  - `GET /stream?format=int16&scale=1000000` — live IQ/spectra stream
  - HTTP server block — remote-control commands to running RTSA mission
  - `.rtsa` binary file format — IQ + SPECTRA recordings, chunk-based, optionally Rice-compressed
  - MATLAB integration — full bidirectional via RTSA-Suite PRO blocks

## Example call

```bash
# Live spectra stream from a running RTSA-Suite PRO instance
curl "http://localhost:54664/stream?format=int16&scale=1000000" --output spectra.bin
```

```python
# Load an .rtsa IQ file in Python (uncompressed)
import numpy as np
# RTSA file format is documented in Aaronia's PDF; chunk-based, similar to PNG
with open("capture.rtsa", "rb") as f:
    header = f.read(...)  # parse per Aaronia spec
    iq = np.frombuffer(f.read(), dtype=np.complex64)
```

## Rate limits

Bound by hardware and PC USB throughput, not API quotas. Multi-V6 coupling scales horizontally.

## SDKs / Libraries

- **Official:** RTSA-Suite PRO (Windows, Linux; macOS in development), MCS software (older V3/V4/NF series), full MATLAB support, .rtsa file-format documentation.
- **Community:** Python parsers for the `.rtsa` binary format; SPECTRAN V6 forum has SDK/API/remote-control discussions.

## Documentation

- Product page: https://aaronia.com/en/products/software/rtsa-software
- Downloads + manuals: https://aaronia.com/en/support/downloads
- Quick guide PDF: https://downloads.aaronia.com/manuals/V6-RTSA_Suite-PRO_Quick-Guide.pdf
- Software blocks PDF: https://downloads.aaronia.com/manuals/RTSA-Suite_PRO_Software-Blocks.pdf
- SDK / API forum: https://v6-forum.aaronia.de/forum/topic/rtsa-suite-pro-file-format/
- US distributor: https://aaroniausa.com/

## Notes

- Aaronia AG is based in Strickscheid, Germany; AaroniaUSA is the North American distributor.
- POI (Probability of Intercept) of 10 ns / 97 ns via FFT — competitive with bench analyzers costing 10×+ at the low end.
- The RTSA HTTP Stream Server has known limitations for live downstream evaluation (per forum threads); consider direct file ingest for production analytics.
- Cross-listing applies to `bluetooth-intelligence` (BT pulse decoding) and `wifi-intelligence` (WiFi pulse decoding).
