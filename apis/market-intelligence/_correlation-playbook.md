# Market Intelligence — Security→Economics Correlation Playbook

> **Reference file (non-entry).** Per GOVERNANCE.md §2, this is a supporting reference for
> the `market-intelligence` category, not an API entry. It maps maritime security triggers to
> the endpoints in this folder (and cross-referenced entries elsewhere) so a report engine knows
> *which data to pull, when, and how to read it.*

**Last reviewed:** 2026-06-11

## Purpose

A maritime security event has a *signature* of economic effects that unfold on a predictable
timeline. When an event lands in a region, pull the endpoints mapped to that region's chokepoint,
compare against a pre-event baseline, and report the deltas. The size and speed of the move is
itself intelligence — and the *absence* of a move is equally diagnostic (the market is pricing the
event as noise).

## Sources referenced

In-category (`apis/market-intelligence/`): `drewry.md`, `eia.md`, `commodities-api.md`,
`alpha-vantage.md`, `imf-data.md`, `world-bank-data.md`, `project44.md`, `fourkites.md`.
Cross-referenced (other categories): `trade-flows/freightos-baltic-index.md`,
`trade-flows/xeneta.md`, `trade-flows/kpler.md`, `trade-flows/vortexa.md`,
`port-congestion/imf-portwatch.md`, `semiconductor-intelligence/fred.md`.

## Trigger → endpoint map

### 1. Chokepoint disruption (Hormuz, Bab el Mandeb, Suez, Malacca, Black Sea)

- **Energy (0–48h):** EIA petroleum spot series (Brent/WTI daily) + weekly crude stocks;
  Commodities-API real-time `BRENTOIL` / `WTIOIL` / `NG` for intraday. Hormuz hits Brent first
  (~20% of seaborne oil transits it). Bab el Mandeb is rerouting-driven, not supply-loss-driven —
  watch freight before crude.
- **Freight (2–14d):** Drewry IACI/WCI + Freightos FBX, *lane-specific*. For Red Sea / Bab el
  Mandeb, pull Asia→North Europe and Asia→Mediterranean lanes (Cape of Good Hope reroute is the
  mechanism). Drewry's IACI already benchmarks vs. "pre-Iran-conflict levels."
- **Transit volumes (2–8wk):** IMF PortWatch chokepoint transit counts — hard evidence the
  disruption is real, not just priced-in fear.

### 2. Regional unrest / sanctions on a producer or trade partner

- **Commodity-specific:** World Bank Pink Sheet (monthly) for the affected class; Commodities-API
  daily for the specific commodity (Black Sea → wheat/grain; DRC → cobalt).
- **Macro context:** IMF Data (WEO/IFS) for the country's trade exposure and currency; World Bank
  WDI for the structural picture.
- **Equity/sector:** Alpha Vantage for affected carriers / insurers / commodity producers — sector
  moves show who the market thinks is exposed.

### 3. Port operational disruption (strike, attack, congestion)

- **Real-time visibility:** Project44 / FourKites for actual shipment ETA degradation and reroute
  behavior — ground truth on whether cargo is actually disrupted.
- **Rate response:** Freightos FBX + Drewry on the affected lane.

## Timeline layering

| Horizon | What fires | Sources | Read |
|---|---|---|---|
| 0–48h | Energy/commodity spot | EIA, Commodities-API, Alpha Vantage | Immediate fear pricing |
| 2–14d | Freight rates, reroute behavior | Drewry, Freightos, Project44/FourKites | Operational reality |
| 2–8wk | Transit volumes, trade flows | IMF PortWatch, Kpler, Vortexa | Whether it's structural |
| 1–3mo | Macro, commodity indices | IMF Data, World Bank | Durable economic damage |

Example report line: "Brent +6% in 24h, FBX Asia–N.Europe +18% over 10d, Hormuz transits −40% over
3wk" — shows a broker exactly how the event is propagating across tiers.

## Implementation notes

- **Always-on baseline pollers** (no key, no rate-limit risk, no cost): EIA, IMF Data, World Bank,
  IMF PortWatch. Run these continuously to maintain the pre-event baseline.
- **Event-triggered only:** Alpha Vantage free tier is ~25 req/day — reserve for event pulls, not
  continuous polling. Alpha Vantage also ships an MCP server, so it can wire directly into a
  report-generation agent rather than via a custom connector.
- **Lane selection is everything** for freight signals — a chokepoint event only moves the lanes
  that route through (or around) it. Map each region to its affected lanes before querying.

## Maintenance

When any referenced entry's slug or scope changes, update the "Sources referenced" list. This file
has no staleness date requirement, but re-review when the category's API set changes.
