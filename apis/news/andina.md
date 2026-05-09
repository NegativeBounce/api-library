# Andina (English) — Andean News Agency

The English-language service of Peru's official state news agency (Agencia Peruana de Noticias Andina), operated by Editora Perú S.A. — the Peruvian state media company. Reports on Peru and the Andean region in English with high domain authority and broad domestic coverage.

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Peru official state perspective on domestic politics, economy, and Andean regional affairs
- Tracking Peruvian government statements, ministry announcements, presidential affairs, congressional events
- Andean-region news (Bolivia, Ecuador edges) with Lima editorial perspective
- Building Latin America news monitors with Peru state-source coverage; complements MercoPress regional coverage

## Pricing

- **Free tier:** Full English website free; RSS access (verify per-section endpoints)
- **Paid tiers:** None for general news consumption
- **Enterprise:** Wire/syndication services via Editora Perú; contact `editoraperu.com.pe`
- **Notes:** Funded by the Peruvian state via Editora Perú S.A.; not a metered or paywalled service

## Authentication

None.

## Endpoints

- **Base URL:** `https://andina.pe/`
- **Key endpoints:**
  - English service landing: `https://andina.pe/ingles/`
  - Section pages (HTML, free): politics, economy, society, regions, sports, tourism, culture
  - RSS feeds are referenced by third-party RSS aggregators; verify exact endpoint paths via the English landing page footer or contact `editoraperu.com.pe`

## Example call

```bash
# English service landing page
curl "https://andina.pe/ingles/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** None — official Andina mobile apps are consumer-facing
- **Community:** Standard RSS parsers

## Documentation

- Main site (Spanish): https://andina.pe/
- English service: https://andina.pe/ingles/
- Parent company contact: `editoraperu.com.pe`

## Notes

Andina is the **official news agency of the Peruvian state**, operated by **Editora Perú S.A.** — Peru's state-owned media holding company. For source-trust analysis: this is **state media** and should be flagged as such; editorial line tracks Peruvian government communications, official ministry releases, and presidential agenda. Note that "Andina" colloquially refers to Andean (mountainous) topics in Spanish — not to be confused with the Andean Community of Nations (CAN); the agency does occasionally cover the broader Andean region but primary focus is Peru. Useful as a primary-source channel for understanding **official Peruvian framing** of regional events including Pacific Alliance, APEC, and US-Peru relations. **Coverage gaps:** lighter on opposition perspectives, investigative reporting, and stories critical of the current administration. Pair with independent sources like Peru Reports (English) or Caretas/Gestión (Spanish) for editorial balance. No public REST/JSON developer API documented; English RSS surface is referenced by aggregators but specific endpoint paths require verification at integration time.
