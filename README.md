Overview

This project is a self-contained, interactive SVG map of the African continent built using D3.js (v7). The application visualizes country-level data and displays a contextual information card when a country with available data is selected.

This tool is intended strictly for internal, controlled use. It is not designed, licensed, or approved for public distribution or third-party reuse.

Access & Usage Restrictions

This codebase and associated datasets are restricted.

Unauthorized reuse, redistribution, or external publication is prohibited.

Any derivative work or data extraction requires explicit approval from the project owner.

The visualization is intended for exploratory and illustrative purposes only.

Functional Description

Renders an Africa-only map using GeoJSON geometry.

Highlights countries for which attribute data exists.

Displays a modal-style information card on user interaction.

Supports zooming, panning, and responsive resizing.

Gracefully handles missing or incomplete data.

Countries without associated data remain visible but inactive.

Technology Stack

HTML5

CSS3 (inline styling)

JavaScript (ES6)

D3.js v7

GeoJSON (country-level geometry)

No backend services or databases are required.

Project Structure
/africa-interactive-map/
├─ index.html        # Main application file (HTML, CSS, JS)
├─ README.md         # Internal documentation
└─ data/             # Optional external data files (if used)

Geographic Data Description
Geometry Source

Format: GeoJSON (FeatureCollection)

Scope: African countries only

Granularity: National-level polygons

Projection: Rendered via d3.geoMercator

Required Geometry Attributes

Each feature must contain at least one valid country identifier:

ISO_A3 (preferred)

iso_a3 (fallback)

ID (fallback)

These identifiers are used to join statistical data to map geometry.

Geometry Assumptions

Multipart countries (e.g., Angola including Cabinda) are preserved.

No sub-national boundaries are included.

Geometry is static and not modified at runtime.

Attribute (Statistical) Data Description
Data Model

Country data is stored as a lookup object keyed by ISO Alpha-3 codes.

{
  "ISO_A3": {
    "country": "Country name",
    "population": "formatted string",
    "projected2050": "formatted string",
    "universities": number,
    "youth_pct": "percentage string"
  }
}

Field Definitions
Field	Type	Description
country	String	Display name of the country
population	String	Total population for the reference year
projected2050	String	Static population projection for 2050
universities	Number	Count of recognized tertiary institutions
youth_pct	String	Share of population classified as youth

Numeric fields may be stored as strings to preserve formatting consistency.
The dataset is not intended for analytical computation within the application.

Data Integration Logic

A country becomes interactive only if its ISO code exists in the data lookup.

Interactive countries receive the CSS class has-data.

Clicking an active country opens an information card populated from the dataset.

Missing fields default to "N/A" and do not break rendering.

This approach ensures robust rendering even with partial coverage.

Angola Data Verification (Example)

ISO Alpha-3 Code: AGO

Geometry includes mainland Angola and Cabinda.

Data presence is verified by matching AGO in both GeoJSON and stats lookup.

Values are checked for internal consistency and reasonable demographic scale.

Angola is treated as a single sovereign unit; no internal subdivisions are shown.

Temporal Scope

All data represents a single reference snapshot.

Projection values (e.g., 2050 estimates) are static and precomputed.

No real-time updates or time-series animation are supported.

Comparisons are valid only within the same documented reference year.

Data Quality & Limitations

Data accuracy depends on upstream sources and reporting lag.

Institutional counts (e.g., universities) may vary by classification criteria.

The application does not perform statistical validation at runtime.

All outputs should be interpreted as indicative, not authoritative.

Maintenance & Update Guidelines

When updating the dataset:

Verify ISO Alpha-3 codes before ingestion.

Update attribute data independently from geometry.

Spot-check values against trusted institutional sources.

Revalidate multipart geometries (e.g., Angola) after GeoJSON changes.

Document reference year and data provenance for each update.

Compliance Notice

This visualization:

must not be cited as an official statistical source,

is not suitable for policy or legal decision-making,

is restricted to internal exploratory use.

Any external publication or presentation derived from this tool requires separate review and approval.

License

Restricted Use License

This project is proprietary and confidential.
No rights are granted for reuse, redistribution, or modification without explicit authorization.
