---
layout: post
title:  "More range test"
date:   2017-01-20 20:10:10 +0200
categories: website
comments: true
---
With almost the same setup as previous test, with more time, my father help and
phone communications to discuss about how it goes, I did some more tests.

### Setup

- 2 ESP32 devkits, one plugged on a laptop usb, and the other one on a usb
  battery
- one setup as an AP, with code ligthing an LED when there is a connected client
- one setup as a client, with LED ligthing up when connected to the AP.
- code si simple [arduino
  framework](https://github.com/espressif/arduino-esp32) based stuff, and there
  is no control of the mode the wifi is set at.

### Testing

As last test, we used one fixed device, and the other one moving. But this time
we went to an extremity of the street for the fixed one, to get us more room
for testing.

I went up to about 200m before the two devices lost signal, I managed to
reconnect and then go further, and lost the signal again at about 240m. That
time it didn't reconnect. Tring again and again to reconnect while coming back,
even at the 200m mark where it previously worked, there was no way to get the
signal back until I was at around 180m from the other device.

It is worth noting that this was in direct line of sight, but on busy and
touristic place, near the Versailles Castle, which means a lot of phones were
likely around and can add noise and make the range fluctuate quite a bit.

### Conclusion

I guess with playing with the modes and speed we can hope to go a little
further. tho, 180m should be sufficient for a 100 cones with 6 feet spacing,
but not for 7 feet.
