# HomeCourseAI
## Geospatial alternative data, relative signals and model validation

HomeCourseAI is a Python-based research prototype that turns aerial imagery, terrain-response layers and golf-course boundaries into interpretable maps of relative firm/soft tendency. The central problem is quantitative: how can several imperfect data sources produce a useful spatial signal without confusing a proxy, a visual pattern and a measured physical outcome?

I built the data-processing pipeline, interactive mapping and boundary-review workflow, surface-specific normalization, independent satellite consistency checks, and PDF yardage-book export. The working demonstration covers nine manually outlined holes at Reunion Resort's Palmer Course.

**Status:** local research prototype with an interactive interface and a shareable nine-hole PDF. An App Store application and on-demand course service are future work.

## The research problem

A course-wide colour scale can produce a misleading result: fairways appear systematically different from rough because the surface classes differ, rather than because a particular location is unusual within its own class. Incorrect boundaries compound that error by contaminating the comparison group.

The approach is to identify comparable surfaces first, build a separate reference distribution for each, and display deviations from those distributions. This resembles peer-group normalization in quantitative research, applied to spatial environmental data.

## Data and pipeline

| Component | Role | Principal constraint |
| --- | --- | --- |
| USDA NAIP RGB + near-infrared imagery, accessed through Microsoft Planetary Computer | High-resolution basemap and imagery context | The Palmer demonstration uses imagery acquired 7 January 2023 at approximately 0.6 m per pixel; it is not live |
| Mapped course geometry and OpenStreetMap hole lines | Hole orientation and estimated yardage references | Mapped geometry and yardages are not an official survey or scorecard |
| Terrain/shade drying and wetting-retention response layers | Inputs to the fine-scale heuristic signal | Their difference is a proxy, not a measured mechanical property |
| User-drawn green, fairway/tee and immediate-rough polygons | Surface identity and eligible comparison regions | Human review improves usability but does not create independent ground truth |
| Sentinel-2 observations | Separate canopy-moisture consistency checks | Native 20 m analysis support, cloud contamination and mixed surface footprints limit coverage |

The pipeline preserves imagery identity, coordinates, acquisition dates, annotation revisions and missing-data status. It aligns masks and raster layers before computing summaries, then uses the same spatial transforms for the full-hole view, heatmap and green close-up.

## Signal construction

For eligible location `i`, the current fine-scale signal is:

```text
p_i = drying_response_i - wetting_retention_response_i

z_i = (p_i - mean(p | surface_i)) / max(std(p | surface_i), 0.02)
```

Fairways, including tees, are compared with fairways; greens with greens; rough with rough. Reference statistics pool eligible equal-area source pixels, so larger eligible areas receive proportionate weight. They are not averages of hole-level averages.

The nine-hole demonstration uses a shared baseline across those nine holes only. It does not claim an 18-hole course baseline. Cross-hole overlaps are excluded to prevent duplicate counting; known non-turf surfaces and boundary guards are excluded; missing values remain missing.

Positive scores indicate relatively stronger drying-minus-retention response within the surface class; negative scores indicate relatively weaker response. These are dimensionless standardized deviations, not firmness units, soil-moisture percentages or ball-roll estimates. A score of +2 is not a probability or a statistical significance claim.

The calmer display leaves deviations within +/-0.5 standard deviations unshaded and gradually increases colour strength to +/-3. These choices control visual sensitivity only; they do not change the underlying scores or establish physical calibration.

## Efficient boundary annotation

The editor uses three nested envelopes: green, fairway/tees, and immediate rough. Polygon subtraction produces disjoint classes:

- Green retains the innermost region.
- Fairway excludes the green.
- Rough excludes the inner regions.
- Areas outside the drawings remain unlabeled.

Multiple polygon parts support separated turf regions. The editor provides individual-action undo/redo, per-hole drafts, versioned saves, geometry checks, conflict handling and recovery of rejected submissions. Drafts, approved runtime overrides and training candidates are distinct; drawing a polygon does not automatically train or promote a model.

## Independent checks and evaluation discipline

**Satellite consistency.** The separate Sentinel workflow compares the fine signal with the direction of a canopy-moisture proxy on matched native cells. It requires at least 80% same-surface footprint support, vegetation-quality filtering and a 60 m cloud/shadow guard. Descriptive Spearman rank correlation and supporting, contradicting or inconclusive cells remain visible. Sentinel observations are not fitted into this predictor and are not mechanical-firmness ground truth. Small greens frequently lack sufficient pure cells.

**Spatial leakage controls.** The model-development workflow separates Train, Validation and Test at course or sealed-hole level rather than treating adjacent pixels as independent observations. Palmer holes 4 and 10 are reserved from model fitting and tuning. Displaying a manually drawn hole in the prototype does not make it training data.

**Multiple evaluation criteria.** A documented segmentation experiment using 241 trusted boundary answers improved held-out mean intersection-over-union from 59.87% to 61.43%, while boundary F1 declined from 8.10% to 5.75%. The promotion gate rejected the candidate and preserved the existing model. Those are segmentation metrics, not heatmap or firmness accuracy.

This illustrates a practical research decision: a better aggregate metric can still produce a worse product when the failure occurs at the boundaries that define the signal's comparison groups.

## Demonstrated output

The saved nine-hole snapshot contains:

| Surface | Eligible source pixels |
| --- | ---: |
| Fairway/tees | 124,183 |
| Rough | 115,718 |
| Green | 9,077 |

These are spatial coverage counts, not independent observations or an effective statistical sample size. The comparison excludes 271 overlapping source pixels.

The prototype provides a shared-scale hole gallery, individual-hole views, surface filtering, local score readouts, aligned green close-ups and a ten-page PDF with estimated yardage markers. The export uses the calmer display without recomputing the reference distributions.

All nine outlines in this snapshot remain drafts. Holes 7 and 9 have rough-envelope containment warnings and are explicitly flagged. Independent Sentinel checks were not recomputed for these new manual comparison regions.

## Quantitative research relevance

- **Alternative-data engineering:** coordinate alignment, source provenance, asynchronous acquisition dates, resolution mismatch and missingness.
- **Signal design:** comparison-group definition, area weighting, standardized deviations and separation of numerical scores from presentation.
- **Research integrity:** spatial holdouts, independent-source checks, contradictory evidence and promotion criteria beyond one headline metric.
- **Reproducible tools:** persisted inputs and revisions, recoverable annotations, frozen numerical comparison arrays and consistent exports.

**Stack:** Python, NumPy, SciPy, Rasterio, Affine, Shapely, Pillow, Matplotlib, JavaScript/HTML and ReportLab, with Python and Node checks for numerical and interface behaviour.

## Current limits and next validation step

The system has not established either absolute or relative mechanical-firmness accuracy. Irrigation, rainfall, rootzone construction, maintenance and differential wetting can change actual conditions and reorder locations. Historical aerial imagery cannot supply live on-course measurements, and resampling satellite imagery cannot manufacture high-resolution independent evidence.

The next substantive validation step is a location- and time-matched field dataset of physical measurements, evaluated across independent courses and dates. Until then, HomeCourseAI is an explainable environmental-signal prototype, not a validated real-time firmness product.

This page documents the working local project; it does not publish the full application source or claim a deployed mobile service.

[Back to portfolio](../README.md#user-content-golf-analytics)
