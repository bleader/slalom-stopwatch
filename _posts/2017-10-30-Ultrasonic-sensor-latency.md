---
layout: post
title:  "Ultrasonic HC-SR04 latency"
date:   2017-10-30 22:29:09 +0200
categories: website
comments: false
---
So, I've postponed working on this project for a long while, but after setting
up the cabled timer with my friend the other day, I got some renewed interest
for this idea, and started working a bit on it.

### Latency issue

So I've realized only recently that, the measurement of ultrasonic sensors are
pretty *slow*. What I mean by that, is that the example code I found online and
used in my previous test, there was a 60ms delay between measurements, and in
case the sensor get stuck, you have to reset it, adding a 100ms delay.

From what I read you can reduce the delay between 2 measures to about 30ms, but
that can lead to more occurences of the device getting stuck...

I imagine you can guess that for a stopwatch, that is a real issue. Worst case
scenario being, you can end up with about 150ms between measurement. If that
happens at start and stop on a given run, the measurement can be off by 300ms,
which on a 10 to 15s run is pretty much awful...

### Other ways

I then searched for other sensors to use, but given I wanted to keep the
simplicity of the, one start, on stop, no cable, easy and fast to setup goal, I
didn't want things with reflectors or modules facing each other.

I found some infrared modules given for 30cm, so I thought that ought to be
enough, unfornately, the truth is that, this is the maximum theorical distance,
it depends of the material and color facing the sensor. Also, they tend to
actual get in detection if when you set them to the highest distance settings.
The best I could achieve was about 20cm with my and, and other materials I had
at hand maxed out at about 5cm... Which wouldn't do the trick.

I looked at laser sensors, but they are way more expensive, and not always
fitting. There's an obstacle detector, but its shortest detection is 80cm, so
way too far for how I intend this thing to work.

So after some time, I went fiddling again with the ultrasonic sensors, which I
really like because I would love to actually allow one of the modules to work
as a measurement tool to help place cones.

### Back to tweaking

So I started to fiddle around with the **pulseIn** timeout option of the
arduino framework, and ended up finding that using a 30000µs there, lead to
some measures being inaccurate, but the sensor never being stuck, without delay
between measurement.

As I'm using it as a trigger, accuracy of measures isn't an actual concern as
long as it doesn't:
1/ miss detection it should be doing
2/ doesn't get false positives

### Conclusion

My current batch of tests showed it seems to work as I expect it, so I'll keep
that for my first tests, and a normal usage if I make the builtin cone
placement helper, using the normal timeout to keep the accuracy.
