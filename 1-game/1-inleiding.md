# Inleiding

## Leeswijzer

Dit is een opdracht waar je één of twee maanden aan gaat werken. De opdracht bestaat uit basisstappen en uitbreidingen. Met de basisstappen maak je een eenvoudig spel waarin je één level kunt spelen. Daarna ga je verder met de uitbreidingen. Je kunt zelf kiezen welke uitbreidingen je gaat maken.

```{figure} scherm1.png
Voorbeeld van een spelletje.
```

Elke basisstap bestaat uit een opdracht, toelichting en tips. In de opdracht staat wat je code moet doen. Lees dit aandachtig door, voordat je begint te coderen. De toelichting geeft aan hoe je de opdracht kunt maken. Een ervaren programmeur kan vaak zonder toelichting de opdracht maken. De tips kun je bekijken als je er niet uitkomt. Bekijk de tips één voor één van boven naar beneden en probeer na elke tip of je verder met de opdracht komt. Bij sommige stappen zijn de laatste tips bedoeld om je meer aan het denken te zetten over wat je gemaakt hebt.

Bij de uitbreidingen heb je meer vrijheid. Ze zijn minder ver uitgewerkt. Daardoor zijn die moeilijker dan de basisstappen. Je leert zelfstandig kleine of grotere uitbreidingen toe te voegen aan bestaande code. Hoe beter je daarin wordt, hoe meer functies uit je eigen fantasie jij kunt maken!

## Geschiedenis

### Arcadekasten
```{figure} arcade.jpg
Plaatje van https://commons.wikimedia.org/wiki/File:Four_Arcade_Games.jpg
```

In de jaren 80 van de vorige eeuw waren Arcadekasten erg populair. Arcadekasten vond je in uitgaansgelegenheden, soms stonde ze in grote aantallen bij elkaar in een arcadehal. Elke kast had zijn eigen spelletje. Als je geld in de kast stopte, dan kon je een spelletje spelen. Toen er steeds betere spelcomputers bij mensen thuis kwamen, verloor de arcadekast zijn populariteit.

 
### Arkanoid
```{figure} arkanoid.png
Schermafdruk van https://www.youtube.com/watch?v=QCfnri9hefQ
```

Een voorbeeld van een spel dat je kon spelen is Arkanoid. Arkanoid is een game waarbij je blokjes moet wegstoten met een bal. De bal kaatst tegen een plank. De speler beweegt de plank. Als de bal langs de plank schiet, dan ben je af.

## Voorkennis en naslagmateriaal

Voor deze opdracht heb je basiskennis nodig van programmeren in Python. Je hebt basiskennis als je geoefend hebt met variabelen, selectie (if-jes), iteratie (for-loop), functies en lijsten.

```{image} pygame.png
```
Deze opdracht maakt gebruik van Pygame. Pygame is een package voor Python waarmee je gemakkelijker grafische spelletjes kunt programmeren. Je hoeft niet eerder met Pygame geoefend te hebben om deze opdracht te kunnen maken.

```{seealso} Python en Pygame
Als je meer over Python of Pygame wilt weten, dan kun je de volgende naslagwerken gebruiken:

Lesmateriaal met basiskennis over Python
: Fundament Kernprogramma, Domein D: Programmeren -> Ontwikkelen met Python (inloggen nodig)
https://fundament-online.nl/leeromgeving/hoofdstuk.php?id=10500

Uitgebreide informatie over Python
: Begin bij de Tutorial, daarna kun je de Library Reference bekijken, als je alles wilt weten dan bekijk je daarna de Language Reference\
https://docs.python.org/3/

Alle mogelijkheden van de pygame library
: Zoek ze op in de reference guide\
https://www.pygame.org/docs/

De Pygame library beter begrijpen
: Bekijk deze tutorial\
https://realpython.com/pygame-a-primer/

Algoritmes in games
: Bekijk de uitgebreide CS50-cursus van Harvard\
(niet meer onderhouden, maar nog steeds heel goed)\
https://cs50.harvard.edu/games/2018/

Plaatjes
: Je kunt meer plaatjes halen van Game Art\
https://opengameart.org/content/breakout-brick-breaker-tile-set-free
```

## Tools

Voordat je kunt programmeren moet je bekend zijn met het gereedschap (de tools) die je voor deze opdracht gaat gebruiken. 

Je kunt deze opdracht maken in GitHub Codespaces. Dit is een professionele online omgeving die door veel programmeurs gebruikt wordt. GitHub CodeSpaces werkt ook op Chromebooks. Een account op GitHub is gratis en daarmee kun je 60 uur per maand gebruik maken van Codespaces. 

Je docent geeft misschien aan dat je een andere programmeeromgeving moet gebruiken voor deze opdracht. Er zijn veel andere programmeeromgevingen die geschikt zijn om deze opdracht op te maken. Bijvoorbeeld op een computer waar Python en het Pygame package lokaal zijn geïnstalleerd. Op Replit kan deze opdracht niet gemaakt worden. De gratis versie van Replit biedt niet voldoende CPU-capaciteit om een aktiespel dat in Python en Pygame gemaakt is soepel te spelen.

```{seealso} GitHub en Codespaces 
Leerlinghandleiding Codespaces
: Meer informatie over GitHub, Codespaces en VSCode vind je in de [bijlage over Codespaces](#game-codespaces)

Lesmateriaal over Git versiebeheer
: Versiebeheer in GitHub is gebaseerd op Git. Als je met Git wilt oefenen, dan kun je dat doen op
Fundament - Kernprogramma  A: Vaardigheden  9. Versiebeheer met Git (inloggen nodig)\
https://fundament-online.nl/leeromgeving/hoofdstuk.php?id=11352
```

## Werkwijze

-	Je maakt deze opdracht in een team van twee personen. Je docent geeft aan hoe de teams gemaakt worden.
-	Je gebruikt de startcode die je voor deze opdracht krijgt van je docent. 
-	Je volgt het stappenplan in de opdracht. Elke stap of uitbreiding sla je op in GitHub; je maakt per stap minimaal één commit. Uit je commit-message blijkt bij welke stap of uitbreiding de commit hoort.
-	Jullie verdelen het werk eerlijk over de teamleden. Elk teamlid codeert evenveel. Als je samen achter één computer zit, dan wissel je elke stap wie er typt. Elke leerling typt op zijn eigen GitHub-account.
-	Problemen binnen het team meld je zo snel mogelijk bij je docent.

## Inleveren

-	De deadline staat in de lesplanner.
-	De versie van de main branche van je opdracht die op het moment van de deadline in GitHub staat wordt gebruikt voor de beoordeling. Zorg dat je ruim op tijd klaar bent. 
-	Uit de commit-historie van de main branche in GitHub blijkt wie wanneer wat gedaan heeft.
-	Je kunt vragen stellen tot de laatste les voor de deadline.

## Beoordeling

Je krijgt één cijfer per team, maar je docent kan hiervan afwijken als teamleden geen gelijkwaardige bijdrage hebben geleverd. 

Er gelden minimale eisen waaraan je opdracht moet voldoen:
-	Je hebt je gehouden aan de voorgeschreven werkwijze.
-	Je opdracht is fatsoenlijk, dus vrij van beledigende of illegale elementen.
-	Je hebt de opdracht helemaal zelf gemaakt, als richtlijn kun je aanhouden dat je maximaal vijf regels code overneemt van anderen of van een tutorial. 

Opdrachten die niet voldoen aan de minimale eisen krijgen het cijfer 1,0.

Een netjes uitgevoerde opdracht met alle basisstappen zal in de meeste gevallen beoordeeld worden met een voldoende. Om een hoog cijfer te halen moet je creatieve en complexe uitbreidingen toevoegen.

Een concept beoordelingsmodel staat hieronder. Je docent kan tijdens het nakijken aanpassingen doen aan het beoordelingsmodel of de berekening van het cijfer.

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
