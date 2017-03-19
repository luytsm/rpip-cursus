---
title: "Lab 3: Alarmsysteem"
description: 
---
# Lab 3: Alarmsysteem

## Opdracht

We gaan een simpel alarmsysteem maken dat het opengaan van een deur detecteert
en deze actie logt.  Het opengaan van de deur kunnen  we detecteren met een IR
afstandssensor. Er zit geen ADC op de RPi maar de de sensor kan wel een logisch
hoog signaal geven wanneer er een voorwerp dicht bij staat. Het loggen van deze
informatie gebeurt door de timestamp van het opengaan van deur weg te schrjven
naar een file.

We kunnen het alarmsysteem aan en uitzetten met een drukknop. Als er een alarm
afgaat dan begint er een rood ledje te flikkeren. Het alarm kunnen we uitzetten
door 5 seconden op een knop te drukken. Eenmaal op de drukknop drukken doet
niks tijdens de alarmfase.

Daarna maken we een tool om de logs van het alarmsysteem op te kuisen. De tool
bevat 2 methodes:

1. Regel per regel:  
   We lezen de file in met alle timestamps en het programma toont lijn per lijn. Bij elke lijn word
   aan de user gevraagd of dat hij/zij deze lijn wilt verwijderen.

2. Range:  
   We lezen de file in met alle timestamps en het programma vraagt aan de
   gebruiker een start en stopdatum. Het programma filter verwijdert dan alle
   entries die tussen deze range ligt.


## Requirements
* Maak gebruik van een toplevel script environment
* Steek de main loop in een `try/except/finally` en vang de keyboardinterrupt op
* Voor de pushbutton maken we gebruik van `add_event_detect()`
* Het formaat voor het wegschrijven van timestamp is: 30-06-89 15:55:33 

## Extra informatie

### Time

**Voor het wegschrijven van een timestamp kan je als volgt doen:**

```
import time
time.strftime("%a, %d %b %Y %H:%M:%S)
'Thu, 28 Jun 2001 14:17:15'
```

[Meer info](https://docs.python.org/3.7/library/time.html?highlight=time#time.strftime)

**Voor het parsen van text naar een tijdsobject kan je het volgende gebruiken:**


```
import time
time.strptime("30 Nov 00", "%d %b %y")   
time.struct_time(tm_year=2000, tm_mon=11, tm_mday=30, tm_hour=0, tm_min=0,
                 tm_sec=0, tm_wday=3, tm_yday=335, tm_isdst=-1)
```

[Meer info](https://docs.python.org/3.7/library/time.html?highlight=time#time.strptime)

## File operaties

**File opendoen en wegschrijven:**

```
f = open(filename, mode)
f.write("Wat moet ik hier wegschrijven?")
f.close
```

**Modes**:
<table border="1" class="docutils">
<colgroup>
<col width="13%">
<col width="88%">
</colgroup>
<thead valign="bottom">
<tr class="row-odd"><th class="head">Character</th>
<th class="head">Meaning</th>
</tr>
</thead>
<tbody valign="top">
<tr class="row-even"><td><code class="docutils literal"><span class="pre">'r'</span></code></td>
<td>open for reading (default)</td>
</tr>
<tr class="row-odd"><td><code class="docutils literal"><span class="pre">'w'</span></code></td>
<td>open for writing, truncating the file first</td>
</tr>
<tr class="row-even"><td><code class="docutils literal"><span class="pre">'x'</span></code></td>
<td>open for exclusive creation, failing if the file already exists</td>
</tr>
<tr class="row-odd"><td><code class="docutils literal"><span class="pre">'a'</span></code></td>
<td>open for writing, appending to the end of the file if it exists</td>
</tr>
<tr class="row-even"><td><code class="docutils literal"><span class="pre">'b'</span></code></td>
<td>binary mode</td>
</tr>
<tr class="row-odd"><td><code class="docutils literal"><span class="pre">'t'</span></code></td>
<td>text mode (default)</td>
</tr>
<tr class="row-even"><td><code class="docutils literal"><span class="pre">'+'</span></code></td>
<td>open a disk file for updating (reading and writing)</td>
</tr>
</tbody>
</table>

**Alle lijnen inlezen van een file:**

```
f = open(logs, r)
lines = f.readlines()
f.close()

print type(lines)
#list

```

