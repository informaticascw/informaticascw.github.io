
# Soort aan product toevoegen
1:n relaties toevoegen

## maak tabel met soorten (database)
create table
insert

## maak veld dat product aan soort koppelt (database)
voeg verwijzende sleutel toe
laat de naam eindigen op _id, dan kan onze website er goed mee omgaan

## beschrijf cardinaliteit (database)
voeg constraint toe

## koppel producten aan soort (database)
vul verwijzingen in

## api (uitleg)
api verbindt de database met de website

back end: api en database
front end: website

webserver voor static files, bij ons in de api, bij grotere projecten vaak op aparte servers. Database draait ook vaak op één of meerdere aparte servers.

## voeg soort toe aan query (api)
api aanpassing: query met join

## niet benodigde velden verwijderen (niet nodig, verwijderen) / namen van velden aanpassen (api)
speciale velden: name, price, description uit de tabel products worden herkend in de html en op speciale wijze getoond
het veld id de tabel products en velden die eindigen op _id worden herkend in de html en niet getoond, deze zijn wel handig om erin te houden

de website gebruikt de naam van de velden, meestal zijn die Engelstalig. Het is handig om die in de api aan te passen
AS gebruiken
