# Numverify

Phone number validation and lookup REST API by APILayer covering 232 countries. Returns line type (mobile/landline/VoIP/toll-free), carrier, country, and city-level location from a phone number.

**Tier:** Freemium
**Auth:** API Access Key (query parameter)
**Last researched:** 2026-05-09

## Use cases

- Phone number validation at signup to block fake/bot accounts
- Carrier identification before SMS sending to filter high-risk routes
- Line-type detection (mobile vs landline vs VoIP) for fraud scoring
- Cleansing / enriching CRM contact databases

## Pricing

- **Free tier:** 100 API requests/month (no time limit; HTTP-only on free).
- **Paid tiers:** Starting at $9.99–14.99/mo (depending on promo); higher volume tiers scale up. Annual billing offers up to 15% discount.
- **Enterprise:** Custom volume pricing via APILayer sales.
- **Notes:** Paid plans get HTTPS, prioritized support, and overage billing on going past the cap. Free plan is HTTP-only.

## Authentication

Sign up at numverify.com (or apilayer.com marketplace) to get a unique Access Key. Pass as `?access_key=YOUR_KEY` on every request.

## Endpoints

- **Base URL:** `http://apilayer.net/api` (free) / `https://apilayer.net/api` (paid)
- **Key endpoints:**
  - `GET /validate?access_key=...&number=...&country_code=...&format=1` — validate a number, return JSON with `valid`, `number`, `local_format`, `international_format`, `country_code`, `country_name`, `location`, `carrier`, `line_type`
  - `GET /countries?access_key=...` — list supported countries with dial codes

## Example call

```bash
curl "http://apilayer.net/api/validate?access_key=$NUMVERIFY_KEY&number=14158586273"
```

```python
import requests
r = requests.get("http://apilayer.net/api/validate",
                 params={"access_key": "YOUR_KEY", "number": "14158586273"})
print(r.json())
# {'valid': True, 'number': '14158586273',
#  'local_format': '4158586273', 'international_format': '+14158586273',
#  'country_code': 'US', 'country_name': 'United States of America',
#  'location': 'Novato', 'carrier': 'AT&T Mobility LLC',
#  'line_type': 'mobile'}
```

## Rate limits

Free plan: 100 req/month. Paid plans: published monthly request volumes per tier. Notifications fire at 75/90/100% utilization; overage fees apply past 100%.

## SDKs / Libraries

- **Official:** None; vendor recommends raw HTTP.
- **Community:** Numerous wrappers in Python/Node/PHP/Ruby; tutorials abundant.

## Documentation

- Main docs: https://numverify.com/documentation
- Pricing: https://numverify.com/pricing
- FAQ: https://numverify.com/faq
- APILayer marketplace: https://apilayer.com/marketplace/number_verification-api

## Notes

- Run by APILayer (Austrian company), not a carrier — accuracy on line-type/carrier varies by country and may not reflect post-port carriers.
- HTTP on free tier means request data is unencrypted in transit; sensitive numbers should use the paid tier with HTTPS.
- For deeper signals (SIM swap, call forwarding, identity match), see `Twilio Lookup` in this category.
