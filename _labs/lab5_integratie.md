---
title: "Lab 5: Integratie"
description: "Integratie van alle componenten in een werkende applicatie" 
---
# Lab 5: Integratie

Met het volgende labo gaan we de vorige labos met elkaar geintregeren. We
brengen het alarm systeem online door gebruik te maken van MQTT. We maken van
dit programma een service zodat dit in de achtergrond kan draaien. 

Dit labo moet gebeuren in een groep van 2.

Op RPi draait een background service die het alarm constant uitleest, als het
alarm getriggerd is dan stuur het python script een bericht over MQTT. Voor het
alarm gebruiken we een ultrasone afstandsensor, als deze een afstand kleiner
dan 30 cm meet dan word het alarm getriggerd. Als er een alarm getriggerd is,
dan begint er een lichtje te flikkeren op deze RPi. Er is ook nog een andere
ledje dat de status van het alarm weergeeft. Als het alarm actief is dan staat
dit ledje aan, staat het uit dan staat het alarm af.

Op de andere RPi luistert er een background service constant naar het
specifieke topic waaarom het alarm getriggerd word. Als er een alarm getriggerd
word dan zal er ook op deze Pi een ledje beginnen flikkeren. Het status ledjes
is ook anwezig op deze Pi. We voorzien ook nog 3 drukknoppen. Deze hebben
respectievelijk de volgende functies: 

1. Togglen state van het alarm (aan/uit) 
2. Alarm als het getriggerd is (5 sec inhouden knop)
3. Afstand opvragen

Als het alarm getriggerd word sturen we ook een bericht naar slack. Deze
functionaliteit word geimplementeerd op de RPi met de drukknoppen. De alarmen
worden ook gelogd op deze RPi zoals in Labo 3 waarop we dan onze filter tools
kunnen loslaten. 

## Extra informatie

Omdat we onze service in de achtergrond laten draaien moeten we het ook kunnen
killen. Met `systemctl stop myservice` sturen we een `SIGTERM` signaal naar
onze applicatie. Dit kunnen we opvangen in onze python applicatie met volgende
code:

```
import signal

run = True

def handler_stop_signals(signum, frame):
    global run
    run = False

signal.signal(signal.SIGINT, handler_stop_signals)
signal.signal(signal.SIGTERM, handler_stop_signals)

while run:
    pass # do stuff including other IO stuff
```
[source](http://stackoverflow.com/a/41753517) 

Vergeet zeker niet een `gpio.cleanup()` te doen in je handler functie

## Requirements
* Maak de opdracht zoals beschreven
* Toon de functionaliteit aan de Docent
* Load de opdracht op naar Learning
