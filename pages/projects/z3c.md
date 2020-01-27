---
layout: page
title: Meraki Z3C
permalink: /projects/z3c/
---

![Meraki Z3C Router](/assets/images/z3c-mantle.png){:class="img-responsive"}

Meraki is a cloud networking company that develops routers, switches, APs and other devices that are designed to interface over a [cloud management system](https://meraki.cisco.com/form/demo).

My work at Meraki culminated in the platform bringup project for a new router with built-in LTE and WiFi capabilities, designed to be a teleworker gateway. I took existing hardware designs and a basic software stack provided by the JDM and brought up the Meraki's OS on this device. This included implementing hardware-assisted secureboot through the bootloader (U-boot), validation of peripherals (ethernet switch, PoE, LTE modem, WiFi), and integration into the Meraki backend systems (database migrations, device state query tools, RF regulation management).

The bringup work involved collaboration with not only several of the engineering, product management, and hardware teams at Meraki, but also with our cellular modem vendors, and JDM engineers as well. It was a truly eye-opening experience to see just how much talent and effort goes into launching a single product at a worldwide scale.

[Product page](https://meraki.cisco.com/products/appliances/z3c)
