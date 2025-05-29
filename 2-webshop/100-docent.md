---
numbering:
    heading_2:
        enabled: false
---
# Voor de docent

## Voorkennis en leerdoelen

Veronderstelde voorkennis voor leerlingen
- database: sql (SELECT, JOIN met 3 tabellen, WHERE, CREATE)
- api: python (variabelen, selectie, iteratie, functies, lijsten)
- website: html en css (kunnen werken met enkele html5 tags en css properties, denk aan h1-3, p, ul/li, a href, img src, div id/class, content/padding/border/margin, color/background-color)

Handige voorkennis, maar niet noodzakelijk
- database: normaliseren van een database
- api: kennis van json en basale kennis van REST api's
- website: javascript, al dan niet in combinatie met het Document Object Model

Leerdoel voor leerlingen
- Opdoen van praktisch inzicht in de werking van hedendaagse webbased systemen die gebruikt worden voor het opvragen van gestructureerde informatie. We beperken we ons tot de context van een webshop.

Leerdoelen in meer detail
- Informatie opvragen met sql uit een database met meerdere tabellen (veronderstelde voorkennis)
- Opzetten van een database met meerdere tabellen in sql
- Bepalen van de cardinaliteit van relaties tussen tabellen (1:n en n:m) in sql
- Begrijpen hoe REST-api's werken aan de hand van begrippen zoals endpoint, CRUD en json
- Uitbreiden van gegeven REST-api's in python met de fastAPI library
- Statische webpagina's in html en css aanpassen en uitbreiden (veronderstelde voorkennis)
- Begrijpen wat DOM manipulatie met de javascript is
- Aanpassen van gegeven javascript programma's die DOM manipulatie doen

## Lesplanner

Hoofdstuk|Aantal lessen|Basis of optioneel
--|--|--
1 Inleiding | 1 | basis
2 Aanpassen | 2 | basis
3 1:n | 2 | basis
4 n:m | 2 | basis
5 Filters | 2 | optioneel
6 Front end | 2 | optioneel
7 Uitbreidingen | 2 tot 8 | optioneel
Totaal | 7 tot 19 |

Opmerkingen:
- We gaan uit van een lesduur van 45 tot 60 minuten per les.
- Hoofdstuk 1, 2, 3 en 4 bouwen op. 
- Hoofdstukken 5 en 6 staan los van elkaar maar bouwen door op hoofdstuk 1, 2, 3 en 4.
- Hoofdstuk 7 kan worden gedaan als 5 en 6 zijn overgeslagen, maar niet alle voorgestelde extra's zullen voor alle leerlingen haalbaar zijn.

## Startcode en uitwerking

Startcode volgt

Uitwerking volgt

Een concept (work in progress) van de code staat op 
[https://github.com/informaticascw/h5v5-sql-webshop-template](https://github.com/informaticascw/h5v5-sql-webshop-template)

## Beoordelingsmodel

volgt

## Ontwikkelomgeving inrichten

Minimale variant voor docenten die niet eerder gewerkt hebben met GitHub.
- Laat leerlingen 1 account per groepje maken
- Laat leerlingen startcode kopieren (use template in GitHub)
- Verzamel de linkjes naar de repositories, zodat je kunt meekijken en nakijken
- Uitleg onder de ontwikkelomgeving staat in de leerlinghandleiding Codespaces (zie bijlage)
- Het kost tijd om de ontwikkelomgeving (GitHub + Codespaces + VSCode en voor docenten ook nog GitHub Classroom) te leren kennen. Een goed begin is het zelf maken van de opdracht.

Varianten voor docenten die ervaring hebben met GitHub.
- Zie minimale variant en voeg daaraan één of meerdere van onderstaande punten toe.
- Groepjes van meerdere personen met elke persoon een eigen account (voordeel: beter voor samenwerken in groepjes, complicatie: toegangsrechten tot repositories per repository instellen en merge conflicten oplossen)
- Inrichten van eigen github organisaties (voordeel: toegang tot repositories voor docenten eenvoudiger)
- Inschrijven via GitHub Classroom (voordeel: toegangsrechten automatisch ingesteld, eenvoudiger voor leerlingen om startcode te krijgen)

Aanbevolen variant voor docenten die ervaring hebben met GitHub Classroom.
- Opdracht met startcode aanmaken in Github Classroom.
- Inschrijflink verspreiden onder leerlingen.

Docentenhandleiding
- Een eerste aanzet vind je op\
https://stanislas.informatica.nu/docenten/codespaces
- Een uitgebreide handleiding, toegespitst op docenten die hun leerlingen deze opdracht willen laten maken, is (nog) niet beschikbaar. 
- Er is veel informatie te vinden op internet, maar het vergt tijd om bekend te raken met de ontwikkelomgeving.
