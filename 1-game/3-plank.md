# Stap 4-9: plank
```{pull-quote}
De bal beweegt, maar je kunt het spel nog niet spelen. Daarom gaan we een plank toevoegen.
````

```{figure} scherm3.png
Schermafdruk van spelletje met basisstap 4 t/m 9.
```

(game-stap-4)=
## Stap 4: Teken de plank

````{note} Opdracht
Teken de plank (Engels: paddle) op het scherm. Gebruik de variabele `paddle_img` om het plaatje van de plank in op te slaan. Gebruik de variabelen `paddle_x` en `paddle_y` om de linkerbovenhoek van de plank aan te geven. Maak de startpositie van de plank ongeveer midden onder op het scherm. Gebruik de constanten `PADDLE_WIDTH` en `PADDLE_HEIGHT` voor de breedte en hoogte van de plank. Maak je plank 144 pixels breed en 32 pixels hoog.
````

````{attention} Toelichting
Kopieer de code van de bal en pas de kopie aan, zodat hij werkt voor de plank.

Regels uit de startcode die het plaatje van de bal inlezen:
```python
ball_img = pygame.Surface((64, 64), pygame.SRCALPHA) # create new image
ball_img.blit(spritesheet, (0, 0), (1403, 652, 64, 64))  # copy part of sheet to image
ball_img = pygame.transform.scale(ball_img, (BALL_WIDTH, BALL_HEIGHT)) # resize image
```

-	De eerste regel maakt een variabele ball_img met een leeg plaatje erin. `(64, 64)` zijn de breedte en hoogte van het plaatje. `pygame.SRCALPHA` zorgt ervoor dat de achtergrond van je plaatje transparant kan zijn.
-	De tweede regel kopieert een stuk uit het spritesheet naar het lege plaatje. `(0, 0)` betekent dat het stukje spritesheet linksboven in je lege plaatje komt. `(1403, 652, 64, 64)` zijn de x, y, width en height van het stuk dat je uit het spritesheet kopieert.
-	De derde regel verkleint het plaatje tot de afmeting die je in de game nodig hebt. `(BALL_WIDTH, BALL_HEIGHT)` is de breedte en hoogte die je nodig hebt in je game.

Regels uit de startcode die het plaatje van de bal op het scherm zetten:
```python
screen.blit(ball_img, (ball_x, ball_y))
```

-	`ball_img` is de naam van de variabele waar het plaatje in zit dat je op het scherm wil zetten. `ball_x` en `ball_y` zijn de linkerbovenhoek van de plek waar het plaatje op het scherm wordt gezet.
````

````{hint} Tips
:class: dropdown
-	De breedte van de plank in het spritesheet is 243 pixels, de hoogte is 64 pixels. Dat is de afmeting die het nieuwe plaatje moet hebben.
-	De plank staat in het spritesheet op x is 1158 en y is 396. Dat is de linkerbovenhoek van het stuk dat je uit het spritesheet moet kopieren.
-	Definieer de constanten `PADDLE_WIDTH` en `PADDLE_HEIGHT` en geef ze de waarde 144 en 32. Dit is de afmeting waarnaar je het plaatje van de paddle moet verkleinen.
-	Maak de variabelen `paddle_x` en `paddle_y` om bij te houden waar de paddle staat. Geef ze een startwaarde, bijvoorbeeld `SCREEN_WIDTH / 2` en `SCREEN_HEIGHT – 100`. Gebruik `paddle_x` en `paddle_y` om de plank op de goede plaats op het scherm te zetten. 
````

(game-stap-5)=
## Stap 5: Beweeg de plank

````{note} Opdracht
Beweeg de plank als de D-toets (rechts) of A-toets (links) is ingedrukt. Beweeg de plank met één pixel per frame. Gebruik `keys` uit de startcode om te zien welke toets momenteel worden ingedrukt.
````

````{attention} Toelichting
Kijken of de D-toets is ingedrukt doe je als volgt:
if keys[pygame.K_d] : # key d is down
````

````{hint} Tips
:class: dropdown
-	Als de D-toets is ingedrukt, beweeg je de plank naar rechts door bij `paddle_x` tien op te tellen. De plank wordt daardoor verderop in de code op een nieuwe plek getekend.
-	Als de A-toets is ingedrukt, beweegt de plank naar links.
-	Gebruik maar één keer de regel `keys = pygame.key.get_pressed()` om de stand van de toetsen te lezen
````

(game-stap-6)=
## Stap 6: Stop de plank aan de randen van het scherm

````{note} Opdracht
Zorg dat de plank niet verder beweegt als hij de rand van het scherm raakt. Gebruik `paddle_x` en `SCREEN_WIDTH` om te kijken of de plank aan de rand is. Gebruik `PADDLE_WIDTH` om rekening te houden met de breedte van de plank.
````

````{attention} Toelichting
Pseudo-code om de plank te laten stoppen aan de rechterkant van het scherm.
```{code} pseudo
:caption: Pseudo-code
:linenos:
als plank_x + plank_breedte > breedte_van_scherm dan
    plank_x = breedte_van_scherm – plank_breedte
```
Maak zelf de Python-code en zet die op een logische plaats in je programma. 
Pseudo-code om de plank te laten stoppen aan de linkerkant van het scherm kun je zelf maken.
````

````{hint} Tips
:class: dropdown
-	`plank_x` in de pseudo-code is `paddle_x` in je code,\
    `breedte_van_scherm` in de pseudo-code is `SCREEN_WIDTH` uit je code en\
    `plank_breedte` uit de pseudo-code is `PADDLE_WIDTH` in je code. 
````

(game-stap-7)=
## Stap 7: Stuiter de bal tegen de plank

````{note} Opdracht
Zorg dat de bal kaatst tegen je plank. Hiervoor zijn veel algoritmen te bedenken. Het algoritme uit deze stap kijkt of een stukje van de bal op dezelfde plek is als een stukje van de plank. Als dat zo is dan wordt de y-richting van de bal negatief gemaakt, zodat de bal omhoog beweegt. 
````

````{attention} Toelichting
```{code} pseudo
:caption: Pseudo-code
:linenos:
  als rechter_kant_bal is groter dan   linker_kant_paddle en 
      linker_kant_bal  is kleiner dan  rechter_kant_paddle en
      onderkant_kant_bal is groter dan boven_kant_paddle en 
      boven_kant_bal  is kleiner dan   onder_kant_paddle dan
          bal_snelheid_y = de positieve waarde van bal_snelheid_y keer -1
```
````

````{hint} Tips
:class: dropdown
-	Gebruik de pseudo-code. Gebruik nu geen ingebouwde functie van pygame om een botsing te detecteren. 
-	Je kunt een lange conditie achter if over meerdere regels spreiden om het leesbaarder te maken. Zet de conditie dan tussen ( en ), bijvoorbeeld
```python
if (x > 100 and 
    x < 200 and 
    y > 50 and 
    y < 150) :
```
-	rechter_kant_bal uit de pseudo-code is `ball_x + BALL_WIDTH` in je code.
-	linker_kant_plank uit de pseudo-code is `paddle_x` in je code.
-	De y-snelheid van de bal moet negatief (kleiner dan nul) zijn om te zorgen dat de bal omhoog beweegt. Want bovenaan het scherm is y gelijk aan nul en hoe verder naar onderen je komt hoe groter de y wordt. 
-	Je kunt de y-snelheid negatief maken door een eventuele min eraf te halen en dan keer -1 te doen. De functie `abs(getal)` geeft als resultaat een getal zonder min. Dus `abs(-2)` is 2 en `abs(2)` is ook 2. Dus `abs(ball_speed_y) * -1` geeft de negatieve waarde van de y-snelheid. 
-	Wat doet het algoritme als de bal tegen de zijkant van de plank kaatst? Wat zou je in het echt verwachten?
-	Hou het algoritme voor nu simpel, je kunt het bij de uitbreidingen nog aanpassen. 
````

(game-stap-8)=
## Stap 8: Stop het spel als je af bent

````{note} Opdracht
Zorg dat je af bent als de bal de onderkant van het scherm raakt. Voeg daarvoor code toe die kijkt of de onderkant van de bal voorbij de onderkant van de plank is. Als dat waar is, dan zet je code de snelheid van de bal op 0. Op die manier stopt het spel zodra je de bal langs de plank hebt laten gaan.
````

````{attention} Toelichting
Een logische plek voor je nieuwe code is onder afhandelen van botsingen en voor je begint met tekenen. Dat is op de plek van de <<hier toevoegen>> in onderstaande stukjes.
```python
    # move everything
    ...

    # handle collisions
    <<hier toevoegen>>

    # draw everything
    ...
```
````

````{hint} Tips
:class: dropdown
-	Bovenaan het scherm is y gelijk aan 0. Hoe verder je naar beneden op het scherm komt, hoe groter het getal y wordt. De y-coördinaat van de bovenkant van de bal bewaar je in de variabele `ball_y`. De hoogte van de bal bewaar je in `BALL_HEIGHT`. Hoe bereken je de y-coördinaat van de onderkant van de bal?
-	Wat gebeurt er met de code die de bal tegen de onderkant van het scherm laat stuiteren? Wordt die code nog uitgevoerd? 
````

(game-stap-9)=
## Stap 9: Toon een bericht als je af bent

````{note} Opdracht
Zet een bericht op het scherm als de speler af is. Dat is duidelijker voor de speler.
````

````{attention} Toelichting
Deze drie stukjes code zetten een bericht op het scherm. Kopieer en plak ze op de juiste plekken.
```python
# define global variables
game_status_msg = ""
```

```python
# if dead
game_status_msg = "You lost!"
```

```python
# draw game status message
game_status_img = font.render(game_status_msg, True, 'green')
screen.blit(game_status_img, (0, 0)) # (0, 0) is top left corner of screen
```
````

````{hint} Tips
:class: dropdown
-	Je kunt tijdens het spelen een ander bericht op het scherm zetten, bijvoorbeeld:\
    `game_status_msg = "Speel met [A] en [D]"`
-	Je kunt het bericht netjes in het midden van de regel uitlijnen met een berekening met `SCREEN_WIDTH` en `game_status_img.get_width()`.
````
