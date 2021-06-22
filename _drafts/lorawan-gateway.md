---
layout: post
title:  LoRaWAN-Gateway mit Raspberry Pi und iC880A
date:   2016-07-31
categories: rtk rtklib gps
permalink: /steigerung-gps-genauigkeit
---

Vor einiger Zeit hatte ich in einem [Golem-Beitrag](https://www.golem.de/news/iot-mit-lora-und-raspberry-pi-die-dna-des-internet-der-dinge-1812-137845.html) beschrieben, wie man mit einem Raspberry Pi, dem iC880A-SPI  Concentrator Board und der Software des [GitHub-Accounts von The Things Network Zurich](https://github.com/ttn-zh/ic880a-gateway/wiki) einen günstigen LoRaWAN-Gateway ins TheThingsNetwork bringen kann .

Auch wenn inzwischen fast drei Jahre vergangen sind, das Board und die Software sind nach wie vor aktuell. Allerdings wechselt TheThingsNetwork auf den Software Stack V3, so dass nach der erfolgreichen Installation der Software auf dem Pi nun eine neue Server-URL in /opt/ttn-gateway/bin/local_conf.json einzutragen ist:

    eu1.cloud.thethings.network

Danach legt man wie zuvor einen neuen Gateway im ThingsNetwork an. Die neue V3-Konsole sieht etwas anders aus
