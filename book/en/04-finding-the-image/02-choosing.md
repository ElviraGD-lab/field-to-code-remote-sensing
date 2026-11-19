---
title: "4.2 What we found and what we choose"
---

## Where we left off

We moved through the dates inside the frame round the burn scar and checked each one for clouds, shadows, smoke and snow. Now we compare what we found with the rules we wrote down before the search, and choose our pair of images.

## What turned up

In April 2026 there were 9 passes over our frame: on 3, 8, 10, 13, 18, 20, 23, 28 and 30 April. First we checked the dates around the fire:

| Date | What's in the frame | Usable? |
|---|---|---|
| 3 April | clear, no snow | yes |
| 8 April | almost clear, but two small white spots in the south of the frame | uncertain |
| 10 April | clear | yes |
| 13 April | clouds | no |
| 18 April | clouds | no |
| 20 April | clear, but a white spot in the centre of the burn scar | uncertain |

## The image record sheets

For each suitable date, we read the image name:

| Date | Satellite | Time, UTC | Orbit | Tiles | Processing version |
|---|---|---|---|---|---|
| 3 April | Sentinel-2B | 11:21:09 | R037 | 29TPH, 29TPJ | 05.12 |
| 8 April | Sentinel-2C | 11:21:11 | R037 | 29TPH, 29TPJ | 05.12 |
| 10 April | Sentinel-2A | 11:21:31 | R037 | 29TPH, 29TPJ | 05.12 |
| 20 April | Sentinel-2A | 11:21:31 | R037 | 29TPH, 29TPJ | 05.12 |

Three things stand out straight away.

1. **All the images come from the same relative orbit, R037.** Rule 6 takes care of itself: on every image, the satellite views the slopes at the same angle.
2. **The fire sits on the border between two tiles, 29TPH and 29TPJ.** That's why the catalogue shows two products for each date.
3. **The acquisition time hardly changes:** about 11:21. That's the sun-synchronous orbit from Chapter 3 at work.

## Scene cloud cover is misleading

We also tested the cloud cover filter that the catalogue offers. If we keep only images with scene cloud cover up to 25%:

- 18 April passes the filter, even though it's cloudy over the fire;
- 10 and 20 April fail it, even though it's clear over the fire.

The 8 April scene is cloudy too: the clouds lie to the north and south, but not over our frame.

**A filter based on the cloud cover of the whole scene would have thrown out two good images and let a bad one through.** That's direct confirmation of the rule: we check for clear skies inside our frame, not by the figure for the whole scene.

```{figure} ../../images/ch04-scene-cloud-filter-25.jpg
:label: en-fig-ch04-scene-cloud-filter-25
:alt: With the scene cloud cover filter at 25%, only 3, 8 and 18 April remain.
:width: 100%

With the scene cloud cover filter at 25%, only 3, 8 and 18 April remain. Contains modified Copernicus Sentinel data (2026).
```

```{figure} ../../images/ch04-whole-scene-2026-04-08.jpg
:label: en-fig-ch04-whole-scene-2026-04-08
:alt: The 8 April 2026 scene: clouds to the north and south, the frame almost clear.
:width: 100%

The 8 April 2026 scene: clouds to the north and south, the frame almost clear. Contains modified Copernicus Sentinel data (2026).
```

## The white spots on 8 April: clouds or not?

The white spots in the south of the frame on 8 April could have been tiny clouds, or they could have been pale rocks. We checked in two ways.

**Method 1: automatic classification.** L2A images come with a ready-made Scene classification layer:[^scl] the processing software has assigned every pixel to a class, such as 'vegetation', 'cloud', 'cloud shadow' or 'water'. We switched it on for 8 April.

The classification didn't confidently mark the spots as cloud: there are just a few pixels of 'cloud, medium probability' and 'unclassified'. But the layer showed us something else, something far more important. The software put most of the burn scar into the 'cloud shadows' or 'terrain shadows' class. A burn scar is dark, and to the software it looks like shadow.

**So if we used this layer as a cloud and shadow mask, it would cut out half our burn scar.** We can't trust an automatic mask blindly. We have to check it by eye, especially over a burn scar.

**Method 2: comparing with a neighbouring date.** Rocks and crags stay put; clouds move on. On the image of 10 April, two days later, there are no white spots in the same places.

**So on 8 April there are two tiny clouds inside the frame.** They cover a minute fraction of it, but they're there.

```{figure} ../../images/ch04-small-clouds-2026-04-08.jpg
:label: en-fig-ch04-small-clouds-2026-04-08
:alt: 8 April 2026, natural colour: two small white spots in the south of the frame.
:width: 100%

8 April 2026, natural colour: two small white spots in the south of the frame. Contains modified Copernicus Sentinel data (2026).
```

```{figure} ../../images/ch04-scene-classification-2026-04-08.jpg
:label: en-fig-ch04-scene-classification-2026-04-08
:alt: Scene classification layer of 8 April 2026: much of the burn scar is classed as shadow.
:width: 100%

Scene classification layer of 8 April 2026: much of the burn scar is classed as shadow. Contains modified Copernicus Sentinel data (2026).
```

## Deciding by the rules

Now we apply the rules we wrote down before the search, with no exceptions.

- **The 'before' image is 3 April 2026.** It's the nearest clear image before the fire: 3 days before it. There are no clouds, shadows or snow in the frame. The only snow is far to the south, in the high mountains.
- **The 'after' image is 10 April 2026.** Rule 4 says there must be no clouds in the frame. 8 April breaks that rule, so the first completely clear image after the fire is 10 April.
- **There are 7 days between the images.** Under rule 3, anything up to two weeks counts as 'good'.

**We're not taking 8 April, even though it's the image the 681 ha was outlined on, and even though the clouds are tiny.** This is exactly why we wrote the rules down in advance: so that our choice doesn't depend on which image is more familiar or looks nicer.

The price of this decision is small. The trace of the fire barely fades in two days, and we keep the 8 April image as a reserve and for comparison.

We don't need the 20 April image for the pair, but it will be useful for the time series in Chapter 13. There, the white spot in the centre of the burn scar will have to be excluded from the calculation.

```{figure} ../../images/ch04-before-2026-04-03-swir.jpg
:label: en-fig-ch04-before-2026-04-03-swir
:alt: The 'before' image: 3 April 2026, SWIR.
:width: 100%

The 'before' image: 3 April 2026, SWIR. Contains modified Copernicus Sentinel data (2026).
```

```{figure} ../../images/ch04-after-2026-04-10-swir.jpg
:label: en-fig-ch04-after-2026-04-10-swir
:alt: The 'after' image: 10 April 2026, SWIR.
:width: 100%

The 'after' image: 10 April 2026, SWIR. Contains modified Copernicus Sentinel data (2026).
```

We'll download both tiles for each date we need. In Chapter 5 we'll open the files and check which tile covers our whole frame.

:::{admonition} Your data
For your own fire, make the same table: date, what's in the frame, whether it's usable, and the image record sheet. The Scene classification layer is useful, but over a burn scar it can mistake burnt areas for shadow. Check it by eye.
:::

## Summary

**New terms**

- **Scene classification (SCL):** a ready-made layer of classes that comes with an L2A image: vegetation, cloud, shadow, water, snow and others.
- **Cloud mask:** a layer used to exclude pixels with clouds and shadows from a calculation.

**Key points**

- The cloud cover of the whole scene doesn't tell us whether our area is clear.
- An automatic cloud mask can mistake a burn scar for shadow, so we check it by eye.
- We tell a cloud from a rock by comparing with a neighbouring date: clouds move on, rocks stay.
- We decide by the rules written down in advance, even if another image is more familiar.

## Questions for an engineer

1. Why didn't we take the 8 April image, even though the clouds cover only a minute fraction of the frame?

:::{dropdown} Answer
Because the rule we wrote down before the search says there must be no clouds in the frame, and the 10 April image meets that rule. If we start bending the rules 'just a little', our choice will once again depend on what we want. Besides, two days hardly change the trace of the fire.
:::

2. We want to exclude clouds and shadows automatically using the Scene classification layer. Why is that risky over a burn scar?

:::{dropdown} Answer
The layer puts many burn scar pixels into the shadow classes, because a burn scar is dark. A mask based on this layer would cut out most of the burn scar, and the area would come out much smaller than it really is.
:::

3. How can we tell a small cloud from a pale rock without leaving Copernicus Browser?

:::{dropdown} Answer
Look at the same place on a neighbouring date. Within a few days a cloud will have gone or moved, while a rock stays where it is. A cloud also usually has a shadow next to it.
:::

## The open question

Our pair of images is chosen: 3 and 10 April 2026. But what exactly is in the file we'll download? What are the numbers in it, and why are they already surface reflectance rather than just the light that reached the satellite? That's Chapter 5.

---

## Notes and sources

[^scl]: [Copernicus SentiWiki, *Sentinel-2 processing*](https://sentiwiki.copernicus.eu/web/s2-processing): the Sen2Cor processor delivers a scene classification layer (SCL) with each L2A product.
