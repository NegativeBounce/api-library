# PubMed E-utilities (NCBI)

NCBI's Entrez Programming Utilities — a set of REST endpoints providing programmatic access to PubMed (biomedical literature), PubMed Central (full-text open access), and 38 additional NCBI databases covering biomedical and life science research.

**Tier:** Free
**Auth:** API Key (optional; recommended)
**Last researched:** 2026-05-13

## Use cases

- Searching PubMed for biomedical, pharmacology, and clinical research literature
- Retrieving full-text articles from PubMed Central (PMC) for text mining pipelines
- Fetching citation links and related articles across NCBI databases via ELink

## Pricing

- **Free tier:** Unlimited; API key is free from NCBI account settings
- **Paid tiers:** None
- **Enterprise:** N/A
- **Notes:** Without an API key, usage is rate-limited to 3 requests/second shared by IP. API key raises this to 10 req/sec. Higher limits available on written request to info@ncbi.nlm.nih.gov.

## Authentication

API key is optional but strongly recommended. Register at https://www.ncbi.nlm.nih.gov/account/ and generate a key in account settings. Pass as `&api_key=<KEY>` query parameter.

## Endpoints

- **Base URL:** `https://eutils.ncbi.nlm.nih.gov/entrez/eutils/`
- **Key endpoints:**
  - `GET /esearch.fcgi` — query a database; returns list of matching UIDs. Params: `db`, `term`, `retmax`, `sort`, `datetype`, `mindate`, `maxdate`
  - `GET /efetch.fcgi` — retrieve full records by UID list. Params: `db`, `id`, `rettype`, `retmode`
  - `GET /esummary.fcgi` — retrieve document summaries by UID list
  - `GET /elink.fcgi` — find related records or citations across databases
  - `GET /einfo.fcgi` — list all NCBI databases or fields for a specific database
  - `GET /egquery.fcgi` — global search across all Entrez databases

**Common `db` values:** `pubmed`, `pmc`, `gene`, `nuccore`, `protein`, `mesh`

## Example call

```bash
# Step 1: search for IDs
PMIDS=$(curl -s "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esearch.fcgi?db=pubmed&term=large+language+model+medicine&retmax=10&retmode=json&api_key=$NCBI_API_KEY" \
  | python3 -c "import sys,json; print(','.join(json.load(sys.stdin)['esearchresult']['idlist']))")
# Step 2: fetch abstracts for those IDs
curl "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=pubmed&id=$PMIDS&rettype=abstract&retmode=text&api_key=$NCBI_API_KEY"
```

```python
from Bio import Entrez

Entrez.email = "you@example.com"
Entrez.api_key = NCBI_API_KEY

handle = Entrez.esearch(db="pubmed", term="large language model medicine", retmax=10)
ids = Entrez.read(handle)["IdList"]

handle = Entrez.efetch(db="pubmed", id=ids, rettype="abstract", retmode="text")
print(handle.read())
```

## Rate limits

Without API key: 3 requests/second (shared per IP). With free API key: 10 requests/second. Higher limits available on written request to info@ncbi.nlm.nih.gov. PubMed Central (PMC) E-utilities were updated in early 2026 — verify PMC-specific behavior against current docs.

## SDKs / Libraries

- **Official:** None — REST API only
- **Community:** `Biopython` (Python; `Bio.Entrez` module is the standard E-utilities wrapper); `rentrez` (R); `pymed` (Python, simplified PubMed client)

## Documentation

- General introduction: https://www.ncbi.nlm.nih.gov/books/NBK25497/
- Utilities reference: https://www.nlm.nih.gov/dataguide/eutilities/utilities.html
- API key setup: https://support.nlm.nih.gov/kbArticle/?pn=KA-05317

## Notes

- Always include `Entrez.email` or `tool` and `email` query parameters per NCBI's usage policy — requests without contact info may be blocked without notice.
- ESearch + EFetch is the standard two-step retrieval pattern: ESearch to get UIDs, EFetch to get full records.
- PubMed and PMC are separate databases: `db=pubmed` indexes citations and abstracts; `db=pmc` indexes full-text open-access articles.
- For very large dataset access (millions of records), use the NCBI FTP bulk downloads rather than E-utilities: https://ftp.ncbi.nlm.nih.gov/pub/pmc/
