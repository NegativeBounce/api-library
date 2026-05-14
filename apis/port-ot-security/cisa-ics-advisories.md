# CISA ICS Advisories

Free US Cybersecurity and Infrastructure Security Agency (CISA) RSS feeds providing machine-readable ICS/SCADA/OT vulnerability advisories — covering industrial control system products used in ports, terminals, maritime facilities, and critical infrastructure, issued multiple times per week.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-13

## Use cases

- Ingesting ICS/OT vulnerability advisories automatically to alert port security teams when new CVEs affect installed control system products (PLCs, HMIs, SCADA, historians)
- Filtering advisories by vendor or product to maintain a targeted feed relevant to the specific OT equipment deployed at a port facility
- Feeding ICS advisory data into MISP, SIEM platforms, or vulnerability management workflows for automated threat intelligence correlation

## Pricing

- **Free tier:** Unlimited access; no registration required
- **Paid tiers:** None
- **Enterprise:** N/A — US government public service
- **Notes:** Published under the US government open data policy; no license restrictions on use or redistribution.

## Authentication

No authentication required. Access RSS feeds directly via HTTP GET.

## Endpoints

- **ICS Advisories RSS feed:** `https://www.cisa.gov/cybersecurity-advisories/ics-advisories.xml` — all ICS/OT/SCADA advisories
- **ICS Medical Advisories RSS feed:** `https://www.cisa.gov/cybersecurity-advisories/ics-medical-advisories.xml` — ICS advisories specific to medical devices
- **Advisory listing page:** `https://www.cisa.gov/news-events/ics-advisories` — human-readable index with filtering
- **Format:** RSS 2.0; each entry includes: advisory ID (ICSA-YYYY-DDD-NN), title, affected vendor/product, CVE IDs, CVSS score, summary, and link to full advisory
- **No JSON API exists** — RSS is the native machine-readable format

## Example call

```bash
# Fetch the ICS advisories feed
curl -s "https://www.cisa.gov/cybersecurity-advisories/ics-advisories.xml" \
  | python3 -c "
import sys, xml.etree.ElementTree as ET
root = ET.parse(sys.stdin).getroot()
for item in root.findall('./channel/item'):
    print(item.find('title').text, item.find('pubDate').text)
"
```

```python
import feedparser
import re

feed = feedparser.parse("https://www.cisa.gov/cybersecurity-advisories/ics-advisories.xml")
# Filter for port-relevant vendors
PORT_VENDORS = {"Siemens", "Rockwell", "Schneider", "ABB", "Honeywell", "GE", "Yokogawa"}
for entry in feed.entries:
    if any(v in entry.title for v in PORT_VENDORS):
        print(entry.title)
        print(f"  Published: {entry.published}")
        print(f"  Link: {entry.link}")
        # Extract CVEs from summary
        cves = re.findall(r"CVE-\d{4}-\d+", entry.get("summary", ""))
        print(f"  CVEs: {cves}")
```

## Rate limits

No published rate limit. Standard US government web server throttling applies; poll no more frequently than once per hour for production pipelines.

## SDKs / Libraries

- **Official:** None — RSS feed only
- **Community:** `feedparser` (Python, PyPI) for parsing; `PyMISP_CISA_alerts` (GitHub: aleprada/PyMISP_CISA_alerts) for MISP integration; n8n workflow template for Slack notification on new advisories

## Documentation

- ICS advisories page: https://www.cisa.gov/news-events/ics-advisories
- Cybersecurity advisories hub: https://www.cisa.gov/news-events/cybersecurity-advisories
- PyMISP CISA integration: https://github.com/aleprada/PyMISP_CISA_alerts

## Notes

- CISA typically issues 10–20 ICS advisories per week covering a wide range of OT vendors; port-relevant products appear regularly including Siemens SIMATIC/SINEMA, Rockwell Automation ControlLogix, Schneider Electric EcoStruxure, ABB AC500, Honeywell Experion, and GE Digital SCADA platforms.
- Each advisory includes: affected product versions, CVE IDs, CVSS v3 score, attack vector (remote/local/physical), and recommended mitigations — sufficient for automated triage.
- Advisories follow a standardized format (ICSA-YYYY-DDD-NN identifier); the ICSA prefix indicates ICS advisory, ICSMA indicates medical device advisory.
- CISA coordinates with vendors before publishing — advisories are typically accompanied by vendor patches or mitigations at time of release.
- For integration into OT vulnerability management workflows: match advisory CVEs against the installed asset inventory from Nozomi Guardian (`nozomi-guardian.md`), Claroty xDome (`claroty-xdome.md`), or Forescout eyeInspect (`forescout-eyeinspect.md`) to identify affected devices.
- The RSS feed is the primary programmatic access path; CISA does not publish a JSON REST API for advisories as of 2026-05-13.
- CISA also publishes Known Exploited Vulnerabilities (KEV) catalog at `https://www.cisa.gov/known-exploited-vulnerabilities-catalog` — a separate high-priority feed worth monitoring alongside ICS advisories.
