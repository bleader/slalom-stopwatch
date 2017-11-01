---
layout: post
title:  "WiFi and HTTP on ESP32 latency"
date:   2017-11-01 14:48:09 +0200
categories: website
comments: false
---
After I started getting worried about the latency of the trigger, I got
concerned about the possible latency issues of the networking system.

Wireless is known to be pretty unreliable, slow, and prone to some odd latency
peaks. In addition, my goal was to use the webserver I intend to make so we can
watch the history on times as the mean to start/stop the timer via an API,
given the ESP32 are low power devices, I started to wonder how slow this would
be.

So I started to write the basic code common for the **start** and **stop**
branches. Along the way, I got a bit carried away, and started make some debug
helpers.

### Debug stuff

I started making some blinker code with error codes so I can add them, and have
a blinking led to know what's happening. It may no be that useful as long as
I'm in front of my computer with a serial monitor at hand, but as soon as we'll
get a real working device and want to test it in real conditions, it may become
handy to have something to help out debugging.

Then I added some printing debug macro allowing debug prints to show timestamp,
function and line, and being disabled when building without debug.

That done, I went back to the wifi stuff.

### WiFi

So the goal was to do 2 codes:

- stop branch:
  - WiFi AP
  - Webserver on 80, answering simple short fixed page
- Client
  - WiFi Client
  - http client making a request on /
  - timing http connexion
  - timing request
  - min / max / average total processing time of the http request

That done, I started to measure the latency

### Latency measurement

Of course, I first simply tried the ideal condition, both devices are nearby on
my desk powered by USB.

Note that there are various WiFi access points around, here we have the ps4,
     our 2 phones, a chromecast and a printer on it, but without real activity
     on any of these.

Also in the 2.4GHz band, I do have bluetooth enabled on my phone, and one
iBeacon advertising at about 30cm from where the 2 esp32 are standing.

In this condition, after a pretty long run I got:

```
connect/req/total: 4 / 0 / 4 min/max/avg 4 / 65 / 4)
```

From what I saw, I had one 35ms, one 49, and one 65, the rest of the
measurements are between 4 and 7ms. That's not ideal as there is indeed some
jitter from time to time, but it is pretty uncommon (that was over 2000
measurements).

Now, the next step is to see if that increase with distance, but I didn't
receive my 18650 *power bank* cases, that I'll use to power the devices, and
allow easy recharging, so I hooked up one of the ESP32 to a phone charger, and
the second one to my laptop, and to wander around in the courtyard.

As I moved around, the measures jittered around, but at every stop I made, the
measures were going back to the same 4ms.

The further I was able to go in plain sight was about 30m, and it was still
stable. I then hoped a bit further and got surrounded by concrete, and there
the things started to be a lot more funky, with timing jumping around quite a
bit, from 4ms up to 5s.

I need to go and test this at my usual spot, but I'll need someone to come with
me to avoid letting it sits alone in the middle of the path. Given the range
tests I did, I'm pretty confident that it should work as it did at 25m, so with
a pretty low delay. We'll see.
