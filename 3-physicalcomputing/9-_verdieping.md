(physcomp-h9)=
# Verdieping: Timers

## Toestandsdiagram met timer
% bron: https://maken.wikiwijs.nl/135424/Cyclus_2#!page-4903449

Uit het voorbeeld met de PIR-sensor blijkt dat er een soort klokje in de sensor zit verwerkt. De sensor blijft een tijdje HIGH als output geven, ook al loopt er niemand meer voorbij. Je kunt echter ook zelf zo'n klokje programmeren, dat noemen we een timer. In dit hoofdstuk leer je om zelf een timer te gebruiken.

Een timer is een soort kookwekker. Je kunt de wekker instellen zodat deze over een bepaalde tijd, bijvoorbeeld 5 minuten, afloopt en dan een bel of alarm laat horen. Zo is het ook met een timer, alleen gaat het meestal niet om minuten, maar om seconden of zelfs miliseconden.

Hoe kun je een timer in een toestandsdiagram gebruiken? Daarvoor heb je een actie en een gebeurtenis nodig. Dit is de actie die je kunt gebruiken voor een timer:
- start timer / reset timer

Als je het vergelijkt met een kookwekker: stel de wekker in, bijvoorbeeld op 10 seconden van nu. Resetten betekent dat je de timer weer terugzet naar de oorspronkelijke tijd nog voordat de timer is afgelopen. Het resetten van de timer is eigenlijk hetzelfde als het starten van de timer, daarom hebben we ze bij elkaar gezet.

Een gebeurtenis die hoort bij de timer is:
- timer loopt af

Als je het vergelijkt met een kookwekker: de kookwekker laat een bel of alarm horen.

Hieronder vind je een voorbeeld voor een systeem met een lantaarnpaal. De lantaarnpaal gaat aan zodra er beweging is gedetecteerd. De lantaarnpaal gaat weer uit als er een bepaalde tijd geen beweging is gedetecteerd. Er zijn twee toestanden:
- Toestand 1: lamp is uit
- Toestand 2: lamp is aan



```{figure} 9-timer-td.png
Toestandsdiagram met timer
```

```{attention} Verschil tussen timer en pauze

Los van deze toepassing met de lantaarnpaal is het belangrijk dat je timers leert gebruiken. Het is belangrijk om het verschil tussen een timer en een pauze te begrijpen. Een pauze bij de lantaarnpaal zou als volgt werken. Nadat een beweging is gedetecteerd zet het systeem de lamp aan. Daarna komt een pauze van bijvoorbeeld 10 seconden. In die 10 seconden doet het systeem echter helemaal niets en kan het dus ook niet reageren op input vanuit de omgeving. Bij een lantaarnpaal is dat misschien niet zo erg, maar stel je hebt een zelfrijdende auto. Die zou tijdens de pauze nergens op reageren, dus ook niet op andere sensoren die aangeven dat er een andere auto aankomt. Levensgevaarlijk dus.

Bij een pauze reageert het systeem nergens meer op. Bij een timer is dat anders, die werkt als een kookwekker. Het systeem gaat gewoon door terwijl de seconden op de kookwekker wegtikken. Op het moment dat de kookwekker afgaat, kan het systeem actie ondernemen.
```

## Micro:bit code met timer
% bron: https://maken.wikiwijs.nl/135430/Cyclus_2___Micro_bit#!page-4972766

In dit deel laten we zien hoe je een timer kunt programmeren voor de Micro:bit en welke blokken je daarvoor nodig hebt. We laten de volgende onderdelen zien:
- de timer starten
- de timer loopt af
- de timer resetten
- de timer uitzetten

**De timer starten**
Voor het coderen van een timer heb je een variable nodig, we noemen deze variabele: `timerEindtijd`.
```{figure} 9-timer-code1.png
:width: 100px
```

Het starten van de timer doe je als volgt.
```{figure} 9-timer-code2.png
:width: 300px
```

De looptijd (ms) geeft aan hoe lang de Micro:bit al aan staat, in miliseconden. Daar tel je 5000 miliseconden (= 5 seconden) bij op. De timer loopt dus over 5 seconden af.

**De timer loopt af**

Om na te gaan of de timer afloopt gebruik je het volgende:
```{figure} 9-timer-code3.png
:width: 300px
```

Je controleert dus op de looptijd van de Micro:bit inmiddels groter of gelijk is aan de eindtijd van de timer. Als dat zo is, zijn de 5 seconden verstreken en loopt de timer dus af.

Een voorbeeld:

Je start de timer bij de looptijd van 12.000 milliseconden (dat is 12 seconden). De timerEindtijd wordt dan 12.000 + 5.000 = 17.000 milliseconden. Bij een looptijd van 12.500 milliseconden gaat de timer niet af, want de volgende uitdrukking is dan NIET WAAR:

    12.500 >= 17.000

Een paar seconden later is de looptijd bijvoorbeeld 17.400 milliseconden. De timer loopt dan wel af, want de volgende uitdrukking is dan WAAR:

    17.400 >= 17.000

**De timer resetten of herstarten**

Het resetten of herstarten van een timer is hetzelfde als het starten van de timer.

**De timer uitzetten**

Het uitzetten van een timer kan niet en hoeft ook niet. Als in een bepaalde toestand binnen het toestandsdiagram de timer niet belangrijk is, wordt simpelweg niet gecontroleerd of de timer afloopt. Eigenlijk is de vergelijking met de kookwekker in die zin niet helemaal goed. Een kookwekker geeft namelijk een alarm (hard piepen bijvoorbeeld) waardoor jij weet dat het tijd is om de eieren uit de pan te halen. Als je niet wilt dat het alarm afgaat moet je de kookwekker eerder uitzetten.

Bij een timer werkt dat iets anders. Het programma controleert steeds of de tijd al is verstreken. En als de timer niet meer nodig is, controleer het programma niet meer of de tijd al is verstreken.

```{exercise} Vraag timer
:label:opdracht9-timer-1
Waarom staat er >= en niet = bij het controleren of de timer afloopt?
```
```{solution} opdracht9-timer-1
:class: dropdown
De looptijd wordt bijgehouden in milliseconden. Het uitvoeren van de blokjes kost veel meer tijd dan 1 milliseconde, vaak zelfs meer dan 100 milliseconden. De kans is dus groot dat de looptijd niet precies gelijk is aan de eindtijd van de timer. Dus moet je ook controleren of de looptijd groter is dan de eindtijd, vandaar >= (groter of gelijk aan) en niet = (gelijk aan).
```

## Opdracht: knipperend lampje
% bron: https://maken.wikiwijs.nl/135424/Cyclus_2#!page-4904947

```{exercise} Toestandsdiagram voor een knipperend lampje
:label: opdracht9-timera

Maak een toestandsdiagram voor een lampje dat knippert. Maak gebruik van een timer.

Als gebeurtenis gebruik je:
- timer loopt af

De acties die je kunt gebruiken zijn:

start timer / reset timer
- zet lampje aan
- zet lampje uit
```

```{exercise} Code voor een knipperend lampje
:label: opdracht9-timerb

Maak op je Micro:bit code voor een lampje dat knippert. Gebruik het toestandsdiagram uit de vorige opgaven. Gebruik van een timer, het blok `pauzeer` mag je niet gebruiken.
```
 
```{exercise} Toestandsdiagram voor twee knipperende lampjes
:label: opdracht9-timerc

Maak een toestandsdiagram voor een systeem met twee knipperende lampjes. Zorg dat de lampjes knipperen met verschillende tussenpozen. (Bijvoorbeeld: het eerste lampje knippert elke 1,3 seconde: 1,3 seconde aan, 1,3 seconde uit. Het tweede lampje knippert om de 1,7 seconde: 1,7 seconde aan, 1,7 seconde uit.)

Bedenk zelf welke toestandsovergangen je hebt en welke acties. Je zult twee timers moeten gebruiken (bijvoorbeeld timer1 en timer2).

Hint: als je uitgaat van de twee lampjes die allebei aan en uit kunnen zijn, hoeveel toestanden heb je dan nodig voor alle mogelijke combinaties?
```

```{exercise} Code twee knipperende lampjes
:label: opdracht9-timerd

Maak op je Micro:bit code voor twee knipperende lampjes. Elk lampje knippert op zijn eigen snelheid. Gebruik het toestandsdiagram uit de vorige opgaven. Gebruik van een timer, het blok `pauzeer` mag je niet gebruiken.
```

## Opdracht: dodemansknop
% bron: https://maken.wikiwijs.nl/135424/Cyclus_2#!page-5382606

```{exercise} Dodemansknop toestandsdiagram
:label: opdracht9-dodea

Een dodemansknop zit in de bestuurderscabine van een trein (zeg maar de cockpit). Om de zoveel tijd gaat er een lamp branden. De machinist moet daar op reageren door op een knop te drukken. De lamp gaat dan uit. Daarmee laat de machinist merken dat hij/zij nog alert is. Als de machinist niet binnen zoveel seconden reageert, zal de trein afremmen en tot stilstand komen.

Maak een toestandsdiagram voor een prototype van een dodemansknop. Om de 10 seconden gaat er een lamp branden. De treinmachinist moet dan binnen 5 seconden op een knop drukken, de lamp gaat dan uit. Als hij/zij dat niet doet, gaat een alarm (bijvoorbeeld een zoemer of een lamp aan). Zodra de knop weer wordt ingedrukt gaat het alarm uit.
```

```{exercise} Dodemansknop code
:label: opdracht9-dodeb

IMaak op basis van het toestandsdiagram dat je voor deze opdracht hebt gemaakt een prototype op de Micro:bit. Bepaal zelf hoe je de knop, lamp en het alarm nabootst.
```
