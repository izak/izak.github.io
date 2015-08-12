---
layout: post
title: Uniontech MR16 downlight
---

This is a short review of a 5W 12V LED downlight, made by the South African
company called Uniontech.

## Priced well and reliable

I bought the first couple of lamps about three years ago for around R140 a
piece. The most recent ones were around R100 each. Of all the lamps I've
bought so far (around 24), only one has failed. It failed because one of the
three LEDs, configured in series, has failed.

![In pieces](/assets/uniontech-mr16-split.jpg)

## What's on the board

The driver board contains a full-bridge rectifier, a small inductor and a
PT4115 chip. This is a step-down LED driver that can operate from as much
as 30V at efficiencies above 90%.

![Driver front](/assets/uniontech-mr16-driver-front.jpg)

Don't be tempted to feed this directly from a 24V battery though: The smoothing
capacitor on the back is only rated for 16V. The full-bridge rectifier is also
of interest: The SS14 diode is a schottky diode.

![Driver back](/assets/uniontech-mr16-driver-back.jpg)

## Power factor

Rated at 5W, budget up to 20VA or so per lamp, especially when using an
inverter. Sadly I didn't adjust my vertical scale properly, so you cannot
really read peak current off this. I also swapped the second channel around
so it goes the wrong way, it's actually in phase.

![Power factor](/assets/uniontech-mr16-power-factor.jpg)

Overall I'm impressed with the quality and the design. This is a good South
African product I can recommend.
