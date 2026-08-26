# Print-and-Cut Stencil Template Generator

A web service that converts any image into a set of printable, cuttable stencil templates that together reproduce a large-scale drawing on a wall, ceiling, or floor — enabling anyone to spray or paint complex artwork without artistic skill.

# Problem

Creating large-scale murals, graffiti art, or decorative wall drawings requires either professional skill or expensive commissioned work. Hobbyists, street artists, and interior decorators have no accessible tool to:

- Scale a complex image up to room size
- Break it into layers or panels that fit a standard printer
- Produce registration marks so panels align correctly when applied

Current options are manual (projectors, grid method) or expensive (vinyl cutting services, professional plotters).

# Product

A user uploads an image (photo, logo, illustration, or generated art). The service:

1. **Scales** the image to the target dimensions (e.g. 2m × 3m wall)
2. **Tiles** it into A4/Letter-sized panels with overlap and registration marks
3. **Converts** each panel into a stencil-friendly version:
   - Reduces to 1–4 color layers (like screen printing separation)
   - Removes isolated islands that would fall out when cut (bridge generation)
   - Optionally applies a posterization or edge-detection style
4. **Exports** a print-ready PDF — one page per panel per color layer
5. Each panel includes:
   - **Orientation arrow** — clearly marked TOP/NORTH so the panel is placed correctly regardless of rotation
   - **Adhesive zones** — printed rectangles at the corners and midpoints indicating exactly where to apply double-sided tape; sized to avoid the spray area so tape residue doesn't land on the artwork
6. User prints, cuts with scissors or a craft knife, applies double-sided tape at the marked zones, positions on surface, sprays

Output can also target a home craft cutter (Cricut, Silhouette) via SVG export.

# Use Cases

- Large graffiti murals and street art
- Wall and ceiling murals for homes, nurseries, event venues
- Floor graphics for events or warehouses
- Stage backdrops and theater sets
- School and community art projects

# Business Model

- **Free tier** — individuals: small image size limit, watermarked PDF, limited color layers
- **Pay-per-export** — full resolution, no watermark, multi-layer color separation, craft cutter SVG export
- **Pro / agency plan** — bulk exports, custom panel sizes, priority processing

# Multi-Panel Alignment

## Existing approaches

- **Registration holes + pencil marks** — punch 3–4 small holes at the corners of each panel, mark the wall through them with a pencil, align the next panel to those marks. Simple, accurate, no tools needed.
- **Overlap zones** — panels are generated with a 2–3 cm overlap strip; registration crosses printed in the overlap let you visually snap the next panel to the previous one before taping. No measuring required.
- **Laser level grid** — a cheap cross-laser level ($15–30) projects a horizontal and vertical line; panels are generated with matching hairline marks on their edges. Fast for large surfaces.
- **Numbered grid on wall** — lightly tape a measured string grid to the wall first; panel PDF includes grid coordinates printed at the edges.

## Modular / master-frame concept

Instead of one panel per spray pass, generate a **single rigid master frame** that stays taped to the wall throughout the entire job:

- The frame is a full-size backing sheet (foam board, acetate/mylar, or card) with the outer border and registration features
- Individual color layers or detail zones are separate **inserts** — small cut pieces that slot into openings in the frame
- Workflow: tape frame once → insert layer 1 pieces → spray → remove layer 1 inserts → insert layer 2 pieces → spray → repeat
- The frame itself never moves, so all layers are perfectly registered automatically
- Inserts can be repositioned or reused for repeating patterns

This is how professional screen-print registration frames work — the stencil generator could output both the frame file and numbered insert files as separate PDFs, with slot margins sized to allow easy finger removal without disturbing the frame.

**Advantage over separate panels:** zero alignment error between color layers; the frame doubles as a mask protecting the surrounding wall.

## Magnetic strip rail system

A reusable alternative to taping directly to the wall:

- Stick **self-adhesive magnetic strips** to the wall once, arranged as a measured grid (horizontal rows at panel-height intervals)
- Print templates on **ferro-paper** (magnet-receptive paper, available for home printers) or laminate the back of normal paper with a thin ferro sheet
- Templates snap onto the strips, hold firmly enough for spraying, and peel off cleanly with no tape residue on the wall
- The strips stay on the wall permanently and serve as a registration grid for every future session

The stencil generator would output **strip placement guides** — a separate PDF showing exactly where to stick the strips for a given image size and panel layout, so the grid is set up correctly once and reused across all panels and all future projects on that wall.

Magnetic strips are removable from walls without damage (3M Command-style backing), making this viable for rental spaces and indoor murals. Ferro-paper and magnetic strips are commodity products available on Amazon.

# Implementation Notes

- Image processing pipeline: upload → posterize/threshold → stencil bridge insertion → tile → PDF generation
- Bridge insertion (connecting isolated islands) is the key hard problem — existing open-source tools (Inkscape, potrace) handle parts of this
- Registration marks and panel numbering are straightforward PDF layout work
- SVG output for Cricut/Silhouette opens a large hobbyist market (Cricut has ~10M active users)
- Could integrate with AI image generation so users describe a mural and get stencils directly

# Links

* https://github.com/charlesreid1/stencil — basic stencil generation reference
* https://potrace.sourceforge.net — bitmap to vector tracing (core building block)
* https://inkscape.org — stencil-friendly SVG editing, automation via CLI
* https://cricut.com — largest consumer craft cutter platform (SVG import target)
