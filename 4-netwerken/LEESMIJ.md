# Uitpakken in GitHub

Vervang de inhoud van `4-netwerken/` in je repository door de inhoud van dit archief. Er is geen extra buitenmap en geen eigen `myst.yml`. De bestaande inhoudsopgave met `4-netwerken/*-*.md` blijft bruikbaar.

Verwijder de oude bestanden die dit pakket vervangt, anders blijven die ook in de inhoudsopgave staan. Dat geldt bij deze herziening onder meer voor `03-netwerken-scheiden.md`, `12-aantonen.md` en `13-verdieping.md`. De oude inhoud is samengevoegd of verplaatst; laat die niet naast de nieuwe hoofdstukken staan.

## Nieuwe ordening

1. Bits versturen
2. Een lokaal netwerk
3. Lagen en inkapseling
4. IP-netwerken en subnetten
5. ARP en de standaardgateway
6. Door meerdere netwerken
7. Het juiste programma bereiken
8. Een website opvragen
9. Verbinden en beschermen
10. Van URL naar webpagina
11. Praktische eindopdracht — beide beoordelingslessen in één hoofdstuk

`90-verdieping.md`, `99-begrippenlijst.md`, `100-docent.md` en de startpagina tellen niet mee als hoofdstuk. De startpagina heeft geen nummering, zodat haar twee tussenkoppen de nummers 1 en 2 niet opgebruiken. Binnen de hoofdstukken zijn handmatig toegevoegde paragraafnummers verwijderd: de bestaande MyST-configuratie verzorgt de nummering.

## Begrippen en paden

De definities staan één keer in `99-begrippenlijst.md`. De hoofdstukken linken met de MyST term-rol naar die definities. De complete leesversie staat buiten de hoofdstukwildcard in `extra/leesversie.md` en kopieert de glossary niet. Publiceer die leesversie niet daarnaast als extra MyST-hoofdstuk; daarin worden de hoofdstukken immers herhaald.

Afbeeldingen staan in `images/`. Alle interne paden zijn relatief. Als je een andere modulemap kiest, pas je alleen de moduleverwijzing en wildcard in de hoofdconfiguratie aan; de onderlinge bestandsverwijzingen blijven werken.

Het pakket is niet gepubliceerd. De uitleg, referenties en bronstructuur worden gecontroleerd; de Filius-opstellingen en lestijden zijn nog niet praktisch getest.
