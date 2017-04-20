---
title: "Lab 4: MQTT"
description: 
---
# Lab 4: MQTT

## Voorbereiding
Ga door de slides van les 3 en maak een werkende opstelling van de demo applicatie

### Todo 

* Installeren van:   

  * MQTT Lens
  * Mosquitto (+ Clients)
  * Paho Pyhton library

* Maken van de opstelling
* Runnen van de demo code
* **Werkende applicatie tonen aan de docent**

## Opdracht
**Voor de volgende opdracht werk je met 2 samen**

Je maakt 2 maal de opstelling die bestaat uit:

* Raspberry Pi
* 3 drukknoppen 
* 2 leds

Je schrijft nu een programma waarbij je de leds van je partner bedient met je
eigen drukknoppen. Je partner moet jou leds kunnen bedienen met zijn
drukknoppen.

Je hebt ook een master drukknop die alle ledjes uitschakelt.

Met de drukknoppen toggle je de state van de leds.

Hiervoor moet je MQTT gebruiken voor het opzetten van communicatie tussen de 2
verschillende Raspberry Pis. 

je maakt gebruik van volgende topic constructie
```
home/groundfloor/livingroom/lights/lightx
home/groundfloor/kitchen/lights/lightx
```


##Requirements

* Maak gebruik van een toplevel script environment
* Steek de main loop in een try/except/finally en vang de keyboardinterrupt op
* Gebruik de opgelegde topic constructie
* Maak een schema van de gebruikte opstelling
