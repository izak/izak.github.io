---
layout: post
title: Repairing the Microcare MPPT controller, 2 attempts
---

## Ordering electronics in small quantities is a pain

I order my electronics from [RS Components](http://za.rs-online.com/web/) for
no particular reason other than that in South Africa we are somewhat limited
for choice, and our state-owned mail-delivery service has become quite useless
as a timeous means of delivery. Though ordering from RS is really painless
and the prices are reasonable -- the cost of delivery really means you should
attempt to order larger quantities.

In addition, it's not like you can order just one of a particular component.
Not that I want to: I'm perfectly happy to order in packs of 10, but this is
where it gets interesting: ordering the smaller quantity sometimes means it
isn't in stock locally so it takes three days or more before you get it. All
of which is fine if you're just a hobbyist such as myself.

## Attempt 1

In any case, to make a long story short, my components arrived and I replaced
the shorted Zener diode.

Sadly it didn't help. I won't say this is unexpected. I always knew chances are
that the transformer is burnt beyond simply re-using it.

## Attempt 2

So I figured I'll rewind the transformer. If I carefully count the windings,
and since I had some enamelled copper wire left from a project many years ago,
I might as well try. So I unwound it and found the transformer to be a 1:2
ratio, 58 on the primary and 116 on the secondary.

Now that's interesting. I would have expected at least 1:4.

After rewinding the transformer, I decided to test it out of the circuit
in order to be safe. I programmed up an Arduino to generate a 40khz signal,
borrowed a MOSFET from an old Chinese Charge controller, and rigged it all up.

![Rewound transformer test](/assets/microcare-transformer-rewound.jpg)

It didn't work. In fact, the magic smoke came out of it again.

I think it is fair to say -- and I won't be too proud to admit -- that I am
no SMPS engineer. I actually have no idea what I'm doing here. At least I can
say I tried.

## Plans

The obvious solution is to source a ready-made isolated DC-DC supply. Such
devices exist for the precise purpose used here: to drive MOSFETS on the high
side. I've ordered one with the next (small) batch of components, which will
be delivered in three batches as some things are in stock, some comes from the
UK, and some are on backorder.
