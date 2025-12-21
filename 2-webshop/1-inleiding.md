# Inleiding

## Leeswijzer

Dit is een opdracht waar je één of twee maanden aan gaat werken. De opdracht bestaat uit meerdere hoofdstukken. Je docent vertelt welke hoofdstukken je moet maken.

Een hoofdstuk bevat uitleg en opdrachten. In de opdracht staat wat je code moet doen. Lees dit aandachtig door, voordat je begint te coderen. Bij een opdracht staan tips die je kunt gebruiken als je er niet uitkomt. Bekijk de tips één voor één van boven naar beneden en probeer na elke tip of je verder met de opdracht komt.

## Webshop

Je webshop bevat een plaatje en informatie over wat je verkoopt. Bezoekers kunnen filteren welke producten ze willen zien. Ze kunnen bestellen door je een mailtje te sturen.

Bezoekers kunnen niet inloggen op je webshop en er zit geen betaalmogelijkheid in de webshop. Dat maakt de webshop een stuk eenvoudiger. Bezoekers die willen bestellen sturen een mailtje (of appje). De webshop houdt geen winkelmand, geen oude bestellingen en geen voorraad bij.

Je webshop maak je in een ontwikkelomgeving. Zodra je de ontwikkelomgeving afsluit, is je webshop niet meer bereikbaar. Als je wilt dat je webshop altijd bereikbaar is, dan moet je je code neerzetten op een server die altijd bereikbaar is. Dat noemen ze hosten. Je kunt een oude server gebruiken die je thuis hebt, of er eentje bij een bedrijf huren. Je webshop heeft een server met het Unix-besturingssysteem nodig. Als je dit wilt doen dan heb je handigheid met Unix nodig. Het hosten van je webshop is geen onderdeel van deze opdracht. 

## Voorkennis en naslagmateriaal

Voor deze opdracht heb je basiskennis nodig van SQL. Basiskennis van SQL betekent dat je opdrachten gemaakt hebt met `SELECT`, `WHERE`, `JOIN` en `GROUP BY`. 

Voor hoofdstuk 6 (filters) heb je tevens basiskennis nodig van Python. Je hebt basiskennis als je geoefend hebt met variabelen, selectie (if-jes), iteratie (for-loop), functies en lijsten.

Voor hoofdstuk 7 (client) heb je tevens basiskennis nodig van HTML en CSS. Je komt in dit hoofdstuk ook in aanraking met JavaScript.

```{seealso} Naslagmateriaal
Als je meer over de gebruikte technieken wilt weten, dan kun je de volgende naslagwerken gebruiken:

Lesmateriaal met basiskennis over SQL
: Fundament Kernprogramma, Domein C: Informatie -> C5 Databases en SQL (inloggen nodig)\
https://fundament-online.nl/leeromgeving/hoofdstuk.php?id=10497

Uitgebreide informatie over SQL
: W3schools biedt uitgebreide en tegelijk praktische informatie over SQL. Gebruik de MySQL variant, die lijkt erg veel op de SQLite variant die de webshop gebruikt
: https://www.w3schools.com/sql/

Lesmateriaal met basiskennis over Python
: Fundament Kernprogramma, Domein D: Programmeren -> Ontwikkelen met Python (inloggen nodig)
: https://fundament-online.nl/leeromgeving/hoofdstuk.php?id=10500

Uitgebreide informatie over Python
: Begin bij de Tutorial, daarna kun je de Library Reference bekijken, als je alles wilt weten dan bekijk je daarna de Language Reference
: https://docs.python.org/3/

Lesmateriaal met basiskennis over HTML en CSS
: Fundament Kernprogramma, Domein A: Vaardigheden -> HTML & CSS (2025) (inloggen nodig)
: https://fundament-online.nl/leeromgeving/hoofdstuk.php?id=12181

Uitgebreide informatie over HTML, CSS en JavaScript
: W3schools biedt uitgebreide en tegelijk praktische informatie over HTML, CSS en JavaScript
: HTML op https://www.w3schools.com/html/
: CSS op https://www.w3schools.com/css/
: JavaScript op https://www.w3schools.com/js/
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

- Je maakt deze opdracht in een team van twee personen. Je docent geeft aan hoe de teams gemaakt worden.
- Je gebruikt de startcode die je van de docent krijgt en je volgt de opdrachten.
- Je werkt regelmatig, minimaal één keer per les sla je werk op, dat doe je door een commit in github te zetten.
- Als je in een groepje werkt, dan programmeert iedereen evenveel. De opdrachten in hoofdstuk 1 tot en met 7 maak je samen, de uitbreidingen in hoofdstuk 8 mag je verdelen.
- Je werkt op je eigen account. Als je samen aan dezelfde opdracht werkt dan gebruik je het account van degene die typt, na elke opdracht wissel je wie typt en wiens account gebruik wordt.
- Als je bronnen gebruikt, dan zet je een verwijzing naar de bron als commentaar in je code. Verwijzingen zijn linken chats op chat-gpt, tutorials op youtube of webpagina's. In elk geval moet duidelijk zijn welke stukken code je helemaal zelf hebt bedacht en waar je hulp hebt gehad. 

## Inleveren

- De deadline staat in de lesplanner.
- De versie van de main branche van je opdracht die op het moment van de deadline in GitHub staat wordt gebruikt voor de beoordeling. Zorg dat je ruim op tijd klaar bent. 
- Uit de commit-historie van de main branche in GitHub blijkt wie wanneer wat gedaan heeft.
- Als je uitbreidingen op de opdracht hebt gemaakt, dan zijn die toegevoegd aan het lijstje in het bestand `uitbreidingen.md`
- Je kunt vragen stellen tot de laatste les voor de deadline.

(webshop-beoordeling)=
## Beoordeling

De opdracht die je inlevert wordt grotendeels per team beoordeeld, maar je docent kan hiervan afwijken als teamleden geen gelijkwaardige bijdrage hebben geleverd. 
Een netjes uitgevoerde opdracht waarvan je alle basisstappen begrepen hebt, zal in de meeste gevallen beoordeeld worden met een voldoende. Om een hoog cijfer te halen moet je creatieve en complexe uitbreidingen toevoegen.

**Minimale eisen**

Er gelden minimale eisen waaraan je opdracht moet voldoen:
-	Je hebt je gehouden aan de voorgeschreven werkwijze.
-	Je opdracht is fatsoenlijk, dus vrij van beledigende of illegale elementen.
-	Je hebt de opdracht helemaal zelf gemaakt, als richtlijn kun je aanhouden dat je maximaal vijf regels code overneemt van anderen of van een tutorial.

Opdrachten die niet voldoen aan de minimale eisen krijgen het cijfer 1,0.

**Test**

Een beperkt deel van je eindcijfer wordt bepaald door een test. 
- De test wordt individueel beoordeeld. 
- Tijdens de test laat je zien dat je de opgaven die je gemaakt hebt begrijpt. 
- Het is niet nodig om voor de test te leren. 
- De test bestaat uit multiple choice vragen en duurt ongeveer een kwartier. 
- Je docent geeft drie momenten op verschillende dagen waarop je de test kunt maken. 
- Je mag de test maximaal twee keer doen, de hoogste score telt. 

Als je de test geen enkele keer maakt, dan is je score voor de test 0 punten.

**Beoordelingsmodel**

Een concept beoordelingsmodel staat hieronder. Je docent kan tijdens het nakijken aanpassingen doen aan het beoordelingsmodel of de berekening van het cijfer.

Onderdeel|Punten havo|Punten vwo|Toelichting 
-|-|-|-
**Code**
Stijl|5|5|- Netjes uitgelijnd,<br> - helder commentaar, <br>- logische naamgeving van variabelen, <br>- logische volgorde van opdrachten, <br>- consistente code.
Basistest|20|15|- Score op test met multiple-choice vragen over de basisopdrachten (hoofdstuk 2 tot en met 7, zonder uitbreidingen)
**Functionaliteit**
Gebruikerservaring|5|5|- Geen slordigheden in opmaak<br>- Logische indeling / producten vindbaar
Basisfunctionaliteit|20|15|- Hoofdtuk 3: minimaal 5 artikelen met plaatjes, prijs en beschrijving,<br>- hoofdtuk 4: 1:n relatie,<br>- hoofdtuk 5: n:m relatie,<br>- hoofdtuk 6: filters,<br>- hoofdtuk 7: client aanpassingen.<br>- Punten per hoofdstuk is totaal aantal punten gedeeld door aantal hoofdstukken dat gemaakt moest worden. Voor een hoofdstuk krijg je alle punten als het geheel volgens de opdracht is gemaakt.             
**Uitbreidingen**
Eenvoudige uitbreidingen|15|20|- Eenvoudige uitbreidingen zijn uitbreidingen van één of twee sterren. Elke ster is een punt.
Ingewikkelder uitbreidingen|15|20|- Ingewikkelder uitbreidingen zijn uitbreidingen van drie of vier sterren. Elke ster is een punt.
**Proces**	 
Planning|5|5|Uit de commits en/of tijdens de les blijkt dat het stappenplan gevolgd is en dat er regelmatig is gewerkt.
Samenwerking|5|5|Uit de commits en/of tijdens de les blijkt dat het werk gelijk verdeeld is onder teamleden. Als één teamlid beduidend minder doet, dan is dat een gezamenlijke verantwoordelijkheid van het team om dat op te lossen of te melden bij de docent. Maak vanaf het begin afspraken en spreek elkaar daarop aan. Als je er niet uitkomt, dan meld je dat zo snel mogelijk bij je docent.

Cijfer = 1 + 9 * behaalde punten / maximale punten
