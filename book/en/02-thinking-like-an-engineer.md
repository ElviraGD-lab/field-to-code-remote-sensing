---
title: "Chapter 2: Thinking like an engineer"
---

## Where we left off

We've seen the burn scar on an image, and we've realised that to measure it we need to compare images from before and after the fire. The simplest thing now would be to grab two images straight away, calculate something and get a figure.

But we won't do that. First, let's see why.

## Why we can't just start calculating

We'll get a figure whatever we do. Software always calculates something. The real question is different: can we trust that figure and explain it?

If we start with the calculation, this is what usually happens:

1. we take the first images that come to hand;
2. we try a threshold: we get 650 ha;
3. we try another: 720 ha;
4. we pick the one that 'looks right', meaning the one closest to EFFIS's 700 ha.

What we end up with isn't a measurement. It's a fit to someone else's figure. And nobody, ourselves included, can explain why it came out that way.

**An engineer first decides what to measure, how to measure it and how to check the result. Only then do they measure.**

## The method in six steps

We'll repeat this sequence in every chapter of the book. It works for any problem with satellite data.

1. **The question.** We turn a vague problem into a question that a measurement can answer: what exactly, where, when and how precisely.
2. **What we know and what we don't.** We separate the known from the unknown.
3. **The options.** The ways we could answer the question.
4. **The choice.** We choose one way and write down why we chose it.
5. **The check.** We write down in advance how we'll check the result and what we'll count as a failure.
6. **Do it and compare.** We carry it out and compare the result with what we expected.

**Steps 1 and 5 are the ones that matter most. A good question and a check written down in advance protect us from fooling ourselves.**

## Step 1: Turning 'how much burned?' into a question

'How much burned?' sounds clear, but no measurement can answer it as it stands. The question has five gaps.

1. **What 'burned' means.** Unburnt islands remain inside the fire perimeter. Do we count them or not? Our decision: a burn scar is any area where the fire of 6 April 2026 destroyed or damaged the vegetation. We don't count the islands inside it. We'll also record the area inside the overall perimeter, but separately, because that's often the figure the services give.
2. **Where.** Only this fire at Bustantigo. Areas burnt in 2017 and 2023 aren't included, even where they border ours.
3. **When.** On the date of the first clear image after the fire. Later on, the trace fades, as we know from the prologue.
4. **How precisely.** Not a single figure, but an area with an interval that contains the true value with 95% probability.
5. **In what units.** In hectares.

Now the question reads:

**Q1. What area of vegetation burned in the fire of 6 April 2026 at Bustantigo, measured on the first clear Sentinel-2 image after the fire, with a 95% interval, and how far does that area depend on how the slopes are lit?**

It's long, but a measurement can answer it, and the answer can be checked.

We build the second question the same way:

**Q2. How does the trace of a fire on Sentinel-2 images change from the first clear image after the fire until November 2026, for five fires in Asturian mountain heathland between February and April, and how much of that change is explained by changes in how the slopes are lit rather than by regrowing vegetation?**

## Step 2: What we know and what we don't

**We know:**

- the date of the fire (6 April 2026) and the place;
- two estimates of the area by others: 681 and 700 ha, with no uncertainty;
- that a burn scar shows up well in the infrared bands;
- that the 8 April image is clear over the fire;
- that the light on the slopes changes with the seasons.

**We don't know:**

- which 'before' image is clear and suitable for us;
- which method is best for drawing the burn scar boundary;
- how much the light affects the result on our particular slopes;
- what the uncertainty is.

**Everything we don't know is the plan of the book.** Each chapter that follows ticks off one item on the second list.

## Why the check is written down before the calculation

This is step 5, and it's the least familiar. When the result is right in front of us, we badly want to believe it's correct if it 'looks right'. Everyone does this, even an experienced scientist.

So this is what we do:

1. **We write down the rules before calculating:** which images we take, how we check, and what result we'll count as a failure.
2. **We save that record, with its date, in the book's repository.** The commit date proves that the rules existed before the result.
3. If we do change a rule, we write down why and show the result under both rules.

**Any result is a result, even one we don't like. No adjusting it to fit.**

## Rules for choosing images

Questions Q1 and Q2 are written down. Now we need images: one from before the fire and one from after. Before we open the catalogue, let's write down the rules we'll use to choose them. If we look first and decide afterwards, our hand will reach for the 'nice' image all by itself.

## Why we need rules at all

We'll compare two images and count whatever has changed as burn scar. So anything that changed for a reason other than the fire becomes an error. And a lot can change between two images:

- clouds and their shadows;
- snow on the summits;
- the height of the sun and the shadows on the slopes;
- the angle at which the satellite views the slope;
- spring growth, which comes through with or without a fire.

**A good pair of images is two images that differ only because of the fire.** Each rule below removes one of these unwanted differences.

You'll know this from repeat surveys for deformation monitoring. To see whether a structure has moved, we measure it with the same instrument, from the same stations, in similar conditions. Otherwise the difference in readings shows a change in conditions, not movement.

## First: our area

We check the rules not on the whole scene but on our area: the burn scar plus a 1 km strip around it.

We need the strip because later we'll take unburnt areas next to the burn scar for comparison. They need a clear image too.

The cloud cover for the whole scene shown in the catalogue only tells us where to look. We make the decision on the basis of our area.

## The rules

1. **Processing level L2A.** This is a ready-made product in which the effect of the atmosphere has already been removed. We'll look at exactly what's been done to it in Chapter 5.
2. **The 'after' image is the first clear image after the fire is out.** Later on, the trace fades. There must be no smoke and no active flames in the image.
3. **The 'before' image is the nearest clear image before the fire started.** The closer the dates, the smaller the difference in sun and in spring growth.
   - good: up to 2 weeks between the images;
   - acceptable: up to 6 weeks;
   - more than 6 weeks: we take the nearest clear one, but record it as a weak point and test its effect in Chapter 7.
4. **No clouds, cloud shadows or haze over our area.** We check by eye in two visualisations, natural colour and SWIR, because in natural colour a shadow and a burn scar look alike.
5. **No snow on the area.** In February and March it can lie on summits above 1,000 metres.
6. **The same orbit, if possible.** The satellite passes over Asturias along different 'tracks', and from each one it views the slopes at its own angle. From the same track, the shadows and the lighting are the same. If we can't find a matching orbit, we record that.
7. **Nothing burned on the area before the fire.** Otherwise part of the 'before' image will already be burn scar.

**If no pair passes all the rules, we don't quietly relax them.** We take the best pair available, write down which rule it breaks, and test how much that affects the result.

## What we record for each image

For each image we choose, we keep a short record sheet:

- the date and time it was taken;
- the satellite: Sentinel-2A, 2B or 2C;
- the orbit number and the scene (tile) number;
- the cloud cover for the whole scene and the cloud cover over our area;
- the sun's elevation and azimuth;
- the processing version.

The record sheet is there for reproducibility. Anyone can use it to find exactly the same image. And we'll need the sun's elevation in Chapter 7, where we deal with the light on the slopes.

## Summary

**New terms**

- **A question a measurement can answer:** a question that makes clear what we measure, where, when and how precisely.
- **Criterion:** a rule written down in advance that we use to choose data or to decide whether a result has succeeded.
- **Reproducibility:** anyone else can repeat our calculation from our records and get the same result.
- **Study area:** the burn scar plus a strip around it, where the rules are checked.
- **Orbit:** the 'track' along which the satellite passes over the ground; from each one it views the ground at its own angle.
- **Tile:** one of the 110 by 110 km squares into which Sentinel-2 images are cut; each has its own number.
- **Image record sheet:** a record of all the details needed to find and check an image.

**Key points**

- The question and the rules first, then the calculation.
- A good question makes clear what, where, when, how precisely and in what units.
- We write down the check and the failure criterion before calculating, with a date.
- Fitting to someone else's figure isn't measurement.
- A good pair differs only because of the fire.
- We check for clear skies over our area, not by the cloud cover of the whole scene.
- 'Before' is as close to the fire as possible; 'after' is the first clear image after the fire.
- We don't hide a broken rule: we record it and test its effect.

## Questions for an engineer

1. We got 698 ha, almost the same as EFFIS. Does that mean our result is right?

:::{dropdown} Answer
No. Agreeing with someone else's figure proves nothing: EFFIS has no uncertainty either. A result is tested by a check written down in advance, for example with random points and in the field, not by how close it is to another estimate.
:::

2. Why does it matter that Q1 says 'on the first clear image after the fire'?

:::{dropdown} Answer
Because the trace of a fire fades over time. An image three months later will give a smaller area. Without a date, two people will get different figures, and both will be 'right'.
:::

3. Why did we decide not to count the unburnt islands inside the perimeter?

:::{dropdown} Answer
Because the question is how much vegetation burned, and the islands didn't burn. But we'll also record the area of the whole perimeter separately, so that we can make a fair comparison between our figure and the figures from services that measure by perimeter.
:::

4. There's a completely clear scene from 10 weeks before the fire, and an image from 5 days before the fire that's clear over our area but has clouds 50 km away. Which do we take?

:::{dropdown} Answer
The image from 5 days before. Clouds 50 km away don't affect our measurement, whereas 10 weeks means a noticeably lower sun and different vegetation, and that difference would end up counted as burn scar.
:::

5. Why do we check for clear skies in SWIR as well, and not just in natural colour?

:::{dropdown} Answer
Because in natural colour a cloud shadow looks like a burn scar, and light haze is barely visible. In SWIR a shadow is almost black and a burn scar is reddish-brown, so we can't mix them up.
:::

6. Why record the sun's elevation if we aren't using it yet?

:::{dropdown} Answer
We'll need it in Chapter 7 to estimate how much the difference in light between 'before' and 'after' changes the result. Writing it down now takes a second; looking it up later means extra work and a risk of error.
:::

## The open question

The rules are written down. But they're full of words we only roughly understand so far: bands, SWIR, orbit, why the satellite passes over at the same time of day. What does Sentinel-2 actually measure? That's the subject of Chapter 3.
