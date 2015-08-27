---
layout: post
title: Repairing the Microcare MPPT controller, viability test
---

## I still don't know why it blew up in the first place

As any doctor would tell you, it's important to find the cause rather than
just treating the symptoms. Now perhaps the cause really was the shorted Zener
diode, though it wasn't a poor quality component, and it's unlikely that we
managed to push 1W of power through there. I also don't think the problem
is downstream of the DC-DC converter, as the 78L15 chip is in perfect shape,
and this does not account for the blown Zener.

I'm therefore stuck with the theory that the transformer failed for some
reason. The only other long-shot possibility is that the frequency it operates
at changed.  Perhaps the old microcontroller -- which was replaced -- worked
differently.  It seems I will never know.

## Test-driving the repair plan

If the only problem is the blown DC-DC stage, I should be able to get it
working by temporarily driving it from an external power supply. So this
is what I did. Only problem was, the various 12V SLA batteries I have standing
around the house are all completely destroyed, so I had to resort to using a
vehicle battery. At least this meant it came with built-in loads: Vehicle
lights.

Here then, if you will excuse the horrible Wikus-van-der-Merwe South African
accent, a short video of my test.

<iframe width="640" height="360"
        src="https://www.youtube.com/embed/NzaMJKaBUdY" frameborder="0"
        allowfullscreen></iframe>

## Intelligence gathering

While I have all this rigged up, might as well take a look at the PWM signal
frequency. After all, some day I might want to put my own controller in there.
I also measured the quiescent current, and the current drawn by the MOSFET
driver. In hindsight, I should have measured the peak current with the scope.

![PWM waveform](/assets/microcare-pwm-waveform.jpg)

The quiescent current drawn in sleep mode is 50mA. Including the 5mA drawn by
the driver circuit, I expect around 55mA total quiescent current. The LCD
backlight is probably responsible for most of that. Not bad.

When it's actually charging, the driver circuit draws around 9mA. This is an
average value measured with a multimeter.

## Next steps

The last of my ordered parts arrived yesterday, specifically, a package with
one small component: A Murata CMR0515S3C. This is a little DC-DC converter
in a single package. It's overkill for what I need: It has both a positive and
negative 15V supply. The load regulation and ripple looks good enough that it
can simply replace the entire chain of components including the 78L15.
