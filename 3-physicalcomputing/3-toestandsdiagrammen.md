# Toestandsdiagrammen

## Voorbeeld: Toestanden in games

### Inleiding
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4855353

In deze module leer je te werken met toestandsdiagrammen. Als introductie daarop kun je met de gehele klas de volgende opdracht doen.

```{note} Opdracht: Toestanden in games
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
Toestanden in game
```

Je kunt in het toestandsdiagram bijvoorbeeld zien dat als de bewaker in toestand 1 is en hij ziet een vijand, dan wordt de toestand van de bewaker 2.

In de bovenstaande uitwerking zie je totaal 5 toestanden en 6 toestandsovergangen. Misschien zijn er wel meer hoor, alleen in dit korte fragment kun je ze niet allemaal zien.

Het losse pijltje naar toestand 1 betekent dat dit de begintoestand is, oftewel de initiële toestand.

```{note} Opdracht: Unplugged Nooddienstregeling bij de spoorwegen
Je kunt ook als inleiding ook de unplugged activiteit doen die je via de onderstaande link vindt.

[Nooddienstregeling bij de spoorwegen](http://www.informaticaunplugged.nl/de-werkvormen/nooddienstregeling-bij-de-spoorwegen/)
```

## Voorbeeld: Frisdrankautomaat

### Frisdrankautomaat
%bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4875018

### Acties in een toestandsdiagram
%bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4875030

## Correcte toestandsdiagrammen

### Tabel met alle toestandsovergangen
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4875031

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
:class: dropdown
Je kunt toestandsdiagrammen prima op papier tekenen. Dat gaat vaak het snelst, maar pas op dat het wel leesbaar blijft. Een handige tool om toestandsdiagrammen mee te maken vind je via de volgende site.

[Finite State Machine Designer](http://madebyevan.com/fsm/)
```