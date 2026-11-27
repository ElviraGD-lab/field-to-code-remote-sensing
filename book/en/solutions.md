---
title: "Solutions"
---

Answers to the exercises in each lesson.

## Lesson 5.1

1. The folder name ends in `.SAFE`.
2. Band B12 is captured with a 20 m pixel, so the name should end in `20m`, not `10m`: `T29TPJ_20260403T112109_B12_20m.jp2`. There's no 10 m copy of B12 in the product.
3. The Scene classification layer put most of the burn scar into the shadow classes, because a burn scar is dark. A mask based on this layer would have cut out the burn scar along with the 'shadows', and the area would have come out much smaller than it really is.

## Lesson 5.2

1. The product record sheet, `MTD_MSIL2A.xml`, in the `.SAFE` folder.
2. There are 12 bands, not 13. The satellite captures 13 bands, but B10 isn't included in the L2A product. In SNAP: B1–B9, B8A, B11, B12.
3. So that we check for clouds only where they matter: over the burn scar and in a strip of about 1 km round it, not over the whole 110 × 110 km scene. Otherwise we would have thrown out images that were clear over the burn scar because of clouds tens of kilometres away from it.

## Lesson 5.3

1. TOA is top of atmosphere, the reflectance at the top of the atmosphere, level L1C. BOA is bottom of atmosphere, the reflectance at the surface, level L2A.
2. It's the other way round. Short-wave, blue light is scattered the most, so band B2. Long waves, as in B12, are scattered the least.
3. In natural colour, both the burn scar and the shadow look like a dark patch on a green background: in visible light, both reflect little. The infrared bands help to tell them apart. In SWIR, the burn scar is reddish-brown and the shadow almost black.

## Lesson 6.1

1. Because the same reflectance gives a different brightness on the screen with a different min and max. A difference in colour may be a difference in the settings, not in the ground. In our case, the B12 reflectance at the point outside the burn scar differed by 3%, but the blue light by 2.6 times.
2. The brightness on the screen depends on the stretch. To talk about reflectance, we need to look at the numbers in Pixel Info or Pin Manager, or first set the same stretch on both images.
3. In L1C, light from the atmosphere is mixed in with the ground's reflectance, and the amount varies from day to day. Part of the difference between the dates would then be a difference in the weather. In L2A, that contribution has been removed.
