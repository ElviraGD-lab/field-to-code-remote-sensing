---
title: "5.1 Downloading an image"
---

## Where we left off

Our pair of images is chosen: 3 April 2026 ('before') and 10 April 2026 ('after'). So far we've only looked at them in Copernicus Browser. The browser showed us a picture, but we can't work with the numbers there. For that, we need the actual files on our own computer.

In this lesson we do just one thing: download the 3 April image and see what lands in the folder.

## What we want to know

**The question:** what exactly do we get when we download a Sentinel-2 image?

**Our hypothesis before we start:**

1. We'll get a single archive of about 1 GB. That's what the catalogue showed.
2. Inside, there won't be one picture but lots of files: one for each band. After all, the satellite measures its 13 bands separately.
3. The files will be sorted by pixel size: 10, 20 and 60 metres.

**How we'll know we were wrong:** if there are fewer or more files than we expect, or they're organised differently.

## Step 1: Which of the two products to download

We remember that the fire sits on the border between two tiles, 29TPH and 29TPJ. There are two products for each date. We don't need to download both if our frame fits entirely inside one.

1. In Copernicus Browser, we open the Search tab.
2. We choose Sentinel-2 L2A and the date 3 April 2026, and click Search.
3. There are two products in the list. Each has a crosshair icon. We click it, and the product's outline appears on the map.
4. We check whether our yellow frame lies entirely inside the outline. First one product, then the other.

We download the product that our frame fits inside completely.

```{figure} ../../images/ch05-search-2026-04-03-tile-29TPH.jpg
:label: en-fig-ch05-search-2026-04-03-tile-29TPH
:alt: Outline of the 29TPH product of 3 April 2026 (green): its northern edge crosses the frame (yellow).
:width: 100%

Outline of the 29TPH product of 3 April 2026 (green): its northern edge crosses the frame (yellow). Contains modified Copernicus Sentinel data (2026).
```

```{figure} ../../images/ch05-search-2026-04-03-tile-29TPJ.jpg
:label: en-fig-ch05-search-2026-04-03-tile-29TPJ
:alt: Outline of the 29TPJ product of 3 April 2026 (green): the frame (yellow) lies entirely inside.
:width: 100%

Outline of the 29TPJ product of 3 April 2026 (green): the frame (yellow) lies entirely inside. Contains modified Copernicus Sentinel data (2026).
```

## Step 2: Downloading

1. For the chosen product, we click the download icon (the down arrow).
2. We save the file in the project's `data` folder, in a subfolder called `sentinel2`. If it doesn't exist, we create it.
3. We wait for the download to finish. The file is large, so it may take a few minutes.

## Step 3: Unpacking

The downloaded file is an archive ending in `.zip`. We open it with a double click in Finder. A folder appears next to it, with a name ending in `.SAFE`.

`.SAFE` is the standard 'packaging' for Sentinel images. The folder name is the same as the product name, which we learnt to read in Chapter 4.

## Step 4: Looking inside

We open the `.SAFE` folder in Finder and work our way down it step by step.

1. At the top there are several folders and files. Two of them matter to us:
   - the file `MTD_MSIL2A.xml`, the record sheet for the whole product;
   - the folder `GRANULE`, which holds the data itself.
2. We open `GRANULE`. Inside there's one folder named after the tile, for example `L2A_T29TPJ_...`.
3. We open that. It contains an `IMG_DATA` folder with the images, and the file `MTD_TL.xml`, the tile's record sheet. This records the sun's elevation and azimuth at the moment the image was taken.
4. We open `IMG_DATA`. Inside are three folders: `R10m`, `R20m` and `R60m`. The number is the pixel size.
5. We open `R20m` and count the files in it.

```{figure} ../../images/ch05-safe-tree-2026-04-03.jpg
:label: en-fig-ch05-safe-tree-2026-04-03
:alt: The .SAFE folder of 3 April 2026 in Finder.
:width: 100%

The `.SAFE` folder of 3 April 2026 in Finder.
```

Before we count, let's write down what we expect. In Chapter 3 we saw that bands B05, B06, B07, B8A, B11 and B12 have 20-metre pixels. So in the `R20m` folder we expect 6 band files.

Each file has a name something like `T29TPJ_20260403T112109_B12_20m.jp2`. It reads like this:

| Part | What it means |
|---|---|
| T29TPJ | tile |
| 20260403T112109 | date and time of acquisition |
| B12 | band |
| 20m | pixel size |
| .jp2 | file format (JPEG 2000) |

## What we found

**Our hypothesis was half right: we guessed how the folders are organised, but not how many files there would be.**

**Which product.** Only tile 29TPJ covers our whole frame. The northern edge of tile 29TPH runs straight through the frame, and part of the burn scar falls outside it. So one product is enough for our fire, 29TPJ, and there's no need to download both.

**Size.** The 3 April archive is 887 MB, a little less than we expected. The neighbouring tile, 29TPH, is 1,151 MB for the same date. The size also changes from date to date: the same tile 29TPJ on 8, 10 and 20 April comes in at between 911 and 991 MB. JPEG 2000 compresses the image, and how much space a file takes depends on what's in it: sea, clouds, mountains.

**What's at the top of the `.SAFE` folder.** Besides `MTD_MSIL2A.xml` and `GRANULE`, there are also:

- the folders `DATASTRIP`, `HTML` and `rep_info`;
- the files `manifest.safe` and `INSPIRE.xml`;
- a small preview image ending in `-ql.jpg`.

These are housekeeping files: a description of the acquisition, a list of the contents, and schemas for checking the record sheets. We don't need them to work with the image.

**The tile folder** is called `L2A_T29TPJ_A047396_20260403T112705`. Its name has three parts:

- the tile: T29TPJ;
- the number of the satellite's orbit since it started work: A047396;
- the start time of the imaging strip.

```{figure} ../../images/ch05-r10m-r20m-2026-04-03.jpg
:label: en-fig-ch05-r10m-r20m-2026-04-03
:alt: Contents of the R10m and R20m folders of 3 April 2026.
:width: 100%

Contents of the `R10m` and `R20m` folders of 3 April 2026.
```

**How many files are in `R20m`.** We expected 6. There were 14:

```text
T29TPJ_20260403T112109_AOT_20m.jp2
T29TPJ_20260403T112109_B01_20m.jp2
T29TPJ_20260403T112109_B02_20m.jp2
T29TPJ_20260403T112109_B03_20m.jp2
T29TPJ_20260403T112109_B04_20m.jp2
T29TPJ_20260403T112109_B05_20m.jp2
T29TPJ_20260403T112109_B06_20m.jp2
T29TPJ_20260403T112109_B07_20m.jp2
T29TPJ_20260403T112109_B11_20m.jp2
T29TPJ_20260403T112109_B12_20m.jp2
T29TPJ_20260403T112109_B8A_20m.jp2
T29TPJ_20260403T112109_SCL_20m.jp2
T29TPJ_20260403T112109_TCI_20m.jp2
T29TPJ_20260403T112109_WVP_20m.jp2
```

Let's work out where the extra eight came from:

1. **6 bands with a native 20 m pixel:** B05, B06, B07, B8A, B11, B12. These are the ones we expected.
2. **4 bands resampled from another pixel size.** B02, B03 and B04 are captured with a 10 m pixel, and B01 with a 60 m pixel. What we have here are copies of them resampled onto the 20 m grid. That makes it easy to compare them with the other bands pixel for pixel.
3. **4 files that aren't bands at all:**
   - SCL: the scene classification, the very layer from Lesson 4.2;
   - TCI: a ready-made natural-colour picture, just for viewing;
   - AOT: a map of aerosols, showing how hazy the air was;
   - WVP: a map of water vapour in the atmosphere.

   The processor worked out AOT and WVP itself, while it was recalculating the image 'as if there were no atmosphere'.

**What *isn't* in `R20m`:**

- B08: the narrow band B8A is there instead.
- B09: it's only in `R60m`.
- B10: it isn't anywhere. This band looks at high cirrus clouds and barely reaches the ground, so it's left out of the L2A product.

**The main mismatch:** one band can appear in a product several times, at different pixel sizes. So 'one file, one band' is wrong. The right version is: one file, one band at one pixel size.

```{figure} ../../images/ch05-four-safe-folders.jpg
:label: en-fig-ch05-four-safe-folders
:alt: The four downloaded dates in data/sentinel2: 3, 8, 10 and 20 April 2026, tile 29TPJ.
:width: 100%

The four downloaded dates in `data/sentinel2`: 3, 8, 10 and 20 April 2026, tile 29TPJ.
```

**We've downloaded four dates.** Besides 3 April, the `data/sentinel2` folder now holds 8, 10 and 20 April, all of them tile 29TPJ, orbit R037:

- 10 April is our 'after' image;
- 8 April is the reserve;
- 20 April will be needed when we look at how the burn scar changes over time.

## If something goes wrong

1. **The download button doesn't work.** Only users who are logged in to Copernicus Browser with their own account can download. We log in and try again.
2. **The frame doesn't fit in any tile.** This happens when a burn scar lies right on a tile border. Then we download both products for the same date and stitch them together later. Neighbouring tiles overlap: each tile is a 110 × 110 km square, but they're spaced 100 km apart.
3. **The size doesn't match the catalogue or another date.** That's normal: the compression depends on what's in the image.

:::{tip} Did you know?
The `R10m` folder takes up more than half of the whole product: 541 of 888 MB. Nearly all of that space goes on the four bands with a 10 m pixel: B02, B03, B04 and B08. Half the pixel size means four times as many pixels.
:::

:::{admonition} Your data
For your own fire: find your date in the Search tab, check the product outline against your frame, and download the one that covers it completely. The `.SAFE` folder is organised the same way for every Sentinel-2 L2A image.
:::

## Summary

**New terms**

- **`.SAFE`**: the standard packaging for a Sentinel product, a folder holding the data and the record sheets. Example: `S2B_MSIL2A_20260403T112109_N0512_R037_T29TPJ_20260403T153931.SAFE`.
- **Product record sheet**: the file `MTD_MSIL2A.xml`, a description of the whole product.
- **Tile record sheet**: the file `MTD_TL.xml`. Among other things, it records the sun's elevation and azimuth.
- **JPEG 2000 (`.jp2`)**: the compressed format the bands are stored in.
- **Resampling**: moving a band onto a grid with a different pixel size. Example: `B04_20m.jp2` is band B04 resampled from 10 m to 20 m.
- **SCL, TCI, AOT, WVP**: files in the L2A product that aren't bands: the scene classification, a colour picture for viewing, an aerosol map and a water vapour map.

**Key points**

- One product per date is enough for our burn scar: tile 29TPJ.
- One band can appear in a product at several pixel sizes.
- To find the file we need, we read its name: tile, date, band, pixel size.

## Questions for an engineer

1. B04 is in both `R20m` and `R10m`. Which one do we use?

:::{dropdown} Answer
It depends on the task. If we're calculating something together with the 20 m bands (B12, for example), we take `B04_20m`: then all the pixels are the same size and line up. If we need the most detailed picture, we take `B04_10m`. Resampling can't add more detail than the satellite captured.
:::

2. Why not work straight from TCI? It's already in colour.

:::{dropdown} Answer
TCI holds a picture for the eye, not measurements. Its values are squeezed into the brightness range of a screen, so we can't calculate an index from it.
:::

3. Why did we download 8 and 20 April if the pair is already chosen?

:::{dropdown} Answer
8 April is the reserve 'after' image. 20 April is needed for the second research question: how quickly the trace of the burn scar fades over time.
:::

## Exercises

1. Recall: what does the name of the folder holding a Sentinel-2 image end in once it's unpacked?
2. Fix it: there's one mistake in the file name `T29TPJ_20260403T112109_B12_10m.jp2`. What is it?
3. One lesson back (4.2): why didn't we use the Scene classification layer as a cloud mask over our burn scar?

## The open question

We know where band B12 lives and what its file is called. But what's actually written in each pixel? It isn't yet a reflectance between 0 and 1: it's a whole number. What that number is, and how to convert it into reflectance, we'll find out in Lesson 5.2, when we open the band in SNAP.

---

## Notes and sources

[Copernicus SentiWiki, 'S2 Products'](https://sentiwiki.copernicus.eu/web/s2-products), accessed 19 November 2026. What we took from it:

- the contents of the L2A product in the 10, 20 and 60 m folders;
- that B08 isn't in the 20 m folder and B10 isn't in L2A;
- the SAFE format and JPEG 2000;
- tiles of 110 × 110 km.
