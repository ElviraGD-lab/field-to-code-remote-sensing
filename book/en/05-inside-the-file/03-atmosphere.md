---
title: "5.3 What the atmosphere did"
---

## Where we left off

In Lesson 5.2 we read B12 = 0.1263 in a pixel near the middle of the burn scar. The record sheet calls this reflectance BOA, bottom of atmosphere. In other words, it's how the surface itself reflects, as if there were no air between it and the satellite.

But the satellite flies at an altitude of 786 km, and the light reaching it passes through the whole atmosphere. In this lesson we look at what the air does to light, and how much the processor changed the numbers to remove it.

## What the atmosphere does to light

Light passes through the air twice: from the sun to the ground, and from the ground to the satellite. On the way, two different things happen to it.

1. **Scattering.** Air molecules and droplets of haze knock part of the light sideways, some of it straight into the satellite's lens. So the satellite receives light that never reached the ground at all. Short-wave, blue light is scattered the most. That's why the sky is blue and distant mountains look bluish.
2. **Absorption.** Water vapour, ozone and other gases take away part of the light at particular wavelengths. Less reaches the satellite than the ground reflected.

That's where the two Sentinel-2 processing levels come from:

- **L1C**: reflectance at the top of the atmosphere, TOA (top of atmosphere). This is what the satellite sees, air included;
- **L2A**: reflectance at the surface, BOA. The Sen2Cor processor has removed the scattering and absorption.

To remove the air, the processor needs to know how much of it there was. For that, it works out two maps from the image itself, the ones we saw in Lesson 5.1: `AOT` (how much haze, that is, aerosols) and `WVP` (how much water vapour).

## What we want to know

**The question:** how much does the atmosphere change the number in a pixel, and is the change the same in every band?

**Our hypothesis before we start:**

1. In the blue band B2, the L1C reflectance will be **higher** than the L2A one. The air scatters blue light and adds it to what the ground reflected.
2. In band B12, the difference between L1C and L2A will be **much smaller** than in B2. Long waves pass through the air with almost no scattering.

**How we'll know we were wrong:** if in B2 the L1C value turns out lower than L2A, or if the difference in B12 is as big as in B2, or bigger.

## Step 1: Downloading the L1C image for the same date

1. In Copernicus Browser, we open the **Search** tab.
2. In the list of data sources, we keep only **Sentinel-2** and tick **L1C** under it. We untick L2A and the other satellites.
3. We set the date to **3 April 2026** and click **Search**.
4. There are two products in the list, as in Lesson 5.1: tiles 29TPH and 29TPJ. We take **29TPJ**: `S2B_MSIL1C_20260403T112109_N0512_R037_T29TPJ_20260403T152544.SAFE`. Its size in the list is **611 MB**.
5. We download it to the same `data/sentinel2` folder and unpack it.

The acquisition time in the list is 11:21:09 UTC, the same as our L2A. It's the very same image, the same pass of the satellite. The only difference is the processing.

```{figure} ../../images/ch05-search-l1c-2026-04-03.jpg
:label: en-fig-ch05-search-l1c-2026-04-03
:alt: Search for Sentinel-2 L1C on 3 April 2026: two products, tiles 29TPH and 29TPJ; we take 29TPJ (611 MB).
:width: 100%

Search for Sentinel-2 L1C on 3 April 2026: two products, tiles 29TPH and 29TPJ; we take 29TPJ (611 MB). Contains modified Copernicus Sentinel data (2026).
```

## Step 2: Opening both products in SNAP

1. **File → Open Product…** and we open `MTD_MSIL1C.xml` from the new L1C folder.
2. If the L2A isn't open yet, we open it too: `MTD_MSIL2A.xml`, as in Lesson 5.2.

Product Explorer now has two products: `[1]` and `[2]`. We check their names to see which is `MSIL1C` and which is `MSIL2A`.

## Step 3: Putting a pin on the same point in both products

To compare fairly, we need the same pixel in both products. We can't hit exactly the same spot with the cursor. That's what SNAP's pins are for: a point with exact coordinates.

We take the coordinates from the EFFIS record, as in Lesson 5.2: latitude 43.3468, longitude −6.6746. In the SNAP window we type them as `43.3468` and `-6.6746`, with a point and the ordinary hyphen on the keyboard.

1. We open band **B2** of the L2A product with a double click.
2. We open **View → Tool Windows → Pin Manager**.
3. In Pin Manager, we click the **New pin** button (the plus icon).
4. In the window that opens, we enter **Lat** = `43.3468` and **Lon** = `-6.6746`, and click **OK**.
5. We open band **B2** of the L1C product and repeat steps 3–4 for it.

## Step 4: Reading the reflectance at the pin

Pin Manager has a **Filter pixel data to be displayed in table** button (the funnel icon). We click it. A list of all the product's layers opens, with the bands at the top. We tick **B2** and **B12** and click **OK**. Their values at the pin now appear in the pin table.

We do this for both products. For the L2A product we also tick **quality_aot** and **quality_wvp**: we'll need them in Step 6.

## Step 5: Checking that SNAP converted the numbers in the same way

In Lesson 5.2 we saw that SNAP converts the number from the file into reflectance by itself, using the formula from the record sheet. For L1C we check the same thing: we can only subtract numbers from each other if they're in the same units.

1. In Product Explorer, we select **B2** of the L1C product and open **Analysis → Information**. We write down the **Scaling factor** and **Scaling offset**.
2. We open the L1C record sheet: **Metadata → Level-1C_User_Product → General_Info → Product_Image_Characteristics**. We write down the **QUANTIFICATION_VALUE**. We expand **Radiometric_Offset_List** and write down the **RADIO_ADD_OFFSET** values.

## Step 6: How much haze and vapour there was

The pin table for the L2A product already shows **quality_aot** and **quality_wvp**. We write down their values. Then we check what units they're in:

1. In Product Explorer, we select **quality_aot** and open **Analysis → Information**. We write down the **Geophysical unit** and **Scaling factor**.
2. We do the same for **quality_wvp**.
3. In the L2A record sheet, under **Product_Image_Characteristics → QUANTIFICATION_VALUES_LIST**, we find **AOT_QUANTIFICATION_VALUE** and **WVP_QUANTIFICATION_VALUE**.

The L1C product doesn't have these layers. The Sen2Cor processor calculates them when it turns L1C into an L2A product. Before that processing, they simply don't exist.

## How we'll calculate

Once the numbers are written down, we calculate two things for each band.

**1. The difference:** how much the atmosphere added or took away.

difference = TOA − BOA

If the difference is positive, the satellite saw more light than the ground reflected: the air added some. If it's negative, less light reached the satellite.

**2. The difference as a percentage:** how big it is compared with the ground's own reflectance.

difference in % = (TOA − BOA) / BOA × 100%

Why the second number? A difference of 0.02 for a dark surface with a reflectance of 0.04 is half the signal. For a bright surface with a reflectance of 0.4, it's only a twentieth. The percentage shows how wrong someone would be if they took L1C instead of L2A.

## What we found

**The first part of the hypothesis held up. The second didn't, and that's the most interesting thing in this lesson.**

### The numbers we got

The pin sits on the same point in both products: Lon −6.674600, Lat 43.346800. Pin Manager shows:

| | B2 | B12 |
|---|---|---|
| L1C (TOA) | 0.1213 | 0.166 |
| L2A (BOA) | 0.0848 | 0.198 |

### Can we compare them?

Yes. For L1C, the Information window for B2 shows **Scaling factor 1.0E-4** and **Scaling offset −0.1**. In the L1C record sheet: **QUANTIFICATION_VALUE = 10000**, and every **RADIO_ADD_OFFSET = −1000**. That's the same formula as for L2A in Lesson 5.2:

reflectance = (value in the file − 1,000) / 10,000

So both products are shown in the same units, as reflectances. We can subtract them.

As a check, let's find the numbers in the files, as in Lesson 5.2: value = reflectance × 10,000 + 1,000.

- L1C, B2: 0.1213 × 10,000 + 1,000 = 1,213 + 1,000 = 2,213
- L2A, B2: 0.0848 × 10,000 + 1,000 = 848 + 1,000 = 1,848
- L1C, B12: 0.166 × 10,000 + 1,000 = 1,660 + 1,000 = 2,660
- L2A, B12: 0.198 × 10,000 + 1,000 = 1,980 + 1,000 = 2,980

Whole numbers in the thousands, just as they should be.

### The calculation for B2

1. The difference: 0.1213 − 0.0848 = **0.0365**.
2. As a percentage: 0.0365 / 0.0848 × 100% = 0.4304 × 100% ≈ **43%**.

The difference is positive: in the blue band, the satellite saw 43% more light than the ground reflected. **Hypothesis 1 held up.** Most of that difference is light scattered by the atmosphere itself. But another correction is at work in B2 too; we'll meet it a little further down, when we look at B12.

### The calculation for B12

1. The difference: 0.166 − 0.198 = **−0.032**.
2. As a percentage: −0.032 / 0.198 × 100% = −0.1616 × 100% ≈ **−16%**.

The difference is negative: the reflectance at the surface is **higher** than what the satellite saw. And it's almost as big as in B2: 0.032 against 0.0365. **Hypothesis 2 didn't hold up.** We expected the processor to change almost nothing in B12. Instead, the satellite saw 16% less in B12 than the surface value after processing.

### Why B12 behaves like this

Let's look at the pictures themselves. We open band B2 from L1C and from L2A side by side (see the figure). In L1C the slopes stand out clearly: one side of each ridge is light and the other dark. In L2A this light and shade is much weaker, as if the relief had been smoothed out.

```{figure} ../../images/ch05-snap-pin-l1c-b2-2026-04-03.jpg
:label: en-fig-ch05-snap-pin-l1c-b2-2026-04-03
:alt: Band B2 on 3 April 2026: L2A on the left, L1C on the right, with the same pin. The slopes are far more contrasted in L1C. Below, the pin table for L1C: B2 = 0.1213, B12 = 0.166.
:width: 100%

Band B2 on 3 April 2026: L2A on the left, L1C on the right, with the same pin. The slopes are far more contrasted in L1C. Below, the pin table for L1C: B2 = 0.1213, B12 = 0.166. Contains modified Copernicus Sentinel data (2026).
```

This is the second part of the processor's work, which we haven't talked about yet. Besides the atmosphere, Sen2Cor also corrects for **how the slopes are lit**: from a digital elevation model, it knows the angle at which the sun shines on each pixel. On a slope facing away from the sun it raises the reflectance, and on a slope facing the sun it lowers it. The aim is for the same surface to give the same number on any slope.

In our B12 pixel, two corrections are at work at once:

- the atmospheric one: in B12 it's small, as there's almost no scattering;
- the slope correction: it acts in every band, and it can be large.

From two numbers in a single pixel, we can't say which of them produced the −16%. But the picture shows that the terrain correction is working, and working noticeably. And in the prologue we read that on poorly lit slopes this correction can be too strong. **This matters for our second research question: L2A already contains a correction for lighting, and we have to take that into account.** We'll deal with this in detail in Chapter 7.

### How much haze and vapour there was

At the same L2A pin:

- **quality_aot = 0.147**;
- **quality_wvp = 0.819**.

```{figure} ../../images/ch05-snap-pin-l2a-aot-wvp-2026-04-03.jpg
:label: en-fig-ch05-snap-pin-l2a-aot-wvp-2026-04-03
:alt: The pin table for L2A: B2 = 0.0848, B12 = 0.198, quality_aot = 0.147, quality_wvp = 0.819.
:width: 100%

The pin table for L2A: B2 = 0.0848, B12 = 0.198, quality_aot = 0.147, quality_wvp = 0.819. Contains modified Copernicus Sentinel data (2026).
```

**Where these numbers come from and what units they're in.** In the Information window, both layers show **Scaling factor 0.001** and **Scaling offset 0.0**. In the L2A record sheet: **AOT_QUANTIFICATION_VALUE = 1000** and **WVP_QUANTIFICATION_VALUE = 1000**; for the water vapour, the unit is cm. The formula works the same way, just without the offset:

value = value in the file / 1,000

The values in the file: 0.147 × 1,000 = 147 and 0.819 × 1,000 = 819.

**What AOT = 0.147 means.** AOT is the aerosol optical thickness, that is, the optical thickness of the haze, at a wavelength of 550 nm (green light). It isn't a thickness in metres but a measure of how much light the haze stops. The share of light that passes straight through the haze, vertically from top to bottom, is e^(−AOT), where e ≈ 2.718. We work it out on a calculator:

e^(−0.147) = 1 / e^0.147 = 1 / 1.158 = **0.863**

So about 86% of the direct light got through the haze, and the haze scattered or absorbed about 14%. The air on 3 April was fairly clean, but not perfectly so.

**What WVP = 0.819 cm means.** If all the water vapour above this pixel, from the ground to the top of the atmosphere, condensed into water, it would make a layer 0.819 cm thick, that is, about 8 mm.

## If something goes wrong

1. **The search results show Sentinel-1, not Sentinel-2.** If Sentinel-1 is ticked in the search, the list will include products with names like `S1A_…` and `S1C_…` and the SAR instrument. That's a radar satellite: it passes over at a different time and doesn't measure sunlight. We keep only Sentinel-2 L1C in the search. The first letters of a product name always tell us which satellite it is: `S2` is Sentinel-2, `S1` is Sentinel-1.
2. **The B12 number doesn't match Lesson 5.2.** In Lesson 5.2, B12 read 0.1263, but here the L2A value is 0.198. These are different pixels. The pin sits at X = 8847.3, Y = 9806.6 (the X and Y columns in Pin Manager). These numbers are on the 10 m grid. Band B12 is on the 20 m grid, where the pixels are twice as big, so we divide by 2: 8847.3 / 2 = 4423.65 → pixel **4423**; 9806.6 / 2 = 4903.3 → pixel **4903**. In Lesson 5.2 the pixel was 4425, 4903. The difference is 2 pixels along X, that is, 40 m. In the mountains, 40 m is enough for the slope or the vegetation to change. That's why we only compare numbers at the very same point, and that's what pins are for.
3. **The pin table has no quality_aot or quality_wvp.** That means the pin is in the L1C product, which doesn't have these layers. We open Pin Manager for the L2A product.

:::{admonition} Your data
For our own fire, we download the L1C for the same date and the same tile as the L2A, and put a pin on our point, taking the coordinates from the `"centroid"` in our EFFIS record. The pixel must be the same in both products; otherwise the comparison isn't fair.
:::

## Summary

**New terms**

- **TOA** (top of atmosphere): reflectance at the top of the atmosphere, as the satellite sees it. The L1C level. Example: B2 = 0.1213.
- **BOA** (bottom of atmosphere): reflectance at the surface, without the effect of the air. The L2A level. Example: B2 = 0.0848.
- **Scattering**: the air knocks part of the light sideways; blue light most of all.
- **Absorption**: gases take away part of the light at particular wavelengths.
- **Atmospheric correction**: converting TOA into BOA. For Sentinel-2, it's done by the Sen2Cor processor.
- **AOT**: aerosol optical thickness, how much light the haze stops. Example: 0.147, meaning about 86% of the direct light gets through.
- **WVP**: the water vapour in a column of air, in centimetres of water. Example: 0.819 cm.
- **Terrain correction**: recalculating reflectance to allow for how the sun lights a slope.
- **Pin** in SNAP: a point with exact coordinates, where we can read the values of different layers and products.

**Key points**

- The atmosphere changes the blue band the most: at our point, B2 at the top of the atmosphere is 43% higher than at the surface.
- L2A isn't only atmospheric correction: it also corrects for how the slopes are lit. In the mountains, this can change the numbers at least as much as the atmosphere does.
- We compare products only at the very same point and only in the same units.

## Questions for an engineer

1. Why do we use L2A rather than L1C to work out the burn scar?

:::{dropdown} Answer
In L1C, light from the atmosphere is mixed in with the ground's reflectance, and the amount varies from day to day as the haze and vapour change. If we compared 'before' and 'after' using L1C, part of the difference would simply be a difference in the weather. In L2A, that contribution has been removed.
:::

2. Why do we also work out the difference as a percentage?

:::{dropdown} Answer
The same difference means different things for a dark surface and a bright one. At our point, the difference in B2 is 0.0365, and that's 43% of the ground's reflectance. For a surface with a reflectance of 0.4, the same 0.0365 would be about 9%.
:::

3. In B12, L2A came out higher than L1C. Does that mean the processor got it wrong?

:::{dropdown} Answer
Not necessarily. The processor also corrects for how the slopes are lit, and in a pixel on a shaded slope the reflectance goes up after the correction. To find out whether the correction is right, we need to compare the same surface on slopes facing different ways. We'll do that in Chapter 7.
:::


## Exercises

1. **Recall:** what do the abbreviations TOA and BOA stand for, and which processing level does each one belong to?
2. **Fix it:** there's a mistake in the sentence 'The atmosphere scatters light most strongly in band B12, because it has the longest wavelength'. What is it?
3. **Seven lessons back (Chapter 1):** why is it easy to mistake a burn scar for a cloud shadow in natural colour?

The answers are on the [Solutions](../solutions.md) page.

## The open question

We now know that each L2A pixel holds the reflectance at the surface, already corrected for the atmosphere and for the slope. We can read it at a single point. But a burn scar is thousands of pixels. How do we show the 'before' and 'after' images so that the whole burn scar is visible and the comparison is fair: the same bands, the same brightness and the same contrast? That's Chapter 6.

---

## Notes and sources

- The product record sheets `MTD_MSIL1C.xml` and `MTD_MSIL2A.xml` for the 3 April 2026 image: QUANTIFICATION_VALUE = 10000, RADIO_ADD_OFFSET = −1000 (L1C); AOT_QUANTIFICATION_VALUE = 1000, WVP_QUANTIFICATION_VALUE = 1000 (L2A).
- ESA, *Sen2Cor Level-2A Algorithm Theoretical Basis Document*, v2.10: atmospheric correction, AOT and water vapour, terrain correction from a digital elevation model. https://step.esa.int/thirdparties/sen2cor/2.10.0/docs/S2-PDGS-MPC-L2A-ATBD-V2.10.0.pdf
- Copernicus SentiWiki, 'S2 Processing': the L1C and L2A processing levels, AOT and water vapour. https://sentiwiki.copernicus.eu/web/s2-processing (accessed 19 November 2026)
