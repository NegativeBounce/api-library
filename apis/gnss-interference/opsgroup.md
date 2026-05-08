# OPSGROUP

International aviation operations community that publishes GPS spoofing/jamming briefings, location maps, and crew guidance — primarily through a members-only dashboard and the public ops.group blog.

**Tier:** Paid (membership)
**Auth:** None for public blog; member login for full reports
**Last researched:** 2026-05-07

## Use cases

- Operational reading on emerging GPS spoofing/jamming hotspots and crew procedures, written by working pilots and dispatchers (not signal-processing data).
- Reference document for the **2024 GPS Spoofing WorkGroup Final Report** (128 pages) and the Technical Guide to GPS Spoofing (29 pages) — widely cited in industry.
- Periodic location maps for the Mediterranean, Black Sea, Russia/Baltics, and India/Pakistan spoofing corridors.
- Member ALL CALLs gathering crew reports of spoofing incidents.

## Pricing

- **Free tier:** Public blog posts at ops.group/blog and the famous weekly Ops Bulletin (free email signup). No data API.
- **Paid tiers:** OPSGROUP Membership (the Members Dashboard contains the full GPS Spoofing Special Briefing, technical guides, and the rolling spoofing report). Pricing for OPSGROUP membership is per-pilot or per-organization and not publicly listed; check current rates at ops.group.
- **Enterprise:** Organizational/airline memberships available; contact OPSGROUP.
- **Notes:** OPSGROUP is fundamentally a community and content organization, **not a data provider**.

## Authentication

Public blog and weekly Ops Bulletin: none. Members Dashboard: standard email/password login provisioned to paying members.

## Endpoints

- **Base URL:** `https://ops.group/`
- **Key endpoints:** None — OPSGROUP does **not** offer a documented public API. Content is delivered as blog posts, PDF reports, member emails, and a member dashboard. Some content is on Slack channels (e.g., the GPS Spoofing WorkGroup channel during its 2024 run).

## Example call

```bash
# OPSGROUP has no public API. The closest "programmatic" access is fetching their public blog HTML/RSS:
curl "https://ops.group/blog/feed/"
```

## Rate limits

Not applicable.

## SDKs / Libraries

- **Official:** None.
- **Community:** None.

## Documentation

- Main site: https://ops.group/
- Blog: https://ops.group/blog/
- GPS Spoofing tag: https://ops.group/blog/tag/gps-spoofing/
- 2024 GPS Spoofing Final Report: https://ops.group/blog/gps-spoofing-final-report/

## Notes

- **No public API.** This entry is cataloged as a reference because OPSGROUP is the most-cited human-readable source for GPS spoofing operational impact in commercial aviation, and the 2024 Final Report (950 contributors across airlines, ATC, OEMs, and authorities) is a foundational document. For programmatic data, OPSGROUP itself **points users to** GPSwise (SkAI) and GPSJAM.
- Founded by Mark Zee (former airline pilot, ATCO, dispatcher); based in Christchurch, NZ.
- Best treated as authoritative editorial commentary on the human/operational side of GPS interference, paired with a real data source for machine-readable content.
- If your use case requires programmatic interference data, this is **not the right tool** — use GPSwise, ADS-B Exchange, OpenSky Network, or Aireon depending on tier and coverage needs.
