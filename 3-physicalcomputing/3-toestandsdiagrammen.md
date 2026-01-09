# Toestandsdiagrammen

## Ontwerpen met behulp van toestandsdiagrammen

### Inleiding
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4855353

In deze module leer je te werken met toestandsdiagrammen. Als introductie daarop kun je met de gehele klas de volgende opdracht doen.

```{exercise} Toestanden in games
:label: opdracht3game
Bekijk gezamenlijk het volgende fragment uit een game waarin de hoofdrolspeler een bewaker moet proberen uit te schakelen. Kijk goed naar de bewaker en beschrijf in welke toestanden de bewaker kan zijn. Beschrijf ook hoe de bewaker in elk van die toestanden terecht komt. Met andere woorden: wat moet er gebeuren voordat de bewaker in een bepaalde toestand terecht komt.
```

```{iframe} https://www.youtube.com/embed/it9t0whAyPg
:width:100%
Automaat bewaker
```

### Toestanden
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4913221
Wellicht heb je de volgende toestanden gevonden, ook al noem je ze waarschijnlijk anders

1. Waakzaam, rondkijkend
2. Alert, klar voor actie, rondkijkend
3. Gealarmeerd, achter vijand aan lopend
4. Verdwaasd, rondlopend
5. Dood

Op basis van deze toestanden kun je een toestandsdiagram maken, waarin duidelijk wordt hoe de bewaker van de ene toestand in de andere komt. De getallen geven de toestanden aan zoals hierboven staat beschreven.

```{figure} 3-game-toestanden.png
```

Je kunt in het toestandsdiagram bijvoorbeeld zien dat als de bewaker in toestand 1 is en hij ziet een vijand, dan wordt de toestand van de bewaker 2.

In de bovenstaande uitwerking zie je totaal 5 toestanden en 6 toestandsovergangen. Misschien zijn er wel meer hoor, alleen in dit korte fragment kun je ze niet allemaal zien.

Het losse pijltje naar toestand 1 betekent dat dit de begintoestand is, oftewel de initiële toestand.

```{exercise} Unplugged Nooddienstregeling bij de spoorwegen
:label: opdracht3unplugged
Je kunt ook als inleiding ook de unplugged activiteit doen die je via de onderstaande link vindt.

[Nooddienstregeling bij de spoorwegen](http://www.informaticaunplugged.nl/de-werkvormen/nooddienstregeling-bij-de-spoorwegen/)
```

### Frisdrankautomaat
%bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4875018

Hieronder zie je een voorbeeld van een onderdeel van een frisdrankautomaat. Dit onderdeel houdt bij hoeveel geld de gebruiker van de automaat heeft ingeworpen. Voor het gemak gaan we uit van slechts twee munten: 50 cent en 1 euro. En alle frisdranken in de automaat kosten 2 euro.

```{figure} 3-frisdrank-toestanden.png
```

De bollen zijn _toestanden_. Dit toestandsdiagram kent dus vijf toestanden. De frisdrankautomaat begint in de starttoestand, dat is in dit geval de toestand ‘Start: 0 euro’. Bij elke toestand zie je enkele _overgangen_. Bijvoorbeeld de overgang van de _starttoestand_ ‘0 euro’ naar ‘0,5 euro’. Die toestandsovergang vindt plaats als de gebruiker begint met het inwerpen van een muntstuk van 50 eurocent.  
Je ziet dat een toestandsovergang ook naar dezelfde toestand kan gaan. Kijk maar bij de toestand ‘2 euro’. Na de toestandsovergang ‘Inworp 50 cent’ is de toestand nog steeds ‘2 euro’. 

Je kunt er zelf even mee oefenen. Klik op het plaatje hieronder om te activeren. Via de blauw en oranje knop kun je zogenaamd 50 cent of 1 euro inwerpen en dan zie je in welke toestand de automaat terecht komt.

```{figure} 3-frisdrank-toestanden-kleur.png
```

Een toestandsovergang wordt meestal uitgevoerd op basis van informatie uit één van de sensoren. Als iemand één euro in de frisdrankautomaat doet, wordt dat door één of meerdere sensoren gedetecteerd. Hoe dat precies werkt is hierbij niet belangrijk. Uit de toestandsdiagram kun je opmaken naar welke toestand de automaat moet gaan als iemand die euromunt inwerpt.

```{exercise} Frisdrankautomaat
:label: opdracht3fris
Vul in. In welke toestand komt de automaat als iemand de volgende munten ingooit: 50 cent en nog eens 50 cent? Dat is toestand
`______`
. In welke toestand komt de automaat als iemand de volgende munten ingoot: 50 cent, 1 euro, 1 euro? Dat is toestand
`______`
.  Het is (wel of niet?)
`______`
mogelijkheid dat de automaat van de toestand ‘2 euro’ nog in een andere toestand komt.
```

```{solution} opdracht3fris
:class: dropdown
- `1`
- `2`
- `niet`
```

### Acties in een toestandsdiagram
%bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4875030

Het vorige toestandsdiagram is nog niet volledig, de gebruiker moet immers wel een frisdrank kunnen selecteren. In het volgende toestandsdiagram voegen we een overgang ‘selectie’ toe aan alle toestanden. ‘Selectie’ betekent dat de gebruiker een frisdrank kiest.

```{figure} 3-frisdrank-toestanden-actie.png
```

Aan een toestandsovergang kan een actie worden gekoppeld. Bij de frisdrankautomaat wordt de actie: ‘geef frisdrank’ uitgevoerd als de gebruiker een frisdrank selecteert en de toestand is: ‘2 euro’. Acties zijn altijd gekoppeld aan toestandsovergangen en niet aan toestanden. Een toestandsovergang mag één of meer acties hebben, maar dat hoeft niet. Voor het uitvoeren van acties worden vaak actuatoren gebruikt, zoals een lampje, display of motor.

In deze module gebruiken we steeds een dubbele punt om het onderscheid te maken tussen toestandsovergang en actie.

```
<toestandsovergang> : <actie>
```

```{exercise} Werking frisdrankautomaat
:label: opdracht3werkfris
Beschrijf de werking van deze frisdrankautomaat in 2 of 3 zinnen.
```

```{solution} opdracht3werkfris
:class: dropdown
**Uitleg**

De automaat houdt bij hoeveel geld (50 cent en 1 euro-muntstukken) er is ingeworpen. Pas als het totaal gelijk is of meer dan 2 euro kan de gebruiker een frisdrank selecteren. De automaat geeft geen geld terug (niet een erg klantvriendelijke automaat dus).
```

## Voorbeelden

### Inleiding
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-5379818

In dit deel vind je enkele voorbeelden, deels uitgewerkt, en deels zijn het opdrachten. Deze helpen om toestandsdiagrammen te begrijpen en te oefenen met het maken van toestandsdiagrammen. Kies zelf welke je interessant vindt.

### Voorbeeld: lichtregulering
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-5379587

In dit voorbeeld gaat het om een systeem waarmee je de intensiteit van een lamp kunt reguleren. Het systeem bestaat uit een lamp en twee knoppen.

De lamp kan in drie standen worden gezet:

- Uit (geen licht)
- Half aan (zacht licht)
- Helemaal aan (fel licht)

Het systeem heeft twee knoppen zonder toggle-functie (A en B). Met knop A gaat de lamp feller branden. Bijvoorbeeld: als de lamp half aan is en knop A wordt ingedrukt, dan gaat de lamp helemaal aan. Met knop B gaat de lamp minder fel branden. De lamp is altijd in één van de drie bovengenoemde standen.

```{exercise} Opdracht: maak toestandsdiagram lichtregulering
:label: opdracht3lichtregulering

a) Maak een toestandsdiagram voor dit systeem. In de volgende paragraaf wordt dit uitgewerkt, probeer het echter eerst zelf.
b) Het systeem wordt verder uitgebreid. De lamp heeft twee kleuren (rood en blauw). Er wordt een derde knop (C) toegevoegd waarmee kan worden gewisseld tussen de kleur rood en de kleur blauw. Pas het toestandsdiagram hier op aan.
```

### Uitwerking opdracht a)
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-5379547

Hieronder volgt een mogelijke uitwerking van opdracht a) over de lichtregulering.

Het begint met het proberen te bepalen welke toestanden er zijn. In de opdrachtomschrijving staat dat de lamp in drie standen kan staan. Het ligt voor de hand dat we die gebruiken voor de toestanden:

1. Lamp is uit
2. Lamp is half aan
3. Lamp is helemaal aan

Die toestanden kunnen we vast tekenen, als drie bollen

```{figure} 3-lichtregulering-antwoord-a-td1.png
```

Belangrijk om te weten is welke gebeurtenissen er zijn, op basis daarvan kun je de toestandsovergangen bepalen. Als je de tekst van de opdracht leest blijkt dat er twee knoppen zijn. Dat zijn de gebeurtenissen, er zijn er dus twee:

- knop A wordt ingedrukt (en weer losgelaten)
- knop B wordt ingedrukt (en weer losgelaten)

Voor elke toestand (dat zijn er drie) en elke gebeurtenis (dat zijn er twee) kunnen we bepalen wat de toestandsovergang wordt (3 x 2 = 6). Elke toestandsovergang teken je als een pijl. Dan krijg je zoiets als hieronder.

```{figure} 3-lichtregulering-antwoord-a-td2.png
```

A betekent: knop A wordt ingedrukt, B betekent: knop B wordt ingedrukt.

Nu moeten de acties er nog bij. Bijvoorbeeld, wat moet er gebeuren als de lamp in toestand 2 is en op knop B wordt gedrukt? Dan moet de lamp uit gaan. Een actie zet je altijd bij een toestandsovergang (dus niet bij een toestand). Je krijgt dan dit:

```{figure} 3-lichtregulering-antwoord-a-td3.png
```

Je ziet, niet bij iedere toestandsovergang hoeft een actie te staan.

We zijn nog niet helemaal klaar, begintoestand moet er bij. Dat is de initiele toestand waar het systeem in begint. Het lijkt logisch dat de lamp eerst uit is, we kiezen daarom toestand 1 als begintoestand. En om het toestandsdiagram overzichtelijk te houden, laten we de toestandsovergangen die naar zichzelf verwijzen en geen actie hebben weg. Dan krijg je dit.

```{figure} 3-lichtregulering-antwoord-a-td4.png
```

We houden de teksten kort in het diagram om het overzichtelijk te houden. Het nadeel is dat misschien niet helemaal helder is wat er wordt bedoeld. Bijvoorbeeld, de pijl van toestand 1 naar toestand 2 waar bij staat A: lamp half aan zou beter kunnen zeggen:

(gebeurtenis) knop A wordt ingedrukt -> (actie) zet de lamp met halve intensiteit aan.

Je kunt het toestandsdiagram voor jezelf testen en daarmee controleren of het klopt. Bijvoorbeeld, wat gebeurt er is als ik op A, B en dan weer B druk? Klopt dit met wat het systeem zou moeten doen?

Probeer nu eerst zelf opdracht b) te doen voordat je de uitwerking bekijkt.

### Uitwerking opdracht b)
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-5379568

Hieronder volgt een mogelijke uitwerking van opdracht b) over de lichtregulering.

De eerste vraag die je jezelf moet stellen is: welke toestanden herken ik? De lamp kent nu naast de drie standen (uit, half aan, fel) ook nog de mogelijkheid voor twee kleuren (rood en blauw). Hoeveel toestanden zijn er dan? Het lijkt er op dat dat er zes zijn, namelijk 3 standen x 2 kleuren:

1. Lamp is uit / rood
2. Lamp is half aan / rood
3. Lamp is helemaal aan / rood
4. Lamp is uit / blauw
5. Lamp is half aan / blauw
6. Lamp is helemaal aan / blauw

Laten we proberen het toestandsdiagram uit a) uit te breiden. We laten de acties nog even weg.

```{figure} 3-lichtregulering-antwoord-b-td1.png
```

Wat zijn de mogelijke gebeurtenissen? Er zijn nu drie knoppen, dus drie gebeurtenissen:

- knop A wordt ingedrukt
- knop B wordt ingedrukt
- knop C wordt ingedrukt

Dat betekent dat er mogelijk 6 (toestanden) x 3 (gebeurtenissen) = 18 mogelijke toestandsovergangen zijn. Nu kun je gaan kijken wat die toestandsovergangen precies zijn en ze als een pijl gaan tekenen. Eerst maar eens kijken wat er moet gebeuren als knop C wordt ingedrukt voor ieder van de toestanden.

```{figure} 3-lichtregulering-antwoord-b-td2.png
```

Dan zijn we er nog niet, want we moeten ook duidelijk maken wat er gebeurt als knop A of B wordt ingedrukt als het systeem in toestand 4, 5 of 6 is.

```{figure} 3-lichtregulering-antwoord-b-td3.png
```

Vervolgens moeten de acties erbij, dat doen we hieronder, weliswaar in het kort, anders wordt het onoverzichtelijk.

```{figure} 3-lichtregulering-antwoord-b-td4.png
```

Het nadeel van korte teksten is dat het misschien niet helemaal helder is wat er moet gebeuren. Bijvoorbeeld, de pijl van toestand 2 naar toestand 5 waar bij staat C: blauw, zou beter kunnen zeggen:

(gebeurtenis) knop C wordt ingedrukt : (actie) zet het rode licht uit en zet het blauw licht half aan

Nog een voorbeeld: de pijl van toestand 1 naar toestand 2 waar bij staat A: 50% rood, zou beter kunnen zeggen:

(gebeurtenis) knop A wordt ingedrukt : (actie) zet het rode licht half aan

Een begintoestand hadden we al, dus dit zou het moeten zijn. Test je toestandsdiagram vervolgens voor jezelf. Wat gebeurt er bijvoorbeeld als je de knoppen C, dan A, dan C, dan A indrukt? En klopt dat met wat je verwacht dat het zou moeten doen?

```{exercise} Geen acties bij toestandsovergangen
:label: opdracht3geenacties
Aan de linkerkant van het toestandsdiagram staan twee toestandsovergangen zonder actie:

- van toestand 1 naar 4 (knop C wordt ingedrukt)
- van toestand 4 naar 1 (knop C wordt ingedrukt)

Waarom staat hier geen actie bij?
```

```{solution} opdracht3geenacties
:class: dropdown
** Uitleg **
Er staat geen actie bij omdat het licht al uit is en uit moet blijven, zowel in toestand 1 als in toestand 4. Er hoeft dus niets te gebeuren als dan knop C wordt ingedrukt en dus is er geen actie.
```

### Voorbeeld: tamagotchi

### Voorbeeld: valdetectie

## Correcte toestandsdiagrammen

### Tabel met alle toestandsovergangen
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4875031

Voor het overzicht laten we de toestandsovergangen die naar dezelfde toestand verwijzen ook wel eens weg, zoals hieronder.

```{figure} 3-frisdrank-toestanden-tabel.png
```

Het is echter wel verstandig om goed na te denken over wat er in alle gevallen gebeurt. Bijvoorbeeld, wat gebeurt er in toestand ‘1 euro’ als de gebruiker een frisdrank selecteert? Door over alle mogelijkheden na te denken voorkom je fouten die je later veel tijd kosten om te herstellen. Je kunt dat ook in een tabel weergeven door alle toestanden te combineren met alle mogelijke toestandsovergangen. Daarbij geef je voor alle mogelijkheden aan wat de nieuwe toestand wordt.

```{table} 
| Toestand ↓ / Toestandsovergang → | Inworp 50 cent | Inworp 1 euro | Selectie |
| --- | --- | --- | --- | 
| Start: | 0 euro | 0,5 euro | 1 euro | 0 euro |
| 0,5 euro | 1 euro | |  |
| 1 euro |  |  |  |
| 1,5 euro |  |  |  | 	 
| 2 euro |  |  |  |
```	 

In de bovenstaande tabel zie je alle toestanden in de linker kolom. Je ziet ook alle mogelijke gebeurtenissen in de bovenste rij. Voor iedere combinatie moet de tabel beschrijven wat de nieuwe toestand wordt. Dit kan dus ook dezelfde toestand blijven. De tabel hierboven is nog niet volledig ingevuld.

```{exercise} Tabel toestandsdiagram
:label: opdracht3tabel
Maak de tabel hierboven af.
```

````{solution} opdracht3tabel
:class: dropdown
**Uitleg**

```{table}
| Toestand ↓ / Toestandsovergang → | Inworp 50 cent | Inworp 1 euro | Selectie |
| --- | --- | --- | --- | 
| Start: | 0 euro | 0,5 euro | 1 euro | 0 euro |
| 0,5 euro | 1 euro | 1,5 euro | 0,5 euro |
| 1 euro | 2 euro | 2 euro | 1 euro |
| 1,5 euro | 2 euro | 2 euro | 1,5 euro | 	 
| 2 euro | 2 euro | 2 euro | 2 euro |
```	
````

### Regels voor een toestandsdiagram
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4875036

Een toestandsdiagram is gebonden aan strenge regels:

- Een toestandsdiagram bestaat uit toestanden (bollen) en toestandsovergangen (pijlen)
- Alle toestanden worden weergegeven als bollen. In de bol staat een korte beschrijving van de toestand.
- Er is altijd precies één starttoestand, die herken je aan de pijl die niet verbonden is aan een andere toestand.
- Alle toestandsovergangen worden weergegeven als een pijl, die één kant op wijst. Bij de pijl staat een korte beschrijving van de toestandsovergang.
- Een toestand kan nooit twee of meer keer dezelfde toestandsovergang hebben.
- Een toestandsovergang mag dezelfde toestand als begin en eind hebben.
- Bij een toestandsovergang mogen één of meerdere acties staan. In deze module gebruiken we steeds een dubbele punt om het onderscheid te maken tussen toestandsovergang en actie.

```{seealso} Toestandsdiagrammen tekenen
Je kunt toestandsdiagrammen prima op papier tekenen. Dat gaat vaak het snelst, maar pas op dat het wel leesbaar blijft. Een handige tool om toestandsdiagrammen mee te maken vind je via de volgende site.

[Finite State Machine Designer](http://madebyevan.com/fsm/)
```