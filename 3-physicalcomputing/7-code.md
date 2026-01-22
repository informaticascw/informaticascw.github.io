# Van toestandsdiagram naar code

## Inleiding
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4886279

Een toestandsdiagram geeft de werking van een systeem weer. Als je een toestandsdiagram maakt voordat je het systeem echt gaat bouwen of programmeren, kun je jezelf een hoop fouten besparen. Uit het toestandsdiagram kun je namelijk opmaken of het systeem werkt zoals het moet werken. Als je ziet dat er een fout in zit, pas je eerst het toestandsdiagram aan. Dat kost veel minder tijd dan het aanpassen van een programma. Begin daarom altijd eerst met het maken van een toestandsdiagram.

Als je denkt dat het toestandsdiagram goed is kun je het programma gaan maken. Gelukkig is het omzetten van een toestandsdiagram naar een programma redelijk eenvoudig, in dit hoofdstuk leggen we uit hoe dat moet.

### Ondersteuning: klassikale unplugged opdrachten

Doe ter voorbereiding op het werken met logische operatoren en met if-then-else structuren de volgende unplugged activiteiten met de klas.

```{exercise} Dobbelen met booleans
:label: opdracht8-1dobbelen
De opdrachtbeschrijving voor **Dobbelen met booleans** staat op\
http://www.informaticaunplugged.nl/de-werkvormen/dobbelen-met-booleans/
```

```{exercise} Kiezen met kaarten
:label: opdracht8-2kaarten
De opdrachtbeschrijving voor **Kiezen met kaarten** staat op\
http://www.informaticaunplugged.nl/de-werkvormen/kiezen-met-kaarten/
```

## Van plaatje naar pseudocode
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4886280

Als je het toestandsdiagram eenmaal klaar hebt, dan is het maken van een programma dat kan worden uitgevoerd op de Microbit eenvoudig. We laten dat zien aan de hand van het volgende toestandsdiagram voor een systeem bestaande uit een lamp en een drukknop. Als de drukknop wordt ingedrukt (en weer losgelaten) gaat de lamp aan. Wordt de drukknop nogmaals ingedrukt (en weer losgelaten) gaat de lamp uit. Je hebt dit toestandsdiagram al gezien in het vorige hoofdstuk.
% TODO: verwijzing toevoegen

```{figure} 6-td-toggle.png
:label: 6-td-toggle
Toestandsdiagram van led en drukknop met toggle-functie
```

Om een toestandsdiagram om te zetten in een programma gebruik je ALS-DAN-constructies. De toestand sla je op in een variabele. Hieronder zie je een uitwerking in pseudo-code. Het bestaat uit twee delen:

```{code} pseudocode
EENMALIG BIJ OPSTARTEN
```
Dit deel wordt één keer uitgevoerd. Hierin kun je bijvoorbeeld de starttoestand aangeven.
 
```{code} pseudocode
HERHAAL:
```
Alles wat hier staat wordt steeds weer opnieuw uitgevoerd, zolang het systeem aan is.

Alle toestanden krijgen een nummer:
1 - Lamp is uit, knop is los
2 - Lamp is aan, knop is ingedrukt 
3 - Lamp is aan, knop is los
4 - Lamp is uit, knop is ingedrukt
 
```{code} pseudocode
EENMALIG BIJ OPSTARTEN:
    toestand wordt 1

HERHAAL:
    ALS (toestand is 1) DAN
        ALS (de drukknop is ingedrukt) DAN
             toestand wordt 2
             zet lamp aan
    ANDERS ALS (toestand is 2) DAN
        ALS (de drukknop is losgelaten) DAN
             toestand wordt 3
             lamp blijft aan
    ...
```

Zie je de relatie tussen het toestandsdiagram en de pseudo-code?


```{exercise} Opdracht: maak de pseudocode af
:label: opdracht4pseudo
Maak de bovenstaande pseuscode af. Gebruik het toestandsdiagram uit de vorige paragraaf.
```

````{solution} opdracht4pseudo
:class: dropdown
```{code} pseudocode
EENMALIG BIJ OPSTARTEN:
    toestand wordt 1

HERHAAL:
    ALS (toestand is 1) DAN
        ALS (de drukknop is ingedrukt) DAN
             toestand wordt 2
             zet lamp aan
    ANDERS ALS (toestand is 2) DAN
        ALS (de drukknop is losgelaten) DAN
             toestand wordt 3
             lamp blijft aan
    ANDERS ALS (toestand is 3) DAN
        ALS (de drukknop is ingedrukt) DAN
             toestand wordt 4
             zet lamp uit
    ANDERS ALS (toestand is 4) DAN
        ALS (de drukknop is losgelaten) DAN
             toestand wordt 1
             lamp blijft uit
```
````


```{attention} ALS ... ANDERS ALS is beter dan ALS ... ALS
Je ziet dat we in de pseudocode gebruik maken van `ANDERS ALS`. Je zou op de plaatsen waar `ANDERS ALS` staat ook alleen `ALS` kunnen gebruiken. 

Als je alleen `ALS` gebruikt, dan kan het bij sommige toetsdiagrammen gebeuren dat het systeem binnen één keer uitvoeren van de HERHAAL-code twee toestandsveranderingen doet. Dat is minder netjes en kan soms zelfs tot fouten leiden.

Gebruik daarom altijd `ANDERS ALS`.
```

````{attention} Verdieping: toestand-eerst of overgang-eerst

Er is ook een andere manier, waarbij je start vanuit de toestandsovergangen in plaats van de toestanden.

```{code} pseudocode
EENMALIG BIJ OPSTARTEN:
    toestand wordt 1

HERHAAL:
    ALS (de drukknop is ingedrukt) DAN
        ALS (toestand is 1) DAN
             toestand wordt 2
             zet lamp aan
        ANDERS ALS (toestand is 3) DAN
             toestand wordt 4
             zet lamp uit
    ANDERS ALS (de drukknop niet is ingedrukt) DAN
        ALS (toestand is 2) DAN
             toestand wordt 3
        ANDERS ALS (toestand is 4) DAN
             toestand wordt 1
```

Beide manieren werken. Het hangt van de situatie en het specifieke platform dat je gebruikt (Micro:bit, Arduino, Lego Mindstormd) af wat het makkelijkste is.

Gebruik in deze module altijd toestand-eerst, tenzij duidelijk anders is aangegeven.
````

````{attention} Verdieping: events
Bij sommige platformen, waaronder Micro:bit, kun je gebruik maken van events. Events zijn gebeurtenissen die gekoppeld kunnen worden aan een stukje code. Een voorbeeld van een event is het indrukken van een knop. De Micro:bit houdt op de achtergrond in de gaten of een event plaatsvindt. Zodra het event gebeurt, start de Micro:bit met uitvoeren van de gekoppelde code. In pseudocode ziet dat er zo uit:

```{code} pseudocode
EENMALIG BIJ OPSTARTEN:
    toestand wordt 1

BIJ (knop indrukken)
        ALS (toestand is 1) DAN
             toestand wordt 2
             zet lamp aan
        ANDERS ALS (toestand is 3) DAN
             toestand wordt 4
             zet lamp uit
```

Gebruik in deze module altijd HERHAAL en geen BIJ (events), tenzij duidelijk anders is aangegeven.
````

## Pseudocode controleren met een tabel
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4886282

Om er zeker van te zijn dat je hebt nagedacht over alle toestandsovergangen is het goed om een tabel maken met alle mogelijke combinaties. Neem het toetstandsdiagram uit @6-td-toggle van de vorige paragraaf.

- Toestand 1: schakelaar los, lamp uit
- Toestand 2: schakelaar ingedruk, lamp aan
- Toestand 3: schakelaar los, lamp aan
- Toestand 4: schakelaar ingedrukt, lamp uit

Hieronder zie je een tabel met alle mogelijke toestandsovergangen. Voor elke combinatie moet er staan wat de nieuwe toestand wordt en welke actie wordt uitgevoerd. Als er een streepje staat (-), dan is er geen toestandsovergang en geen actie. 

```{table}
| Toestand ↓ / Toestandsovergang → | knop los | knop ingedrukt |  
| --- | --- | --- | 
| 1	| - | 2: zet lamp aan |
| 2	| 3 | - |
| 3	| - | 4: zet lamp uit | 	 	 
| 4 | 1 | - |
```

Controleer of de pseudocode uit de vorige paragraaf past bij de tabel. Begin bij toestand 1, kijk of alle acties kloppen en kijk of alle overgangen kloppen. Ga daarna door met toestand 2 en zo verder tot je de hele tabel gehad hebt.

## Van pseudocode naar programma
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4886290

Bekijk je pseudocode uit @opdracht4pseudo nog eens en maak dan volgende opdracht. 

````{exercise} Opdracht: maak de code in Micro:bit
:label: opdracht4code
Maak de Micro:bit code op basis van de pseudocode.

Gebruik de volgende blokken. Je mag de blokken kopieren. Gebruik geen andere blokken. 

```{figure} 7-code-toggle-blokken.png
```

Test op je Micro:bit of je code goed werkt.
````

````{solution} opdracht4code
:class: dropdown
% broncode voor plaatje op: https://makecode.microbit.org/_g78PvVU6aeDx
```{figure} 7-code-toggle.png
```
````

