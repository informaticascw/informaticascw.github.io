# Van toestandsdiagram naar code

## Inleiding
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4886279

Een toestandsdiagram geeft de werking van een systeem weer. Als je een toestandsdiagram maakt voordat je het systeem echt gaat bouwen of programmeren, kun je jezelf een hoop fouten besparen. Uit het toestandsdiagram kun je namelijk opmaken of het systeem werkt zoals het moet werken. Als je ziet dat er een fout in zit, pas je eerst het toestandsdiagram aan. Dat kost veel minder tijd dan het aanpassen van een programma. Begin daarom altijd eerst met het maken van een toestandsdiagram.

Als je denkt dat het toestandsdiagram goed is kun je het programma gaan maken. Gelukkig is het omzetten van een toestandsdiagram naar een programma redelijk eenvoudig, in dit hoofdstuk leggen we uit hoe dat moet.

Doe ter voorbereiding op het werken met logische operatoren en met if-then-else structuren de volgende unplugged activiteiten met de klas.

[Dobbelen met booleans](http://www.informaticaunplugged.nl/de-werkvormen/dobbelen-met-booleans/)

[Kiezen met kaarten](http://www.informaticaunplugged.nl/de-werkvormen/kiezen-met-kaarten/)

## Stappenplan
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4886280

Als je het toestandsdiagram eenmaal klaar hebt, dan is het maken van een programma dat kan worden uitgevoerd op bijvoorbeeld de Microbit, Arduino of Lego Mindstorms eenvoudig. We laten dat zien aan de hand van het volgende toestandsdiagram voor een systeem bestaande uit een lamp en een drukknop. Als de drukknop wordt ingedrukt (en weer losgelaten) gaat de lamp aan. Wordt de drukknop nogmaals ingedrukt (en weer losgelaten) gaat de lamp uit.

```{figure} 7-stappenplan-td1
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
1 - Lamp is uit
2 - Lamp is aan

 
```{code} pseudocode
EENMALIG BIJ OPSTARTEN:
    toestand wordt 1

HERHAAL:
    ALS (toestand is 1) DAN
        ALS (de drukknop wordt ingedrukt) DAN
             toestand wordt 2
             zet lamp aan
    ALS (toestand is 2) DAN
        ALS (de drukknop wordt ingedrukt) DAN
             toestand wordt 1
             zet lamp uit
```

Zie je de relatie tussen het toestandsdiagram en de pseudo-code?

Er is ook een andere manier, waarbij je start vanuit de gebeurtenissen.

```{code} pseudocode
EENMALIG BIJ OPSTARTEN:
    toestand wordt 1
    zet lamp aan

HERHAAL:
    ALS (de drukknop wordt ingedrukt) DAN
        ALS (toestand is 1) DAN
            toestand wordt 2
            zet lamp aan
         ANDERS ALS (toestand is gelijk aan 2) DAN
             toestand wordt 1   
             zet lamp uit
```
 

Beide manieren zijn toegestaan. Het hangt van de situatie en het specifieke platform dat je gebruikt (Micro:bit, Arduino, Lego Mindstormd) af wat het makkelijkste is. Soms gebruik je een mix van beide aanpakken.

## Pas op voor de valkuil
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4886281

Blijf goed opletten bij het omzetten van een toestandsdiagram naar een programma. Neem het volgende voorbeeld. Iemand heeft op basis van het eerdere toestandsdiagram het volgende programma gemaakt.
 
```{code} pseudocode
EENMALIG BIJ OPSTARTEN:
    toestand wordt 1
 
HERHAAL:
    ALS (de drukknop wordt ingedrukt) DAN
        ALS (toestand is 1) DAN
             toestand wordt 2
             zet lamp aan
        ALS (toestand is 2) DAN
             toestand wordt 1   
             zet lamp uit
```

```{exercise} Omzetten toestandsdiagram naar programma
:label: opdracht4omzetten
Waarom is dit niet een juiste vertaling van toestandsdiagram naar programma? 
```

```{solution} opdracht4omzetten
Ga na wat er gebeurt als het systeem in toestand 1 is en iemand drukt het knopje in (en laat het weer los). Het programma controleert of het systeem in toestand 1 is (dat is waar). Dan wordt de lamp aangezet en wordt de toestand 2. Dan controleert het programma of het systeem in toestand 2 is (en dat is dan waar!) en wordt de lamp uitgezet en wordt de toestand 1. De lamp zal dus heel even aan zijn en gelijk weer uit worden gezet.
```

## Tabel met alle toestandsovergangen
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4886282

Om er zeker van te zijn dat je hebt nagedacht over alle toestandsovergangen is het goed om een tabel maken met alle mogelijke combinaties. We geven een voorbeeld op basis van het volgende toestandsdiagram. Dit is een uitwerking van de hotelschakeling die je eerder hebt gezien. Het systeem bestaat uit twee schakelaars en een lamp. Met beide schakelaars moet de lamp aan en uit kunnen worden gezet.

SA staat voor Schakelaar A, SB voor Schakelaar B

- Toestand 1: SA = uit, SB = uit (de lamp is uit )
- Toestand 2: SA = aan, SB = uit (de lamp is uit )
- Toestand 3: SA = aan, SB = aan (de lamp is uit )
- Toestand 4: SA = uit, SB = aan(de lamp is uit )

Hieronder zie je een tabel met alle mogelijke toestandsovergangen. Voor elke combinatie moet er staan wat de nieuwe toestand wordt en welke actie wordt uitgevoerd. Als er een streepje staat (-), dan is er geen toestandsovergang en geen actie. Hieronder hebben we vast een begin gemaakt.

```{figure} 7-tabel-td1
```

```{table}
| Toestand | SA gaat aan | SA gaat uit | SB gaat aan | SB gaat uit |  
| --- | --- | --- | --- | --- | 
| 1	| 2 zet lamp aan | – | | |
| 2	| – | 1 zet lamp uit | | | 	 
| 3	| | | | | 	 	 	 
| 4 | | | | |	 
``` 	 	 
 
```{exercise} Opdracht: maak de tabel compleet
:label: opdracht4maaktabelcompleet
Maak de bovenstaande tabel compleet
```

```{solution} opdracht4maaktabelcompleet
:class: dropdown
| Toestand | SA gaat aan    | SA gaat uit    | SB gaat aan    | SB gaat uit.   |  
| ---      | ---            | ---            | ---            | ---            | 
| 1	       | 2 zet lamp aan | –              | 4 zet lamp aan | -              |
| 2.       | –              | 1 zet lamp uit | 3 zet lamp uit | -              | 	 
| 3	       | -              | 4 zet lamp aan | -              | 2 zet lamp aan | 	 	 	 
| 4        | 3 zet lamp uit | -              | -              | 1 zet lamp uit |	 
```

## Opdracht: maak programma
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4886290

Hieronder vind je een start voor het programma dat hoort bij het toestandsdiagram voor de hotelschakeling uit de vorige paragraaf.

```{code} pseudocode
EENMALIG BIJ OPSTARTEN:
    toestand wordt 1

HERHAAL:
    ALS (toestand is 1) DAN
        ALS (SA gaat aan) DAN
             toestand wordt 2
             zet lamp aan
        ANDERS ALS (SB gaat aan) DAN
             toestand wordt 4   
             zet lamp aan
    ALS (toestand is 2) DAN
         ...
```

```{exercise} Opdracht: maak de pseudocode
:label: opdracht4pseudocodehotelschakeling
Maak op basis van het toestandsdiagram en de bijbehorende tabel het programma in pseudocode af.
```
