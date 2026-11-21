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

1. In SNAP, each band will appear once, not at three pixel sizes as in the folders. That makes 12 bands in all: the satellite captures 13, but B10 isn't included in the L2A product (Lesson 5.1).
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

The burn scar isn't visible on this image yet: on 3 April there was no fire. We're looking for the place itself, and for that we need its coordinates.

### Where to get the coordinates

We take the coordinates of the middle of the burn scar from the EFFIS record for our fire. The record number is 294223; we've already referred to it in the prologue.

1. In the browser, we open the address `https://api.effis.emergency.copernicus.eu/rest/2/burntareas/current/294223/`
2. The browser shows text in JSON format. This is the fire record: its number, date, area and outline.
3. Near the beginning, we look for the line `"centroid"`. This is the geometric centre of the burn scar outline. Next to it are two numbers: `[-6.674615360799909, 43.346846622747705]`.

Important: in JSON (as in GeoJSON), **longitude comes first, then latitude**. So:

- longitude = −6.674615;
- latitude = 43.346847.

We don't need that many decimal places. Four decimal places is about 10 m on the ground, less than one pixel. We round: latitude **43.3468**, longitude **−6.6746**.

### How to convert to degrees, minutes and seconds

SNAP shows coordinates not in decimal degrees but in degrees, minutes and seconds. We do the conversion ourselves. There's just one rule: there are 60 minutes in a degree and 60 seconds in a minute. So each time, we multiply the decimal part by 60.

**Latitude 43.3468:**

1. The whole number is the degrees: **43°**.
2. We multiply the decimal part by 60: 0.3468 × 60 = 20.808. The whole number is the minutes: **20′**.
3. We multiply the decimal part by 60 again: 0.808 × 60 = 48.48. Rounded to a whole number, that's the seconds: **48″**.

That gives **43°20′48″ N**. The N means north latitude, because the number is positive.

**Longitude −6.6746.** The minus sign means 'west of Greenwich'. We work without the sign:

1. Degrees: **6°**.
2. 0.6746 × 60 = 40.476 → minutes **40′**.
3. 0.476 × 60 = 28.56 → seconds **29″**.

That gives **6°40′29″ W**. The W means west longitude.

**Checking by working backwards:** degrees + minutes / 60 + seconds / 3600. For the latitude: 43 + 20/60 + 48/3600 = 43 + 0.3333 + 0.0133 = 43.3466. That matches 43.3468, give or take the rounding of the seconds.

### Finding the spot in SNAP

1. We zoom in with the mouse wheel. Our point is in the lower right part of the tile, not far from its southern edge.
2. We open the **Pixel Info** tab, move the cursor and watch the **Latitude** and **Longitude** lines.
3. We stop when they read roughly **43°20′48″ N** and **6°40′29″ W**.

## Step 5: Reading the number

We hover the cursor over a pixel at this spot and look at the Pixel Info tab. We write down:

- the value in the **B12** line of the **Bands** section;
- the **Latitude** and **Longitude** lines;
- the **Image-X** and **Image-Y** lines: the pixel number;
- the **Map-X** and **Map-Y** lines: the pixel's coordinates in metres;
- what kind of number B12 holds: whole or decimal.

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

### Bands

The Bands folder holds exactly 12 bands: B1–B9, B8A, B11, B12. There's no B10, as we expected.

Each band appears once, at its native pixel size. We can see this in the Information window:

- for B12, the **Raster width** and **Raster height** lines read 5,490 × 5,490 pixels;
- for the product as a whole, the **Product scene width** and **Product scene height** lines read 10,980 × 10,980 pixels.

Let's check what that means. We multiply the number of pixels by the pixel size:

- 5,490 pixels × 20 m = 109,800 m: that's the side of the tile in band B12;
- 10,980 pixels × 10 m = 109,800 m: the same side in the bands with a 10 m pixel.

It's the same square, about 110 km across. In B12 it's divided into 20 m pixels; in the 10 m bands, into pixels half that size. So SNAP keeps bands of different sizes in one product, each at its own size.

Besides the bands, Bands holds some more folders:

- **sun** and **view**: the angles of the sun and the satellite;
- **quality**: quality maps, including the scene classification and the cloud probability;
- **detector_footprint**, **nodata**, **opaque_clouds**, **cirrus_clouds** and others: masks showing which detector captured where, where there's no data, and where there are clouds.

### The number in the pixel

The pixel near the middle of the burn scar, as Pixel Info showed it:

- Latitude 43°20′48″ N, Longitude 6°40′27″ W: two seconds from the EFFIS point;
- Image-X = 4425, Image-Y = 4903;
- Map-X = 688,510 m, Map-Y = 4,801,950 m;
- **B12 = 0.12630**.

That's a decimal number, not a whole number in the thousands. Hypothesis 2 didn't hold up.

### How the pixel number relates to metres

Let's check the pixel number ourselves. For that we need the corner of the tile.

**Where to get it.** We open the file `MTD_TL.xml` (the tile record sheet, Lesson 5.1) in any text editor or browser. We look for the line `Geoposition resolution="20"`: this is the grid with a 20 m pixel. Below it are four values:

- `ULX` = 600000: the X coordinate of the tile's top left corner, in metres;
- `ULY` = 4900020: the Y coordinate of the same corner;
- `XDIM` = 20: the pixel step along X, 20 m;
- `YDIM` = −20: the step along Y. It's negative because pixel numbers increase from top to bottom, while the Y coordinate increases from bottom to top.

The coordinates are in the UTM projection, zone 29 of the northern hemisphere (in the record sheet: `EPSG:32629`). This is the same system in which SNAP shows Map-X and Map-Y.

**The formula.** How many metres is it from the left edge of the tile to our pixel? Map-X − ULX. How many pixels is that? We divide by the pixel size:

- Image-X = (Map-X − ULX) / 20
- Image-Y = (ULY − Map-Y) / 20. This one is the other way round, because we count down from the top edge.

**The calculation:**

- Image-X = (688,510 − 600,000) / 20 = 88,510 / 20 = **4425.5**
- Image-Y = (4,900,020 − 4,801,950) / 20 = 98,070 / 20 = **4903.5**

The half tells us that Map-X and Map-Y are the coordinates of the **middle** of the pixel. Pixel number 4425 itself covers the stretch from 4425.0 to 4426.0, and its middle is 4425.5. That matches what SNAP showed: Image-X = 4425, Image-Y = 4903.

```{figure} ../../images/ch05-snap-b12-information-2026-04-03.jpg
:label: en-fig-ch05-snap-b12-information-2026-04-03
:alt: The Information window for band B12: data type, multiplier and offset.
:width: 100%

The **Information** window for band B12: data type, multiplier and offset.
```

### Why the pixel holds a decimal number

The Information window explains what happened:

- **Raw data type: uint16**: the file stores unsigned whole numbers written with 16 bits. 16 bits give 2¹⁶ = 65,536 different values, that is, numbers from 0 to 65,535.
- **Scaling factor: 1.0E-4**: a multiplier. The notation 1.0E-4 means 1.0 × 10⁻⁴ = 0.0001.
- **Scaling offset: −0.1**: a shift of −0.1.

SNAP reads the whole number from the file and converts it straight away:

**reflectance = value in the file × 0.0001 − 0.1**

What we see on screen is already the result: the reflectance.

### The same formula in the record sheet

The product record sheet says the same thing in other words:

- **BOA_QUANTIFICATION_VALUE = 10000**: what the reflectance was multiplied by to store it as a whole number;
- **BOA_ADD_OFFSET = −1000**: what to add to the number from the file before dividing.

That gives us the formula:

**reflectance = (value in the file + BOA_ADD_OFFSET) / BOA_QUANTIFICATION_VALUE = (value in the file − 1,000) / 10,000**

Why is it set up like this?

1. **Why multiply by 10,000.** Reflectance is a decimal number between 0 and 1. Whole numbers are simpler and more compact to store than decimals. If we multiply 0.1263 by 10,000, we get 1,263: a whole number, and the four decimal places aren't lost.
2. **Why add 1,000.** Over very dark surfaces, water for example, the reflectance after atmospheric correction sometimes comes out slightly below zero. An unsigned whole number can't be negative. So since 25 January 2022 (processing version 04.00), 1,000 has been added to every value before it's written, and it's taken off again when the value is read[^offset].

It's the same formula as SNAP's. Let's expand the brackets:

(value − 1,000) / 10,000 = value / 10,000 − 1,000 / 10,000 = value × 0.0001 − 0.1

### Checking on our pixel

SNAP showed a reflectance of 0.1263. What number is stored in the file? We follow the formula backwards:

1. reflectance = (value − 1,000) / 10,000
2. we multiply both sides by 10,000: reflectance × 10,000 = value − 1,000
3. we add 1,000: value = reflectance × 10,000 + 1,000

Substituting: 0.1263 × 10,000 + 1,000 = 1,263 + 1,000 = **2,263**.

A whole number in the thousands, exactly what we expected in our hypothesis. So the hypothesis is right about the file; SNAP simply shows us the number after conversion.

### What 0.1263 means

Reflectance is a share of the light. To turn it into a percentage, we multiply by 100: 0.1263 × 100 = 12.63%. **The surface in this pixel reflects about 13% of the sunlight in band B12.**

## If something goes wrong

1. **The pixel shows −0.1.** That isn't a reflectance but 'no data'. In these pixels the file holds 0. Putting it into the formula: (0 − 1,000) / 10,000 = −0.1. This happens around the edges of the image, where the satellite didn't look. SNAP excludes these pixels from calculations by itself: it's written in the **Valid pixel expression** line of the Information window.
2. **Pixel Info shows a number, but not B12.** We look specifically at the **B12** line in the **Bands** section. Higher up in the same tab are the coordinates and pixel numbers, and they're easy to mix up.
3. **Another program shows whole numbers.** If we open the `.jp2` file in another program rather than SNAP, we'll see the number from the file, for example 2,263. Then we do the conversion ourselves, using the formula above.

:::{admonition} Your data
For your own fire:

1. we find our fire's number in EFFIS and open its record at the same address, putting in our own number;
2. we take the `"centroid"` (longitude first, then latitude) and convert it into degrees, minutes and seconds;
3. we open the `MTD_MSIL2A.xml` file of our image and find this point in the Pixel Info tab.

The conversion formula is the same for every Sentinel-2 L2A image since 2022, but we always check the multiplier and offset values in the record sheet of our own product.
:::

## Summary

**New terms**

- **SNAP**: free software from the European Space Agency for working with Sentinel images.
- **Product** in SNAP: the whole contents of the `.SAFE` folder, opened as a single unit: bands, masks, record sheets.
- **Value in the file** (raw value, DN): the whole number stored in a band's file. Example: 2,263.
- **Reflectance**: the share of sunlight that a surface reflects. Example: 0.1263, that is, about 13%.
- **Scaling factor and Scaling offset**: the multiplier and the shift that SNAP uses to convert the value in the file into reflectance. Example: 1.0E-4 and −0.1.
- **Degrees, minutes, seconds**: a way of writing coordinates with 60 minutes in a degree and 60 seconds in a minute. Example: 43°20′48″ N = 43.3468.
- **UTM**: a coordinate system in metres, used for Sentinel-2 tiles. Example: our tile is in zone 29 of the northern hemisphere, `EPSG:32629`.

**Key points**

- A Sentinel-2 L2A file stores a whole number, not a reflectance.
- Reflectance = (value in the file − 1,000) / 10,000.
- SNAP does this conversion by itself and shows us the reflectance.
- We can check a pixel number from its coordinates in metres and the tile corner in `MTD_TL.xml`.

## Questions for an engineer

1. If SNAP converts the values itself, why do we need to know the formula?

:::{dropdown} Answer
Because not every program does it. If we open the file in Python or another GIS, we'll get the number from the file. If we forget to subtract 1,000, every reflectance will be too high by 1,000 / 10,000 = 0.1, and the indices we're going to calculate will come out wrong.
:::

2. Why take the multiplier and offset from the record sheet rather than remembering them?

:::{dropdown} Answer
They depend on the processing version. The offset arrived with version 04.00 in January 2022. Older products don't have it, and for them the formula is different: value / 10,000. The record sheet always tells the truth about its own product.
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

- Copernicus SentiWiki, 'S2 Products': the contents of the L2A product and the SAFE format. https://sentiwiki.copernicus.eu/web/s2-products (accessed 19 November 2026)
- EFFIS, burnt area record 294223 (Allande): the centre of the outline. https://api.effis.emergency.copernicus.eu/rest/2/burntareas/current/294223/ (accessed 21 November 2026)
- The product record sheet `MTD_MSIL2A.xml` and the tile record sheet `MTD_TL.xml` for the 3 April 2026 image: BOA_QUANTIFICATION_VALUE = 10000, BOA_ADD_OFFSET = −1000; tile corner ULX = 600000, ULY = 4900020.
[^offset]: ESA, 'Copernicus Sentinel-2: Major Products Upgrade Upcoming': the offset was added so that negative values over dark surfaces aren't lost. https://sentinels.copernicus.eu/-/copernicus-sentinel-2-major-products-upgrade-upcoming ; ESA STEP forum, 'Introduction of additional Radiometric Offset in PB04.00 products': the −1000 offset in L1C and L2A products since 25 January 2022. https://forum.step.esa.int/t/info-introduction-of-additional-radiometric-offset-in-pb04-00-products/35431 (accessed 21 November 2026)
