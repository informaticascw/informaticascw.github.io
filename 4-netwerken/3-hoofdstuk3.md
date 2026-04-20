(netwerken-h3)=
# Datalink laag

## Inleiding: Foutdetectie

::: {exercise} Klassikaal: 64 bits onthouden.
:label: netwerken-h3-o1
- Een vrijwillige leerling verlaat de klas.
- De klas 49 getallen op het bord. Een getal is 0 of 1. De getallen worden in 7 rijen en 8 kolommen opgeschreven.
- De docent maakt een extra rij en een extra kolom om het extra moeilijk te maken. Er staan nu 8 x 8 = 64 getallen (bits) op het bord.
- De vrijwillige leerling komt terug in het lokaal, krijgt 1 minuut om de getallen uit het hoofd te leren.
- De vrijwillige leerling verlaat het lokaal.
- De klas verandert 1 getal.
- De vrijwllige leerling komt het lokaal in en vertelt welk getal is veranderd.
:::

::: {solution} netwerken-h2-o1
:class: dropdown
Wil je dit ook kunnen? Zoek dan op hoe parity werkt.
:::

## Functie van de datalink
Frames versturen van en naar meerdere computers met een redelijke betrouwbaarheid.

## Wat doen we met fouten
Vooral een probleem bij draadloos.

## Voor wie is het bericht?
MAC-adressen

## Hoe voorkomen we door elkaar praten?
Niet zo'n groot probleem bij LAN's met switches, maar wel bij Wifi.
- detect collision or timeout of ack and retransmit after random time.
