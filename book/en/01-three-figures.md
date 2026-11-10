---
title: "Chapter 1: Three figures for one fire"
---

## Where we left off

In the prologue we found that the Bustantigo fire has two figures for its area, 681 and 700 ha, and neither comes with an uncertainty. We also learnt that in the mountains a satellite can mistake spring sunshine for regrowing grass.

Before we calculate anything, we need to sort out three things:

1. what a satellite actually measures;
2. where those two figures came from;
3. why they differ.

And at the end, we'll look at the fire ourselves for the first time.

## What remote sensing is

**Remote sensing means measuring without touching.** We don't walk the slope with a tape measure. We measure it from a distance: from a plane, a drone or a satellite. Hence the name: we sense it remotely.

The closest familiar comparison is aerial photography. A plane flies over the area and photographs it, and then a map is drawn from the photos. Sentinel-2 does the same job, with two important differences.

1. **It measures rather than photographs.** Each point in the image holds not a 'colour for the eye' but a number: the share of sunlight the surface reflected. That's a measurement, like an instrument reading. We can calculate with it, compare it and check it.
2. **It sees more than the eye.** The eye sees three colours: red, green and blue. Sentinel-2 measures light in 13 narrow parts of the spectrum.[^s2] Some of them are invisible to us: near-infrared and shortwave infrared. And it's in the infrared that living vegetation and burnt ground differ most.

There's a third thing to understand: Sentinel-2 emits nothing itself. It only receives sunlight reflected by the ground. An instrument like this is called passive. An active instrument, such as the laser rangefinder in a total station or a LiDAR, sends out its own signal and catches the reflection. For us, the key consequence is that a passive instrument depends on the sun. Where the sun is weak, the measurement is worse. And that's where our problem with slopes comes from.

**So a satellite is a measuring instrument. And every measurement has an uncertainty that we need to know.**

## Who calculated 681 and 700 hectares

Both figures come from satellite images, but they were obtained in different ways.

1. 681 ha comes from the open catalogue of Spain's large wildfires. Its author took the Sentinel-2 image of 8 April and outlined the burn scar, that is, drew its boundary on the image. He warns himself that the boundary may be out by hundreds of metres.[^edu]
2. 700 ha comes from EFFIS, the European service that maps fires across Europe. Its boundaries are found semi-automatically from satellite images: software picks out the areas that have changed, and a person checks them.[^rda] The record was last updated on 9 April.[^effis]

**So these aren't two 'truths'. They're two measurements, made by different people in different ways.**

## Why one fire has different figures

As engineers, we ask: is a difference of 19 ha a lot or a little? To answer that, we need to know what error is possible at all. Let's work it out ourselves.

Sentinel-2 divides the ground into cells, called pixels. In the infrared bands used to find burn scars, a pixel is 20 by 20 metres. That's our 'measurement step'. A burn scar boundary can't be more precise than one pixel.

Now let's estimate what happens if the boundary shifts outwards by just one pixel.

1. The fire covers about 700 ha, that is, 7,000,000 m².
2. **The length of the boundary.** If the fire were a circle, its radius would be about 1.5 km and its boundary about 9.4 km. A real fire perimeter twists and turns, so the boundary is longer. Let's take about 15 km.
3. **A one-pixel shift:** 15,000 m × 20 m = 300,000 m², which is 30 ha.

**The difference between 681 and 700 ha is smaller than a one-pixel shift of the boundary.** So from these two figures we can't tell which is more accurate. They agree within an uncertainty that nobody stated.

Besides pixel size, the figures differ for three more reasons:

- different images and dates: the later the image, the weaker the trace of the fire;
- different ways of drawing the boundary: by hand or by software;
- what counts as burnt: whether to include unburnt islands inside the perimeter and the lightly burnt edge.

**So our job isn't to pick one of the two figures. It's to get our own, with an uncertainty and an explanation of how we got it.**

## Looking at the fire ourselves

Now let's open an image. We'll work in Copernicus Browser. It's a free European Union website where we can view every Sentinel-2 image straight in the browser, without downloading anything. Today it's the main tool for a first look at the images.

Step by step:

1. Open https://browser.dataspace.copernicus.eu
2. **Create a free account:** 'Login' at the top right, then 'Register'. We'll need it throughout the book.
3. **Find the place.** In the search bar at the top, type the fire's coordinates, 43.361, -6.671, or the name Bustantigo.
4. **Choose the data.** In the search tab on the left: the Sentinel-2 collection, level L2A. Set the date to 8 April 2026, the image on which the 681 ha was outlined.
5. **Look in natural colour:** the True Color visualisation. This is what the eye would see.
6. **Look in the infrared:** the SWIR visualisation. Here the invisible bands are put in place of the visible colours.

**Before we look, let's write down what we expect.** It's an engineer's habit: predict first, then check. We expect that:

- in natural colour the burn scar will be hard to see: a dark patch that looks like a shadow cast by the slope;
- in SWIR the burn scar will stand out clearly in colour from the living heathland, and its boundary will be sharper.

## What we saw

```{figure} ../images/ch01-true-color-2026-04-08.jpg
:label: en-fig-ch01-true-color-2026-04-08
:alt: Sentinel-2 L2A image of 8 April 2026 in natural colour (True Color), Copernicus Browser.
:width: 100%

Sentinel-2 L2A image of 8 April 2026 in natural colour (True Color), Copernicus Browser. Contains modified Copernicus Sentinel data (2026).
```

```{figure} ../images/ch01-wildfires-layer-2026-04-08.jpg
:label: en-fig-ch01-wildfires-layer-2026-04-08
:alt: The same image with the Wildfires visualisation.
:width: 100%

The same image with the Wildfires visualisation. Contains modified Copernicus Sentinel data (2026).
```

```{figure} ../images/ch01-swir-2026-04-08.jpg
:label: en-fig-ch01-swir-2026-04-08
:alt: The same image in the infrared (SWIR: bands B12, B8A and B4). The Bustantigo burn scar is the reddish-brown patch in the centre.
:width: 100%

The same image in the infrared (SWIR: bands B12, B8A and B4). The Bustantigo burn scar is the reddish-brown patch in the centre. Contains modified Copernicus Sentinel data (2026).
```

### Natural colour

In the first image, from 8 April 2026, in natural colour, there's a dark brown patch in the centre. That's the burn scar at Bustantigo.

But look further right, near Tineo: there's another dark patch, almost the same. That isn't a fire. It's the shadow of a cloud, and the cloud itself is right next to it.

**In natural colour, a burn scar and a shadow look the same:** a dark patch on green. If we searched for burn scars by eye in ordinary colours alone, we could easily get it wrong. The first part of our expectation is confirmed.

### Infrared bands

In the third image, with the SWIR visualisation, the picture changes:

- Living vegetation is bright green.
- The burn scar is dark reddish-brown, with a sharp boundary. We can see it straight away.
- The cloud shadow near Tineo is almost black, not red.
- The clouds are white.

**In the infrared bands, the burn scar stands out from both living vegetation and shadow.** The second part of our expectation is confirmed too.

We'll look at why this happens in Chapter 3. For now, one thing is enough: living plants hold water, so they reflect infrared light differently from burnt ground. The satellite measures that difference even when the eye can't see it.

### What else we can see

The SWIR image also shows other small reddish-brown patches, for example lower down, near Cangas del Narcea. They're probably traces of other fires from the same spring. We'll check that later, when we look for the other four fires.

The second screenshot shows the Wildfires visualisation. It highlights active flames: fire is very hot and glows strongly in the shortwave infrared. By 8 April the fire is already out, so there's nothing to highlight, and the picture looks like natural colour. This layer is only useful while a fire is still burning.

### One figure worth remembering

Next to the date, Copernicus Browser shows a cloud cover of 30%. But there are no clouds over our fire: they're further west and south.

That's because the 30% is the cloud cover of the whole scene, a square 110 by 110 km. **For our work, what matters is whether there are clouds over the area we're studying, not over the whole scene.** We'll come back to this in Chapter 4, when we choose our images.

:::{admonition} Your data
You can do all of this for any fire. You need the coordinates of the place and a date: the first clear day after the fire. You can find the coordinates and dates of large fires in Europe in EFFIS.
:::

## Summary

**New terms**

- **Remote sensing:** measuring the ground without contact, from a plane, a drone or a satellite.
- **Passive sensor:** an instrument that receives reflected sunlight and emits nothing itself.
- **Pixel:** a cell of an image holding one measured value; for Sentinel-2 in the infrared bands, 20 by 20 metres.
- **Spectral band:** a narrow part of the spectrum in which an instrument takes its measurement.
- **Scene:** a single Sentinel-2 image, a square 110 by 110 km.

**Key points**

- A satellite is a measuring instrument, and its results have an uncertainty.
- The difference between 681 and 700 ha is smaller than a one-pixel shift of the boundary, so these figures can't tell us which is more accurate.
- In natural colour, a burn scar is easy to confuse with a shadow; in the infrared bands, they look different.
- Cloud cover for the scene and cloud cover over our area are two different things.

## Questions for an engineer

1. In the natural-colour image we see a dark patch. How can we check whether it's a burn scar or a shadow?

:::{dropdown} Answer
Switch to the infrared bands (SWIR): a burn scar will be reddish-brown, and a shadow almost black. We can also check whether there's a cloud nearby casting the shadow.
:::

2. Two services gave 681 and 700 ha. Can we say which one got it wrong?

:::{dropdown} Answer
No. Shifting the boundary by just one pixel changes the area by about 30 ha, and the difference between the figures is 19 ha. Without an uncertainty for both estimates, we can't say which is more accurate.
:::

3. The image has 30% cloud cover, but there are no clouds over the fire. Can we use it?

:::{dropdown} Answer
For a first look, yes: the 30% refers to the whole scene, and all that matters to us is our area. But we'll make the final choice of images by clear rules that we write down in advance.
:::

## The open question

We've seen the burn scar. But to measure it, we need to compare an 'after' image with a 'before' image. Which images should we choose, and by what rules, so that we can trust the result later? Before we search, we'll learn to think like engineers: the question and the rules first, then the search.

---

## Notes and sources

[^edu]: [edu.forestry.es, 'Grandes Incendios Forestales 2026 en España'](https://edu.forestry.es/p/gif2026.html) (in Spanish): Allande, 681 ha, perimeter drawn on a Sentinel-2 image of 8 April 2026; the author warns that the boundaries 'may contain errors of hundreds of metres'.
[^rda]: [EFFIS, *Rapid Damage Assessment*](https://forest-fire.emergency.copernicus.eu/about-effis/technical-background/rapid-damage-assessment): fires are mapped with an unsupervised procedure, then visually verified and corrected.
[^effis]: EFFIS, burnt area 294223 (Allande): 700 ha, updated 9 April 2026. [EFFIS burnt areas API](https://api.effis.emergency.copernicus.eu/rest/2/burntareas/current/).
[^s2]: [Copernicus SentiWiki, *Sentinel-2 mission*](https://sentiwiki.copernicus.eu/web/s2-mission): 13 spectral bands; four at 10 m, six at 20 m and three at 60 m.
