# KiwiSDR

Network of 700+ publicly-accessible 14-bit wideband HF (10 kHz – 30 MHz) software-defined radios deployed worldwide. Each Kiwi is a BeagleBone-based standalone receiver running OpenWebRX-derived firmware that streams audio + waterfall to up to 4 simultaneous browser users.

**Tier:** Free (public access to listed KiwiSDRs; hardware purchase to host your own)
**Auth:** None for public Kiwis; admin password for owner control
**Last researched:** 2026-05-09

## Use cases

- Free remote HF radio monitoring from any geographic vantage point in the global network
- TDoA (time-difference-of-arrival) signal direction finding using multiple distributed Kiwis
- WSPR, FT8, JT65, CW, RTTY, and other digital-mode decoding
- Shortwave broadcast monitoring and HF propagation studies
- Self-propagation reports for ham operators (TX locally, RX from a remote Kiwi)
- Crowd-sourced SIGINT / amateur RF observation

## Pricing

- **Free tier:** Free use of any public Kiwi listed at rx.kiwisdr.com. No account required for public receivers.
- **Paid tiers:** N/A — Kiwi is open-source software; revenue is from hardware sales.
- **Enterprise:** Hardware kits / boards / complete units sold by KiwiSDR NZ for ~$300–500 USD depending on configuration; private password-protected installations are common.
- **Notes:** Hosting a public Kiwi requires a fixed public IP, port mapping (default 8073), and ~30 GB/month outbound bandwidth for 4×24/7 streams.

## Authentication

Public Kiwis: no authentication required. Owner/admin: per-Kiwi admin password set at `kiwisdr.local:8073/admin`. Owners can also restrict their Kiwi to specific user passwords or whitelisted IPs.

## Endpoints

- **Base URL:** Each public Kiwi is at its own URL, e.g. `http://N.proxy.kiwisdr.com:8073/` or `http://owner-domain.example.com:8073/`
- **Directory:** `https://rx.kiwisdr.com/` lists all public receivers with location, frequency range, and load
- **Key interfaces:**
  - Browser UI at `:8073` — user-facing, no API key
  - WebSocket protocol for streaming I/Q + control commands (used by SDRangel, `kiwi_sdr` Dart, `SuperSDR` Python clients)
  - Pavlova dispatcher (priyom.org) — programmatic discovery of available Kiwis by region/frequency
  - Admin REST endpoints at `:8073/admin` — owner-only

## Example call

```bash
# Browser access — open in any modern browser
xdg-open "http://22274.proxy.kiwisdr.com:8073/"
```

```dart
// Dart — kiwi_sdr package
import 'package:kiwi_sdr/kiwi_sdr.dart';
await KiwiSDR.connect('http://22274.proxy.kiwisdr.com:8073/');
```

```python
# Python — kiwiclient (community library) for headless access
# pip install git+https://github.com/jks-prv/kiwiclient
from kiwi import kiwirecorder
kiwirecorder.run(host='22274.proxy.kiwisdr.com', port=8073,
                 freq=14074.0, mode='usb', user='client_test')
```

## Rate limits

Per-Kiwi: max 4 simultaneous user connections. Owners can configure inactivity time limits and per-IP daily time limits to keep slots fair. No global rate limit; there are 700+ Kiwis to round-robin across.

## SDKs / Libraries

- **Official:** Open-source firmware on GitHub (`jks-prv/KiwiSDR`).
- **Community:** `kiwiclient` (Python, headless I/Q), `kiwi_sdr` (Dart), SDRangel KiwiSDR plugin, `SuperSDR` (Python waterfall viewer with CAT support), QiwiQ (Android client), Pavlova dispatcher API.

## Documentation

- Project home: http://kiwisdr.com/
- Public Kiwi list: https://rx.kiwisdr.com/
- Quickstart guide: http://kiwisdr.com/quickstart/
- Source: https://github.com/jks-prv/KiwiSDR
- SDRangel plugin readme: https://github.com/f4exb/sdrangel/blob/master/plugins/samplesource/kiwisdr/readme.md

## Notes

- Hardware platform is BeagleBone Green/Black/AI/AI-64 + Kiwi cape; single-board, headless, web-only access.
- HF only (10 kHz – 30 MHz). For higher frequencies, look at WebSDR or OpenWebRX-on-RTL-SDR public networks.
- Built-in TDoA extension allows multi-Kiwi direction finding without external software.
- Some popular public Kiwis are heavily loaded — Pavlova dispatcher helps find free slots.
- Cross-listing: complementary to `gnss-interference` (HF anomaly observation) and to satellite SDR networks like SatNOGS for VHF/UHF amateur sat ops.
