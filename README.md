# Africa Interactive Map  
**Internal / Restricted Use Only**

---

## Overview

This project is a self-contained interactive SVG map of the African continent built using **D3.js (v7)**.  
The map renders country-level geographic boundaries and displays contextual demographic and institutional data through an on-click information card.

This application is intended **strictly for internal use**. It is not designed, licensed, or approved for public access, reuse, or redistribution.

---

## Access & Usage Restrictions

- This codebase and all associated datasets are **confidential and restricted**.
- Unauthorized copying, reuse, redistribution, or publication is prohibited.
- Any derivative work, data extraction, or external presentation requires explicit approval from the project owner.
- The visualization is intended for **internal exploratory, analytical, and demonstrative purposes only**.

---

## Functional Description

The application provides the following functionality:

- Renders an Africa-only map using GeoJSON country boundaries
- Highlights countries for which attribute data exists
- Displays a modal-style information card when a country is selected
- Supports zooming, panning, and responsive resizing
- Gracefully handles missing or incomplete data without runtime failure

Countries without associated data remain visible but are not interactive.

---

## Technology Stack

- HTML5
- CSS3 (inline styling)
- JavaScript (ES6)
- D3.js v7
- GeoJSON (country-level geometry)

No backend services, databases, or authentication layers are required.

---

## Geographic Data Description

### Geometry Source

- **Format:** GeoJSON (FeatureCollection)
- **Coverage:** African continent only
- **Granularity:** National-level polygons
- **Projection:** Rendered using `d3.geoMercator`

### Required Geometry Attributes

Each GeoJSON feature must contain at least one stable country identifier:

- `ISO_A3` (preferred)
- `iso_a3` (fallback)
- `ID` (fallback)

These identifiers are used to associate attribute data with geographic features.

### Geometry Assumptions

- Multipart countries (e.g., Angola including Cabinda) are preserved
- No sub-national or administrative boundaries are included
- Geometry is static and not altered at runtime

---

## Attribute (Statistical) Data Description

### Data Model

Country-level attributes are stored as a lookup object keyed by **ISO Alpha-3 codes**.

```json
{
  "ISO_A3": {
    "country": "Country name",
    "population": "formatted string",
    "projected2050": "formatted string",
    "universities": number,
    "youth_pct": "percentage string"
  }
}

## Field Definitions

| Field | Type | Description |
|------|------|-------------|
| `country` | String | Display name of the country |
| `population` | String | Total population for the reference year |
| `projected2050` | String | Static population projection for 2050 |
| `universities` | Number | Count of recognized tertiary institutions |
| `youth_pct` | String | Share of population classified as youth |

> Numeric values may be stored as formatted strings to preserve display consistency.  
> The dataset is not intended for computational or analytical processing within the application.

---

## Data Integration Logic

- A country becomes interactive only if its **ISO Alpha-3 code** exists in the attribute dataset
- Interactive countries are assigned the CSS class `has-data`
- Clicking an active country opens an information card populated from the dataset
- Missing values default to `"N/A"` and do not interrupt rendering

This design ensures stability even with partial or incomplete data coverage.

---

## Angola Data Verification (Example)

- **Country:** Angola  
- **ISO Alpha-3 Code:** `AGO`
- Geometry includes mainland Angola and the Cabinda exclave
- Data presence is validated by matching `AGO` across GeoJSON and attribute data
- Values are checked for internal consistency and reasonable demographic magnitude
- Angola is treated as a single sovereign unit with no sub-national differentiation

---

## Temporal Scope

- All data represents a **single reference snapshot**
- Projection values (e.g., 2050 estimates) are static and precomputed
- No real-time updates or time-series visualization are supported

Comparisons between countries are valid **only within the same documented reference year**.

---

## Data Quality & Limitations

- Data accuracy depends on upstream reporting sources and update cycles
- Institutional counts (e.g., universities) may vary based on definitional criteria
- No automated validation, reconciliation, or update pipeline exists in the current version

All outputs should be interpreted as **indicative rather than authoritative**.

---

## Maintenance & Update Guidelines

When updating the dataset or geometry:

1. Verify ISO Alpha-3 codes prior to data ingestion
2. Update attribute data independently from map geometry
3. Spot-check values against trusted institutional sources
4. Revalidate multipart countries after GeoJSON changes
5. Document reference year and data provenance for each update

---

## Compliance Notice

This visualization:

- must not be cited as an official statistical source
- is not suitable for policy, legal, or regulatory decision-making
- is restricted to internal exploratory and demonstrative use

Any external publication, sharing, or presentation derived from this tool requires separate review and authorization.

---

## License

### Restricted Use License

This project is proprietary and confidential.  
No rights are granted for reuse, redistribution, modification, or publication without explicit written authorization.

