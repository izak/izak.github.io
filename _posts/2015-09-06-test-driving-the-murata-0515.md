---
layout: post
title: Test driving the Murata 0515S3C DC/DC converter
---

The Murata 0515S3C is a small 0.75W 5V to 15V DC-DC converter. It's an
isolated converter, which means the output is in no way connected to the
input. This makes it ideal for driving an N-channel MOSFET on the high side.
Here it's already mounted on a small bit of strip board.

![Murata 0515s3c](/assets/murata_05015_plan.jpg)

The idea is to mount this to the original board in the charge controller, in
place of the DC-DC converter. To that end, I cleaned up the old converter. I
decided to leave the driving MOSFET in place, simply because it's attached to
the board and a little hard to remove cleanly.

![Getting ready](/assets/microcare-stripped-dc-dc-converter.jpg)

But first, I grabbed the nearest 5V supply I had, which turned out to be an old
Arduino Duemilanove, and took a few measurements. The 0515S3C, when left open
circuit, puts out about 19.2V. When you load it down with a 5mA load, it comes
down to 15.3V. According to the data sheet, this is the minimum load you need
if you want the voltage to be within spec.

A quick test with the oscilloscope indicates a 60mV ripple peak to peak with
the 5mA load and no smoothing capacitor. The original charge controller has
a 10uF on the output side, which I will keep. Once again the data sheet says
10uF is the maximum recommended value.

Finally, here it is installed. It's wired directly into the holes of the old
converter, with the output 0V and 15V lines going into the pins formerly
occupied by the 78L05. The only problem was that there is no easy place to
source ground on the input side. I eventually settled for sourcing this from
the source pin of the MOSFET.

![Installed](/assets/murata_0515_in_microcare.jpg)

I haven't had time to test it yet, and to really test it, I really should feed
it with a bit more power than the small battery charger I was using. This means
that the next order of business is to build something more suitable to that
purpose. I could test it with the small kit first, but I won't feel comfortable
declaring this fixed until I put some decent power through it.
