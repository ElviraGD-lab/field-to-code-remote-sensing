---
title: "Prologue: When the mountain burns"
---

## What happened on 6 April 2026

On 6 April 2026 it was hot in Asturias – over 30 degrees – and a southerly wind was blowing. Within 24 hours, 26 fires broke out.[^1]

We'll take the largest of them. It burned near the hamlet of Bustantigo in the municipality of Allande, on the border with Tineo.[^2] This is a mountain parish with 18 inhabitants.[^3]

It wasn't forest that burned. Almost 99% of the burnt area was open heathland: heather, gorse and grass.[^4]

And this isn't the first time the place has burned:

1. **April 2017:** 720 ha.[^5]
2. **Late March 2023:** about 1,200 ha.[^6]
3. **April 2026:** Bustantigo again.

**On these slopes, fire is a repeat, not an accident.**

## Why Asturias burns in spring

In Asturias the big fires don't come in summer, as they do in the south of Spain. They come in late winter and spring. Over the past 40 years, more than half of the large fires – those over 500 hectares each – happened in February, March or April.[^7]

The reason is simple. After winter the slopes are full of dry grass and dead branches, and the new green growth hasn't come through yet.

So the typical Asturian fire means spring, heathland and a steep slope. But most methods for mapping burn scars were designed for something else: summer forest fires.

**That's why we don't take these methods on trust. We test them.**

## Why we need to know how much burned

The area and the boundary of a burn scar drive real decisions:

1. **The law.** Burnt forest land can't be turned over to another use for 30 years.[^8] For that, we need to know exactly where the edge of the burn scar runs.
2. **Statistics and plans.** The regional fire plan is built on the areas of past fires.[^7]
3. **Recovery.** The burn scar map is used to decide where to protect slopes from erosion before the autumn rains.

**A mistake in the area doesn't stay on paper. It feeds into the law, the plans and the decisions.**

## One fire, different figures

How much burned at Bustantigo? It depends on whom we ask:

- the open catalogue of Spain's large wildfires gives **681 ha**, and its author warns that the boundary may be out by hundreds of metres;[^9]
- the European service EFFIS gives **700 ha**;[^4]
- we couldn't find an official perimeter that's openly available.

The problem isn't that the figures differ. The problem is that none of them comes with an uncertainty. We don't know whether 681 means 'between 670 and 690' or 'between 500 and 850'. And a measurement without an uncertainty can't be checked.

**The right answer to 'how much burned?' is a figure with an interval, plus an explanation of how we got it.**

## Why the satellite gets it wrong in the mountains

A satellite doesn't see fire. It measures the light reflected by the ground. A burnt slope reflects light differently from a living one, and that difference is how we find the burn scar.

But in the mountains, the amount of light depends on which way a slope faces and how high the sun is. Sentinel-2 images Asturias at around midday. Here's how much direct light the surface gets at that moment, where 1 means the sun is exactly perpendicular to it and 0 means the light is just grazing the slope:[^10]

| Date | Sun elevation | Flat ground | North slope, 25° | South slope, 25° |
|---|---|---|---|---|
| 20 February | 32° | 0.54 | 0.16 | 0.81 |
| 8 April | 51° | 0.77 | 0.46 | 0.94 |
| 21 June | 66° | 0.91 | 0.69 | 0.96 |

What we see here:

1. **The south slope** gets almost the same light all year round.
2. **The north slope** gets four times as much light in June as in February.
3. In February, **steep north slopes** sit in their own shadow.

Now take a spring fire. The 'before' image was taken in winter, with the sun low. The 'after' images are taken in spring and summer, as the sun climbs higher and higher. On each new image the north slope looks brighter, simply because more light falls on it – even if nothing has grown there yet.

The standard processing of Sentinel-2 images partly corrects for this. But on poorly lit slopes, according to its own documentation, it overcorrects.[^11] So the problem remains.

**If we don't account for light, the satellite will mistake spring sunshine for regrowing grass.**

## What's already known

Each piece of this is already known:

1. **How to find a burn scar.** We compare images from before and after the fire. The authors of the method themselves advise using images from the same season.[^12]
2. **That the signal fades over time.** In Portugal, researchers found that 3–4 months after a fire, a lightly burnt patch can already look unburnt on the image.[^13]
3. **That terrain and light get in the way.** This has been shown in Alaska[^14] and in Greece.[^15]

But we haven't found any study that, for spring fires in mountain heathland, separates the effect of light from what has actually grown back on the burn scar.

## What we'll do

We'll answer two questions:

1. **How much burned at Bustantigo** – with an uncertainty, and how far that figure depends on how the slopes are lit.
2. **How quickly the trace of the fire fades from the images**, and how much of that fading is just light rather than regrowing grass. We'll test this on the Bustantigo fire and on four more fires from the same spring.

We'll work with open Sentinel-2 images, in Copernicus Browser and QGIS.

We'll check every result in three ways:

1. **With random points** on high-resolution imagery.
2. **On the ground:** we'll go to the fire site.
3. **In autumn.** In October the sun is as low again as it is in March. If the trace faded because of the light, it will partly come back in autumn. If grass has grown there, it won't.

**What we don't claim:**

- anything about how badly the fire damaged the soil: that would need measurements on the ground straight after the fire, and there aren't any;
- anything about the causes of the fires;
- anything about fires in general: five fires from one spring are still just five fires.

Any answer will be a result – even the answer 'light and grass can't be separated'.

All of this can be repeated for any fire: Sentinel-2 images are open and free for anywhere on Earth. Wherever you need to plug in your own data, we'll show you how.

We'll go the whole way together: how we search for images, how we think, where we go wrong and how we check.

**In the mountains of Asturias, a satellite can mistake spring sunshine for regrowing grass. We'll learn to tell the two apart – and say honestly how much really burned.**

---

## Notes and sources

[^1]: [RTPA, 'Preocupan los incendios del suroccidente', 7 April 2026](https://www.rtpa.es/noticias-asturias/2026-04-07/Preocupan-los-incendios-del-suroccidente_111775542887.html) (in Spanish).
[^2]: [La Voz del Trubia, 7 April 2026](https://lavozdeltrubia.es/2026/04/07/se-dispara-en-extension-el-incendio-de-belmonte-y-en-tineo-el-fuego-corta-la-as-15-2/); [elDiario.es, 8 April 2026](https://www.eldiario.es/asturias/asturias-sufre-nueva-oleada-incendios-principado-atribuye-mayoria-accion-delincuentes_1_13125911.html) (both in Spanish).
[^3]: [Wikipedia, 'Bustantigo'](https://en.wikipedia.org/wiki/Bustantigo); population as of 1 January 2024.
[^4]: EFFIS, the European Forest Fire Information System: burnt area 294223, Allande, start 6 April 2026 at 01:30, updated 9 April 2026; 700 ha, 98.9% other natural land cover and 1.1% broadleaved forest. [EFFIS burnt areas API](https://api.effis.emergency.copernicus.eu/rest/2/burntareas/current/).
[^5]: [ORT Noticias, 29 June 2017](https://ort-ort.com/allande-ibias-y-grandas-de-salime-victimas-de-los-3-grandes-incendios-forestales-que-ha-sufrido-asturias-en-los-cinco-primeros-meses-del-ano/) (in Spanish): Bustantigo (Allande) fire, 720.62 ha.
[^6]: [elDiario.es, 5 May 2023](https://www.eldiario.es/asturias/fiscalia-pide-ingreso-prision-causante-incendio-allande-quemo-1-200-hectareas_1_10179347.html) (in Spanish): fire at Bustantigo on 28 March 2023, 1,200 ha.
[^7]: [Principality of Asturias, EPLIFA 2026–2030](https://www.asturias.es/documents/d/guest/eplifa_2026-2030-con-anejos_03062026) (in Spanish): 40 of the 73 large fires of 1984–2024 occurred in February, March and April (54.8% of the fires and 57.3% of their area).
[^8]: [Spanish Forest Act 43/2003, Article 50](https://www.boe.es/buscar/act.php?id=BOE-A-2003-21339#a50) (in Spanish).
[^9]: [edu.forestry.es, 'Grandes Incendios Forestales 2026 en España'](https://edu.forestry.es/p/gif2026.html) (in Spanish): Allande, 6 April 2026, 681 ha, perimeter drawn on a Sentinel-2 image of 8 April 2026. The author warns that the boundaries 'may contain errors of hundreds of metres'.
[^10]: Own calculation for 43.36° N, 6.67° W at 11:20 UTC, the approximate Sentinel-2 overpass time. The sun's position is computed with the NOAA formulas; the fraction of direct light is the cosine of the angle at which the rays strike the slope.
[^11]: [ESA, *Sen2Cor Level-2A Algorithm Theoretical Basis Document*, v2.10](https://step.esa.int/thirdparties/sen2cor/2.10.0/docs/S2-PDGS-MPC-L2A-ATBD-V2.10.0.pdf), section on mountainous terrain; see also the [Copernicus Data Space forum, 2024](https://forum.dataspace.copernicus.eu/t/please-make-sentinel-2-l2a-available-without-the-terrain-over-correction/417).
[^12]: Key, C. H. and Benson, N. C. (2006). *Landscape Assessment (LA)*. USDA Forest Service, RMRS-GTR-164-CD.
[^13]: [Jahanianfard, D. et al. (2025). *Earth System Science Data* 17: 4957](https://doi.org/10.5194/essd-17-4957-2025): for each day's delay in the image, dNBR drops by about 0.0009, and after 110 days the error exceeds 0.1 – the boundary between 'unburnt' and 'low severity' on the Key and Benson (2006) scale.
[^14]: [Verbyla, D. et al. (2008). *International Journal of Wildland Fire* 17: 527](https://doi.org/10.1071/WF08038).
[^15]: [Veraverbeke, S. et al. (2010). *International Journal of Applied Earth Observation and Geoinformation* 12: 60–70](https://doi.org/10.1016/j.jag.2009.10.004).
