(physcomp-h8)=
# Coderen met toestandsdiagram (opdrachten)
Hier even de relatie met de eerder behandelde toestandsdiagrammen uitleggen, of bij beide dezelfde voorbeelden gebruiken?

## Oefenopdracht: hotelschakelaar
%bron: https://maken.wikiwijs.nl/135429/Cyclus_1___Micro_bit#!page-4889687

``` {exercise} Hotelschakelaar
:label: opdracht8-1
Maak Micro:bit code voor de hotelschakelaar (versie 2). Gebruik het toestandsdiagram met drie toestanden van [](#opdrachgt6-hotelknoppen) uit [hoofdstuk %s](#physcomp-h6).
```
```` {solution} opdracht8-1
:class: dropdown
```{figure} 8-hotelschakeling-code.png
```
````

## Oefenopdracht: lichtregulering
%bron https://maken.wikiwijs.nl/135429/Cyclus_1___Micro_bit#!page-5379783

Bij deze opdracht worden toestandsovergangen met _gebeurtenissen_ gebruikt. 

``` {exercise} Lichtregulering
:label: opdracht8-2a
Maak Micro:bit code voor de lichtregulering (deel 1). Gebruik het toestandsdiagram van [](#opdracht3lichtregulering-1) uit [hoofdstuk %s](#physcomp-h6)
```
``` {solution} opdracht8-2a
:class: dropdown
Er is geen antwoord beschikbaar.
```

``` {exercise} Versterking: Lichtregulering
:label: opdracht8-2b
Maak Micro:bit code voor de lichtregulering (deel 2). Sluit daarvoor een ledje aan op je Micro:bit. Gebruik het toestandsdiagram van [](#opdracht3lichtregulering-2) uit [hoofdstuk %s](#physcomp-h6)
```
``` {solution} opdracht8-2b
:class: dropdown
Tip: In [paragraaf %s](#physcomp-h4-2) staat hoe je een led aansluit op je Micro:bit en hoe je deze kunt dimmen.

Er is geen antwoord beschikbaar.
```

## Oefenopdracht: toegangscode
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4886253

Bij deze opdracht worden toestandsovergangen met _gebeurtenissen_ gebruikt. 

Het volgende toestandsdiagram beschrijft een systeem voor toegang tot een beveiligde omgeving. Het systeem bestaat uit twee drukknoppen, A en B. Om toegang te krijgen tot het systeem moet de gebruiker de knopjes indrukken in de juiste volgorde. Dan gaat de deur van het slot. Zodra iemand er doorheen loopt valt de deur automatisch weer in het slot.

```{figure} 8-toegangscode-td.png
Toestandsdiagram voor toegangscode.
```

``` {exercise} Toegangscode vraag a)
:label: opdracht8-3a
Toegangscode
Vul aan. \
Als iemand de knoppen ABA invoert, dan is het systeem in toestand ... .\
Om de deur te openen moeten de volgende knoppen worden ingedrukt: ...
```
``` {solution} opdracht8-3a
:class: dropdown
Vul aan. \
Als iemand de knoppen ABA invoert, dan is het systeem in toestand `2`` . 
Om de deur te openen moeten de volgende knoppen worden ingedrukt: `AAB`
```

``` {exercise} Toegangscode vraag b)
:label: opdracht8-3b
Opdracht: toegangscode

Pas nu het toestandsdiagram aan zodat de deur open gaat bij de code ABBA.
```
``` {solution} opdracht8-3b
:class: dropdown

Tip: je hebt 4 toestanden nodig.

Geen antwoord beschikbaar.
```

``` {exercise} Toegangscode vraag c)
:label: opdracht8-3c
Maak nu een in pseudocode op basis van het bovenstaande toestandsdiagram uit de vorige vraag.
```
``` {solution} opdracht8-3c
:class: dropdown

Geen antwoord beschikbaar.
```

``` {exercise} Toegangscode vraag d)
:label: opdracht8-3d
Maak nu de Micro:bit code op basis van de pseudocode uit de vorige vraag.
```
``` {solution} opdracht8-3d
:class: dropdown

Geen antwoord beschikbaar.
```

``` {exercise} Toegangscode vraag e)
:label: opdracht8-3e
Ga nu uit van 3 knoppen: A, B en C. De kluis moet opengaan met de volgende twee codes:
- ABCA. Maar ook bijvoorbeeld AABCA, ABABCA. Zolang het maar eindigt op ABCA.
- ABBA. Ook hier geldt: zolang het maar eindigt op ABBA.

Maak het toestandsdiagram en de pseudocode. Sluit knop C aan op de Micro:bit en maak de Micro:bit code.
```
``` {solution} opdracht8-3e
:class: dropdown

Test je schakeling, klopt de werking met de beschrijving?
```
