# SatNOGS (Network + DB)

Open-source, distributed network of crowdsourced satellite ground stations operated by the Libre Space Foundation. Provides scheduling and observation data via the SatNOGS Network API and a community-curated database of satellite transmitter frequencies/modes via the SatNOGS DB API. The largest open archive of received satellite RF observations (waterfalls, audio, decoded telemetry) — invaluable for amateur radio satellite tracking, transmitter coordination, and satellite-RF research.

**Tier:** Free (CC BY-SA license)
**Auth:** None for read-only DB API; account token for Network scheduling
**Last researched:** 2026-05-10

## Use cases

- Looking up active satellite transmitter frequencies, modulations, baud rates, modes
- Scheduling RF observations on global ground stations (VHF, UHF, L-band, S-band)
- Downloading historical waterfalls, audio, and decoded telemetry frames
- Verifying frequency coordination claims against actual on-air observations
- Crowdsourced TLE collection and satellite identification
- CubeSat and amateur-radio mission engineering data
- Optical observation archive (newer endpoint)

## Pricing

- **Free tier:** Fully free. All API access open. Data licensed CC BY-SA.
- **Paid tiers:** None.
- **Enterprise:** None — community/non-profit project under the Libre Space Foundation.
- **Notes:** No commercial support tier; report issues via SatNOGS GitLab or community forums.

## Authentication

- **SatNOGS DB API (read):** No auth required for queries.
- **SatNOGS DB (transmitter suggestions):** Account login required to suggest transmitters; moderator review before approval.
- **SatNOGS Network (scheduling observations on ground stations):** API token from your account profile after registration at network.satnogs.org.

## Endpoints

- **DB API root:** `https://db.satnogs.org/api/`
- **Network API root:** `https://network.satnogs.org/api/`
- **Key DB endpoints:**
  - `GET /api/satellites/` — all known satellites with NORAD IDs, names, status
  - `GET /api/transmitters/` — transmitter records (uplink, downlink, mode, baud, drift)
  - `GET /api/modes/` — list of modulation/encoding modes (~70+)
  - `GET /api/telemetry/` — decoded telemetry archive
  - `GET /api/tle/` — TLE records by satellite
  - `GET /api/artifacts/` — downloadable observation artifacts
  - `GET /api/optical-observations/` — optical observation feed (newer)
- **Key Network endpoints:**
  - `GET /api/observations/` — list scheduled / completed RF observations (with filtering)
  - `POST /api/observations/` — schedule a new observation (requires API token)
  - `GET /api/stations/` — registered ground stations and their capabilities
  - `GET /api/jobs/` — observation jobs (per-station)

## Example call

```bash
# Get all transmitters for ISS (NORAD ID 25544)
curl "https://db.satnogs.org/api/transmitters/?satellite__norad_cat_id=25544"

# Get current TLE for a satellite
curl "https://db.satnogs.org/api/tle/?norad_cat_id=25544"

# List recent observations for a satellite
curl "https://network.satnogs.org/api/observations/?satellite__norad_cat_id=25544"
```

```python
import requests
# Find downlinks for AMSAT OSCAR-7 (NORAD 7530, oldest active amateur satellite)
r = requests.get(
    "https://db.satnogs.org/api/transmitters/",
    params={"satellite__norad_cat_id": 7530, "alive": "true"},
)
for tx in r.json():
    print(f"{tx['description']}: {tx['downlink_low']/1e6:.4f} MHz, mode {tx['mode']}")
```

## Rate limits

No formal published rate limits. Polite-use convention: cache TLE / transmitter data locally; don't poll the live observation list at high frequency.

## SDKs / Libraries

- **Official:** SatNOGS Client (`satnogs-client`) for ground stations; satnogs-network and satnogs-db are Django web apps with auto-documented DRF endpoints.
- **Community:**
  - `python-satnogsclient` (Python wrapper)
  - `gr-satnogs` (GNU Radio out-of-tree module for SDR demodulation)
  - Many notebooks (e.g., Daniel Estévez's AX.25 / FSK / GMSK decoders)

## Documentation

- DB API browsable root: https://db.satnogs.org/api/
- DB OpenAPI schema docs: https://db.satnogs.org/api/schema/docs/
- DB API reference: https://docs.satnogs.org/projects/satnogs-db/en/stable/api.html
- SatNOGS Wiki (DB): https://wiki.satnogs.org/SatNOGS_DB
- SatNOGS Wiki (Observations + modes): https://wiki.satnogs.org/Observations
- Project home: https://satnogs.org/
- Source (GitLab): https://gitlab.com/librespacefoundation/satnogs

## Notes

- **Source-of-truth for amateur/open satellite frequencies.** SatNOGS DB is what most modern open-source satellite trackers (Gpredict, Look4Sat, Hamsters, etc.) pull transmitter data from.
- ~70+ modulation modes catalogued. Includes APT, AX.25, BPSK, FSK, GMSK, CW, AFSK, LoRa, DUV, etc.
- Ground stations cover VHF (~144 MHz), UHF (~430 MHz), L-band (~1.2 GHz), and S-band (~2.4 GHz) typically — with additional ranges depending on individual station hardware.
- Observation artifacts include waterfall plots (PNG/HDF5), audio (OGG), and decoded telemetry (JSON).
- The Network and DB share a satellite identifier scheme (SatNOGS Satellite ID) plus NORAD Catalog Number — link them on `norad_cat_id`.
- Cross-listing: `satellite-tracking` (CelesTrak/Space-Track for orbital data), `rf-monitoring` (KiwiSDR for HF spectrum, Aaronia/CRFS for terrestrial RF). SatNOGS is uniquely the open-archive of *what was actually heard* from satellites, not just ephemerides or terrestrial RF.
