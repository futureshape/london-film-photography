# Venue Front Matter Template (Reference Only)

This file documents the front matter schema used for venue-like entries (e.g. darkrooms, labs). It is NOT an active venue page and can be copied & adapted when adding a new entry under the appropriate collection (e.g. `_darkrooms/`, `_film-labs/`, or `_venues/` if you later configure it as a collection).

> Copy the example front matter block below into a new file, then fill in / prune fields as needed. Keep keys but remove any unused nested sections to avoid clutter.

---
## Quick Rules
- File name: use a lowercase, hyphenated slug (e.g. `example-darkroom.md`). The slug becomes part of the URL if the collection outputs pages.
- YAML front matter must start and end with `---`.
- Quote values containing special characters (`:`, `&`, `£`, `%`, `–`, `–`), or leading zeros.
- Latitude/longitude should be numeric (no quotes) for easier programmatic use.
- Remove whole optional sections you do not need (don’t leave them empty).
- Use straight quotes (`"`) in YAML; smart quotes can break parsing.

---
## Top-Level Keys (Overview)

| Key | Type | Required | Purpose |
|-----|------|----------|---------|
| `title` | String | Yes | Display name of the venue. |
| `categories` | Space‑separated list (string) | Optional | Tagging / filtering (e.g. `darkroom film-dev`). |
| `last-checked-date` | Date (YYYY-MM-DD) | Optional | When info was last manually verified; currently displayed only on darkroom pages if present. |
| `contact` | Mapping | Strongly recommended | Address & communication details. |
| `opening` | Mapping | Optional | Public opening hours / availability notes. |
| `darkroom` | Mapping | Optional | Details specific to printing darkrooms. |
| `film-dev` | Mapping | Optional | Details about film development / processing services. |
| (body content) | Markdown | Optional | Descriptive text shown on the page. |

### `contact` subsection
| Key | Type | Required | Notes |
|-----|------|----------|-------|
| `address-summary` | String | Recommended | Short area/neighbourhood (shown in lists). |
| `email` | String | Optional | Primary contact email. |
| `address` | String | Recommended | Street address (no city/postcode). |
| `postcode` | String | Recommended (UK) | Keep uppercase; quote it. |
| `phone` | String | Optional | Include country code only if needed (`+44 ...`). |
| `official-site` | URL String | Recommended | Canonical service / booking page. |
| `facebook` | URL String | Optional | Social media. |
| `instagram` | URL String | Optional | Social media. |
| `gmaps-link` | URL String | Optional | Google Maps short link. |
| `longitude` | Number | Optional | Decimal degrees (W negative). |
| `latitude` | Number | Optional | Decimal degrees (N positive). |

### `opening` subsection
Typical day keys: `monday` … `sunday` (String). Use `Closed` if not open.
Supplemental keys sometimes used:
- `open-weekends`: Short note (e.g. `Saturday only`).
- `open-weekday-evenings`: Note for evening availability.
- You can add a clarifying note like `booking-window` if needed (custom keys are allowed, but stay consistent across files if you start using them widely).

### `darkroom` subsection
| Key | Type | Notes |
|-----|------|-------|
| `pricing` | Mapping | Aggregated pricing info (membership, induction, printing, etc.). |
| `black-and-white` | Mapping | Capabilities for B&W printing. |
| `colour` | Mapping | Capabilities for colour (RA‑4 / enlargers). |
| `additional` | Mapping | Links to training / extras. |

Suggested nested keys:
- `pricing.membership`: Membership fee or note (string).
- `pricing.induction`: Induction requirements.
- `pricing.printing`: Core session pricing / structure.
- `pricing.discount-students`: `Yes` / `No` or explanatory string.
- `black-and-white.formats`: List of supported film formats (e.g. `["35mm", "medium format", "large format (5x4)"]`).
- `black-and-white.max-size`: Largest print size achievable (e.g. `16x20").`
- `colour.formats`: List.
- `colour.max-size`: Size string.
- `additional.training`: URL or short note.

### `film-dev` subsection
| Key | Type | Notes |
|-----|------|-------|
| `details` | URL String | Film processing service page. |
| `dev-types` | String / list | Space or comma separated keywords (`colour black-and-white`). |
| `pricing` | Mapping | Per‑service pricing keys you standardise (e.g. `c41-35mm-dev-scan`). |
| (custom) | Any | Add more as needed; keep slug‑like keys for consistency. |

If a specific price changes frequently, you can either:
- Keep a placeholder: `c41-35mm-dev-scan: "see site for current price"`
- Or store only a `notes` field summarising pricing model.

---
## Annotated Example Front Matter

```yaml
---
title: "Example Darkroom Lab"
categories: darkroom film-dev
last-checked-date: "2025-09-09"

contact:
  address-summary: "Hackney, E8"
  email: "info@examplelab.org"
  address: "12 Sample Street"
  postcode: "E8 4AB"
  phone: "+44 20 7000 0000"
  official-site: "https://www.examplelab.org/darkroom"
  facebook: "https://www.facebook.com/examplelab"
  instagram: "https://www.instagram.com/examplelab/"
  gmaps-link: "https://goo.gl/maps/xyzExample"
  longitude: -0.055321
  latitude: 51.543210

opening:
  monday: "Closed"
  tuesday: "10:00 - 18:00"
  wednesday: "10:00 - 18:00"
  thursday: "10:00 - 18:00"
  friday: "10:00 - 18:00"
  saturday: "11:00 - 17:00"
  sunday: "Closed"
  open-weekends: "Saturday only"
  open-weekday-evenings: "Thursdays by arrangement"

# Include this only if the venue offers public darkroom printing
# Omit entirely otherwise.
darkroom:
  pricing:
    membership: "£50/year (optional)"
    induction: "Required once; free 15 min orientation"
    printing: "£40 per 6‑hour session (members £32)"
    discount-students: Yes
  black-and-white:
    formats:
      - "35mm"
      - "medium format"
      - "large format (5x4)"
    max-size: "16x20"
  colour:
    formats:
      - "35mm"
      - "medium format"
    max-size: "20x24"
  additional:
    training: "https://www.examplelab.org/courses/"

# Include only if film processing is offered
film-dev:
  details: "https://www.examplelab.org/film-processing/"
  dev-types: "colour black-and-white"
  pricing:
    c41-35mm-dev-scan: "£15.00"
    bw-35mm-dev: "£8.00"
    push-pull: "+£2 per stop"
---

Intro paragraph about the venue – what makes it unique, history, or any
special policies (e.g. bring your own paper, chemistry provided, membership benefits).
```

---
## Blank Scaffold (Copy & Fill)
```yaml
---
title: ""
categories: 
last-checked-date: ""
contact:
  address-summary: ""
  email: ""
  address: ""
  postcode: ""
  phone: ""
  official-site: ""
  facebook: ""
  instagram: ""
  gmaps-link: ""
  longitude: 
  latitude: 
opening:
  monday: ""
  tuesday: ""
  wednesday: ""
  thursday: ""
  friday: ""
  saturday: ""
  sunday: ""
  open-weekends: ""
  open-weekday-evenings: ""
# darkroom: (remove this comment and section if not applicable)
#   pricing:
#     membership: ""
#     induction: ""
#     printing: ""
#     discount-students: 
#   black-and-white:
#     formats: []
#     max-size: ""
#   colour:
#     formats: []
#     max-size: ""
#   additional:
#     training: ""
# film-dev:
#   details: ""
#   dev-types: ""
#   pricing:
#     c41-35mm-dev-scan: ""
---
```

---
## Common Pitfalls
- Smart quotes copied from web pages cause YAML parse errors – replace them.
- Trailing spaces after a quote sometimes break diffs; trim them.
- If you remove all keys from a mapping, delete the mapping header too.
- Keep numeric lat/long unquoted so tools can parse them as numbers.

---
## Extending the Schema
You can safely add custom keys in subsections (e.g. `darkroom.equipment:` list) – keep names lowercase with hyphens if multiword. Document new keys here if you decide to standardise them.

---
(End of template)
