# CDDIS / IGS

NASA's Crustal Dynamics Data Information System (CDDIS) is the principal global archive for GNSS observation data, broadcast ephemerides, and IGS (International GNSS Service) products. Multi-decade RINEX archive from a worldwide network of 500+ permanent ground-based receivers — the source-of-truth for GNSS research, geodesy, and (increasingly) GNSS interference detection studies. Mirrors at IGN (France) and ESA GSSC for redundancy.

**Tier:** Free
**Auth:** NASA Earthdata Login (URS) over HTTPS or FTP-SSL
**Last researched:** 2026-05-10

## Use cases

- GNSS interference / jamming / spoofing detection research using high-rate (1 Hz) RINEX archives
- Precise point positioning (PPP) and post-processing using IGS ultra-rapid / rapid / final orbits and clocks
- Ionospheric / tropospheric studies via IGS atmospheric products
- Multi-GNSS monitoring (GPS, GLONASS, Galileo, BeiDou, QZSS, IRNSS/NavIC, SBAS) using MGEX merged broadcast nav files
- Receiver / antenna benchmarking against IGS reference stations
- Earth rotation parameters and station position time series for geodesy

## Pricing

- **Free tier:** Fully free. Full archive access included with an Earthdata Login account.
- **Paid tiers:** None.
- **Enterprise:** None — operated as a NASA EOSDIS DAAC under public funding.
- **Notes:** Citation required for any publication using CDDIS data — see Earthdata catalog DOIs (e.g., `10.5067/GNSS/GNSS_DAILY_G_001`).

## Authentication

NASA Earthdata Login (URS) single sign-on. Anonymous FTP was discontinued on October 31, 2020 due to US Government security requirements. Two access methods now supported:

1. **HTTPS** (preferred) — TLS-secured, single-port, fewer firewall issues
2. **FTP-SSL** — TLS-secured FTP for legacy script compatibility

Both methods require an Earthdata account at `https://urs.earthdata.nasa.gov/` and a `.netrc` file for command-line tools.

## Endpoints

- **Base URL (HTTPS archive):** `https://cddis.nasa.gov/archive/`
- **Base URL (FTP-SSL):** `ftp://gdc.cddis.eosdis.nasa.gov/`
- **Earthdata catalog (search/discovery):** `https://www.earthdata.nasa.gov/centers/cddis-daac`
- **Mirror (IGN, France):** `ftp://igs.ign.fr/pub/igs/`
- **Mirror (ESA GSSC):** `ftp://gssc.esa.int/gnss/`
- **Key directory paths (from archive root):**
  - `/gnss/data/daily/YYYY/DDD/YYo/` — daily 30-second observation RINEX files (one per site)
  - `/gnss/data/hourly/YYYY/DDD/HH/` — hourly 30-second observation files
  - `/gnss/data/highrate/YYYY/DDD/YYd/HH/` — sub-hourly high-rate (1-second) observation files (great for interference / scintillation studies)
  - `/gnss/data/daily/YYYY/DDD/YYn/brdcDDD0.YYn.Z` — daily merged GPS broadcast ephemeris (RINEX V2)
  - `/gnss/data/daily/YYYY/DDD/YYg/` — daily GLONASS broadcast ephemeris
  - `/gnss/data/daily/YYYY/DDD/YYp/BRDC00IGS_R_YYYYDDD0000_01D_MN.rnx.gz` — daily merged multi-GNSS broadcast (RINEX V3)
  - `/gnss/products/WWWW/` — IGS products by GPS week (orbits/clocks/ERP/SINEX)

## Example call

```bash
# One-time setup
echo "machine urs.earthdata.nasa.gov login YOURUSER password YOURPASS" > ~/.netrc
chmod 600 ~/.netrc

# List files in a daily directory
curl -c ~/.urs_cookies -b ~/.urs_cookies -n -L \
  "https://cddis.nasa.gov/archive/gnss/data/daily/2026/130/26o/*?list"

# Download a single daily 30-second observation file
curl -c ~/.urs_cookies -b ~/.urs_cookies -n -L -O \
  "https://cddis.nasa.gov/archive/gnss/data/daily/2026/130/26o/abmf1300.26o.gz"

# Download a daily merged multi-GNSS broadcast nav file (RINEX 3)
curl -c ~/.urs_cookies -b ~/.urs_cookies -n -L -O \
  "https://cddis.nasa.gov/archive/gnss/data/daily/2026/130/26p/BRDC00IGS_R_20261300000_01D_MN.rnx.gz"
```

```python
# Python with requests + .netrc
import requests, netrc
auth = netrc.netrc().authenticators("urs.earthdata.nasa.gov")
s = requests.Session()
s.auth = (auth[0], auth[2])
url = "https://cddis.nasa.gov/archive/gnss/data/daily/2026/130/26o/abmf1300.26o.gz"
r = s.get(url, allow_redirects=True)
open("abmf1300.26o.gz", "wb").write(r.content)
```

## Rate limits

No formal per-account rate limits are published. CDDIS expects polite use — automated scripts should rate-limit themselves and avoid full-archive scrapes. NASA reserves the right to throttle abusive traffic.

## SDKs / Libraries

- **Official:** None proprietary; CDDIS provides example cURL/Wget/Python/Java snippets in their access docs.
- **Community:**
  - `gnsspy`, `gnsscal`, `georinex` (Python — RINEX parsing)
  - `RTKLIB` (C/C++ — full GNSS post-processing toolkit, native CDDIS support)
  - `gpys`, `pyrinex` and many others on PyPI
  - `gLAB` (ESA precise positioning toolkit)

## Documentation

- CDDIS landing (Earthdata-hosted as of June 2025): https://www.earthdata.nasa.gov/centers/cddis-daac
- Archive access guide: https://www.earthdata.nasa.gov/centers/cddis-daac/archive-access
- Archive root: https://cddis.nasa.gov/archive/
- Web Unification notice: https://cddis.nasa.gov/Web_Unification.html
- File-download FAQ (Earthdata Forum): https://forum.earthdata.nasa.gov/viewtopic.php?t=6745
- IGS Access to Products: https://igs.org/products-access/
- Earthdata Login portal: https://urs.earthdata.nasa.gov/

## Notes

- **Web Unification (June 2025):** the cddis.nasa.gov web pages have been migrated to the Earthdata website, but the **archive URL `https://cddis.nasa.gov/archive/` remains stable**. Existing scripts continue to work without changes.
- **High-rate (1-second) data is the GNSS interference / spoofing researcher's friend** — 285+ stations, 96 files/site/day, ~25 GB/day, ~9.1 TB/year — pinpoint the time and location of jamming events at sub-second resolution.
- IGS produces ultra-rapid (predicted) orbits 4×/day, rapid combined orbits with ~17-hour latency, and final products with longer latency. Choose by your latency requirement.
- MGEX (Multi-GNSS Experiment) extended IGS to non-GPS systems starting in 2011 — Galileo, BeiDou, QZSS, IRNSS, and SBAS broadcast and observation data are all archived.
- Mirror chain: when CDDIS is slow or unreachable, IGN (`igs.ign.fr`) and ESA GSSC (`gssc.esa.int`) are fully synchronized alternatives — use them as fallbacks in production scripts.
- Cross-listing: directly relevant to `gnss-interference` (raw data underlying GPSJAM, Zephr, Hidden Level analytics).
