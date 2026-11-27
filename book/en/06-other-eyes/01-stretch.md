---
title: "6.1 Why the same slope changes colour"
---

## Where we left off

We opened the 3 and 10 April images in SNAP in the B8A–B11–B12 composite, and on 10 April the burn scar shows up as a blue patch. But there's something odd about the images. The 3 April image is bluish, while the 10 April image is orange-green. Yet in those seven days only the area around Bustantigo burned, and everything around it should have stayed the same.

Let's work out where this difference comes from. If we don't understand it, any by-eye comparison of 'before' and 'after' will mislead us.

## What we want to know

**The question:** why is the unburnt ground a different colour on the two images?

**Our hypothesis before we start:**

1. The ground has hardly changed. Its reflectance is roughly the same on both images.
2. The different colour comes from SNAP itself: it set the brightness and contrast for each image separately, based on that image's own numbers.

**How we'll know we were wrong:** if, at the same point outside the burn scar, the reflectance in the bands is noticeably different on the two images. Or if SNAP shows both images with the same brightness settings.

## How the screen shows reflectance

First, let's recall Lesson 3.1. Each point on the screen has three lights: red, green and blue. The brightness of each is a number from 0 (off) to 255 (fully on). Reflectance in a band, on the other hand, is a decimal number, usually between 0 and 0.5. The software has to turn one into the other.

To do that, it picks two numbers for the band: **min** and **max**.

- Reflectance at **min** or below → the light is off (0).
- Reflectance at **max** or above → the light is fully on (255).
- Everything in between is shared out evenly.

The formula is:

**brightness = (reflectance − min) / (max − min) × 255**

Why it looks like this. First we subtract min: that turns a reflectance equal to min into 0. Then we divide by (max − min), the width of the range: that turns a reflectance equal to max into 1, and everything in between into a fraction between 0 and 1. The fraction tells us how far along the way from min to max our reflectance has got. Finally, we multiply by 255 to move onto the scale of the light.

If the result is below 0, we take 0. If it's above 255, we take 255.

This is called a **contrast stretch**: we stretch a narrow range of reflectances across the screen's whole brightness scale.

**An example with made-up numbers.** Say the reflectance is 0.20, min = 0.05 and max = 0.35:

- reflectance − min = 0.20 − 0.05 = 0.15;
- max − min = 0.35 − 0.05 = 0.30;
- 0.15 / 0.30 = 0.5;
- 0.5 × 255 = 127.5 ≈ **128**: the light is half on.

Now let's take the same reflectance, 0.20, but with min = 0.10 and max = 0.25:

- reflectance − min = 0.20 − 0.10 = 0.10;
- max − min = 0.25 − 0.10 = 0.15;
- 0.10 / 0.15 ≈ 0.667;
- 0.667 × 255 ≈ **170**: the light is noticeably brighter.

**One reflectance, two different colours on the screen.** It all depends on which min and max are chosen.

## Step 1: Opening both images in the same composite

1. In SNAP, we open the 3 and 10 April products (`MTD_MSIL2A.xml`, as in Lesson 5.2).
2. For each one: **Window → Open RGB Image Window**, with the bands **Red** = `B8A`, **Green** = `B11`, **Blue** = `B12`.
3. We put the windows side by side: **Window → Tile Horizontally**.

In our case the 3 April product opened first, so its window is called [1]. The 10 April product is [3]. The numbers can differ: they depend on the order in which the products were opened. It's easy to check which date is which: the 10 April image shows the blue burn scar.

## Step 2: Seeing which min and max SNAP chose by itself

1. We click on the 3 April image window to make it active.
2. We open **View → Tool Windows → Colour Manipulation**.
3. At the top of the window there are three buttons: **Red**, **Green** and **Blue**. Each one shows its own band: Red is B8A, Green is B11, Blue is B12.
4. Under each button there's a histogram (how many pixels have each reflectance) and a coloured bar with two triangular sliders: min on the left, max on the right. Their values are written under the sliders.
5. We write down min and max for all three bands.
6. We click on the 10 April window and write down the same.

```{figure} ../../images/ch06-colour-manip-b8a-2026-04-03.jpg
:label: en-fig-ch06-colour-manip-b8a-2026-04-03
:alt: Colour Manipulation for 3 April, Red button (band B8A). Top right, the band statistics (Min −0.1, Max 0.783); under the sliders, the stretch SNAP chose: −0.00339 and 0.44.
:width: 100%

**Colour Manipulation** for 3 April, **Red** button (band B8A). Top right, the band statistics (Min −0.1, Max 0.783); under the sliders, the stretch SNAP chose: −0.00339 and 0.44. Contains modified Copernicus Sentinel data (2026).
```

**Careful: the window has two sets of numbers, and they're different things.**

1. **In the box at the top right** (for example, `Min: -0.1`, `Max: 0.783`): the smallest and largest reflectance among all the pixels in the image. These are the band's statistics, not the stretch. The label 'Rough statistics!' means that SNAP worked them out quickly, from a sample of the pixels.
2. **Under the sliders** (for example, `-3.39E-3` and `0.44`): these are the min and max of the stretch. **These are the ones we need.**

**How to read numbers with an E.** This is how software writes very small or very large numbers. E means 'multiply by 10 to the power of':

- `3.39E-3` = 3.39 × 10⁻³ = 3.39 × 0.001 = 0.00339. So `-3.39E-3` = −0.00339.
- `2.91E-4` = 2.91 × 0.0001 = 0.000291.
- `2.58E-2` = 2.58 × 0.01 = 0.0258.
- `2E-2` = 2 × 0.01 = 0.02.
- `1.67E-2` = 1.67 × 0.01 = 0.0167.
- `9.77E-6` = 9.77 × 0.000001 = 0.00000977, practically zero.

Here's what we got (the numbers under the sliders; reflectance rounded to four decimal places):

| | B8A min | B8A max | B11 min | B11 max | B12 min | B12 max |
|---|---|---|---|---|---|---|
| 3 April | −0.0034 | 0.44 | −0.0003 | 0.27 | 0.00001 | 0.16 |
| 10 April | 0.0258 | 0.49 | 0.02 | 0.42 | 0.0167 | 0.39 |

Let's compare the max values band by band: how many times bigger is the 10 April max than the 3 April one?

- B8A: 0.49 / 0.44 ≈ 1.1 times.
- B11: 0.42 / 0.27 ≈ 1.6 times.
- B12: 0.39 / 0.16 ≈ 2.4 times.

**The biggest difference is in band B12, which shows as blue on the screen.** Let's keep that in mind.

Where does such a difference come from? SNAP sets the sliders by itself, from the histogram of the whole image. And the 10 April image is the whole 110 × 110 km scene, with 43% cloud cover (Lesson 4.2). Clouds are very bright in the SWIR bands. They add lots of high values to the histogram and drag max upwards. There are no clouds over our burn scar, but SNAP chooses the stretch from the whole scene.

## Step 3: Checking the reflectance at a point outside the burn scar

We need a point that definitely didn't burn. Our pin from Lesson 5.3 (Pin 1) is in the middle of the burn scar, so it won't do. We put in a new one.

1. **View → Tool Windows → Pin Manager → New pin**.
2. We enter Lat `43.3468`, Lon `-6.7000`. The latitude is the same as Pin 1's, and the longitude is further west.
3. In the Pin Manager filter (the funnel button), we tick `B8A`, `B11` and `B12`. We do this for both images.
4. We write down six numbers: three bands for two dates. Pin Manager shows the numbers for whichever image window is active. So we click on the 3 April window and write them down, then on the 10 April window and write them down.

**How far the new pin is from the burn scar.** Let's work out how many kilometres there are in one degree of longitude at our latitude. At the equator, one degree of longitude is 111.32 km. Closer to the pole the meridians converge, and the degree gets shorter. It shrinks by the cosine of the latitude:

- 1° of longitude = 111.32 km × cos(latitude);
- cos(43.35°) ≈ 0.7272;
- 111.32 × 0.7272 ≈ **80.9 km**.

Now the distances:

- **From Pin 1 to the new pin:** −6.6746 − (−6.7000) = 0.0254°. 0.0254 × 80.9 ≈ **2.05 km** to the west.
- **From the western edge of the burn scar:** according to the EFFIS outline, the western edge is at longitude −6.6930. −6.6930 − (−6.7000) = 0.0070°. 0.0070 × 80.9 ≈ **0.57 km** beyond the edge of the burn scar.

So the pin is about half a kilometre from the burn scar and definitely outside the outline. We check this on the 10 April image: Pin 2 isn't on the blue.

```{figure} ../../images/ch06-snap-own-stretch-pins-2026-04-03.jpg
:label: en-fig-ch06-snap-own-stretch-pins-2026-04-03
:alt: Both images with SNAP's stretch: 3 April on the left (bluish), 10 April on the right (olive-orange). Below, Pin Manager with the 3 April values for Pin 1 (inside the burn scar) and Pin 2 (outside).
:width: 100%

Both images with SNAP's stretch: 3 April on the left (bluish), 10 April on the right (olive-orange). Below, **Pin Manager** with the 3 April values for Pin 1 (inside the burn scar) and Pin 2 (outside). Contains modified Copernicus Sentinel data (2026).
```

Here's what Pin Manager showed:

| | B8A | B11 | B12 |
|---|---|---|---|
| Pin 2, 3 April | 0.2175 | 0.2059 | 0.1155 |
| Pin 2, 10 April | 0.2343 | 0.2172 | 0.1192 |

Let's work out how much the reflectance changed. Difference = 10 April value − 3 April value. Change as a percentage = difference / 3 April value × 100.

- **B8A:** 0.2343 − 0.2175 = 0.0168. 0.0168 / 0.2175 ≈ 0.077 → **+7.7%**.
- **B11:** 0.2172 − 0.2059 = 0.0113. 0.0113 / 0.2059 ≈ 0.055 → **+5.5%**.
- **B12:** 0.1192 − 0.1155 = 0.0037. 0.0037 / 0.1155 ≈ 0.032 → **+3.2%**.

**At the point outside the burn scar, the reflectance changed by only 3–8%.** The ground is almost the same.

For comparison, here's the same check in the middle of the burn scar (Pin 1):

| | B8A | B11 | B12 |
|---|---|---|---|
| Pin 1, 3 April | 0.1773 | 0.2637 | 0.198 |
| Pin 1, 10 April | 0.1344 | 0.2207 | 0.2054 |

- **B8A:** 0.1344 − 0.1773 = −0.0429. −0.0429 / 0.1773 ≈ −0.242 → **−24%**.

In the burn scar, the near-infrared band dropped by a quarter. That's a real change: the plants that reflected this light have burned. Outside the burn scar, there's no such change.

## Step 4: Working out what colour SNAP gave the point outside the burn scar

Now we have everything we need to test hypothesis 2 by calculation. We take Pin 2's reflectance (Step 3) and the min and max that SNAP chose (Step 2), and put them into the formula:

**brightness = (reflectance − min) / (max − min) × 255**

**3 April, SNAP's stretch:**

- **Red light (B8A):** min = −0.0034, max = 0.44, reflectance 0.2175.
  - reflectance − min = 0.2175 − (−0.0034) = 0.2175 + 0.0034 = 0.2209;
  - max − min = 0.44 − (−0.0034) = 0.44 + 0.0034 = 0.4434;
  - 0.2209 / 0.4434 ≈ 0.498;
  - 0.498 × 255 ≈ **127**.
- **Green light (B11):** min = −0.0003, max = 0.27, reflectance 0.2059.
  - 0.2059 + 0.0003 = 0.2062;
  - 0.27 + 0.0003 = 0.2703;
  - 0.2062 / 0.2703 ≈ 0.763;
  - 0.763 × 255 ≈ **195**.
- **Blue light (B12):** min = 0.00001, max = 0.16, reflectance 0.1155.
  - 0.1155 − 0.00001 ≈ 0.1155;
  - 0.16 − 0.00001 ≈ 0.16;
  - 0.1155 / 0.16 ≈ 0.722;
  - 0.722 × 255 ≈ **184**.

**10 April, SNAP's stretch:**

- **Red (B8A):** min = 0.0258, max = 0.49, reflectance 0.2343.
  - 0.2343 − 0.0258 = 0.2085;
  - 0.49 − 0.0258 = 0.4642;
  - 0.2085 / 0.4642 ≈ 0.449;
  - 0.449 × 255 ≈ **115**.
- **Green (B11):** min = 0.02, max = 0.42, reflectance 0.2172.
  - 0.2172 − 0.02 = 0.1972;
  - 0.42 − 0.02 = 0.40;
  - 0.1972 / 0.40 = 0.493;
  - 0.493 × 255 ≈ **126**.
- **Blue (B12):** min = 0.0167, max = 0.39, reflectance 0.1192.
  - 0.1192 − 0.0167 = 0.1025;
  - 0.39 − 0.0167 = 0.3733;
  - 0.1025 / 0.3733 ≈ 0.275;
  - 0.275 × 255 ≈ **70**.

Let's put it in a table:

| Pin 2 | red (B8A) | green (B11) | blue (B12) | what we see |
|---|---|---|---|---|
| 3 April | 127 | 195 | 184 | light blue: green and blue are bright |
| 10 April | 115 | 126 | 70 | olive-orange: blue has almost gone out |

On 3 April the blue light is 184 / 70 ≈ 2.6 times brighter than on 10 April. Yet the reflectance in B12 differs by only 3%. **All the 'blue' on 3 April comes from SNAP's stretch, not from the ground.**

## Step 5: Setting the same stretch

For a fair comparison, the same reflectance has to give the same colour on both images. So the min and max of each band have to be the same on both dates.

Which numbers do we use? We need a range that holds the values from both images. For each band:

- **common min** = the smaller of the two mins (from the table in Step 2);
- **common max** = the larger of the two maxes.

Choosing from the table in Step 2:

- **B8A:** min −0.0034 and 0.0258 → the smaller is **−0.0034**. Max 0.44 and 0.49 → the larger is **0.49**.
- **B11:** min −0.0003 and 0.02 → the smaller is **−0.0003**. Max 0.27 and 0.42 → the larger is **0.42**.
- **B12:** min 0.00001 and 0.0167 → the smaller is 0.00001. We enter **0**: a difference of 0.00001 changes the brightness by less than a hundredth of a step. Max 0.16 and 0.39 → the larger is **0.39**.

What we enter:

| Button | Band | min | max |
|---|---|---|---|
| Red | B8A | `-0.0034` | `0.49` |
| Green | B11 | `-0.0003` | `0.42` |
| Blue | B12 | `0` | `0.39` |

**Where to enter them.** The numbers go right under the sliders, but the spot is easy to miss:

1. We click on the 3 April image window to make it active.
2. In Colour Manipulation, we choose **Red**.
3. We click on the number under the left (black) slider. A small input box opens next to it, showing the current value.
4. We delete it, type `-0.0034` and press Enter. The slider moves.
5. We click on the number under the right (coloured) slider, type `0.49` and press Enter.
6. The same for **Green** (`-0.0003`, `0.42`) and **Blue** (`0`, `0.39`).
7. We click on the 10 April window and enter the same six numbers.

```{figure} ../../images/ch06-colour-manip-edit-value.jpg
:label: en-fig-ch06-colour-manip-edit-value
:alt: Clicking the number under the slider opens a box for typing the value; here, the B8A min: -0.0034.
:width: 100%

Clicking the number under the slider opens a box for typing the value; here, the B8A min: `-0.0034`.
```

We type the numbers with a point and the ordinary hyphen for the minus sign, as in the table.

**What we expect to see.** Let's work out Pin 2's colour with the common stretch in advance.

3 April:

- red: (0.2175 + 0.0034) / (0.49 + 0.0034) × 255 = 0.2209 / 0.4934 × 255 ≈ 0.448 × 255 ≈ **114**;
- green: (0.2059 + 0.0003) / (0.42 + 0.0003) × 255 = 0.2062 / 0.4203 × 255 ≈ 0.491 × 255 ≈ **125**;
- blue: (0.1155 − 0) / (0.39 − 0) × 255 = 0.1155 / 0.39 × 255 ≈ 0.296 × 255 ≈ **76**.

10 April:

- red: (0.2343 + 0.0034) / 0.4934 × 255 = 0.2377 / 0.4934 × 255 ≈ 0.482 × 255 ≈ **123**;
- green: (0.2172 + 0.0003) / 0.4203 × 255 = 0.2175 / 0.4203 × 255 ≈ 0.518 × 255 ≈ **132**;
- blue: 0.1192 / 0.39 × 255 ≈ 0.306 × 255 ≈ **78**.

| Pin 2, common stretch | red | green | blue |
|---|---|---|---|
| 3 April | 114 | 125 | 76 |
| 10 April | 123 | 132 | 78 |

The difference is no more than 9 steps out of 255. To the eye, it's the same colour. So after Step 5, the 3 April image should stop being blue and turn olive, like 10 April.

And in the burn scar (Pin 1), with the same common stretch:

- 3 April: red (0.1773 + 0.0034) / 0.4934 × 255 ≈ **93**, green (0.2637 + 0.0003) / 0.4203 × 255 ≈ **160**, blue 0.198 / 0.39 × 255 ≈ **129**;
- 10 April: red (0.1344 + 0.0034) / 0.4934 × 255 ≈ **71**, green (0.2207 + 0.0003) / 0.4203 × 255 ≈ **134**, blue 0.2054 / 0.39 × 255 ≈ **134**.

The red has dropped by 22 steps, and the blue is now as strong as the green. In the burn scar, the colour shifts towards blue. That change stays even with the common stretch, because it's real.

## What we found

**Both hypotheses held up.**

1. **The ground has hardly changed.** At the point outside the burn scar, the reflectance rose by 3–8% in seven days (Step 3).
2. **The different colour came from SNAP.** It chose a stretch for each image separately, from the whole scene. On 10 April, the clouds pushed max up: in band B12, from 0.16 to 0.39, 2.4 times higher. Because of that, at the very same point, the blue light was at 184 on 3 April and at 70 on 10 April (Step 4).

Once we entered the same min and max, **the images turned the same colour**. The slopes, fields and woods around look the same on both dates. Only the burn scar is different: on 10 April it's blue.

```{figure} ../../images/ch06-snap-common-stretch-2026-04-03-10.jpg
:label: en-fig-ch06-snap-common-stretch-2026-04-03-10
:alt: The same two images with the common stretch: the unburnt ground is the same colour on 3 and 10 April; only the burn scar changes, blue on 10 April.
:width: 100%

The same two images with the common stretch: the unburnt ground is the same colour on 3 and 10 April; only the burn scar changes, blue on 10 April. Contains modified Copernicus Sentinel data (2026).
```

And one more thing. A small dark blue patch east of the burn scar is already visible on 3 April, before our fire. With the common stretch it stands out more. We'll look at what it is in Lesson 6.2.

## If something goes wrong

1. **We wrote down the numbers from the box at the top right, not from under the sliders.** The numbers in the box (Min, Max) are the band's statistics. The stretch is the numbers under the sliders.
2. **A number like `-3.39E-3` makes no sense.** E means 'multiply by 10 to the power of'. `-3.39E-3` = −0.00339 (Step 2).
3. **The input box won't open.** We click exactly on the number under the slider, not on the slider itself. If a single click doesn't work, we try a double click.
4. **We entered the numbers, but the colour didn't change.** Most likely the numbers went into the other image's window. Colour Manipulation always shows the active window: its name is on the tab at the top (for example, Navigation − [3] RGB).
5. **SNAP won't accept the minus sign.** We type the minus as an ordinary hyphen `-`, and the decimal separator as a point.

:::{tip} Did you know?
In the statistics box, the 3 April image has Min = −0.1. That isn't a real reflectance. Those are pixels with no data: the file holds 0 there, and by the formula from Lesson 5.2, (0 − 1000) / 10000 = −0.1. Even the statistics faithfully show how the file is built.
:::

:::{admonition} Your data
- We put the pin outside the burn scar next to our own fire: the same latitude as the pin in the burn scar, and a longitude beyond the edge of the outline. We work out the distance in the same way: 111.32 km × cos(latitude) for one degree of longitude.
- Our min and max will be different: they depend on the scene, the clouds and the date. The order is the same: write down the numbers under the sliders for both dates → common min = the smaller, common max = the larger → enter them in both windows.
:::

## Summary

**New terms**

- **Contrast stretch**: converting reflectance into screen brightness using two numbers, min and max. Example: with min 0.05 and max 0.35, a reflectance of 0.20 gives a brightness of 128.
- **Histogram**: a graph of how many pixels in an image have each value. Example: in Colour Manipulation, a tall peak on the left is the dark pixels of water and shadow.
- **Same stretch**: the same min and max for each band on all the images being compared. Example: B12 min 0, max 0.39 for 3 and 10 April.

**Key points**

- The colour on the screen depends not only on the reflectance but also on the min and max of the stretch.
- SNAP chooses a stretch for each image from the whole scene; clouds far from our site can change the colour of our slope.
- We can only compare 'before' and 'after' images by eye with the same stretch.
- If we need an answer rather than a picture, we look at the reflectance numbers in Pin Manager or Pixel Info.

## Questions for an engineer

1. Why did clouds far out over the sea change the colour of our slope?

:::{dropdown} Answer
SNAP chooses min and max from the histogram of the whole scene. Bright clouds add lots of high values and push max up. The higher max is, the dimmer the light for the same reflectance.
:::

2. Why is the common min the smaller of the two, and the common max the larger?

:::{dropdown} Answer
That way the range holds the values from both images, and neither image has more 'clipped' to 0 or 255 than the other.
:::

3. Once the stretch is the same, can we measure the burn scar by its colour?

:::{dropdown} Answer
No. The stretch is only for the eye. For calculations we use the reflectance numbers themselves; in Chapter 8 we'll build an index from them.
:::


## Exercises

1. **Understand:** why can't we compare 'before' and 'after' images by eye if the software has set the contrast for each one by itself?
2. **Fix it:** 'On the 10 April image the unburnt slope is brighter, so its reflectance went up after the fire.' What's wrong?
3. **One lesson back (5.3):** why do we use L2A rather than L1C to compare 'before' and 'after'?

The answers are on the [Solutions](../solutions.md) page.

## The open question

With the same stretch, a dark blue patch is visible east of the burn scar, and it was already there on 3 April, before the fire. It looks like an older burn scar. Does it fall inside our frame, and could we mistake it for the burn scar of 6 April? We'll look at that in Lesson 6.2, and draw a quick outline of the burn scar there too.

---

## Notes and sources

- Sentinel-2 L2A images of 3 and 10 April 2026, tile T29TPJ, orbit R037 (Copernicus Data Space Ecosystem), opened in SNAP 14.
- EFFIS burn scar outline, record 294223: western edge at −6.6930. https://api.effis.emergency.copernicus.eu/rest/2/burntareas/current/294223/ (accessed 21 November 2026)
- Length of a degree of longitude: 111.32 km × cos(latitude), on a spherical Earth model; accurate enough for our distances.
