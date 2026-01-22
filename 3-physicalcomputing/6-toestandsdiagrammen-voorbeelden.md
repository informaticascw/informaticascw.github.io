# Toestandsdiagrammen (opdrachten)

% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-5379818

In dit deel vind je enkele voorbeelden, deels uitgewerkt, en deels zijn het opdrachten. Deze helpen om toestandsdiagrammen te begrijpen en te oefenen met het maken van toestandsdiagrammen. Kies zelf welke je interessant vindt.

## Voorbeeld: lichtbediening

### Zonder toggle functie (versie 1)

In deze paragraaf ga je een toestandsdiagram maken voor een lamp die aan en uit kan met een drukknop.

Gebruik een drukknop om een lamp aan en uit te zetten. Zolang de drukknop is ingedrukt staat de lamp aan. Zodra de drukknop wordt losgelaten gaat de lamp uit.

Er zijn de volgende overgangen:
- Knop los (niet-ingedrukt)
- Knop ingedrukt

Er zijn de volgende acties:
1. Lamp aan
2. Lamp uit

```{exercise} Lichtschakelaar(versie 1)
:label: opdracht6-zondertoggle
Maak een toestandsdiagram bij bovenstaande beschrijving van een lichtschakelaar. 

Gebruik twee toestanden. Gebruik de hierboven beschreven toestandsovergangen en acties.
```

````{solution} opdracht6-zondertoggle
:class: dropdown
```{figure} 6-td-knop.png
```
````

### Met toggle functie (versie 2)

In deze paragraaf ga je een toestandsdiagram maken voor een lamp die aan en uit kan met een drukknop die een toggle functie heeft.

Bij de lamp uit de vorige opdracht ging de lamp uit zodra je de knop losliet. Dat is erg onhandig als je het licht wilt gebruiken om een boek te lezen. Je kunt in de plaats van een drukknop gebruik maken van een schakelaar. Een schakelaar blijft in de stand staan waarnaar je hem duwt. Het kan ook met een drukknop, maar dan moet je een toestandsdiagram maken dat een toggle functie nadoet.

Bij een drukknop met toggle functie zijn de volgende overgangen:
- Knop los (niet-ingedrukt)
- Knop ingedrukt

Er zijn de volgende acties:
1. Lamp aan
2. Lamp uit

Dit zijn dezelfde overgangen en acties als bij de drukknop zonder toggle, maar om een toggle te maken gebruik je elke overgang twee keer. Dit werkt als volgt. 
- Begin met de knop los en de lamp uit.
- Druk de knop in: de lamp gaat aan.
- Laat de knop los: de lamp blijft aan (er verandert niks aan de lamp, dus er is geen actie nodig).
- Druk de knop in: de lamp gaat uit.
- Laat de knop los: geen aktie.
- Enzovoort.

```{exercise} Lichtschakelaar(versie 2)
:label: opdracht6-mettoggle
Maak een toestandsdiagram bij bovenstaande beschrijving van een lichtschakelaar met toggle-functie. 

Gebruik vier toestanden. Gebruik de hierboven beschreven toestandsovergangen en acties.
```

````{solution} opdracht6-mettoggle
:class: dropdown
```{figure} 6-td-toggle.png
```
[Kik hier voor een interactieve versie van het toestandsdiagram](https://maken.wikiwijs.nl/userfiles/ed3e0b32cbb0dd7ae561e558b0d290b55faaef72.html)
````

## Voorbeeld: hotelschakelaar

### Met schakelaars (versie 1)
% geinspireerd op bron: https://maken.wikiwijs.nl/135892/Cyclus_1___Arduino#!page-4957251
% en bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4886282

In deze paragraaf ga je een toestandsdiagram maken voor een lamp die aan en uit kan met twee schakelaars.

In hotels zijn vaak twee schakelaars aanwezig om het licht te bedienen: een schakelaar bij de deur en een schakelaar bij het bed. Dit voorbeeld gaat over het toestandsdiagram van een hotelschakelaar met twee schakelaars en een lamp (led). 

Een hotelschakelaar werkt als volgt: als de stand van één van de schakelaars verandert, dan verandert de status van de lamp. Begin met alle schakelaar omlaag en de lamp uit. Als schakelaar A omhoog wordt gezet dan gaat de lamp (LED) aan. Als vervolgens B omhoog wordt gezet, dan gaat de lamp weer uit. Wordt vervolgens aan weer omlaag gezet, dan gaat de lamp weer aan, enzovoort.

Je hebt de volgende mogelijke toestandsovergangen:
- SA aan (schakelaar A gaat omhoog)
- SA uit (schakelaar A gaat omlaag)
- SA aan (schakelaar B gaat omhoog)
- SA uit (schakelaar B gaat omlaag)

De mogelijke acties zijn:
- lamp aan (doe ledje aan)
- lamp uit (doe ledje uit)

```{exercise} Toestandsdiagram voor hotelschakelaars (versie 1)
:label: opdracht6-hotelschakelaars
Maak een toestandsdiagram bij bovenstaande beschrijving van een hotelschakelaar. 

Gebruik vier toestanden. Gebruik de hierboven beschreven toestandsovergangen en acties.
```

````{solution} opdracht6-hotelschakelaars
:class: dropdown
```{figure} 6-td-hotelschakelaars.png
```

````

### Met drukknoppen (versie 2)
% bron: https://maken.wikiwijs.nl/135892/Cyclus_1___Arduino#!page-4942190

In deze paragraaf ga je een toestandsdiagram maken voor een lamp die aan en uit kan met twee drukknoppen met een toggle functie.

In nieuwe hotels zijn de schakelaars vaak vervangen door drukknoppen zonder toggle functie. Dit voorbeeld gaat over een toestandsdiagram van een hotelschakelaar met twee drukknoppen en een lamp (led).

Je gaat nu het toestandandsdiagram voor de hotelschakeling nog eens maken, alleen met drukknoppen werkt het op een iets andere manier dan met schakelaars. Als je een drukknop indrukt en vervolgens loslaat moet de lamp aangaan. Als een drukknop weer indrukt en vervolgens loslaat gaat de lamp weer uit. De drukknopjes krijgen dus een toggle-functie.

Je kunt de volgende toestandsovergangen gebruiken:
- drukknop A ingedrukt
- drukknop A niet ingedrukt
- drukknop B ingedrukt
- drukknop B niet ingedrukt 

De mogelijke acties zijn:
- lamp aan (doe ledje aan)
- lamp uit (doe ledje uit)

```{exercise} Toestandsdiagram voor hotelschakelaars (versie 2)
:label: opdrachgt6-hotelknoppen
Gebruik bovenstaande toestandsovergangen en acties heb je nodig in je toestandsdiagram. Op het moment dat een knop wordt ingedrukt, dan is er een toestandsovergang en een actie. Als een knop wordt losgelaten, dan verandert de toestand, maar dan is er geen actie. Er kunnen niet twee knoppen precies tegelijk ingedrukt of losgelaten worden, in dat geval is er altijd één knop net iets eerder. Je hebt 8 toestanden nodig.

Maak het toestandsdiagram. 
```

````{solution} opdrachgt6-hotelknoppen
:class: dropdown
```{figure} 6-td-hotelknoppen.png
```
Legenda:
- L- (licht uit)
- L+ (licht aan)
- A- (knop A ingedrukt)
- A+ (knop A niet ingedrukt)
- B- (knop B ingedrukt)
- B+ (knop B niet ingedrukt)
````

## Voorbeeld: lichtregulering
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-5379587

### Deel 1: drie standen

In deze paragraaf ga je een toestandsdiagram maken voor een lamp waarvan de felheid kan worden ingesteld met twee drukkknoppen.

Het systeem bestaat uit een lamp en twee knoppen. De lamp kan in drie standen worden gezet:

- Uit (geen licht)
- Half aan (zacht licht)
- Helemaal aan (fel licht)

Het systeem heeft twee knoppen (A en B). Met knop A gaat de lamp feller branden. Bijvoorbeeld: als de lamp half aan is en knop A wordt ingedrukt, dan gaat de lamp helemaal aan. Met knop B gaat de lamp minder fel branden. De lamp is altijd in één van de drie bovengenoemde standen. 

```{exercise} Opdracht: maak toestandsdiagram lichtregulering deel 1
:label: opdracht3lichtregulering-1

Maak een toestandsdiagram voor dit systeem. 

Gebruik toestandsovergangen bij gebeurtenissen. De gebeurtenis vindt plaats het moment dat de status van een knop verandert van niet-ingedrukt naar ingedrukt. Lees [het kader in het vorige hoofdstuk over toestandsovergangen met gebeurtenis of status](=physcomp-5-gebeurtenis) als je het verschil tussen een gebeurtenis of status niet begrijpt.

Je kunt je toestandsdiagram voor jezelf testen en daarmee controleren of het klopt. Bijvoorbeeld, wat gebeurt er is als ik op A, B en dan weer B druk? Klopt dit met wat het systeem zou moeten doen?

Probeer het eerst zelf, voordat je de uitwerking bekijkt.
```

````{solution} opdracht3lichtregulering-1
:class: dropdown
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
```
````

### Deel 2: drie standen en twee kleuren
```{exercise} Opdracht: maak toestandsdiagram lichtregulering deel 2
:label: opdracht3lichtregulering-2

Breidt het systeem uit de vorige opgave uit. De lamp heeft twee kleuren (rood en blauw). Er wordt een derde knop (C) toegevoegd waarmee kan worden gewisseld tussen de kleur rood en de kleur blauw. Pas het toestandsdiagram hier op aan.

Probeer het eerst zelf, voordat je de uitwerking bekijkt.
```

````{solution} opdracht3lichtregulering-2
:class: dropdown
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-5379568

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

````

```{exercise} Geen acties bij toestandsovergangen
:label: opdracht3geenacties
Aan de linkerkant van het laatste toestandsdiagram in de uitwerking van de vorige opgave staan twee toestandsovergangen zonder actie:

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

