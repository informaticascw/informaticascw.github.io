# Sensoren en actuatoren (opdrachten)

## LED
Zie Drukknop

## Voorbeeld: aansluiten LED en drukknop

### Inleiding
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4889671

In deze paragraaf laten we zien hoe je een externe led en externe drukknop kunt koppelen aan de Micro:bit. We volgen deze stappen:

1. Aansluiten van de drukknop en vervolgens testen daarvan
2. Aansluiten van de LED en vervolgens testen daarvan
3. Een programma maken waarmee je de LED aan en uit kunt zetten met de drukknop.

Bekijk eerst de onderstaande filmpjes over de drukknop en de LED.

```{iframe} https://www.youtube.com/embed/t_Qujjd_38o
:width:100%
Behind the MakeCode Hardware - Buttons
```

```{iframe} https://www.youtube.com/embed/qqBmvHD5bCw
:width:100%
Behind the MakeCode Hardware - LEDs
```
### Stap 1: Aansluiten van de drukknop
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4870491

Maak de volgende opstelling.

```{figure} 4-knop-aansluitschema.png
```

De bovenste rij op het breadboard in het plaatje hierboven is dus de min (0V), de rij daaronder is de plus (3V). Het knopje is dus verbonden met pin P0 en de min (0V).

Het drukknopje heeft vier pinnen, die twee aan twee zijn verbonden. Als je het knopje indrukt worden alle vier pinnen met elkaar verbonden. Zie: http://www.teachwithict.com/uploads/5/5/8/2/5582303/published/button-fig-1.png?1531054399.

Je kunt nu op pin P0 meten of het knopje wordt ingedrukt. Belangrijk is om eerst te testen of dit werkt. Dat kan bijvoorbeeld met het volgende programma. Probeer het uit en kijk of het knopje werkt. Als je het knopje indrukt moet er een hartje verschijnen op de Micro:bit.

```{figure} 4-knop-code.png
:width: 300px
```

Enkele opmerkingen voor de experts:

- De pinnen P0, P1, P2, maar ook P5 en P11 hebben een ingebouwde weerstand, die hoeft er dus niet bij worden geplaatst.
- De Micro:bit heeft een ingebouwde pull-up, zie ook: https://makecode.microbit.org/reference/pins/set-pull.

### Stap 2: Aansluiten van de LED
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4870492

Nu je weet dat het drukknopje werkt kun je het ledje gaan aansluiten. Daarbij zijn twee dingen belangrijk:

Een led kan doorbranden als er teveel spanning op staat. Daarom moet je altijd een weerstand gebruiken. Voor de ledjes die bij de uitvinderskit zitten kun je een ledje gebruiken van 47 Ohm. Dit zijn de weerstanden met de kleuren: geel, paars, zwart, goud. Als je meer wilt weten over deze kleurcodering, zie bijvoorbeeld: https://www.weerstandcalculator.nl/
Een led is een diode. Dat betekent dat de stroom er maar van één kant door kan. Zorg dat je de platte zijde verbindt met de – (min, 0V) en de bolle zijde met de + (plus, 3V). Doe je het andersom, dan zal de led niet branden. Je kunt het ook zien aan de lengte van de twee pootjes van de led, het lange pootje is de +, het korte pootje de min.
Breid het systeem uit met een led zoals in het onderstaande schema. Je ziet, de led is aangesloten op pin P1. Die fungeert als een soort schakelaar waarmee je de led aan en uit kunt zetten.

```{figure} 4-led-aansluitschema.png
```

Nu moet je eerst de led testen. Je kunt de led bijvoorbeeld steeds aan en uit zetten, met het onderstaande programma. Let op: we gebruiken hier ‘pauzeer’ puur voor het testen van de afzonderlijke LED. In de module leer je om een timer te gebruiken in plaats van 'pauzeer', zie cyclus 2.

```{figure} 4-led-code.png
:width: 300px
```

```{exercise} Aansluiten drukknop en led
:label: opdracht2-ledknop
Kies de juiste woorden op de lege plekken.

De drukknop is aangesloten op ______(1) en ______(2). 
De led is aangesloten op ______(3) en ______(4).
De drukknop is een ______(5) en de led is een ______(6).
Daarom fungeert pin 0 als ______(7) en pin 1 als ______(8).               .

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

```{solution} opdracht2-ledknop
:class: dropdown
1. pin 0
2. GND
3. pin 1
4. 3V
5. sensor
6. actuator
7. output-pin
8. input-pin

Als de drukknop niet wordt ingedrukt is de spanning op pin 0 dus 0 volt. Dat noemen we ook wel LOW. Als de drukknop wel wordt ingedrukt wordt de spanning op pin 1 dus 3 volt. Dat noemen we ook wel HIGH.
Als de spanning op pin 1 gelijk is aan 0V gaat er geen stroom door de led en blijft deze uit. Als de spanning op pin 1 gelijk wordt aan 3 volt, dan gaat er stroom lopen van pin 1 naar GND via de led en de weerstand. Dan gaat de led dus aan.
```

### Stap 3: Bedien de LED met de drukknop
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4870493

De volgende stap is om de twee onderdelen (drukknop en led) te combineren: als het knopje wordt ingedrukt (en weer wordt losgelaten) gaat de led aan. Wordt het knopje nogmaals ingedrukt, dan gaat de led weer uit. In deze module werken we altijd met een toestandsdiagram, dus ook nu. Je kunt bijvoorbeeld het volgende toestandsdiagram gebruiken.

```{figure} 4-knopled-toestand.png
```

Toestand 1: de lamp is uit

Toestand 2: de lamp is aan

Het programma ziet er dan als volgt uit:

```{figure} 4-knopled-code.png
:width: 400px
```

Werkt het?

```{exercise} Vraag over pinnen
:label: opdracht2pinnen

Zet een vinkje bij de stelling(en) die waar zijn.

- [ ] Een pin op de Micro:bit kan zowel input als output zijn.
- [ ] Een pin kan zowel digitale als analoge signalen verwerken.
- [ ] Computers werken met enen (1) en nullen (0). Je kunt voor de Micro:bit zeggen: als er 0 volt op een pin staat is dat gelijk aan een 0. Als er 3 volt op een pin staat is dat gelijk aan een 1.
```

```{solution} opdracht2pinnen
:class: dropdown
Alle stellingen zijn waar.
```

## Voorbeeld: sterkte van een LED aanpassen

### Inleiding
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4889672
In deze paragraaf leer je hoe je de sterkte, oftewel de lichtintensiteit, van een led kunt aanpassen. Het doel is om de lichtintensiteit van een led aan te passen met behulp van de A-knop en de B-knop. Als de A-knop wordt ingedrukt gaat de led feller branden. Als de B-knop wordt ingedrukt gaat de led minder fel branden. Dat werkt op basis van Pulse Width Modulation (PWM), ook dat zullen we toelichten.

We doorlopen de volgende stappen:

1. Aansluiten van de led en het testen daarvan
2. Maken van een toestandsdiagram
3. Omzetten naar een programma

### Stap 1 Aansluiten van de led
Maak de onderstaande opstelling (die is gelijk aan Voorbeeld: aansluiten LED en drukknop). Je ziet:
% TODO: verwijzing naar voorbeeld aanpassen

- De led is aangesloten op pin 1.
- We gebruiken een weerstand van 47 Ohm om te voorkomen dat de led doorbrandt
- De platte kant van de led sluiten we aan op de min (0V). Je kunt ook kijken naar de pootjes van de led: het korte pootje sluiten we aan op de min (0V).

```{figure} 4-leddim-aansluitschema.png
```

Test of de led werkt, bijvoorbeeld met onderstaande programma. Dit programma laat het lampje steeds met een andere sterkte branden. Daarbij is 1023 de maximale waarde.

```{figure} 4-leddim-code.png
:width: 300px
```

Let op: we gebruiken hier ‘pauzeer’ puur voor het testen. In de module leer je hoe je hiervoor een timer kunt gebruiken, zie cyclus 2 - timers.
% TODO: verwijzing aanpassen

### Over PWM: Pulse With Modulation
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

### Stap 2 Maken van een toestandsdiagram
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4870499

We maken een programma met 4 toestanden.

- Toestand 1: de led is uit
- Toestand 2: de led is aan op 33% sterkte
- Toestand 3: de led is aan op 66% sterkte
- Toestand 4: de led is aan op 100% sterkte

Het toestandsdiagram ziet er dan zo uit:

```{figure} 4-leddim-toestand.png
```

### Stap 3 Omzetten naar een programma
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4870500

Dit was de bedoeling van ons systeem: als de A-knop op de Micro:bit wordt ingedrukt gaat de led feller branden. Als de B-knop wordt ingedrukt gaat de led minder fel branden.

Als je met de Micro:bit wilt nagaan of een knopje is gedrukt en weer losgelaten kun je het volgende commando gebruiken:

```{figure} 4-leddim-code3a.png
:width: 300px
```

Daarom hebben het programma als volgt opgebouwd.

```{figure} 4-leddim-code3b.png
:width: 600px
```

Test het programma. Werkt het?

## Voorbeeld: aansluiten piezobuzzer
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-5383224

Met een piezo-buzzer kun je een alarm laten klinken of een muziekje laten horen. In dit deel laten we zien hoe je de piezo-buzzer kunt aansluiten. De piezo buzzer zit bij de uitvinderskit. Zie ook: https://www.kitronik.co.uk/blog/inventors-kit-experiment-6-help.

Mocht je geen piezo-buzzer hebben, dan kun je ook gebruikmaken van oortjes om geluid te laten (zie de afbeelding hieronder). Daarvoor heb je krokodillebekjes nodig. Zie ook het volgende filmpje over het maken van geluid met de Micro:bit.

```{iframe} https://www.youtube.com/embed/cxfPNc4Wefo
:width:100%
```

Voor het aansluiten van een een piezo-buzzer kun je het onderstaande schema gebruiken. Je ziet dat de piezo-buzzer is aangesloten op pin 2 (P2). Je ziet daarbij ook de aansluiting van de ultrasoonsensor. Je kunt echter ook prima eerst alleen de piezo-buzzer aansluiten en testen, zodat je aan deelprobleem 2 kunt werken.

```{figure} 4-buzzer-aansluitschema.png
```

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
