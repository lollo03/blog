+++
title = 'My minirack!'
date = 2026-01-29T17:18:30+01:00
draft = false
+++

![Foto rack](/blog/minirack.jpeg)

Here it is: my desktop "mini-rack"! The idea was to create an all-in-one solution to solve my desk organization issues... all within arm's reach.

The rack was built using 20x20 aluminum extrusions and various 3D printed parts. Some were designed by me, while others were found online (list at the end of the post).

Top to bottom:

* 3U [TRMNL OG DIY KIT](https://www.seeedstudio.com/TRMNL-7-5-Inch-OG-DIY-Kit-p-6481.html) to display useful info (weather, sensor status, rack status, calendar)
* 1U "blank" panel: the router will go here (I still have to choose one; right now there's a MikroTik RouterBOARD just lying behind the desk)
* 1U RPi 5 (Home Assistant + DNS + API for TRMNL) + air quality sensor (TVOC, CO2, temp, humidity, and PM2.5) and presence detection (MMWave radar) (more info [here](https://www.lolloandr.com/blog/posts/19-minirack-sensor/) and [here](https://github.com/lollo03/esphome-minirack-sensor))
* 1U Optiplex 3040 Mini PC for testing (it runs Proxmox; I turn it on whenever I need to test something)

It's not my main homelab, but it gets the job done.

There are definitely some improvements to be made, like:

* Buying the router
* Adding a fan for the PM2.5 sensor (the readings are currently a bit off)
* Finding a power delivery solution for everything and adding a UPS
* Reprinting some of the 3D parts

3D Printed Parts List:

* [Spacer for T-NUTS](https://www.printables.com/model/1576296-1u-spacer-for-2020-profile-t-nut-insert-nut-95mm) (designed by me)
* [TRMNL Mount](https://www.printables.com/model/1575922-trmnl-og-diy-kit-10-rack-mount) (designed by me)
* [Air Quality Sensor](https://www.printables.com/model/1575922-trmnl-og-diy-kit-10-rack-mount) (designed by me)
* [RPi 5 Mount](https://www.printables.com/model/1576072-raspberry-pi-5-10-half-width-rackmount) (designed by me)
* [1U Blank](https://www.printables.com/model/1576191-10-1u-rack-blank-for-small-printers) (designed by me)
* [Dell OptiPlex Mount](https://www.printables.com/model/587391-dell-optiplex-3040m-3070-micro-10-rack-mount)
* [Handle](https://www.printables.com/model/870035-2020-handle)
* Feet (I can't find the model)

Everything was printed on a Bambu Lab A1 Mini.