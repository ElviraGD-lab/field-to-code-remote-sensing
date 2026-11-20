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
