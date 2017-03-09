---
layout: post
title:  "BLE scanning"
date:   2017-03-04 21:01:01 +0200
categories: website
comments: false
---
It's been a while since I actually did anything on this project, but I decided
to get back to it, and started to try to find out example of scanning code, and
found the [gatt_client
example](https://github.com/espressif/esp-idf/tree/master/examples/bluetooth/gatt_client)
from the *esp-idf* code did so.

After some fiddling and tweaking to reduce the amount of code to only the needed
part, I managed to do a small code that enable scanning, and list devices by
their addresses, and store some RSSI values to be able to do an average over a
given period of time, to check which beacon is the closest.

**NOTE**: Why is there no code here?

I'm actually doing these post a lot later, the reason I'm doing it is to
actually clean my gh-pages branch from the github repository, to be able to push
some code over there. The fact is that the code is currently a real mess with
*#if 0* and *#if 1* everywhere, as I used the same project to test a lot of
various stuff. So I rather not share code that may would be snippets of this
project and may not actually work.
