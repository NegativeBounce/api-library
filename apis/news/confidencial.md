# Confidencial

A Nicaraguan independent investigative digital newspaper founded in 1996 by journalist Carlos Fernando Chamorro Barrios. Now operates entirely in exile from San José, Costa Rica (since June 2021), with all editorial staff distributed across at least four time zones. Free English section plus weekly English newsletter "The Dispatch."

**Tier:** Free
**Auth:** None
**Last researched:** 2026-05-09

## Use cases

- Nicaragua independent investigative journalism on the Ortega-Murillo regime (sanctions, repression, exile, citizenship-stripping)
- Tracking Central American authoritarianism (Nicaragua, El Salvador, parallel coverage with El Faro and Confidencial-Cuba context)
- Following Nicaraguan diaspora affairs in Costa Rica, Spain, US
- Building Latin America press-freedom and human-rights monitoring pipelines

## Pricing

- **Free tier:** All RSS, English section, and weekly "The Dispatch" newsletter free; no paywall
- **Paid tiers:** Optional Membership Program for direct reader support; Premium newsletter with exclusive recommendations and advance content
- **Enterprise:** Banner advertising on `confidencial.digital` (728x90, 300x250, sticky 728x90/320x100, integrated video); commercial inquiries to Enrique Gasteazoro (General Manager) or Cindy Regidor (Commercial Coordinator)
- **Notes:** Funding mix per the publication's own disclosure: **direct reader contributions, advertising revenue, and donations from international cooperation organizations** that support independent journalism and press freedom

## Authentication

None.

## Endpoints

- **Base URL:** `https://confidencial.digital/`
- **Key endpoints:**
  - English homepage: `https://confidencial.digital/english/`
  - English newsletter "The Dispatch" (Wednesday weekly): subscribe via the English page
  - Spanish main site: `https://confidencial.digital/`
  - About / "Quienes somos": `https://confidencial.digital/quienes-somos/`
  - Sister publication: `https://www.revistaniu.com/` (formerly `niu.com.ni`, lifestyle/culture)
- **Important domain note:** the original `confidencial.com.ni` domain was blocked by the Nicaraguan government on March 14, 2025; redirect from old domain is no longer functional. Current canonical domain is `confidencial.digital` (registered June 23, 2022 as a defensive move).

## Example call

```bash
# English homepage
curl "https://confidencial.digital/english/"

# Spanish main site
curl "https://confidencial.digital/"
```

## Rate limits

Not publicly documented.

## SDKs / Libraries

- **Official:** YouTube channel for `Esta Semana` and `Esta Noche` TV programs (Carlos F. Chamorro hosting); WhatsApp and Telegram alert communities
- **Community:** Standard RSS parsers

## Documentation

- Main site: https://confidencial.digital/
- English section: https://confidencial.digital/english/
- About: https://confidencial.digital/quienes-somos/
- ICIJ profile of Chamorro: https://www.icij.org/journalists/carlos-fernando-chamorro/

## Notes

Confidencial is **independent and opposition-aligned to the Ortega-Murillo regime**. Founded in 1996 by **Carlos Fernando Chamorro Barrios** — son of former Nicaraguan president Violeta Barrios de Chamorro and the assassinated journalist Pedro Joaquín Chamorro Cardenal (whose 1978 murder helped catalyze public sympathy for the Sandinista revolution). Carlos F. Chamorro is widely regarded as one of Latin America's most respected investigative journalists.

**The newsroom has been raided twice and now operates entirely in exile:**
- **December 14, 2018:** Police raided Confidencial's Managua offices without a court order, alongside raids on human-rights NGOs.
- **May 2021:** Police raided Confidencial's temporary offices at Invercasa and Chamorro's home; Ministerio Público issued an arrest order for "money laundering."
- **June 2021:** Chamorro went into permanent exile in Costa Rica after his siblings were arrested.
- **February 2023:** Chamorro and 93 other Nicaraguan citizens were stripped of their nationality by the Ortega-Murillo regime; Chamorro's properties and assets confiscated.
- **March 14, 2025:** The Nicaraguan government blocked all `.ni` domain access, including `confidencial.com.ni`. Confidencial had already migrated to `confidencial.digital` in 2022 anticipating exactly this move.

**Awards include:** 2024 WAN-IFRA Golden Pen of Freedom, 2021 Ortega y Gasset Award (El País), 2010 María Moors Cabot Prize (Columbia University Graduate School of Journalism). Sister TV programs `Esta Semana` and `Esta Noche` reach 415,000+ subscribers via YouTube and Facebook (banned from Nicaraguan TV in 2018).

**For source-trust analysis:** independent, opposition-aligned, exile-based. **Wikipedia notes that Confidencial is "financed by the US National Endowment for Democracy"** as part of its diversified funding mix — which is consistent with the publication's own disclosure of funding from "international cooperation organizations." This NED funding is a common pattern among independent investigative outlets in authoritarian-press environments and worth flagging for source-trust analysis. Coverage is strongest on Nicaraguan repression, Ortega-Murillo family corruption, sanctions, exile/diaspora, and broader Central American authoritarianism. No public REST/JSON developer API documented.
