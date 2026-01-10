# Electronica

## Werken met de Micro:bit

### De Micro:bit
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4889670
De Micro:bit is een microcontroller waarop je allerlei sensoren en actuatoren kunt aansluiten. Dat aansluiten gaat via de pinnen. Als je kijkt naar de Micro:bit kun je de pinnen zien: 0, 1, 2, en daarnaast de 3V en GND.

```{figure} 2-microbit-front
Voorkant Micro:bit
```

De 3V is kun je wel de plus noemen en de GND de min, net als bij een batterij. Als de Micro:bit is aangesloten komt er 3 volt te staan op de 3V pin. Ter vergelijking, op het stopcontact staat standaard 230 volt. Je hoeft je niet druk te maken dat je een elektrische schok voelt bij de Micro:bit. GND staat voor ground, oftewel de aarde.

De pinnen 0, 1 en 2 kun je gebruiken om sensoren aan te sluiten. Je kunt bijvoorbeeld een temperatuurmeter aansluiten op pin 0 en daarmee meten welke waarde de temperatuursensor doorgeeft. Je kunt de pinnen ook gebruiken om een actuator aan te sluiten. Dan werkt de pin als een soort schakelaar. Je kunt bijvoorbeeld een motor aansluiten op pin 0 en dan de motor aan en uit zetten. Later leer je meer over het aansluiten van sensoren en actuatoren.

De Micro:bit heeft overigens nog veel meer pinnen, die zijn echter veel kleiner. Toch kun je die wel gebruiken door gebruik te maken van een speciaal breakout board. Daarover later meer.

```{figure} 2-microbit-back
Micro:bit achterkant
```

De Micro:bit heeft op de voorkant 5x5=25 ledjes die je ieder apart aan en uit kunt zetten. 

```{figure} 2-microbit-leds
De leds van de Micro:bit
```

Bekijk de onderstaande link als je meer wilt wilt weten over de pinnen van de Micro:bit.

[BBC micro:bit pinnen](https://makecode.microbit.org/device/pins) (Engelstalig)

### Sensoren en actuatoren op de Micro:bit
% TODO: stukje over sensoren en actuatoren die op de microbit zitten zonder dat je iets hoeft aan te sluiten
Hier komt ooit nog wat, nu mag je het overslaan

### Programmeeromgeving

#### Je eerste programma voor de Micro:bit
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4855374

Je kunt met de Micro:bit al heel snel je eerste programma maken, bijvoorbeeld een knipperend hartje. Daarvoor heb je geen sensoren nodig.

```{figure} 2-microbit-blink.gif
```

Doorloop de volgende stappen. Als je er niet uitkomt, kijk dan op de site https://microbit.org/nl/get-started/getting-started/introduction/ voor meer informatie.

**Stap 1** Verbind de Micro:bit via de USB-kabel met je computer.

```{figure} 2-microbit-connect.gif
```

Als het goed is zie je de Micro:bit als schijf verschijnen.

**Stap 2** Programmeer de Micro:bit vanuit de website: https://makecode.microbit.org/

Open de site en start een nieuw project.
```{figure} 2-nieuw-project.png
```


Maak het programma (zie het filmpje hieronder). Je kunt de blokjes verslepen.

```{figure} 2-maak-code.gif
```

Zorg dat je het volgende programma krijgt:

```{figure} 2-code-stap2.png
```

**Stap 3** Sla het programma op, bijvoorbeeld onder de naam 'Kloppend hart'.

**Stap 4** Download het programma naar de Micro:bit

Klik op de Download-knop en sla het bestand op. Vervolgens sleep je het bestand naar de Micro:bit. De Micro:bit zal opnieuw opstarten en dan het programma starten. Als het goed is zie je een kloppend hart verschijnen.

```{exercise} Opdracht Maak twee projecten na
:label: opdracht1namaken

Je gaat nu de Micro:bit verder verkennen. Werk in tweetallen. Kies twee projecten van de site https://makecode.microbit.org/# en bouw deze na in de Micro:bit.
```

### Programmeeromgeving Micro:bit
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4855375
Hieronder vind je een overzicht van de programmeeromgeving van de Micro:bit en een korte uitleg van de belangrijkste onderdelen.

```{figure} 2-programmeeromgeving.png
De programmeeromgeving van de Micro:bit
```
 
1. Start. Als je terugwilt naar het overzicht jouw projecten en voorbeelden van andere projecten.
2. Zoek je hulp, bijvoorbeeld over de werking van de verschillende blokken, kijk dan hier.
3. Bij de instellingen kun je onder meer de taal instellen.
4. In de simulatie-omgeving kun je je programma testen zonder dat je het eerst hoeft te downloaden.
5. Dit zijn de blokken waarmee je kunt programmeren. Als je een specifiek blok zoekt kan het helpen te kijken naar de kleur van het blok.
6. Je maakt een programma door de blokken naar de programmeeromgeving te slepen.
7. Hier kun je je programma downloaden zodat je het op je Micro:bit kunt zetten.
8. Sla je programma op onder een duidelijke naam zodat je het later makkelijk terug kunt vinden in je projecten overzicht.

```{exercise} Welke blokken gebruik je?
:label: opdracht2blokken

Je kunt de Micro:bit programmeren met behulp van de blokken. 
Een blok dat je bijna altijd gebruikt is het blok ______(1).
Alles wat in dit blok staat wordt continu opnieuw door de Micro:bit uitgevoerd. 
Als je iets maar één keer wilt laten uitvoeren bij het opstarten van de Micro:bit gebruik je het blok ______(2).

Als je een keuze wilt programmeren (als-dan of als-dan-anders) dan gebruik je de blokken die staan bij ______(3).
Voor herhalingen kijk je bij ______(4).
Als je wilt dat er iets gebeurt op het moment dat de Micro:bit wordt geschud, gebruik je het blokje ______(5)
```

```{solution} opdracht2blokken
:class: dropdown
1. de hele tijd
2. bij opstarten
3. Logisch
4. Lussen
5. bij schudden
```

## Uitvinderkit voor het aansluiten van sensoren en actuatoren

### Uitvinderskit
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4866806

Als je externe sensoren gaat aansluiten raden we aan dat je een breadboard en breakout board gebruikt. Die zijn onderdeel van de uitvinderskit van Kitronik. Zonder te solderen kan je alles aansluiten op de Micro:Bit. In de uitvinderskit zit een handleiding, waarin stap voor stap wordt uitgelegd (in het Engels) hoe de Micro:Bit gebruikt kan worden. In het onderstaande filmpje wordt een introductie gegeven van de uitvinderskit en de Micro:bit.

```{iframe} https://www.youtube.com/embed/lmdzM74XyHw
:width:100%
```

```{figure} 2-inventorskit.jpg
Kitronic Breadboard en Breakoutboard
```

Op de eerste pagina van de handleiding die bij de uitvinderskit wordt meegeleverd staat beschreven hoe je deze onderdelen aan elkaar koppelt. Zie ook: https://www.kitronik.co.uk/pdf/5609_prototyping_system_for_the_bbc_micro_bit_assembly_instructions.pdf.

### Breakoutboard
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4855378
Met behulp van het breakoutboard kun je makkelijk verbindingen maken met alle pinnen van de Micro:bit. Hieronder vind je een filmpje waarin de presentator uitlegt waarom het handig is om het breakout board te gebruiken.

```{iframe} https://www.youtube.com/embed/bzm4zepbGAc
:width:100%
```

Het overzicht van de [pinnen](https://makecode.microbit.org/device/pins) (Engelstalig) helpt bij het aansluiten van sensoren via het breakout board. Dit overzicht is ook te vinden op de achterkant van de handleiding van de uitvinderskit.

### Breadboard
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4855379

Ondanks dat de Micro:Bit al allerlei sensoren heeft, zal je waarschijnlijk ook andere dingen op de Micro:Bit willen aansluiten. Die dingen kunnen van alles zijn: extra lampjes, extra knoppen, sensoren, etc. Zeker als we het hebben over een proefopstelling is het erg gemakkelijk om daar een zogenaamd breadboard voor te gebruiken.

Een breadboard is een bordje met gaatjes waar je draadjes en andere onderdelen in kunt steken en zo verbindingen kunt maken.

```{figure} 2-breadboard.jpg
```

De 5 horizontale gaatjes zijn steeds met elkaar verbonden. Bijvoorbeeld: de gaatjes van rij 5 met de letters F G H I J zijn met elkaar verbonden. Steek je dus een draadje in J5 en een pootje van een led in G5 dan zijn die twee met elkaar verbonden. Maar dus niet met een ander onderdeel dat je in D5 hebt gestoken.

De rode en blauwe lijnen zijn bedoeld om daar 3V (de rode lijn, de +) en GND (de blauwe lijn, de -) op aan te sluiten. In de voorbeelden verderop in de module zul je zien hoe je gebruikt kunt maken van het breadboard.

Meer achtergrond over het breadboard vind je [op de site van Sparkfun](https://learn.sparkfun.com/tutorials/how-to-use-a-breadboard).

### Aansluiten met krokodillebekken
% bron: https://maken.wikiwijs.nl/135426/Inleiding___Micro_bit#!page-4866810

Je hoeft niet per se gebruik te maken van het breakoutboard en het breadboard. Je kunt ook werken met draden met zogenaamde krokodillebekjes. Hieronder zie je een voorbeeld van het gebruik daarvan in een opstelling voor het meten van de vochtigheid van aarde. Zie ook: https://makecode.microbit.org/projects/soil-moisture.

```{figure} 2-krokodillenbekken.jpg
Gebruik van krokodillebekjes 
```

Het nadeel van het gebruik van deze krokodillebekjes is dat je alleen maar de pinnen 0, 1 en 2 kunt gebruiken, naast 3V en GND. Als je meerdere sensoren en/of actuatoren wilt aansluiten kom je dan wellicht tekort.

