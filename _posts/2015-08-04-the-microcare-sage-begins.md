---
layout: post
title: The Microcare saga begins
---

## It's a really nice controller

![Better days](/assets/working_microcare.jpg)

It has an easy to read LCD display, three-stage battery charging, and it's
fully configurable. It comes with breakers on the input and output connections
which saves you from having to add a separate breaker. Overall it could be
considered value for money.

## Memory error

Just under two years after I installed it, the controller showed a memory
error. This turned out to be a common problem, so common that it was documented
in the manual. It would have to be sent away for repairs.

The memory error is caused because the flash RAM on the PIC micro-controller is
worn out due to repeated writes. This problem has been fixed in newer versions
of the firmware.

Initially I wasn't too concerned about the error. The charge controller still
appeared to work fine. Over time I realised that the MPPT algorithm seems to
get stuck on the lower early morning power points, causing significant amounts
of power to be lost.

## Repair

Microcare offered to replace the PIC free of charge. I sent my unit by courier
and it was delivered over night. During the course of the next two weeks,
communication can be described as non-existent. I called them on a few
occasions and eventually had the unit shipped back two weeks later. If I had
picked up the phone earlier it might have taken less time -- it seems I had
unreasonable expectations of receiving a phone call or an email.

## It's even more broken after it was repaired

When I unpacked it, I thought it smelled a little strange. I dismissed the
thought, and reinstalled the unit. I turned on the battery breaker and it came
up in sleep mode, as expected. I turned on the panel breaker, it did an MPPT
sweep, and abruptly turned itself off.

Upon inspection I found a very hot mosfet inside, and a transformer that had
clearly been subjected to more heat than was healthy for it.

![Unhappy Transformer](/assets/unhappy_transformer.jpg)

## Replace or repair again?

At this point I fire off another email to Microcare HQ. It's met with deafening
silence as before (Edit: They have since replied, but since I've already
embarked on my own adventure, I have not). I've now lost trust in this unit, so
I go out and buy a new Victron Blue Solar 150/70. It costs almost double what
the Microcare unit costs, but this really is the best there is.

Not wanting to waste more money on couriers, I decide to take a stab at
figuring out what went wrong.

## The design is not bad

I'm not an expert when it comes to electronics, but the design seems good. Good
spec components, properly heatsinked. Better than the chinese designs I saw
on YouTube.

The construction is worrying though. An in-place fix was made to the driver
circuit, and the flux has not been cleaned off the board:

![In place fix](/assets/microcare-in-place-fix.jpg)

There is also a nut missing on the back of the control board, and later I find
the reason it is missing is because the spacer below it is also missing:

![Missing nut](/assets/microcare-missing-nut.jpg)

## What went wrong

Late night debugging on top of my chest freezer in the garage. It helps if you
have an oscilloscope.

![Debugging the MPPT](/assets/debugging-the-mppt.jpg)

This shows that there is a 40khz signal from the PIC driving the hot mosfet,
and that the same square wave exits the mosfet. This is fed into a transformer,
then into a full-bridge rectifier, with a capacitor and a Zener on the output.
That finally goes into a 78L15 regulator before disappearing into a ribbon
cable.

I learn later that the Zener is there to add a minimal load, since this
particular implementation of a flyback converter -- I'm not sure if it could be
considered flyback with the full bridge on the output -- has no feedback loop
and will show large open-circuit voltages.

This does not appear to be the main power-control circuit. I find another opto
gate-driver on the lower board (labelled 3120) that seems to do this. I suspect
the 15V isolated supply that's giving me all this trouble is there to drive the
main switching mosfet. This unit does it the right way: N-channel mosfet on the
high side.

At this point I still suspect something is wrong with that transformer. I
remove it from the circuit. Now the unit powers up, but obviously cannot work.

With the transformer out of the way, I get to test the diode bridge. This
appears shorted out. Bingo! I have a shorted Zener diode:

![Shorted Zener diode](/assets/microcare-boost-converter-diodes.jpg)

The diode shows a large italic F (Fairchild semiconductor) and the number
4750a. 1N4750a happens to be a 27V 1W Zener diode which fits in exactly
with my theory. I knew the Zener would have a voltage below 35V, because that
is the maximum input on the 78L15.

By my estimation, and extremely poor skill with KiCAD, this is roughly the layout:

![Estimated circuit](/assets/microcare-converter-circuit.png)

A replacement diode is currently on order.
