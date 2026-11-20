---
title: "5.2 Opening the image in SNAP"
---

## Where we left off

Four images are now sitting on our computer. We know how the `.SAFE` folder is organised and where band B12 lives inside it. But we haven't yet seen the actual numbers in the files.

In this lesson we open the 3 April image in SNAP and read the number in a single pixel.

## Why SNAP

SNAP is free software from the European Space Agency for working with Sentinel images. It understands the whole `.SAFE` folder: it opens all the bands, record sheets and masks as a single product. We don't have to hunt for files in the folders by hand.

The maps, the frame and the burn scar outline we'll make later in QGIS, which is better for working with vectors. Everything to do with the image itself, we do in SNAP.

## What we want to know

**The question:** what number is stored in a pixel of band B12, and what does it mean?

**Our hypothesis before we start:**

1. In SNAP, each band will appear once, not at three pixel sizes as in the folders. That makes 12 bands in all: the satellite captures 13, but B10 isn't included in the L2A product.
2. In the B12 pixel we'll see a whole number in the thousands, the same as the one stored in the file.

**How we'll know we were wrong:** if there's a different number of bands, or if the pixel holds a decimal number.

## Step 1: Getting to know the SNAP window

We start SNAP. For now we only need three parts of the window:

1. **Product Explorer** on the left: the list of open products and what's in them.
2. **The image window** in the centre: this is where the band will appear.
3. **Pixel Info**: a tab next to Product Explorer. It shows the values in the pixel under the cursor.

If a panel isn't visible, we open it from the menu **View → Tool Windows**. We leave the other buttons and menus alone for now.

## Step 2: Opening the product

1. **File → Open Product…**
2. We go to the `data/sentinel2` folder, then into the folder for the 3 April image (`S2B_MSIL2A_20260403…SAFE`).
3. We select the file `MTD_MSIL2A.xml` (the product record sheet) and click **Open**.

SNAP reads the record sheet and uses it to find all the product's files. A line `[1]` with the product name appears in Product Explorer. No picture appears by itself: the product has only been added to the list.

We expand the `[1]` line with its arrow. Inside are several folders: **Metadata**, **Vector Data**, **Bands** and others. We expand **Bands** and count the bands. While we're there, we look at what else it holds besides bands.

```{figure} ../../images/ch05-snap-bands-2026-04-03.jpg
:label: en-fig-ch05-snap-bands-2026-04-03
:alt: The 3 April 2026 product open in SNAP: under Bands, the 12 bands and the folders of masks and angles.
:width: 100%

The 3 April 2026 product open in SNAP: under **Bands**, the 12 bands and the folders of masks and angles. Contains modified Copernicus Sentinel data (2026).
```

## Step 3: Opening band B12

We double-click **B12**. A tab `[1] B12` appears in the centre, with a black-and-white picture of the whole tile, 110 × 110 km. A big image can take a few seconds to build.

```{figure} ../../images/ch05-snap-b12-tile-2026-04-03.jpg
:label: en-fig-ch05-snap-b12-tile-2026-04-03
:alt: Band B12 on 3 April 2026: the whole 29TPJ tile.
:width: 100%

Band B12 on 3 April 2026: the whole 29TPJ tile. Contains modified Copernicus Sentinel data (2026).
```

## Step 4: Finding the fire site

The burn scar isn't visible on this image yet: on 3 April there was no fire. We're looking for the place itself.

1. We zoom in with the mouse wheel. The fire is in the lower right part of the tile, not far from its southern edge.
2. We open the **Pixel Info** tab, move the cursor and watch the **Latitude** and **Longitude** lines.
3. We stop at about **43°20′46″ N, 6°40′30″ W**. That's the middle of the burn scar according to the EFFIS outline.

SNAP shows coordinates in degrees, minutes and seconds. Many sources, EFFIS among them, give them in decimal degrees: 43.346 and −6.675. Converting from one to the other is simple: there are 60 minutes in a degree and 60 seconds in a minute.

**From decimal degrees to degrees, minutes and seconds:**

1. The whole number is the degrees: 43.346 → **43°**.
2. We multiply the decimal part by 60: 0.346 × 60 = 20.76. The whole number is the minutes: **20′**.
3. We multiply the decimal part by 60 again: 0.76 × 60 = 45.6 ≈ **46″**.

That gives 43°20′46″ N. The N means north latitude, because the number is positive. The longitude −6.675 has a minus sign, so it's west of Greenwich: 6°, 0.675 × 60 = 40.5 → 40′, 0.5 × 60 = 30″. That gives 6°40′30″ W.

**And back again:** degrees + minutes / 60 + seconds / 3600. For example, 43 + 20/60 + 46/3600 = 43.346.

There's a second landmark too: the pixel number. In the **Image-X** and **Image-Y** lines, SNAP shows which pixel this is, counting from the left and from the top. The middle of the burn scar in band B12 is at about X = 4420, Y = 4910, out of 5,490.

## Step 5: Reading the number

We hover the cursor over a pixel at this spot and look at the **B12** line in the **Bands** section of the Pixel Info tab. We write down three things:

- the value of B12;
- the pixel's latitude and longitude;
- what kind of number it is: whole or decimal.

```{figure} ../../images/ch05-snap-b12-pixel-info-2026-04-03.jpg
:label: en-fig-ch05-snap-b12-pixel-info-2026-04-03
:alt: Band B12 near the middle of the burn scar; on the left, Pixel Info with the pixel coordinates and B12 = 0.12630.
:width: 100%

Band B12 near the middle of the burn scar; on the left, **Pixel Info** with the pixel coordinates and B12 = 0.12630. Contains modified Copernicus Sentinel data (2026).
```

## Step 6: Where SNAP got this number from

Now we check what SNAP did to the number from the file.

1. In Product Explorer, we click **B12** once to select it.
2. We open the menu **Analysis → Information**.
3. In the list, we look for three lines: **Raw data type**, **Scaling factor** and **Scaling offset**. We write down their values.

Then we look at the product record sheet:

1. In Product Explorer, we expand **Metadata → Level-2A_User_Product → General_Info → Product_Image_Characteristics**.
2. We open **QUANTIFICATION_VALUES_LIST** and **BOA_ADD_OFFSET_VALUES_LIST**, and write down the values of **BOA_QUANTIFICATION_VALUE** and **BOA_ADD_OFFSET** for band B12.

## What we found

**The first part of the hypothesis held up; the second didn't: the pixel holds a decimal number, not a whole one.**

**Bands.** The Bands folder holds exactly 12 bands: B1–B9, B8A, B11, B12. There's no B10, as we expected. Each band appears once, at its native pixel size. We can see this in the Information window: B12 measures 5,490 × 5,490 pixels (a 20 m pixel), while the product as a whole is 10,980 × 10,980 (a 10 m pixel). SNAP keeps bands of different sizes in one product.

Besides the bands, Bands holds some more folders:

- **sun** and **view**: the angles of the sun and the satellite;
- **quality**: quality maps, including the scene classification and the cloud probability;
- **detector_footprint**, **nodata**, **opaque_clouds**, **cirrus_clouds** and others: masks showing which detector captured where, where there's no data, and where there are clouds.

**The number in the pixel.** The pixel near the middle of the burn scar:

- Image-X = 4425, Image-Y = 4903;
- 43°20′48″ N, 6°40′27″ W;
- **B12 = 0.12630**.

That's a decimal number, not a whole number in the thousands. Hypothesis 2 didn't hold up.

**Why.** The Information window explains what happened:

- **Raw data type: uint16**: the file really does store whole numbers from 0 to 65,535;
- **Scaling factor: 1.0E-4**: a multiplier of 0.0001;
- **Scaling offset: −0.1**: a shift of −0.1.

SNAP reads the whole number from the file and converts it straight away: it multiplies it by 0.0001 and subtracts 0.1. What we see on screen is already the result: the reflectance.

```{figure} ../../images/ch05-snap-b12-information-2026-04-03.jpg
:label: en-fig-ch05-snap-b12-information-2026-04-03
:alt: The Information window for band B12: data type, multiplier and offset.
:width: 100%

The **Information** window for band B12: data type, multiplier and offset.
```

The product record sheet says the same thing in other words: **BOA_QUANTIFICATION_VALUE = 10000**, **BOA_ADD_OFFSET = −1000**. That gives us the formula:

**reflectance = (value in the file − 1,000) / 10,000**

Let's check it on our pixel, working backwards from what SNAP showed: value in the file = 0.1263 × 10,000 + 1,000 = **2,263**. A whole number in the thousands, exactly what we expected in our hypothesis. So the hypothesis is right about the file; SNAP simply shows us the number after conversion.

**0.1263 means that the surface in this pixel reflects about 13% of the sunlight in band B12.**

## If something goes wrong

1. **The pixel shows −0.1.** That isn't a reflectance but 'no data': the file holds 0 there, and after conversion (0 − 1,000) / 10,000 = −0.1. This happens around the edges of the image, where the satellite didn't look. SNAP excludes these pixels from calculations by itself: it's written in the **Valid pixel expression** line of the Information window.
2. **Pixel Info shows a number, but not B12.** We look specifically at the **B12** line in the **Bands** section: higher up in the same tab are the coordinates and pixel numbers, and they're easy to mix up.
3. **Our own software shows whole numbers.** If we open the `.jp2` file in another program rather than SNAP, we'll see the number from the file, for example 2,263. Then we do the conversion ourselves, using the formula above.

:::{tip} Did you know?
Why subtract 1,000? Over dark surfaces, water for example, the reflectance after atmospheric correction sometimes comes out slightly below zero. An unsigned whole number can't be negative, so the processor adds 1,000 to every value before writing it to the file. And when we read it, we take that 1,000 off again.
:::

:::{admonition} Your data
For your own fire: we open the `MTD_MSIL2A.xml` file of our image and look for our coordinates in the Pixel Info tab. If they're given in decimal degrees, we convert them into degrees, minutes and seconds. The conversion formula is the same for every Sentinel-2 L2A image, but we always check the offset and multiplier values in the record sheet of our own product.
:::

## Summary

**New terms**

- **SNAP**: free software from the European Space Agency for working with Sentinel images.
- **Product** in SNAP: the whole contents of the `.SAFE` folder, opened as a single unit: bands, masks, record sheets.
- **Value in the file** (raw value, DN): the whole number stored in a band's file. Example: 2,263.
- **Reflectance**: the share of sunlight that a surface reflects. Example: 0.1263, that is, about 13%.
- **Scaling factor and Scaling offset**: the multiplier and the shift that SNAP uses to convert the value in the file into reflectance. Example: 1.0E-4 and −0.1.
- **Degrees, minutes, seconds**: a way of writing coordinates with 60 minutes in a degree and 60 seconds in a minute. Example: 43°20′46″ N = 43.346.

**Key points**

- A Sentinel-2 L2A file stores a whole number, not a reflectance.
- Reflectance = (value in the file − 1,000) / 10,000.
- SNAP does this conversion by itself and shows us the reflectance.

## Questions for an engineer

1. If SNAP converts the values itself, why do we need to know the formula?

:::{dropdown} Answer
Because not every program does it. If we open the file in Python or another GIS, we'll get the number from the file. If we forget to subtract 1,000, every reflectance will be 0.1 too high, and the indices we're going to calculate will come out wrong.
:::

2. Why take the offset and multiplier from the record sheet rather than remembering them?

:::{dropdown} Answer
They depend on the processing version. The −1,000 offset arrived in 2022 with processor version 04.00; older products don't have it. The record sheet always tells the truth about its own product.
:::

3. The pixel reads 0.1263. Is that a lot or a little for band B12?

:::{dropdown} Answer
We don't know yet: there's nothing to compare it with. We'll compare the engineer's way: the same pixel before and after the fire, and next to it, pixels that didn't burn.
:::


## Exercises

1. **Recall:** which file do we choose in SNAP to open the whole product at once?
2. **Fix it:** there's a mistake in the sentence 'SNAP shows bands B1–B12, 13 bands in all'. What is it?
3. **Three lessons back (4.1):** why did we draw the frame round the burn scar before we even started choosing images?

The answers are on the [Solutions](../solutions.md) page.

## The open question

We've got our reflectance. But the record sheet calls it BOA, 'bottom of atmosphere'. The satellite flies at an altitude of 786 km, and the light reaching it passes through the whole atmosphere. How did the processor work out how much light the ground itself reflected, and how much the air added? That's Lesson 5.3.

---

## Notes and sources

- [Copernicus SentiWiki, 'S2 Products'](https://sentiwiki.copernicus.eu/web/s2-products): the contents of the L2A product and the SAFE format. Accessed 19 November 2026.
- The product record sheet `MTD_MSIL2A.xml` for the 3 April 2026 image: BOA_QUANTIFICATION_VALUE = 10000, BOA_ADD_OFFSET = −1000.
