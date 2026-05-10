# FlightAware Firehose

FlightAware's enterprise-grade real-time streaming flight data feed. Fuses ~41,000 terrestrial ADS-B receivers, Aireon's space-based ADS-B network, MLAT, datalink/ACARS, and radar into a single global stream with surface movement included. Companion to AeroAPI (REST) — Firehose is the streaming firehose, AeroAPI is the on-demand API.

**Tier:** Enterprise (Firehose) / Paid (AeroAPI sister product)
**Auth:** Username/password over SSL-secured TCP socket
**Last researched:** 2026-05-10

## Use cases

- Airline / airport / ANSP operational integration with continuous global flight state
- Air traffic management tool development requiring sub-minute latency at scale
- Predictive ETA / ETD modeling using FlightAware Foresight (ML-driven)
- 24/7 enterprise flight tracking with SLA-backed uptime
- Replay / point-in-time recovery for incident analysis (PITR feature)
- ArcGIS integration via Esri's FlightAware Firehose connector

## Pricing

- **Free tier:** Brief self-signup trial with limited historical data only. Real-time access requires sales contact.
- **Paid tiers:** Firehose pricing is custom per-customer based on (a) data scope (geographic regions, operators) and (b) data layers selected. Fixed monthly fee. AeroAPI starts ~$0.002/query (REST sister product).
- **Enterprise:** Standard route. 24/7 phone support, redundancy, high SLAs included.
- **Notes:** Australian radar/ADS-B has redistribution restrictions (internal use only).

## Authentication

Customer credentials (username/password) provisioned by FlightAware after subscription. Connection to Firehose endpoint is via SSL-secured TCP — not HTTP/REST. JSON Lines streamed as separate UTF-8 messages over the persistent socket.

## Endpoints

- **Base URL:** `firehose.flightaware.com:1501` (TCP/SSL)
- **Key interfaces:**
  - Streaming TCP/SSL socket — JSON Lines (one JSON value per newline-separated message, UTF-8)
  - Subscription layers (combinable): FlightAware Terrestrial ADS-B (worldwide), Aireon Space-Based ADS-B (worldwide), Terrestrial MLAT, Datalink/ACARS, FlightAware Foresight predictions, surface movements
  - PITR (Point-In-Time-Recovery) — resume a connection from where it dropped, or replay historical windows
  - Esri ArcGIS connector for GeoEvent Server
  - Companion REST API: AeroAPI (`https://aeroapi.flightaware.com/aeroapi/`)

## Example call

Firehose is not a traditional REST API. The session is established over TCP/SSL, with login and live commands sent as JSON-Lines.

```bash
# Establish SSL connection (login command schema simplified)
openssl s_client -connect firehose.flightaware.com:1501 << 'EOF'
{"command":"live","username":"YOURUSER","password":"YOURPASS"}
EOF
```

```python
# Python — using FlightAware's reference Firehose client pattern
import socket, ssl, json
ctx = ssl.create_default_context()
sock = socket.create_connection(("firehose.flightaware.com", 1501))
ssock = ctx.wrap_socket(sock, server_hostname="firehose.flightaware.com")
ssock.sendall(json.dumps({"command":"live","username":USER,"password":PASS}).encode() + b"\n")
buf = b""
while True:
    chunk = ssock.recv(4096)
    if not chunk: break
    buf += chunk
    while b"\n" in buf:
        line, buf = buf.split(b"\n", 1)
        if line.strip():
            print(json.loads(line))
```

## Rate limits

No traditional rate limit — Firehose is a streaming feed sized to your subscription scope. Throughput is bound by data layers selected and geographic region (a single global stream of all ADS-B + MLAT + datalink can be tens of MB/s).

## SDKs / Libraries

- **Official:** Reference clients in Python, C++, and Go are documented. Esri ArcGIS GeoEvent Server connector.
- **Community:** Various open wrappers, but most enterprise users implement against the documented JSON Lines protocol directly.

## Documentation

- Product page: https://www.flightaware.com/commercial/firehose/
- Documentation Center: https://www.flightaware.com/commercial/firehose/documentation
- Sister product (AeroAPI): https://www.flightaware.com/commercial/aeroapi/
- Esri connector: https://go.flightaware.com/esriconnector
- Getting started blog: https://blog.flightaware.com/getstartedwithfirehose

## Notes

- Layer-based pricing means you only pay for the data you consume (e.g., terrestrial ADS-B only, or full-stack with Aireon space-based + MLAT + datalink + Foresight predictions).
- PITR is the killer feature for production systems — short network blip doesn't lose data because you can resume from your last cursor.
- Aireon space-based ADS-B integration gives ocean / polar / desert coverage where terrestrial receivers can't reach.
- AeroAPI is REST + JSON, suitable for episodic queries or web dashboards; Firehose is for high-throughput continuous integration.
- Cross-listing: AeroAPI (sister REST product) covers similar use cases at lower throughput. `gnss-interference` already has Flightradar24 — the closest competitor here.
