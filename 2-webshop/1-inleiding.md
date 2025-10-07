# Inleiding

## Leeswijzer

Dit is een opdracht waar je één of twee maanden aan gaat werken. De opdracht bestaat uit meerdere hoofdstukken. Je docent vertelt welke hoofdstukken je moet maken.

Een hoofdstuk bevat uitleg en opdrachten. In de opdracht staat wat je code moet doen. Lees dit aandachtig door, voordat je begint te coderen. Bij een opdracht staan tips die je kunt gebruiken als je er niet uitkomt. Bekijk de tips één voor één van boven naar beneden en probeer na elke tip of je verder met de opdracht komt.

De eerste hoofdstukken werk je aan functionaliteit voor je webshop. Je maakt daarvoor gebruik van de producten (smurfen) die al in de startcode zijn opgenomen. Als je toe bent aan de uitbreidingen, dan kun je zelf kiezen welke producten je in je webshop aanbiedt. Denk aan kleding, sieraden, clubshirts, telefoons, auto's, eten of iets anders dat jij leuk vindt. Zorg ervoor dat het netjes blijft, vraag het aan je docent als je twijfelt.

## Webshop

Je webshop bevat een plaatje en informatie over wat je verkoopt. Bezoekers kunnen filteren welke producten ze willen zien. Ze kunnen bestellen door je een mailtje te sturen.

Bezoekers kunnen niet inloggen op je webshop en er zit geen betaalmogelijkheid in de webshop. Dat maakt de webshop een stuk eenvoudiger. Bezoekers die willen bestellen sturen een mailte (of appje). De webshop houdt geen winkelmand, geen oude bestellingen en geen voorraad bij.

Je webshop maak je in een ontwikkelomgeving. Zodra je de ontwikkelomgeving afsluit, is je webshop niet meer bereikbaar. Als je wilt dat je webshop altijd bereikbaar is, dan moet je je code neerzetten op een server die altijd bereikbaar is. Dat noemen ze hosten. Je kunt een oude server gebruiken die je thuis hebt, of er eentje bij een bedrijf huren. Je webshop heeft een server met het Unix-besturingssysteem nodig. Als je dit wilt doen dan heb je handigheid met Unix nodig. Het hosten van je webshop is geen onderdeel van deze opdracht. 

## Voorkennis en naslagmateriaal

Voor deze opdracht heb je basiskennis nodig van SQL. Basiskennis van SQL betekent dat je opdrachten gemaakt hebt met `SELECT`, `WHERE`, `JOIN` en `GROUP BY`. 

Voor hoofdstuk 6 (filters) heb je tevens basiskennis nodig van Python. Je hebt basiskennis als je geoefend hebt met variabelen, selectie (if-jes), iteratie (for-loop), functies en lijsten.

Voor hoofdstuk 7 (client) heb je tevens basiskennis nodig van html en css. Je komt in dit hoofdstuk ook in aanraking met JavaScript.

```{seealso} Naslagmateriaal
Als je meer over de gebruikte technieken wilt weten, dan kun je de volgende naslagwerken gebruiken:

Lesmateriaal met basiskennis over SQL
: Fundament Kernprogramma, Domein C: Informatie -> C5 Databases en SQL (inloggen nodig)\
https://fundament-online.nl/leeromgeving/hoofdstuk.php?id=10497

Lesmateriaal met basiskennis over Python
: Fundament Kernprogramma, Domein D: Programmeren -> Ontwikkelen met Python (inloggen nodig)\
https://fundament-online.nl/leeromgeving/hoofdstuk.php?id=10500

Uitgebreide informatie over Python
: Begin bij de Tutorial, daarna kun je de Library Reference bekijken, als je alles wilt weten dan bekijk je daarna de Language Reference\
https://docs.python.org/3/

Uitgebreide informatie over HTML, CSS en Javascript
: W3schools biedt uitgebreide en tegelijk praktische informatie over html, css en javascript
: html op https://www.w3schools.com/html/default.asp 
: css op https://www.w3schools.com/css/default.asp
: javascript op https://www.w3schools.com/js/default.asp

```

## Tools

Voordat je kunt programmeren moet je bekend zijn met het gereedschap (de tools) die je voor deze opdracht gaat gebruiken. 

Je kunt deze opdracht maken in GitHub Codespaces. Dit is een professionele online omgeving die door veel programmeurs gebruikt wordt. GitHub CodeSpaces werkt op alle computers met een moderne browser, ook op Chromebooks. Een account op GitHub is gratis en daarmee kun je 60 uur per maand gebruik maken van Codespaces. Je docent geeft misschien aan dat je een andere programmeeromgeving moet gebruiken voor deze opdracht. 

```{seealso} GitHub en Codespaces 
Leerlinghandleiding Codespaces
: Meer informatie over GitHub, Codespaces en VSCode vind je in de [bijlage over Codespaces](#webshop-codespaces)

Lesmateriaal over Git versiebeheer
: Versiebeheer in GitHub is gebaseerd op Git. Als je met Git wilt oefenen, dan kun je dat doen op
Fundament - Kernprogramma  A: Vaardigheden  9. Versiebeheer met Git (inloggen nodig)\
https://fundament-online.nl/leeromgeving/hoofdstuk.php?id=11352
```

## Werkwijze

Je werkt op de volgende manier aan de opdrachten.

- Je gebruikt de startcode die je van de docent krijgt en je volgt de opdrachten.
- Je werkt regelmatig, minimaal één keer per les sla je werk op, dat doe je door een commit in github te zetten.
- Als je in een groepje werkt, dan programmeert iedereen even veel. De opdrachten in hoofdstuk 1 tot en met 6 maak je samen, de uitbreidingen in hoofdstuk 7 mag je verdelen.
- Je werkt op je eigen account. Als je samen aan dezelfde opdracht werkt dan gebruik je het account van degene die typt, na elke opdracht wissel je wie typt en wiens account gebruik wordt.
- Als je bronnen gebruikt, dan zet je een verwijzing naar de bron als commentaar in je code. Verwijzingen zijn linken chats op chat-gpt, tutorials op youtube of webpagina's. In elk geval moet duidelijk zijn welke stukken code je helemaal zelf hebt bedacht en waar je hulp hebt gehad. 

## Inleveren

- De deadline staat in de lesplanner.
- De versie van de main branche van je opdracht die op het moment van de deadline in GitHub staat wordt gebruikt voor de beoordeling. Zorg dat je ruim op tijd klaar bent. 
- Uit de commit-historie van de main branche in GitHub blijkt wie wanneer wat gedaan heeft.
- Als je uitbreidingen op de opdracht hebt gemaakt, dan zijn die toegevoegd aan het lijstje in het bestand `uitbreidingen.md`
- Je kunt vragen stellen tot de laatste les voor de deadline.

## Beoordeling

Je krijgt één cijfer per team, maar je docent kan hiervan afwijken als teamleden geen gelijkwaardige bijdrage hebben geleverd. 

Er gelden minimale eisen waaraan je opdracht moet voldoen:
-	Je hebt je gehouden aan de voorgeschreven werkwijze.
-	Je opdracht is fatsoenlijk, dus vrij van beledigende of illegale elementen.
-	Je hebt de opdracht helemaal zelf gemaakt, als richtlijn kun je aanhouden dat je maximaal vijf regels code overneemt van anderen of van een tutorial. 
Opdrachten die niet voldoen aan de minimale eisen krijgen het cijfer 1,0.

Een netjes uitgevoerde opdracht met alle basisstappen zal in de meeste gevallen beoordeeld worden met een voldoende. Om een hoog cijfer te halen moet je creatieve en complexe uitbreidingen toevoegen.

Een concept beoordelingsmodel staat hieronder. Je docent kan tijdens het nakijken aanpassingen doen aan het beoordelingsmodel of de berekening van het cijfer.

```{attention} Beoordelingsmodel

Dit beoordelingsmodel is een voorbeeld van een andere opdracht, je krijgt meer informatie van je docent. Hou er rekening mee dat je eigen creatieve uitbreidingen moet maken om een hoog cijfer te halen. Om een voldoende te halen zul je ook een korte toets met multiple choice vragen moeten maken om te kijken of je de opdrachten begrepen hebt. 

```

Onderdeel|Punten havo|Punten vwo|Toelichting 
-|-|-|-
**Code**
Stijl|5|5|- Netjes uitgelijnd,<br> - helder commentaar, <br>- logische naamgeving van variabelen, <br>- logische volgorde van opdrachten, <br>- consistente code.
Basiscode|20|15|- If-opdrachten goed toegepast, vergelijkingsoperatoren </>/== gebruikt, logische operatoren and/or gebruikt, <br>- lijsten toegepast, <br>- for (of while)-opdrachten toegepast, <br>- code kan omgaan met verschillende lengtes van lijsten (len goed gebruikt),<br>- code wijzigt aantal elementen in lijst tijdens het runnen.
Uitbreidingen (maantjes)|15|20|- Uitbreidingen gemaakt met technieken die in de opdracht behandeld zijn, zoals meer loops, meer lijsten, meer functies (1 maantje)<br>- uitbreidingen gemaakt met technieken die niet in de opdracht behandeld zijn en je je zelfstandig hebt eigen gemaakt, zoals dicts, geneste loop, lijst in lijst (2 maantjes).
**Functionaliteit**	 	 
Speelbaarheid|5|5|- geen glitches<br>- soepele bediening
Basisfunctionaliteit|20|15|- Bal stuitert tegen randen,<br>- plank beweegt en stopt aan de rand van het scherm en laat bal stuiteren, <br>- 1 blok waartegen bal stuitert,<br>- meer dan 10 blokken waartegen bal stuitert,<br>- blokken verdwijnen, je kunt af gaan en winnen.
Uitbreidingen (zonnetjes)|15|20|Uitbreidingen in het spel die zorgen voor diversiteit en hoe beter je wordt hoe leuker of moeilijker het wordt, <br>- voorbeelden van kleine uitbreidingen (1 zonnetje) zijn steeds snellere bal, verschillende kleuren blokken,<br>- voorbeelden van grotere uitbreidingen (2 zonnetjes) zijn meer levels, ingewikkelde powerups zoals blokken wegschieten, veel ballen.             
**Proces**	 
Planning|5|5|Uit de commits en/of tijdens de les blijkt dat het stappenplan gevolgd is en dat er regelmatig is gewerkt.
Samenwerking|5|5|Uit de commits en/of tijdens de les blijkt dat het werk gelijk verdeeld is onder teamleden. Als één teamlid beduidend minder doet, dan is dat een gezamenlijke verantwoordelijkheid van het team om dat op te lossen of te melden bij de docent. Maak vanaf het begin afspraken en spreek elkaar daarop aan. Als je er niet uitkomt, dan meld je dat zo snel mogelijk bij je docent.

Cijfer = 1 + 9 * behaalde punten / maximale punten
