# Toestandsdiagrammen ontwerpen (opdrachten)

## Inleiding
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-5379818

In dit deel vind je enkele voorbeelden, deels uitgewerkt, en deels zijn het opdrachten. Deze helpen om toestandsdiagrammen te begrijpen en te oefenen met het maken van toestandsdiagrammen. Kies zelf welke je interessant vindt.

## Voorbeeld: lichtregulering
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

```{figure} 6-lichtregulering-antwoord-a-td1.png
```

Belangrijk om te weten is welke gebeurtenissen er zijn, op basis daarvan kun je de toestandsovergangen bepalen. Als je de tekst van de opdracht leest blijkt dat er twee knoppen zijn. Dat zijn de gebeurtenissen, er zijn er dus twee:

- knop A wordt ingedrukt (en weer losgelaten)
- knop B wordt ingedrukt (en weer losgelaten)

Voor elke toestand (dat zijn er drie) en elke gebeurtenis (dat zijn er twee) kunnen we bepalen wat de toestandsovergang wordt (3 x 2 = 6). Elke toestandsovergang teken je als een pijl. Dan krijg je zoiets als hieronder.

```{figure} 6-lichtregulering-antwoord-a-td2.png
```

A betekent: knop A wordt ingedrukt, B betekent: knop B wordt ingedrukt.

Nu moeten de acties er nog bij. Bijvoorbeeld, wat moet er gebeuren als de lamp in toestand 2 is en op knop B wordt gedrukt? Dan moet de lamp uit gaan. Een actie zet je altijd bij een toestandsovergang (dus niet bij een toestand). Je krijgt dan dit:

```{figure} 6-lichtregulering-antwoord-a-td3.png
```

Je ziet, niet bij iedere toestandsovergang hoeft een actie te staan.

We zijn nog niet helemaal klaar, begintoestand moet er bij. Dat is de initiele toestand waar het systeem in begint. Het lijkt logisch dat de lamp eerst uit is, we kiezen daarom toestand 1 als begintoestand. En om het toestandsdiagram overzichtelijk te houden, laten we de toestandsovergangen die naar zichzelf verwijzen en geen actie hebben weg. Dan krijg je dit.

```{figure} 6-lichtregulering-antwoord-a-td4.png
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

```{figure} 6-lichtregulering-antwoord-b-td1.png
```

Wat zijn de mogelijke gebeurtenissen? Er zijn nu drie knoppen, dus drie gebeurtenissen:

- knop A wordt ingedrukt
- knop B wordt ingedrukt
- knop C wordt ingedrukt

Dat betekent dat er mogelijk 6 (toestanden) x 3 (gebeurtenissen) = 18 mogelijke toestandsovergangen zijn. Nu kun je gaan kijken wat die toestandsovergangen precies zijn en ze als een pijl gaan tekenen. Eerst maar eens kijken wat er moet gebeuren als knop C wordt ingedrukt voor ieder van de toestanden.

```{figure} 6-lichtregulering-antwoord-b-td2.png
```

Dan zijn we er nog niet, want we moeten ook duidelijk maken wat er gebeurt als knop A of B wordt ingedrukt als het systeem in toestand 4, 5 of 6 is.

```{figure} 6-lichtregulering-antwoord-b-td3.png
```

Vervolgens moeten de acties erbij, dat doen we hieronder, weliswaar in het kort, anders wordt het onoverzichtelijk.

```{figure} 6-lichtregulering-antwoord-b-td4.png
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

## Voorbeeld: tamagotchi
% TODO: dit voorbeeld van SLO overnemen
Hier komt misschien nog wat, nu mag je het overslaan.

## Voorbeeld: valdetectie
% TODO: dit voorbeeld van SLO overnemen
Hier komt misschien nog wat, nu mag je het overslaan.

