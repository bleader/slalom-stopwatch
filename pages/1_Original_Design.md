---
layout: page
title: Original Design
permalink: /design/
comments: true
---

* content
{:toc}

Here I'll list the original ideas of the design, things will evolve on the real
thing depending how various tests goes.

# Requirements

This needs to be used for a skateboarding slalom stopwatch, so this means:
- a start trigger when riders goes by the first cone
- a stop trigger when riders goes by the last cone
- an accurate timing mechanism between the start and stop triggers
- should work for 40 cones with possible spacing of 5, 6 or 7 feet
- have a convenient way to check time after a run

That's the basic of any stopwatch that could be used for slalom skateboarding.

# Basic features

The minimum feature set that is mandatory for this project to make sense:

- Wireless
- Battery powered
- Small foot print for ease of transportation

# Additionnal features wishlist

This is the ideal feature list I wanted at first, note that I already know some
of these things won't be possible at the time I'm writing this, but I'll still
list them here.

- Rider detection
- Webserver on one of the devices so you can check your time, time history, etc
- Configurable spacing and number of cones to estimate average speed
- Speed at start and speed at stop measurement (note: impossible with
  ultrasonic sensors)
- Configurable trigger distance
- 2 lane racing with beep, remote controlled via wifi
- Cone spacing measurement helper


# Implementation idea

![design]({{site.baseurl}}/static/img/design.png)

## Parts and Features

So my thinking behind this would be to use two ESP32 devices:

### Host

- ultrasonic distance sensor for stop trigger.
- rider detection
- WiFi AP
- Webserver with:

  - configuration: number of cones, spacing
  - mode selection (maybe also available with button and LED ?)
  - Rider token registeration
  - time history, with average speed
  - allow to note number of pushed/hitted cones with a customisable penalty
- screen to display time and time record
- a way to upload times to an online service, with maybe some kind of ranking

### Client

- ultrasonic distance sensor for start trigger.
- rider detection
- send of trigger to Host as timing will be done there

#### Rider token

It should be a bluetooth low energy (BLE) beacon, advertising and power of
reception should be use to identify closer beacon and choose which rider
lilkely triggered the device.

## One racer scenario description

This describe how things should happen according to my current plan for one
racer going through the course.

- The rider gets started
- Rider goes by the first cone and the Client device, so ultrasonic sensors
  detects a range below its trigger
- *Client* device send a start signal to the *Host* via WiFi
- *Host* receive the signal and start a timer right away
- *Client* tries to detect the rider via BLE scanning

  - if a token is close enough, send its ID to *Host*
  - if no token is close enough to make sense, send a cancel to *Host*

- Rider goes through the course, and arrives to the end
- *Host* trigger see the riders passing by, and stops its timer
- *Host* then:

  - Update history with new time for the rider, and the average speed
  - display the time
  - make the new history available to the webserver

And that should be it, of course there will be a lot more to it with configuration
