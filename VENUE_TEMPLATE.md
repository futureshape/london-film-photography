# Venue Front Matter Reference

This file documents the front matter used by darkroom and film-lab listings. It is guidance only; Jekyll does not load it as a template.

## Where venue records live

Add or edit one Markdown file per venue in `_venues/`. In this repository, `_darkrooms/` and `_film-labs/` are symlinks to `_venues/`, and both collections are configured in `_config.yml`. A record can therefore be used by both the darkroom detail pages and the film-lab listing; do not make duplicate copies in the symlinked directories.

Use a lowercase, hyphenated filename such as `example-darkroom.md`. The filename becomes the venue slug. Put YAML front matter between the opening and closing `---` lines; any Markdown after the closing line is the page body.

## General rules

- Use `title` and a space-separated `categories` string. Current category tokens are `darkroom`, `film-dev`, and `temporarily-removed`.
- Set `last-checked-date` to an ISO date (`YYYY-MM-DD`) when the listing has been manually verified. It is shown on darkroom detail pages.
- Use double quotes for string values, especially values containing punctuation, special characters, or leading zeroes. Keep latitude and longitude numeric.
- Use `true` only for the boolean options described below. Omit unused keys and empty mappings; do not use empty strings or `false` as placeholders.
- Only fields consumed by the site templates are displayed. Adding an undocumented field does not add it to the page; a new displayed field also requires a template change.

## Common fields

Every current venue record needs the following fields; the map and detail layouts consume them directly.

| Field | Type | Use |
|---|---|---|
| `title` | String | Venue name. |
| `categories` | Space-separated string | Selects which listings include the venue. Use `darkroom`, `film-dev`, or both. Use `temporarily-removed` to suppress a listing from the public map. |
| `contact.address-summary` | String | Neighbourhood and postcode area, used on cards and map markers. |
| `contact.address` | String | Street address, used on detail pages. |
| `contact.postcode` | String | UK postcode; quote it to preserve formatting. |
| `contact.email` | String | Contact email shown on detail pages. |
| `contact.gmaps-link` | URL string | Google Maps link. |
| `contact.latitude` | Number | Decimal latitude, north positive. |
| `contact.longitude` | Number | Decimal longitude, west negative. |

Optional contact fields: `phone`, `official-site`, `facebook`, and `instagram`. Use absolute URLs, including the protocol. For film-development listings, use `film-dev.details` for the service-specific website link when available.

## Darkroom fields

Use these fields when `categories` contains `darkroom`. The detail layout prints all seven days and the membership and printing values, so provide them rather than leaving them blank.

### Opening

`opening` is a mapping with string values for all seven keys: `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, and `sunday`. Use `Closed` only when closure is confirmed; otherwise give the verified hours or a concise note such as `By appointment`.

Optional `opening.open-weekends` and `opening.open-weekday-evenings` accept `true` or a short explanatory string. A string is shown in parentheses after the availability label. Omit the key when it does not apply.

### Darkroom pricing and facilities

| Field | Type | Notes |
|---|---|---|
| `darkroom.pricing.membership` | String | Required. Fee or `Not needed`. |
| `darkroom.pricing.printing` | String | Required. Session or printing rates. |
| `darkroom.pricing.induction` | String | Optional and displayed under Pricing. Include only a fee or fee-related detail (for example, `Included with membership`); omit induction requirements or scheduling information. |
| `darkroom.pricing.discount-bulk` | Boolean or string | Optional. `true` displays the bulk-booking label; a string is shown after it in parentheses. |
| `darkroom.pricing.discount-students` | Boolean or string | Optional. `true` displays the student-discount label; a string is shown after it in parentheses. |
| `darkroom.black-and-white` | Mapping | Optional. If present, provide `formats` as a list of strings and `max-size` as a string. |
| `darkroom.colour` | Mapping | Optional. If present, provide `formats` as a list of strings and `max-size` as a string. |
| `darkroom.additional.process-film` | Boolean or string | Optional. `true` displays the service label; a string adds a short note. |
| `darkroom.additional.training` | Boolean or URL string | Optional. `true` displays the training label; a URL makes it a link. |

Only the fields listed here are rendered from `darkroom`. In particular, do not add custom fields under `additional` expecting them to appear automatically.

## Film-development fields

Use `film-dev` when `categories` contains `film-dev`.

| Field | Type | Notes |
|---|---|---|
| `film-dev.details` | URL string | Optional link to the film-development service page. |
| `film-dev.dev-types` | Space-separated string | Required. Supported tokens are `colour`, `black-and-white`, and `slide`. |
| `film-dev.pricing.c41-35mm-dev-scan` | String | Required when `dev-types` includes `colour`; this is the starting 35mm colour development-and-scan price shown on the listing card. |
| `film-dev.pricing.bw-35mm-dev-scan` | String | Required when `dev-types` includes `black-and-white` but not `colour`; this is the starting B&W price shown on the listing card. |

When both `colour` and `black-and-white` are listed, the card shows only the colour price. Other pricing keys already present in records are not displayed by the current listing template.

## Example

```yaml
---
title: "Example Darkroom"
categories: "darkroom film-dev"
last-checked-date: 2025-09-09

contact:
  address-summary: "Hackney, E8"
  email: "info@examplelab.org"
  address: "12 Sample Street"
  postcode: "E8 4AB"
  phone: "+44 20 7000 0000"
  official-site: "https://www.examplelab.org/"
  gmaps-link: "https://maps.example.org/example"
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

darkroom:
  pricing:
    membership: "£50 per year"
    printing: "£40 per 4-hour session"
    discount-students: "Reduced membership"
  black-and-white:
    formats:
      - "35mm"
      - "medium format"
      - "large format (5x4)"
    max-size: "16x20"

film-dev:
  details: "https://www.examplelab.org/film-processing/"
  dev-types: "colour black-and-white"
  pricing:
    c41-35mm-dev-scan: "£15.00"
    bw-35mm-dev-scan: "£12.00"
---

Optional Markdown description shown on the darkroom detail page.
```
