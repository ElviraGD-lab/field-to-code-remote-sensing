# Analysis plan (written before any burn-area or time-series computation)

Version 1, 19 November 2026. Image selection criteria were recorded on 10 November 2026 (`image-selection-criteria.md`). Any later change is listed under *Changes* with its date and reason, and results are reported under both the original and the changed plan.

## Questions

**Q1.** What area of vegetation burned in the fire of 6 April 2026 at Bustantigo (Allande, Asturias), measured on the first clear Sentinel-2 image after the fire, with a 95% confidence interval, and how much does this area depend on slope illumination?

**Q2.** How does the spectral trace of fires of February–April 2026 in the mountain heathlands of Asturias change from the first clear post-fire image until November 2026, and what part of that change is explained by the seasonal change of slope illumination rather than by vegetation regrowth?

## Fires

All EFFIS burnt areas in Asturias with a start date between 1 February and 30 April 2026 and an area of at least 200 ha (EFFIS burnt areas API, retrieved 19 November 2026): 7 fires — Allande (Bustantigo, 700 ha, main fire), Salas (437 ha), Cangas del Narcea (341 ha), Onís (250 ha), Peñamellera Alta (229 ha), Belmonte de Miranda (219 ha), Cabrales (201 ha). A fire without at least four clear post-fire observations is reported but not analysed, with the reason.

## Data

- Sentinel-2 L2A products (full SAFE, Copernicus Data Space Ecosystem); product names recorded for every image.
- Q1 pair: 3 April 2026 (S2B) and 10 April 2026 (S2A), relative orbit R037, tiles 29TPH/29TPJ, processing baseline 05.12. 8 April 2026 kept as an alternative (two small clouds in the area of interest).
- Q2 series: all clear observations February–November 2026 over each fire, and anniversary observations (same day of year ± 5 days) in 2024 and 2025 from the same relative orbit.
- Terrain: PNOA MDT05 (CNIG), resampled to 20 m.
- Reference: field points (planned 28–29 November 2026), Sentinel-2 10 m visual interpretation, PNOA orthophoto 2026 if available.
- Cloud screening: visual (Q1); CloudScore+ in Google Earth Engine (Q2). The L2A scene classification (SCL) is not used as the cloud mask, because on our scene it classes much of the burn scar as shadow.

## Methods

**Q1.** NBR, dNBR and RBR from the image pair. Burnt / unburnt by a fixed threshold and by a classifier; area estimated from a stratified random sample following Olofsson et al. (2014), with user's and producer's accuracy and a 95% confidence interval. Area is computed three times: raw; excluding self-shadowed pixels (cos i ≤ 0.2); with an unburnt-control offset per illumination class. Compared with EFFIS (700 ha) and edu.forestry.es (681 ha).

**Q2.** For each fire and each clear date:
1. raw change: NBR(date) − NBR(pre-fire image);
2. anniversary change: NBR(date, 2026) − NBR(same day of year, median of 2024 and 2025), which removes the seasonal change of illumination by design (same orbit, same overpass time);
3. the difference between (1) and (2) is the illumination-plus-phenology part; unburnt controls of the same illumination class separate the 2026 weather anomaly; invariant surfaces (rock, roads, quarries) and near-flat terrain separate illumination from phenology.

Pixels burnt in another fire in 2023–2025 are excluded from anniversary baselines; the 2017 burn overlaps 44% of the 2026 Bustantigo burn and is recorded as fire history.

## Checks (criteria fixed now)

| Check | Pass if |
|---|---|
| L2A value range | reflectance roughly 0–1 after the offset |
| Clear image | no clouds, shadows, haze or snow over the area of interest (visual, true colour and SWIR) |
| Map accuracy (Q1) | overall accuracy ≥ 85%; otherwise causes are analysed, not tuned |
| Agreement with field points | ≥ 85% |
| Negative control (Q2) | unburnt control: corrected change around 0 at all dates (\|median\| < 0.05) |
| Autumn check (Q2) | at dates whose illumination equals the pre-fire image (mid-September to mid-October), corrected and raw curves agree within their spread |
| Placebo fire (Q2) | same computation on unburnt areas with the same slopes: corrected change around 0 at all dates |

## What counts as a result

Any of these is a result and will be reported with numbers: the fading is mostly illumination; mostly regrowth; or the two cannot be separated with these data.

## Limits stated in advance

No field severity data straight after the fire (we study the spectral trace, not severity); April cloudiness leaves gaps; 20 m pixels blur edges and small unburnt islands; seven fires of one spring are not a regional sample; field points near paths are a biased sample.

## Changes

None yet.
