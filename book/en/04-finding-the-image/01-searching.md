---
title: "4.1 Searching for images"
---

## Where we left off

The rules for choosing images are written down in advance. We know what the satellite measures and why many passes are useless because of cloud. Now we're looking for a pair: the nearest clear image before the fire and the first clear image after it.

## What we expect to find

First, as always, let's write down what we expect.

- **The 'after' image.** Most likely it's 8 April 2026: that's the image the 681 ha was outlined on, and in Chapter 1 we saw that it's clear over the burn scar. But the rule asks for the first clear image after the fire. So we need to check whether there's an earlier clear image, on 6 or 7 April, when the fire might still have been burning.
- **The 'before' image.** Here we know nothing. Asturias is often cloudy in spring, so we may have to go back several weeks from the fire.

## Step 1: Marking our area

The rules are checked not on the whole scene but on the burn scar plus 1 km around it. To see this area on every image, let's mark it on the map.

1. In Copernicus Browser, we open the image of 8 April 2026 in the SWIR visualisation: the burn scar shows up best there.
2. We zoom in until the burn scar fills about a third of the screen.
3. On the right, we choose the polygon tool (the pentagon icon) and draw round the burn scar with a margin of about 1 km on all sides. Precision doesn't matter: this is just a frame inside which we'll look for clouds.

The frame now stays on the map as we move through the dates.

```{figure} ../../images/ch04-frame-2026-04-08-swir.jpg
:label: en-fig-ch04-frame-2026-04-08-swir
:alt: The study-area frame (yellow) on the 8 April 2026 image in SWIR; on the left, the calendar of dates with passes.
:width: 100%

The study-area frame (yellow) on the 8 April 2026 image in SWIR; on the left, the calendar of dates with passes. Contains modified Copernicus Sentinel data (2026).
```

## Step 2: Going back through the dates

Next to the date there are arrows, '‹' and '›'. They jump to the previous or next day with a pass. The zoom and the frame stay the same, so it's easy to compare the same place across dates.

For each date, we look inside the frame and ask ourselves four questions:

1. Are there any clouds?
2. Are there any cloud shadows? We check in SWIR: a shadow is almost black.
3. Is there any smoke or active fire?
4. Is there any snow? In SWIR, snow is light, a bluish white.

If the answer to any question is 'yes', the image won't do, and we move on.

First we check 'after': the dates 6, 7 and 8 April. We take the first one where all four answers are 'no'.

Then we check 'before': from 5 April backwards, day by day, until we find the first clear image.

## Step 3: Reading the image's record sheet

For the chosen date, we click 'Find products for current view' under the date. Copernicus Browser shows a list of the images that cover the screen. Each one has a long name, for example:

S2B_MSIL2A_20260408T112119_N0511_R037_T29TPH_20260408T151234

This name is the image's record sheet written as a single line. Let's take it apart (the numbers in the example are made up):

| Part | What it means |
|---|---|
| S2B | satellite: Sentinel-2B |
| MSIL2A | MSI instrument, processing level L2A |
| 20260408T112119 | date and time of acquisition, GMT: 8 April 2026, 11:21:19 |
| N0511 | processing version 05.11 |
| R037 | relative orbit 37 |
| T29TPH | tile 29TPH |
| the last part | when the image was processed |

From this one name, anyone can find exactly the same image. So we always write the name down in full.

```{figure} ../../images/ch04-products-2026-04-03.jpg
:label: en-fig-ch04-products-2026-04-03
:alt: L2A products of 3 April 2026 covering the frame: one per tile (29TPH and 29TPJ).
:width: 100%

L2A products of 3 April 2026 covering the frame: one per tile (29TPH and 29TPJ). Contains modified Copernicus Sentinel data (2026).
```

## Step 4: Screenshots of the whole scene and a close-up

For each image we choose, we take:

1. **A view of the whole scene:** we zoom out until most of the tile is visible, about 100 km across, in natural colour. This screenshot shows the cloud cover of the whole scene.
2. **A close-up of the burn scar:** we zoom in to the frame, in natural colour and in SWIR.

:::{admonition} Your data
This procedure works for any fire: a frame round the burn scar with a margin, moving through the dates with the arrows, four questions inside the frame, and the image name as its record sheet.
:::
