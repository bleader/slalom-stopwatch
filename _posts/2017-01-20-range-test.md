---
layout: post
title:  "First range test"
date:   2017-01-20 20:10:10 +0200
categories: website
comments: false
---
First time testing range to get an idea if long enough range can be achieved
with my ESP32 modules. We went to 40 cones around 6 feet spacing, so about 73m,
and it worked just fine.

### Setup

- 2 ESP32 devkits, plugged into 2 laptops
- one setup as an AP, with code ligthing an LED when there is a connected client
- one setup as a client, with LED ligthing up when connected to the AP.
- code si simple [arduino
  framework](https://github.com/espressif/arduino-esp32) based stuff, and there
  is no control of the mode the wifi is set at.

### Testing

We simply put one laptop with an esp (the AP one) at the beginning of the cone
line, and moved the client to the end of the cone line. The two devices kept
the connexion just fine.

Then I proceeded to go to the end of the street and it was still working, but
that was a quick test, and disconnection detection time could have created a
false impression. I'll need another test with better check, force disconnection
and ensure how far it can still reconnect.

### Conclusion

It apparently went up to 150m without a hitch, more testing will be required,
also it may be interesting to play with
[esp-idf](https://github.com/espressif/esp-idf) if we can set wifi to lower
speed and get better range.
