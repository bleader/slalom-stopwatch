---
layout: post
title:  "OLED display"
date:   2017-03-06 19:09:09 +0200
categories: website
comments: false
---
### Why

I recently looked online for some more parts for this project, the main idea was
to get more *hc-sr04* ultrasonic sensors to be able to have 2 for each device
in case of dual lane racing. While going through ebay stores to see if there
were any other things that could come in handy, I found a little *SSD1306*
monocroche OLED display for less than 10€
[here](http://www.ebay.fr/itm/272479121829), so I thought I'd give it a shot for
such a low price. It actually is about the same price as the 7 segment display
with controllers I could find available around here, which I prefer as I had
some issues with non arriving packages from china sellers with small electronics
parts like that recently.

That was pretty much without looking at how I'll get it working, I only saw
there were quite some libs in platformio for these displays, but didn't actually
knew how I'll manage to get them working with *esp-idf*...

### How

Then once I got some motivation and wanted to get it working I looked online and
found [this video](https://www.youtube.com/watch?v=MipOGBStBbI) from [kolban's
channel](https://www.youtube.com/channel/UChKn_BlaVrMrhEquPNI6HuQ) which cover
using such a display with [u8g2](https://github.com/olikraus/u8g2) which
supports a lot of various display, and also is pretty much hardware agnostic,
you just have to to provide the Hardware Abstraction Layer, which kolban
provides in his
[esp32-snippets](https://github.com/nkolban/esp32-snippets/tree/master/hardware/displays/U8G2).

Unfortunately for me, that wasn't actually working, because my device is working
over *SPI* and the *SPI* init was actually broken in the HAL by a previous
adding *i²c* support. So after [adding back the missing
part](https://github.com/nkolban/esp32-snippets/commit/6caf622543d29e72b1bb6b74dffaabca712b32a3)
it worked like a charm with the code I was trying.

Before understanding that this was the issue I spent quite a lot of time trying
to test *i²c*, other GPIO pins for driving the *SPI*. I even built other
projects with arduino framework and other libs and was actually starting to
think the display wasn't actually working. I also tried connections with pull-up
resistors, even while from what I saw online it shouldn't apparently be
needed... Built an i2c-scanner sample to scan if the device was there.

To sum it up, it took be 2 full days on this, for something that could likely
have taken half an hour while taking my time!

### Finally

I managed to get it to work and tested how many lines of times should fit.
Given this one has a part on top that's yellow, and the rest cyan, I can get the
record in yellow on top, and the 3 last times recorded by the stopwatch, that
should be pretty much perfect for its intended use.

![oled]({{site.baseurl}}/static/img/oled.jpg)
