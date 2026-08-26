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

# Links

* https://www.mapbox.com/maps — Mapbox custom styles as a reference
* https://snazzymaps.com — existing map style customization, no schematic/print focus
* https://felt.com — collaborative maps, different audience
