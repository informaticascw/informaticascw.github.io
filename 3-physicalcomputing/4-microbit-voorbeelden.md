# Sensoren en actuatoren (opdrachten)

## Voorbeeld: aansluiten led
% bron (didactiek aangepast): https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4889671

In deze paragraaf leer je hoe je een externe led kunt koppelen aan je Micro:bit. Een led is een lampje.

### Stap 1: Hoe werkt een led?
Bekijk eerst de onderstaande filmpje over de led.

```{iframe} https://www.youtube.com/embed/qqBmvHD5bCw
:width:100%
Behind the MakeCode Hardware - LEDs
```

### Stap 2: Led aansluiten
Maak de volgende opstelling.

```{figure} 4-leddim-aansluitschema.png
```

Je ziet, de led is aangesloten op pin P1. Die fungeert als een soort schakelaar waarmee je de led aan en uit kunt zetten.

Bij het aansluiten van led zijn twee dingen belangrijk:

1. Een led kan doorbranden als er teveel spanning op staat. Daarom moet je altijd een weerstand gebruiken. Voor de ledjes die bij de uitvinderskit zitten kun je een ledje gebruiken van 47 Ohm. Dit zijn de weerstanden met de kleuren: geel, paars, zwart, goud. Als je meer wilt weten over deze kleurcodering, zie bijvoorbeeld: https://www.weerstandcalculator.nl/
2. Een led is een diode. Dat betekent dat de stroom er maar van één kant door kan. Zorg dat je de platte zijde verbindt met de – (min, 0V) en de bolle zijde met de + (plus, 3V). Doe je het andersom, dan zal de led niet branden. Je kunt het ook zien aan de lengte van de twee pootjes van de led, het lange pootje is de +, het korte pootje de min.

```{exercise} Vraag over pinnen
:label: opdracht2stelling1

Geef aan of deze waar (vinkje) of niet-waar (geen vinkje) is.

- [ ] Computers werken met enen (1) en nullen (0). Je kunt voor de Micro:bit zeggen: als er 0 volt op een pin staat is dat gelijk aan een 0. Als er 3 volt op een pin staat is dat gelijk aan een 1.
```

```{solution} opdracht2stelling1
:class: dropdown
De stelling is waar.
```

```{exercise} Aansluiten led
:label: opdracht2-led
Kies de juiste woorden op de lege plekken.

De led is aangesloten op ______(1) en ______(2).
De led is een ______(3).
Daarom fungeert pin 1 als ______(4).               .

Je kunt kiezen uit de volgende woorden:
- 3V
- GND
- pin 0
- output-pin
- input-pin
- actuator
- sensor
- pin 1
```

```{solution} opdracht2-led
:class: dropdown
1. pin 1
2. 3V
3. actuator
4. output-pin

Als de spanning op pin 1 gelijk is aan 0V gaat er geen stroom door de led en blijft deze uit. Als de spanning op pin 1 gelijk wordt aan 3 volt, dan gaat er stroom lopen van pin 1 naar GND via de led en de weerstand. Dan gaat de led dus aan.
```

### Stap 3: Programma maken voor de led
Je kunt de led bijvoorbeeld steeds aan en uit zetten, met het onderstaande programma. 
% TODO: verwijzing toevoegen

```{figure} 4-led-code.png
:width: 300px
```

Let op: we gebruiken hier ‘pauzeer’ puur voor het testen van de afzonderlijke led. Later in de module leer je om een timer te gebruiken in plaats van 'pauzeer'.

Test het programma. Werkt het?


(physcomp-h4-2)=
## Voorbeeld: sterkte van een led aanpassen
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4889672

In deze paragraaf leer je hoe je de sterkte, oftewel de lichtintensiteit, van een led kunt aanpassen. Dat werkt op basis van Pulse Width Modulation (PWM), ook dat zullen we toelichten.

### Stap 1 Aansluiten van de led
Maak de onderstaande opstelling (die is gelijk aan Voorbeeld: aansluiten led). Je ziet:
% TODO: verwijzing naar voorbeeld toevoegen

- De led is aangesloten op pin 1.
- We gebruiken een weerstand van 47 Ohm om te voorkomen dat de led doorbrandt
- De platte kant van de led sluiten we aan op de min (0V). Je kunt ook kijken naar de pootjes van de led: het korte pootje sluiten we aan op de min (0V).

```{figure} 4-leddim-aansluitschema.png
```

```{exercise} Vraag over pinnen
:label: opdracht2stelling2

Geef aan of deze waar (vinkje) of niet-waar (geen vinkje) is.

- [ ] Een pin kan zowel digitale als analoge signalen verwerken.
```

```{solution} opdracht2stelling2
:class: dropdown
De stelling is waar.
```

### Stap 2 Programma maken
Test of de led werkt, bijvoorbeeld met onderstaande programma. Dit programma laat het lampje steeds met een andere sterkte branden. Daarbij is 1023 de maximale waarde.

```{figure} 4-leddim-code.png
:width: 300px
```

Let op: we gebruiken hier ‘pauzeer’ puur voor het testen. Later in de module leer je hoe je hiervoor een timer kunt gebruiken.
% TODO: verwijzing aanpassen

Test het programma. Werkt het?

### Stap 3: Hoe werkt PWM
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4870502

In het voorbeeld bij stap 1 zie je al een toepassing van Pulse With Modulation (PWM). De Micro:bit kan namelijk alleen maar een spanning van 3 volt of 0 volt op de pinnen zetten. Het is niet mogelijk om bijvoorbeeld 1,5 volt op de pin te zetten en daarmee de led minder fel te laten branden. De led is dus aan (3V) of uit (0V).

Toch is er een oplossing om de led minder fel te laten branden. De Micro:bit wisselt de spanning op de pin heel snel tussen 0V en 3V. Als de spanning voor 50% van de tijd 0 volt is, dan zal de led maar half zo sterk branden. Als de spanning 25% van de tijd 0 volt is, en dus 75% van de tijd 3 volt, dan zal de led op 75% sterkte branden. Je ziet niet dat de led steeds aan en uit gaat omdat het heel snel achter elkaar gaat. Dit noemen we Pulse Width Modulation.

De figuur hieronder laat drie situaties zien. Het gemiddelde geeft aan hoe sterk de led zal branden.

```{figure} 4-pwm.gif
```

Bron: [Wikipedia](https://nl.wikipedia.org/wiki/Pulsbreedtemodulatie).

Je hoeft maar weinig te doen om PWM te gebruiken. Je gebruikt ‘schrijf analoog pin … naar …’ en de Micro:bit handelt het verder af. Als je de led op 50% gebruik je bijvoorbeeld het onderstaande blokje. De waarde is 512, omdat dat de helft is van 1023, wat het maximum is.

```{figure} 4-pwm-code.png
:width: 300px
```

## Voorbeeld: aansluiten drukknop
% bron (didactiek aangepast): https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4889671
% bron (theorie aanraaksensoren): https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4855351

In deze paragraaf leer je hoe je een externe drukknop kunt koppelen aan je Micro:bit. Je leert ook het verschil tussen een drukknop en een schakelaar.

### Stap 1: Hoe werken een drukknoppen en schakelaars?

Bekijk eerst de onderstaande filmpje over de drukknop.

```{iframe} https://www.youtube.com/embed/t_Qujjd_38o
:width:100%
Behind the MakeCode Hardware - Buttons
```

In het filmje heb je kunnen zien dat er twee soorten drukknoppen zijn:

- Normally open (NO) - als je de drukknop niet indrukt kan er geen stroom lopen
- Normally closed (NC) - als je de drukknop niet indrukt kan er wel stroom lopen

```{figure} 4-deurbel.jpg
```

Een deurbel is een drukknop - normally open.

Naast de drukknop zijn er ook aanraaksensoren met een zogenaamde toggle-functie. De meeste lichtschakelaars in huis werken zo. Zo'n schakelaar staat aan (er kan stroom lopen) of uit (er kan geen stroom lopen). De schakelaar houdt dus de toestand vast ook als je de sensor niet meer aanraakt.

```{figure} 4-schakelaars.png
```

Bovenstaande schakelaars hebben allemaal een toggle-functie. Ook het rechter (rode) knopje heeft dat, deze drukknop werkt dus anders dan de drukknop uit het filmpje.

Het is echter mogelijk om een drukknop zonder toggle-functie, zoals bijvoorbeeld die in het filmpje, te laten werken als een schakelaar met toggle-functie door dat te programmeren. Bijvoorbeeld, je kunt een systeem maken met een drukknop (zonder toggle-functie) en een lamp. Als je de drukknop indrukt en weer loslaat gaat de lamp aan. Doe je dat nogmaals gaat de lamp weer uit. Het systeem onthoudt dus of de lamp aan of uit moet, ook al is de drukknop niet ingedrukt. Wat dat betreft is zo'n drukknop handiger dan een schakelaar met toggle-functie. Je kunt immers softwarematig, door het programma te veranderen, het gedrag van de drukknop en het systeem als geheel aanpassen.

Als je met drukknoppen werkt is het belangrijk om wat te weten over pull up en pull down weerstanden. We geven je hierbij één bron, hoewel er veel meer bronnen over te vinden zijn. 

Pull up en pull down: http://www.itela.nl/pull-up-en-pull-down-weerstand/

### Stap 2: Aansluiten van de drukknop
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4870491

Maak de volgende opstelling.

```{figure} 4-knop-aansluitschema.png
```

De bovenste rij op het breadboard in het plaatje hierboven is dus de min (0V), de rij daaronder is de plus (3V). Het knopje is dus verbonden met pin P0 en de min (0V).

Het drukknopje heeft vier pinnen, die twee aan twee zijn verbonden. Als je het knopje indrukt worden alle vier pinnen met elkaar verbonden. Zie het plaatje hieronder.

```{figure} 4-button.png
Schematische werking van een knop.
```

```{exercise} Vraag over pinnen
:label: opdracht2stelling3

Geef aan of deze waar (vinkje) of niet-waar (geen vinkje) is.

- [ ] Een pin op de Micro:bit kan zowel input als output zijn.
```

```{solution} opdracht2stelling3
:class: dropdown
De stelling is waar.
```

```{exercise} Aansluiten drukknop
:label: opdracht2-knop
Kies de juiste woorden op de lege plekken.

De drukknop is aangesloten op ______(1) en ______(2). 
De drukknop is een ______(3).
Daarom fungeert pin 0 als ______(4).               .

Je kunt kiezen uit de volgende woorden:
- 3V
- GND
- pin 0
- output-pin
- input-pin
- actuator
- sensor
- pin 1
```

```{solution} opdracht2-knop
:class: dropdown
1. pin 0
2. GND
3. sensor
4. input-pin

Als de drukknop niet wordt ingedrukt is de spanning op pin 0 dus 0 volt. Dat noemen we ook wel LOW. Als de drukknop wel wordt ingedrukt wordt de spanning op pin 1 dus 3 volt. Dat noemen we ook wel HIGH.
```

### Stap 3: Programma maken voor de drukknop
Je kunt nu op pin P0 meten of het knopje wordt ingedrukt. Belangrijk is om te testen of dit werkt. Dat kan bijvoorbeeld met het volgende programma. Probeer het uit en kijk of het knopje werkt. Als je de knop indrukt is (de knop is dan omlaag), dan toont de Micro:bit een hartje. Als de knop niet ingedrukt is (de knop is dan omhoog), dan toont de Micro:bit een vierkant. Het kan zijn dat het een fractie van een seconde duurt voordat de Micro:bit reageert op de drukknop, dat komt omdat het weergeven van een symbool soms even duurt.

```{figure} 4-knop-code-symbool.png
:width: 300px
```
% TODO: code aanpassen zonder event

Enkele opmerkingen voor de experts:

- De pinnen P0, P1, P2, maar ook P5 en P11 hebben een ingebouwde weerstand, die hoeft er dus niet bij worden geplaatst.
- De Micro:bit heeft een ingebouwde pull-up,\
zie ook: https://makecode.microbit.org/reference/pins/set-pull.

## Voorbeeld: aansluiten piezobuzzer
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-5383224

In deze paragraaf laten we zien hoe je de piezo-buzzer kunt aansluiten. Met een piezo-buzzer kun je een alarm laten klinken of een muziekje laten horen. 

### Stap 1: Hoe werkt een piezobuzzer?
Bekijk het volgende filmpje over het maken van geluid met de Micro:bit.

```{iframe} https://www.youtube.com/embed/cxfPNc4Wefo
:width:100%
```

### Stap 2: Piezobuzzer aansluiten

Voor het aansluiten van een een piezo-buzzer kun je het onderstaande schema gebruiken. Je ziet dat de piezo-buzzer is aangesloten op pin 2 (P2). 

```{figure} 4-buzzer-aansluitschema.png
```

### Stap 3: Programma maken voor piezobuzzer

Met onderstaande programma kun je testen of de piezo-buzzer werkt. Met het blokje 'zet analoge toonhoogte pin P2' laat je weten dat de piezo-buzzer op pin 2 (P2) is aangesloten.

```{figure} 4-buzzer-code1a.png
:width: 300px
```

Als het goed is hoor je een hoge toon bij het starten van het programma. De piezo-buzzer blijft nu de hele tijd aan. Om de piezo-buzzer uit te zetten kun je het volgende blokje gebruiken.

```{figure} 4-buzzer-code1b.png
:width: 300px
```

## Verdieping: Ultrasoon sensor
% TODO: meer sensoren en actuatoren (voor snelle werkers)
Hier komt ooit iets, nu mag je het overslaan.
