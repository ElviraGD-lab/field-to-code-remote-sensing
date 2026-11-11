---
title: "Chapter 3: What a satellite sees"
---

## Where we left off

In Chapter 1 we saw that in the infrared bands a burn scar is reddish-brown, living vegetation is green and a shadow is almost black. In the rules for choosing images we talked about bands and SWIR as well. It's time to understand what lies behind all this. Then we'll be reading an image, not just recognising colours.

## What light means to a satellite

Sunlight is a mixture of waves of different lengths. The eye sees only a narrow part of it, roughly from 0.4 to 0.7 micrometres (µm):

- short waves we see as blue;
- medium ones as green;
- long ones as red.

Beyond red, the light carries on, but the eye can no longer see it:

- near-infrared (NIR): roughly 0.7–1.3 µm;
- shortwave infrared (SWIR): roughly 1.3–2.5 µm.

This is the same sunlight, just at a different wavelength. The thermal radiation given off by a warm body starts further out still, and we don't need it here.

**The satellite doesn't care whether the eye can see the light. It measures all these parts in the same way.**

## What each band measures

Sentinel-2 splits light into 13 narrow parts.[^s2] Each of these parts is called a band. In each band the satellite measures one thing: the share of incoming sunlight that the surface reflected. This number, from 0 to 1, is called reflectance. 0 means the surface absorbed all the light; 1 means it reflected all of it.

Seven bands matter for our work:

| Band | Light | Pixel | Why we need it |
|---|---|---|---|
| B2 | blue | 10 m | natural colour |
| B3 | green | 10 m | natural colour |
| B4 | red | 10 m | natural colour; plants absorb it |
| B8 | near-infrared | 10 m | living plants reflect it strongly |
| B8A | near-infrared, narrow | 20 m | the same; used together with SWIR |
| B11 | shortwave infrared 1 | 20 m | sensitive to water in plants |
| B12 | shortwave infrared 2 | 20 m | the main band for burn scars |

That's where the 20 metres in Chapter 1 came from: the Sentinel-2 infrared bands used to find burn scars have 20 by 20 metre pixels.

## How living vegetation reflects light

Let's take a plant leaf step by step. Each step follows from how the leaf is built.

1. **The leaf absorbs red and blue light.** Chlorophyll takes this energy for photosynthesis. That's why living vegetation is dark in the red band.
2. **It absorbs a little less green.** That's why leaves look green to us.
3. **The leaf strongly reflects near-infrared.** The plant doesn't need it for photosynthesis, and inside the leaf there are many cells with air spaces between them. At every cell–air boundary the light scatters, and most of it heads back out. A living leaf is very bright in the near-infrared, much brighter than in visible light.
4. **Water in the leaf absorbs shortwave infrared.** The more water a plant holds, the darker it is in SWIR.

**So living vegetation has its own pattern:** dark in the red, bright in the near-infrared, dark in SWIR. A pattern of reflectance like this across the bands is called a spectral signature.

## What a fire changes

Now let's burn that leaf and see what happens at each step.

1. **No chlorophyll:** red light is no longer absorbed so strongly.
2. **No cells with air:** charcoal and ash don't scatter near-infrared. The burn scar turns dark in the near-infrared.
3. **No water:** there's nothing left to absorb SWIR, and bare, dry ground reflects this light well. In SWIR the burn scar becomes brighter than the vegetation was.

**A fire turns the pattern upside down:** what was bright in the near-infrared becomes dark, and what was dark in SWIR becomes brighter. No other familiar change on a slope does both of these at once in both bands. That's why the best way to find a burn scar is with the near-infrared–SWIR pair.

## Where the colours in our image come from

Now we can explain what we saw in Chapter 1. The SWIR visualisation sends three bands to the three colours of the screen:

- B12 (SWIR 2) to red;
- B8A (near-infrared) to green;
- B4 (red light) to blue.

Let's work out each colour ourselves:

- **Living vegetation:** B8A bright, B12 dark → green dominates on screen. Green.
- **Burn scar:** B8A dark, B12 brighter → red dominates, and the whole thing is fairly dull. Reddish-brown.
- **Cloud shadow:** little light in any band → almost black.
- **Cloud:** reflects almost everything in every band → white.
- **Water:** absorbs both near-infrared and SWIR → black. In our image, the River Navia and the reservoir really are black.

**A colour in the image isn't 'the colour of the object'.** It's a record of how much light the object reflected in each of three bands. If we know which band goes to which colour, we can predict the colour of any surface.

## What it means to 'send a band to a colour'

### The satellite has already measured everything

**Let's start with the key point:** when we switch visualisations, the satellite does nothing. It passed over Asturias once on 8 April 2026, and on that single pass it measured the light in all 13 bands at once.

For every pixel we have 13 numbers, one per band. We can picture the image as a stack of 13 sheets of tracing paper, all with the same grid. On each sheet, every cell holds one number: how much light that patch of ground reflected in that band.

**The data stay the same. All that changes is how we display them.**

### A screen can only do three colours

Every screen shows colour the same way. At each point on the screen there are three tiny lights: red, green and blue. Each one shines at some brightness, from zero to full. Every colour on the screen is a mix of these three:

- only the red one is on: we see red;
- red and green: yellow;
- all three bright: white;
- all three dim: almost black.

**The screen can't show all 13 layers at once. It only has three lights.**

### We choose which layer controls which light

So we pick three layers out of the thirteen and decide:

- the numbers in this layer control the red light;
- the numbers in this one, the green light;
- the numbers in this one, the blue light.

The bigger the number in a pixel, the brighter the light shines. That's what 'sending a band to a colour' means.

A visualisation in Copernicus Browser is a ready-made recipe: which three bands go to which three lights. When we switch visualisations, all we change is the display recipe.

We know this from surveying. The same set of surveyed points can be coloured on a map by height, or by the date they were measured. The measurements are the same; only the way we show them to the eye changes.

### Taking it pixel by pixel

Let's take three pixels: living heathland, burn scar and water. The numbers below are made up, just for illustration, but the ratios between them are like those of real surfaces:

| Pixel | B3 (green light) | B4 (red light) | B8 (near-infrared) |
|---|---|---|---|
| living heathland | 0.06 | 0.04 | 0.40 |
| burn scar | 0.06 | 0.07 | 0.12 |
| water | 0.05 | 0.03 | 0.01 |

The True color recipe sends B4 to the red light, B3 to the green and B2 to the blue. This is what the eye sees: each band goes to 'its own' colour. The heathland comes out dark green.

The False color recipe sends B8 to the red light, B4 to the green and B3 to the blue. Let's look at the living heathland:

1. The red light gets B8 = 0.40. That's a big number, so the light shines brightly.
2. The green light gets B4 = 0.04, so it barely shines.
3. The blue light gets B3 = 0.06, so it barely shines either.

It's mostly the red light that's on, so living vegetation is red in False color. Not because the grass is red, but because we've sent its bright near-infrared to the red light.

**A colour on the screen doesn't tell us 'what colour the object is'. It tells us 'in which band the object is brightest', under the recipe we've chosen.**

## Testing ourselves on the image

Let's do what we did in Chapter 1: predict first, then look.

In Copernicus Browser, on the same image from 8 April 2026, we switch on the False color visualisation. In it, the bands are sent like this:

- B8 (near-infrared) to red;
- B4 (red light) to green;
- B3 (green light) to blue.

Let's predict the colour of:

- living vegetation;
- the burn scar;
- water.

We write the prediction down before switching the visualisation, then check it against the image.

## What we found

```{figure} ../images/ch03-false-color-2026-04-08.jpg
:label: en-fig-ch03-false-color
:alt: The image of 8 April 2026 in False color (bands B8, B4 and B3), Copernicus Browser. Contains modified Copernicus Sentinel data (2026).
:width: 100%

The image of 8 April 2026 in False color (bands B8, B4 and B3), Copernicus Browser. Contains modified Copernicus Sentinel data (2026).
```

We predicted the colours in False color from the table and checked them on the image from 8 April 2026.

1. **Living vegetation is bright red.** Its near-infrared goes to the red light and shines brightest of all. The prediction matched.
2. **Water is black.** The River Navia and the reservoir show up as black lines. All three numbers are close to zero, so none of the lights is on. It matched.
3. **The burn scar is dark, almost black, with a brownish tinge.** All three lights shine weakly, the red one slightly more than the others. It matched.

But this image also shows something we didn't predict: in False color, cloud shadows are dark too, almost like the burn scar. That makes sense: in shadow there's little light in any band.

**So False color separates the living from the non-living well, but a burn scar and a shadow look alike in it. For finding burn scars, the SWIR visualisation is better: there the burn scar is reddish-brown and the shadow is black.**

**That gives us a rule worth keeping for any work with images: we look at the same image with several recipes, because each recipe shows a different kind of difference.**

:::{admonition} Your data
The bands and their numbers are the same for every Sentinel-2 image, anywhere on Earth. The band table and the reasoning about colours work for any fire.
:::

We know what each band measures and how the bands turn into a picture. Before we search for images, there's one thing left to understand: when, and how often, the satellite passes over our fire.

## The satellite circles the Earth over the poles

Sentinel-2 flies at an altitude of about 786 km[^orb], on an orbit that passes almost over the poles. While it travels from north to south, the Earth turns beneath it. So on each orbit it sees a new strip of ground 290 km wide.

The satellite doesn't work alone:

- most of the work is done by Sentinel-2B and Sentinel-2C;
- the older Sentinel-2A carries on taking extra images, which ESA has decided will continue until the end of 2026.[^s2a]

## Why it always passes over at the same time

Sentinel-2's orbit is sun-synchronous. It slowly turns as the Earth moves around the Sun. As a result, the satellite always crosses the equator at 10:30 local solar time. Over Asturias that's about 11:20 GMT, the time we already used in the prologue.

Why is it done this way? In the morning there are usually fewer clouds than later in the day, and the sun is already fairly high. Most importantly, images from different days can be compared: the sun is in the same position in the daily cycle on all of them.

**This leads to an important conclusion for us. The difference in sun between two images depends only on the time of year, not on the time of day. The closer the dates of the 'before' and 'after' images, the smaller that difference. That's exactly why our rules require a 'before' image as close to the fire as possible.**

## How often it sees our fire

1. A single satellite returns to exactly the same track every 10 days.
2. Two satellites fly on opposite sides of the Earth, so at the equator any place is imaged every 5 days.
3. At our latitudes, the strips from neighbouring orbits overlap, and one place falls into several strips at once. So there are even more images over Asturias. We'll see exactly how many there are over our fire in the catalogue in Chapter 4.

But frequent passes don't mean frequent clear images. Sentinel-2 measures sunlight, and sunlight doesn't get through clouds. Asturias is cloudy in spring, so many passes are useless for our area. Frequent passes are there precisely so that we can find a clear image among the many cloudy ones.

## The flight track: the relative orbit

In 10 days the satellite completes 143 orbits, and then it repeats the same tracks again. Each of the 143 tracks has its own number: this is the relative orbit.

A single place can fall into the strips of several neighbouring tracks:

- from one track, the satellite looks at the slope almost straight down;
- from another, it looks from the side, from the edge of its strip.

A sunlit slope looks different when viewed from different directions. That's why our rules say: wherever possible, the 'before' and 'after' images come from the same relative orbit.

## A pixel on the ground

The number in a pixel isn't a value at a single point. It's an average over the whole square: 20 by 20 metres in the infrared bands. Two things follow from this.

1. **At the edge of a burn scar, the pixels are mixed:** they're partly burn scar and partly living vegetation, and their value is an average. That's where the one-pixel uncertainty in the boundary comes from, which we worked out in Chapter 1.
2. **The satellite won't see an unburnt island smaller than a pixel.** It will 'dissolve' into the average value of the burn scar.

## Tiles

To make the data easy to work with, the image strips are cut into squares of 100 by 100 km with a small overlap, about 110 km. These are tiles. Each has a code, for example something like 29TPH. The first digits are the UTM zone number; the letters give the square's position within the zone. Our fire lies west of 6°W, so its tile is in UTM zone 29. We'll read off exactly which one in the catalogue.

:::{admonition} Your data
Sentinel-2 passes over at the same local solar time anywhere on Earth. The easiest way to find the relative orbit and tile number for your own location is in the image catalogue: they're listed for every image.
:::

## Summary

**New terms**

- **Near-infrared (NIR):** light with a wavelength of roughly 0.7–1.3 µm; living plants reflect it strongly.
- **Shortwave infrared (SWIR):** light with a wavelength of roughly 1.3–2.5 µm; water in plants absorbs it.
- **Band:** a narrow part of the spectrum in which the satellite takes one measurement.
- **Reflectance:** the share of incoming light that a surface reflected, from 0 to 1.
- **Spectral signature:** the pattern of a surface's reflectance across different bands.
- **Sun-synchronous orbit:** an orbit on which the satellite passes over any place at the same local time.
- **Swath width:** the width of ground the satellite sees on one pass; 290 km for Sentinel-2.
- **Revisit time:** how often the satellite images the same place.
- **Relative orbit:** the number of a flight track; Sentinel-2 has 143 of them.
- **Mixed pixel:** a pixel that contains different surfaces; its value is an average.
- **Tile:** one of the coded squares, about 110 by 110 km, into which Sentinel-2 images are cut.

**Key points**

- Living vegetation is dark in the red, bright in the near-infrared and dark in SWIR.
- A fire turns this pattern upside down: near-infrared drops and SWIR rises.
- A colour in an image depends on which band is sent to which screen colour.
- A burn scar shows up best with the near-infrared–SWIR pair.
- Sentinel-2 always passes over Asturias at about 11:20 GMT, so the difference in sun between images depends only on the season.
- There are many passes but few clear images: the satellite can't see through clouds.
- Slopes look different from different relative orbits.
- A pixel is an average over a square; burn scar boundaries and small islands are blurred.

## Questions for an engineer

1. Why is a living leaf brighter in the near-infrared than in visible light?

:::{dropdown} Answer
Visible light, especially red and blue, is absorbed by chlorophyll for photosynthesis. The plant doesn't need near-infrared, and inside the leaf it scatters again and again at the boundaries between cells and air, so most of it heads back out.
:::

2. A slope has dried out after a hot summer, but it hasn't burned. How will it change in SWIR and in the near-infrared?

:::{dropdown} Answer
In SWIR it will get brighter, because the plants hold less water. In the near-infrared it will change only a little: the leaf cells are still there. With a burn scar, both signs change at once: the near-infrared darkens sharply and SWIR rises. That's why drought and fire can be told apart.
:::

3. Why are both shadow and water black in the SWIR visualisation? How can we tell them apart?

:::{dropdown} Answer
Both reflect almost no light in all three bands shown. We can tell them apart by shape and position: water follows the course of the river or the shore of the reservoir, while a shadow lies next to its cloud and moves with it on images from different dates.
:::

4. Two images were taken on 10 March and 8 April. Why is the sun in a different position on them, even though the satellite passes over at the same time?

:::{dropdown} Answer
Because the time of day is the same, but the time of year is different. Over a month the midday sun climbs higher, so the slopes are lit differently.
:::

5. The satellite passed over the fire 12 times in a month, but there are only 2 clear images. Is that a mistake in the catalogue?

:::{dropdown} Answer
No. Sentinel-2 measures reflected sunlight and can't see through clouds. The pass happened, but there were clouds over our area.
:::

6. Inside the burn scar there's an unburnt clearing 10 by 10 metres. Will we see it on the image?

:::{dropdown} Answer
Not on its own: it fills only a quarter of a 20 by 20 metre pixel. Its reflectance will mix with the burn scar's, and the pixel will look slightly lighter than its neighbours, but still like burn scar.
:::

## The open question

We know what the satellite measures, when it passes over and why images are often cloudy. Now we can search for our pair of images: the nearest clear 'before' and the first clear 'after'. That's Chapter 4.

---

## Notes and sources

[^s2]: [Copernicus SentiWiki, *Sentinel-2 mission*](https://sentiwiki.copernicus.eu/web/s2-mission): 13 spectral bands; four at 10 m, six at 20 m and three at 60 m.
[^orb]: [Copernicus SentiWiki, *Sentinel-2 mission*](https://sentiwiki.copernicus.eu/web/s2-mission): sun-synchronous orbit at a mean altitude of 786 km, descending node at 10:30 mean local solar time, 10-day cycle of 143 orbits, 290 km swath.
[^s2a]: [Copernicus Data Space Ecosystem, 'Sentinel-2A Extension Campaign Prolonged Until the End of 2026', 15 May 2026](https://dataspace.copernicus.eu/node/3911).
