# Baltic Exchange

The benchmark authority for dry bulk, tanker and container freight market information, publishing indices (BDI, BDTI, BCTI, FBX) via its information-services subsidiary (BEISL).

**Tier:** Enterprise
**Auth:** License / API (via BEISL / vendors)
**Last researched:** 2026-06-11

## Use cases

- Sourcing authoritative dry-bulk and tanker freight indices (e.g. Baltic Dry Index, Baltic Dirty/Clean Tanker Indices) for shipping-market and commodity-flow context.
- Benchmarking freight derivatives and contracts (Baltic indices underpin the freight derivatives / FFA market).
- Adding index-grade freight cost signals to intelligence reports for shipping, mining-platform and salvage personas.
- Container freight via the FBX (administered by BEISL with Freightos as Calculating Agent).

## Pricing

- **Free tier:** Limited headline figures publicly referenced; full data is licensed.
- **Paid tiers:** Membership/subscription to BEISL for freight market information.
- **Enterprise:** Licences for clearing houses, information vendors and software/application providers; API/data feeds via BEISL or authorized vendors.
- **Notes:** Pricing not public. The Baltic Exchange derives revenue from membership and information licences.

## Authentication

License-based access via Baltic Exchange Information Services Ltd (BEISL); data feeds/API provisioned per licence, or accessed through authorized information vendors.

## Endpoints

- **Base URL:** Provided per BEISL licence / via authorized vendors.
- **Key data:**
  - Dry bulk indices (Baltic Dry Index and sub-indices: Capesize, Panamax, Supramax, Handysize).
  - Tanker indices (Baltic Dirty Tanker Index, Baltic Clean Tanker Index).
  - Container: FBX (Freightos Baltic Index), administered by BEISL.

## Example call

```bash
# No public self-serve API. Data accessed under BEISL licence or via authorized
# information vendors (e.g. financial market data providers).
```

## Rate limits

Per licence/vendor; not publicly published.

## SDKs / Libraries

- **Official:** Data distributed via licence and vendor feeds; no public SDK.
- **Community:** None notable.

## Documentation

- Main docs: https://www.balticexchange.com/
- Reference: FBX Guide (BEISL) — https://www.balticexchange.com/ (data-services documentation)

## Notes

- The historical authority on freight benchmarks; indices are the reference for the freight derivatives market.
- **Cross-reference:** the container index it co-administers is cataloged separately as Freightos Baltic Index (`trade-flows/freightos-baltic-index.md`). This entry covers the **dry-bulk + tanker** indices and the Baltic's overall data-services role.
- For physical commodity flows (vs. freight price indices) use Kpler/Vortexa; for official customs trade stats use UN Comtrade (`semiconductor-intelligence/un-comtrade.md`).
- Many users consume Baltic indices through existing financial-data vendors rather than direct BEISL integration — check what your stack already has access to before licensing direct.
