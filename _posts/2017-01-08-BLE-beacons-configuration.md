---
layout: post
title:  "BLE beacons configuration"
date:   2017-01-08 14:01:01 +0200
categories: website
comments: false
---
I received the beacons a little while ago, but couldn't find a way to actually
configure them, because for our purpose I wish to have them set at lower power
but at 100ms interval for advertisement.

So after being defeated by most android apps I tried, I mailed the ebay seller
and asked for help, they pointed me out to the right app on the play store and
once entered the right password for reconfiguring them, I managed to change
name, power, and advertisement interval.

One of the beacon being credit card sized and not meant to be open, there is no
way to stop it, so I set it to longer interval when my tests are done to save
the battery a little.

Next step for the bluetooth part will be to have code to scan beacons.
Currently there is no way to do this in arduino framework, so I'll have to move
to esp-idf for this.
