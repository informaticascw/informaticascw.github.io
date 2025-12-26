# Uitbreidingen

```{figure} scherm7.png
Schermafdruk van een voorbeeld van een spelletje aan het einde van dit hoofdstuk.
```

```{figure} scherm6.png
Schermafdruk van een voorbeeld van een webshop aan het einde van dit hoofdstuk.
```

Nu je basisgame af is kan het echte werk beginnen. Voeg een aantal uitbreidingen toe aan je game. Gebruik je creativiteit en laat zien dat je complexere code aankunt. 

## Arcadekast

Als je wilt dat je spel gespeeld kan worden in de arcadekast op school, dan moet je aan de volgende eisen voldoen:

1. Je spel gebruikt de toetsen uit de onderstaande toetsenbord-mapping.
2. Het bestand `metadata.json` in de hoofdmap van je startcode heb je aangepast.
3. De inhoud van het bestand `screenshot.jpg` heb je vervangen door een schermafdruk van jouw spel (maximaal 300 Kb).

```{figure} arcade-keys.png
Toetsenbord-mapping van de arcadekast.
```

## Opdracht: Uitbreidingen maken

Je kunt je game uniek maken door er uitbreidingen aan toe te voegen. Je kunt daarvoor ideeën uit de lijst hieronder gebruiken, maar het is natuurlijk het leukst als je creatief bent en zelf iets verzint. 

```{attention} Ideeen voor uitbreidingen
Ter inspiratie staan hier een aantal ideeën voor uitbreidingen. Uitbreidingen met één of twee sterren zijn eenvoudiger dan uitbreidingen met drie of vier sterren.

```{attention} Ideeen voor uitbreidingen
Uitbreiding: Bal die steeds sneller gaat ⭐️
: Een eenvoudige manier om dit te doen, is telkens als er een blok verwijderd wordt, de snelheid van het blok in de x en y richting te vermenigvuldigen met een kommagetal dat groter is dan 1.0. Op deze manier kan het met twee regels code en maakt je spelletje een heel klein beetje spannender. Dit is een makkelijke uitbreiding, nog niet genoeg om een maantje of zonnetje te verdienen.

Uitbreiding: Blokken die van kleur veranderen ⭐️ of ⭐️⭐️
: Een eenvoudige manier om dit te doen, is plaatjes van blokken met een andere kleur inlezen en dan meerdere blokken op dezelfde plek zetten.

Uitbreiding: Beter kaats-algoritme voor plankje ⭐️ of ⭐️⭐️
: In het basisspel kaatst de bal erg eenvoudig tegen de plank. Als je de horizontale snelheid waarmee de bal de plank verlaat, laat afhangen van de plek waar de bal de plank raakt, dan wordt het spel beter speelbaar.

Uitbreiding: Uitlegscherm en gameoverscherm ⭐️ of ⭐️⭐️
: Maak een scherm met uitleg voordat je het spel start en/of een game-over-scherm als je gewonnen of verloren hebt. Dit kan bijvoorbeeld door een variabele `game_status` erbij te maken. Je kunt je gameloop opdelen in een stuk voor uitleg, spelen, winnen en verliezen. De waarde van de variabele `game_status` bepaalt dan welk stuk van de game-loop wordt uitgevoerd.

Uitbreiding: Animaties als een blok verdwijnt ⭐️⭐️⭐️
: Laat een blok niet in één keer verdwijnen, maar toon een effect als het blok verdwijnt. Een effect kan bijvoorbeeld zijn dat het blok snel naar boven uit het scherm vliegt. Het lastige is dat je game moet doorgaan terwijl het effect getoond wordt. Je zult dus elke keer in je game-loop een stukje effect moeten tonen.

Uitbreiding: Powerups die omlaag vallen ⭐️⭐️⭐️ of ⭐️⭐️⭐️⭐️
: Laat bepaalde blokken omlaag vallen als de bal ze raakt en geef extra punten als je je het vallende blok opvangt met je plank.

Uitbreiding: Meerdere levels ⭐️⭐️ of ⭐️⭐️⭐️ of ⭐️⭐️⭐️⭐️
: Maak meerdere levels in het spel. Probeer daarbij zo min mogelijk code te dubbelen.

Uitbreiding: Meerdere ballen tegelijk ⭐️⭐️⭐️ of ⭐️⭐️⭐️⭐️
: Laat voor een bepaalde tijd meerdere ballen in het spel als er een speciaal blok geraakt wordt.
Gebruik array’s om meer dan twee ballen tegelijk te kunnen hebben. Gebruikt een geneste loop om de botsingen van alle ballen tegen alle blokken te maken

Uitbreiding: Schieten ⭐️⭐️⭐️ of ⭐️⭐️⭐️⭐️
: Zorg dat je plank met kogels blokken weg kan schieten als de bal een speciaal blok raakt. 
Gebruikt array’s om meerdere kogels tegelijk te kunnen schieten.

Uitbreiding: Overleg met je docent voor andere uitbreidingen
: Verzin zelf een uitbreiding die je helemaal te gek vindt. Je docent kan je helpen om je idee in stappen op te splitsen, zodat het uitvoerbaar wordt. 
```

:::{note}Opdracht a)
### Maak een uitbreiding
Kies een uitbreiding uit de ideeën hierboven of verzin zelf een uitbreiding. Maak de uitbreiding en geef in de beschrijving van de commit(s) aan om welke uitbreiding het gaat. In het bestand `uitbreidingen.md` hou je een lijst bij van uitbreidingen die je gemaakt hebt.

Als je een uitbreiding klaar hebt, dan kies je een nieuwe uitbreiding. Zo herhaal je deze opdracht totdat je game helemaal naar jullie zin is.
:::

```{hint} Tips
:class: dropdown
- Begin met enkele kleine uitbreiding, probeer daarna pas de grotere uitbreidingen.
- Maak afspraken met elkaar wie welke uitbreiding maakt, probeer te zorgen dat je niet tegelijk in hetzelfde stuk code hoeft te werken.
```
