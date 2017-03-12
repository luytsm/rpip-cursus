---
title: "Lab 2: Whats My Ip"
description: "Het posten van je IP adres op Slack"
---
# Lab 2: Whats My Ip
We hebben nu een draadloos IP maar we weten niet het welk. We kunnen ook niet
aan de DHCP records dus laten moet je Pi het maar vertellen. Dit gaan we doen
door een message op Slack te posten.

Slack heeft een Python Bibliotheek die we kunnen gebruiken.

# Deeltaken

## Installeren van de Slack Python Bibliotheek
Je installeert de Python bibliotheek met het volgend commando:  
`sudo pip3 install slackclient`

pip is de package manager voor python. pip is ook versie afhankelijk. Er is
zowel een versie voor Python 2.7 als voor Python 3. We moeten gebruik maken van
sudo omdat we de package globaal willen installeren.

```
# installeer een package voor python 2.7 op de Pi
sudo pip install <package>

# installeer een package voor python 3 op de Pi
sudo pip3 install <package>
```
## Aanmaken van een Slack token
Om acces te krijgen moeten we een token aanmaken zodat we via ons python
programma aanpassing kunnen maken op Slack. We kunnen zo een token aanmaken op
de volgende webpagina. Je mag kiezen welk Slack Team dat je wilt gebruiken.

<https://api.slack.com/custom-integrations/legacy-tokens>

## Posten van een message op slack

Met volgende code kunnen we een message posten op een kanaal van het team waar
voor we een token hebben gegenereerd.  

```python
from slackclient import SlackClient
token = "mytoken"
sc = SlackClient(token)
resp = sc.api_call(
        "chat.postMessage",
        channel="#2ea"
        text="Posting from Script"
)
```

## Ophalen van een IP

We kunnen ons IP ophalen met volgend stuk code

```
import socket
s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.connect(("gmail.com",80))
print(s.getsockname()[0])
s.close()
```

## Automatisch uitvoeren van script bij boot
Zie volgende link voor deze stap te voltooien  
<http://www.raspberrypi-spy.co.uk/2015/10/how-to-autorun-a-python-script-on-boot-using-systemd/>


# Opdracht

* Integreer de verschillende taken in een werkend geheel.
* Pas de oplossing aan zodat je:
  * Het IP alleen maar doorstuurt als het veranderd is
 

# Meer informatie:
* <https://bruceelgort.com/2016/06/19/using-the-slack-api-with-python-a-simple-example/>
* <https://api.slack.com/custom-integrations/legacy-tokens>
* <https://api.slack.com/methods/chat.postMessage>
* <http://slackapi.github.io/python-slackclient/>
* <http://stackoverflow.com/questions/166506/finding-local-ip-addresses-using-pythons-stdlib>
* <https://api.slack.com/methods>




