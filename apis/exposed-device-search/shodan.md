# Shodan

The primary internet-connected device search engine — indexes banners, service fingerprints, certificates, and metadata from billions of internet-facing services worldwide, covering webcams, industrial control systems, maritime vessel networks, WiFi access points, and VSAT terminals.

**Tier:** Freemium
**Auth:** API Key
**Last researched:** 2026-05-13

## Use cases

- Searching internet-exposed devices by banner, port, geography, ASN, or vulnerability tag to identify open cameras, unsecured WiFi access points, and maritime vessel management systems
- Setting up network alerts to monitor specific IP ranges or CIDR blocks for changes in exposed services — useful for tracking vessel network exposure over time
- On-demand scanning of specific IP ranges to retrieve fresh banner data beyond the continuous scan index (paid plans)

## Pricing

- **Free tier:** Free account provides an API key with access to some endpoints (e.g., `/shodan/host/{ip}`, utility endpoints); 0 query credits included — `/shodan/host/count` is free and does not consume credits
- **Paid tiers:**
  - Freelancer — $69/month: 1M results/month (query credits); 5,120 scan credits/month; 5,120 monitored IPs; most filters (excludes vulnerability and tag search)
  - Small Business — $359/month: 20M results/month; 65,536 scan credits/month; vulnerability search included
  - Corporate — $1,099/month: unlimited query credits; 327,680 scan credits/month; all filters including tag search; batch IP lookups; premium support
  - Enterprise — custom pricing: full database access; real-time data feeds; custom solutions
- **Notes:** All API plans are subject to 1 request/second rate limit. Current subscribers receive grandfathered pricing when rates increase. On-demand scanning (`POST /shodan/scan`) requires a paid plan.

## Authentication

Create a free Shodan account at https://www.shodan.io and retrieve your API key from https://account.shodan.io. Pass as query parameter `key=<API_KEY>` on all requests.

## Endpoints

- **Base URL:** `https://api.shodan.io`
- **Key endpoints:**
  - `GET /shodan/host/{ip}` — all services and banners found on a specific IP; params: `history` (include historical banners), `minify` (return only key fields)
  - `GET /shodan/host/count` — count matching results without consuming query credits; params: `query`, `facets`
  - `GET /shodan/host/search` — search the banner database; params: `query`, `facets`, `page`, `minify`, `fields`; costs 1 query credit per filtered/paginated search
  - `GET /shodan/host/search/facets` — list available facet properties
  - `GET /shodan/host/search/filters` — list all available search filters
  - `GET /dns/domain/{domain}` — DNS records for a domain; costs 1 query credit
  - `GET /dns/resolve` — resolve hostnames to IPs; params: `hostnames` (comma-separated)
  - `GET /dns/reverse` — reverse DNS lookup; params: `ips` (comma-separated)
  - `POST /shodan/scan` — on-demand scan of specified IPs/CIDRs; costs 1 scan credit per IP (paid plans only)
  - `POST /shodan/alert` — create network monitoring alert for IP ranges
  - `GET /shodan/alert/info` — list all active alerts
  - `GET /api-info` — account plan, query credits, and scan credits remaining
  - `GET /tools/myip` — returns caller's external IP

**Shodan dork examples:** `port:554 has_screenshot:true` (RTSP cameras with screenshots), `"KVH TracPhone" port:80` (maritime VSAT terminals), `"Ubiquiti" product:"UniFi"` (WiFi access points), `"Server: Vivotek" port:80`

## Example call

```bash
# Search for exposed RTSP cameras in Singapore (free count first)
curl "https://api.shodan.io/shodan/host/count?key=$SHODAN_API_KEY&query=port%3A554+country%3ASG"

# Full search (consumes 1 query credit)
curl "https://api.shodan.io/shodan/host/search?key=$SHODAN_API_KEY&query=port%3A554+country%3ASG&minify=false"
```

```python
import shodan

api = shodan.Shodan(SHODAN_API_KEY)

# Search for maritime VSAT terminals
results = api.search("KVH TracPhone port:80", limit=100)
for match in results["matches"]:
    print(match["ip_str"], match["port"], match.get("org"), match.get("location", {}).get("country_name"))

# Single host lookup (no query credit consumed for basic lookup)
host = api.host("8.8.8.8")
print(host["org"], host["ports"])

# Count without consuming credits
count = api.count("port:37777 country:CN")  # Dahua DVR cameras in China
print(count["total"])
```

## Rate limits

All plans: 1 request/second. Query credits reset monthly. Scan credits reset monthly. Exceeding the rate limit returns HTTP 503. The `/shodan/host/count` endpoint does not consume query credits and can be polled freely within the rate limit.

## SDKs / Libraries

- **Official:** `shodan` (Python, PyPI — maintained by Shodan); `shodan` (Go, official)
- **Community:** Shodan CLI (`shodan` command after pip install); JavaScript/Node.js clients; Ruby gem

## Documentation

- REST API reference: https://developer.shodan.io/api
- Shodan dorks/filters guide: https://www.shodan.io/search/filters
- Shodan Book (developer guide): https://book.shodan.io/
- Credit types explained: https://help.shodan.io/the-basics/credit-types-explained
- Billing and plans: https://account.shodan.io/billing

## Notes

- Shodan is the most widely used internet scanning API for security research; its banner database is the most comprehensive available for non-enterprise pricing.
- Especially strong for maritime research: Shodan indexes VSAT terminal management interfaces (KVH, Cobham, Intellian, Sailor), ship AIS transponder web panels, and vessel crew WiFi router admin pages.
- The `has_screenshot:true` filter restricts results to services where Shodan captured a screenshot — directly useful for finding open camera feeds without further verification.
- Shodan Dorks for maritime/vessel WiFi: `"Sailor 800 VSAT"`, `"Fleet One"`, `"KVH CommBox"`, `"Cobham SAILOR"`, `net:<vessel_operator_IP_range>`.
- Monitor mode (`/shodan/alert`) is the most operationally useful feature for continuous exposure monitoring — set alerts on your IP ranges and receive webhooks when new services appear.
- Vulnerability search (Small Business+) maps observed service banners to known CVEs — returns hosts running vulnerable versions of specific software.
- Shodan scans the internet continuously; most IPs are re-scanned within 30 days, but popular ports (80, 443, 22) are refreshed more frequently.
