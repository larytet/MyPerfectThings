# Schematic Maps SaaS

A web service that generates clean, stylized schematic maps from Google Maps data — black-on-white line drawings similar to the simplified maps used in advertisements, wedding invitations, and event programs.

# Problem

Designers and individuals regularly need simplified, print-ready maps for:

- Wedding invitations and save-the-dates
- Event programs and signage
- Business cards and brochures
- Real estate marketing materials
- Local advertisement flyers

Creating these manually in Illustrator or Inkscape is time-consuming and requires design skills. Google Maps embeds are too detailed and branded for elegant print use.

# Product

Users enter an address or area, adjust the zoom and style, and receive a clean vector or high-resolution raster map:

- Black on white (or custom colors)
- Roads and landmarks only — no satellite imagery, no clutter
- Adjustable level of detail (major roads only vs. full street grid)
- Label control (show/hide street names, landmarks, custom text)
- Export as SVG, PDF, or PNG

# Business Model

- **Free tier** — individuals: a limited number of exports per month with a small attribution watermark
- **Pay-per-export** — businesses: charged per download, no subscription required; watermark removed
- **Volume plans** — agencies or print shops that need bulk exports

Pricing anchored to the alternative cost: a designer spending 30–60 minutes on a custom map.

# Implementation Notes

- Use Google Maps Static API or OpenStreetMap (Mapbox) as the data source
- Apply SVG/canvas rendering with a stripped-down style (no fill colors, only strokes)
- Vector output enables infinite scaling for large-format print
- OpenStreetMap data avoids Google licensing fees and allows full commercial use

# Competitive Landscape

## Direct Competitors

- **[Printmaps.net](https://www.printmaps.net/)** — closest overall competitor. OSM-based, exports SVG/PSD/PNG, layered output for Illustrator. Charges $7–$906 per print run depending on quantity. Targets print professionals; no free tier; no consumer-friendly self-serve UX.
- **[CCCarto](https://www.cccarto.com/freeweddingmaps/)** — free schematic wedding direction maps. Narrow scope (weddings only), limited style control.
- **[Snazzy Maps](https://snazzymaps.com/style/34506/simple-printable)** — provides a "Simple Printable" Google Maps style JSON snippet for developers to embed. Not a self-contained product.
- **Canva / Visme** — template-based map tools; no live map data extraction into schematic style.
- **Stepmap.de / 123map** — vector map editors aimed at German-market print professionals.

## Market Gaps

1. No free-tier self-serve tool for individuals — Printmaps.net charges per export; CCCarto is free but wedding-only and basic.
2. No style presets for common print aesthetics (B&W line-art, vintage, ink-on-paper, minimal labels) without technical setup.
3. No address-to-schematic-SVG pipeline with instant preview and one-click download aimed at non-designers.
4. The invitation/card niche is served by Etsy illustrators doing it manually — no automated equivalent exists.

The free-for-individuals / pay-per-export-for-businesses model has no direct equivalent in the market.

## Open-Source Building Blocks

- **[Mapnik](https://mapnik.org)** — industry-standard renderer, supports custom CartoCSS stylesheets, SVG output. Powers OSM's own tile layer. Best candidate for the rendering backend.
- **[Map Machine](https://github.com/enzet/map-machine)** (Python) — bounding-box → SVG generation; easy to wrap as a web service.
- **[OSMRender](https://github.com/fergusq/OSMRender)** (GPL3) — renders OSM XML → SVG/PDF/PNG with configurable rule files.

# Links

* https://www.printmaps.net — strongest direct competitor
* https://www.cccarto.com/freeweddingmaps/ — free wedding maps reference
* https://snazzymaps.com — map style customization reference
* https://mapnik.org — rendering backend candidate
* https://github.com/enzet/map-machine — OSM → SVG pipeline
