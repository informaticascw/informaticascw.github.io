# Stap 0-3: bal
```{pull-quote}
We beginnen met een bal die stuitert.
```

```{figure} scherm2.png
Schermafdruk van spelletje met basisstap 0 t/m 3.
```

De basisstappen zijn genummerd van stap 0 tot en met stap 21. In elke basisstap staat onder ‘opdracht’ wat je code moet doen. Lees dit aandachtig door, voordat je begint te coderen. De toelichting geeft aan hoe je de opdracht kunt maken. De tips kun je bekijken als je er niet uitkomt. 

## Stap 0: Run de startcode 

In ‘de opdracht’ staat wat je code moet doen. Lees dit aandachtig door, voordat je begint te coderen. De toelichting geeft aan hoe je de opdracht kunt maken. De tips kun je bekijken als je er niet uitkomt.

```{note} Opdracht
Verander in de code de achtergrondkleur van je spel. Doe het volgende:
-	Run de startcode. De achtergrond is zwart, bovenin beweegt een blauwe bal.
-	Verander in de code de achtergrondkleur van je spel. 
-	Start je code opnieuw.
-	Sla de nieuwe versie van je code op in GitHub.
```

```{attention} Toelichting
Voor deze opdracht krijg je startcode. De startcode beweegt een bal bovenin het scherm van links naar rechts naar links enzovoort. De startcode moet je uitvoeren (Engels: run) en wijzigen (Engels: edit) in een ontwikkelomgeving. Je docent vertelt hoe je aan de startcode komt en welke ontwikkelomgeving je mag gebruiken.
```

```{hint} Tips
:class: dropdown
-	Wijzig de `screen.fill('black')` in het bestand `main.py` om de achtergrondkleur te veranderen.
-	Bij de startcode zit een `README.md` bestand. Hierin staat hoe je code kunt starten, stoppen, wijzigingen en opslaan.
-	Meer informatie over de ontwikkelomgeving GitHub Codespaces vind je op\
  https://stanislas.informatica.nu/help/codespaces/
```

## Stap 1: Voeg commentaar toe 

````{note} Opdracht
Breid het commentaar in je startcode uit. In de toelichting vind je voorbeelden van stukjes code met extra commentaar. Het gaat er bij deze opdracht om dat je de startcode leert begrijpen.
````

````{attention} Toelichting
Stukje code uit `main.py` die constanten en variabelen maakt:
```python
# definitions 
FPS = 30 # Frames Per Second
SCREEN_WIDTH = 1280  # screensize in x-direction in pixels
SCREEN_HEIGHT = 720  # screensize in y-direction in pixels
BALL_WIDTH = 16      # ballsize in x-direction in pixels
BALL_HEIGHT = 16     # ballsize in y-direction in pixels
ball_x = 0           # x-position of ball in pixels
ball_speed_x = 6     # speed of ball in x-direction in pixels per frame
```

Stukje code uit `main.py` die game te initialiseert:
```python
# init game
pygame.init()
font = pygame.font.SysFont('default', 64)
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT), pygame.FULLSCREEN)
fps_clock = pygame.time.Clock()
```

Stukje code uit `main.py` die plaatjes inleest:
```python
# read images

# read spritesheet containing all images
# convert_alpha increases speed of blit and keeps transparency of .png
spritesheet = pygame.image.load('Breakout_Tile_Free.png').convert_alpha() 

# create empty image of 64 x 64 pixels, SRCALPHA supports transparency
ball_img = pygame.Surface((64, 64), pygame.SRCALPHA) 
# copy part (x-left=1403, y-top=652, width=64, height=64) from spritesheet to ball_img at (0,0)
ball_img.blit(spritesheet, (0, 0), (1403, 652, 64, 64)) 
# resize ball_img from 64 x 64 pixels to BALL_WIDTH x BALL_HEIGHT
ball_img = pygame.transform.scale(ball_img, (BALL_WIDTH, BALL_HEIGHT)) 
```

Gameloop in `main.py` op hoofdlijnen, de code in de gameloop wordt steeds herhaalt:
```python
running = True
while running:
  # read events
  # move everything
  # handle collisions
  # draw everything
  # wait until next frame
```

Stukje code uit gameloop die zorgt dat invoer vanuit besturingssysteem wordt afgehandeld:
```python
    # read events

    for event in pygame.event.get(): # read all events
        if event.type == pygame.QUIT: # GUI is closed 
            running = False # end programm
    keys = pygame.key.get_pressed() # read which keys are down
```

Stukje code uit gameloop die alles beweegt:
```python
    # move everything

    # move ball
    ball_x = ball_x + ball_speed_x
    # bounce ball against edges of screen
    if ball_x < 0 : # left edge
      ball_speed_x = abs(ball_speed_x) # positive x-speed = move right
    if ball_x + BALL_WIDTH > SCREEN_WIDTH: # right edge
      ball_speed_x = abs(ball_speed_x) * -1 # negative x-speed = move left
```

Plek in gameloop om later code toe te voegen die botsingen afhandelt:
```python
    # 
    # handle collisions
    #
```

```python
Stukje code uit gameloop die alles tekent:
    # draw everything

    # clear screen
    screen.fill('black') 
    # draw ball
    screen.blit(ball_img, (ball_x, 0))
    # show screen
    pygame.display.flip() 
```

Stukje code uit gameloop die frame-snelheid regelt:
```python
    # wait until next frame
    fps_clock.tick(FPS) # Sleep the remaining time of this frame
```
````

````{hint} Tips
:class: dropdown
-	Alles tussen `#` en het einde van de regel, wordt door de computer overgeslagen.
-	Hoe werkt het tekenen op het scherm in de pygame-library? In welke regels code worden de plaatjes ingelezen? In welke regels code worden plaatjes op het scherm gezet? In welke regel wordt het nieuwe scherm op de monitor getoond? 
-	Hoe wordt het aantal frames per seconde geregeld?
-	Wat moet je veranderen aan de code om de bal op een andere plek te laten starten?
````

## Stap 2: Beweeg de bal schuin

````{note} Opdracht
De bal beweegt nu horizontaal over het scherm. Voeg code toe die ervoor zorgt dat de bal diagonaal (schuin) over het scherm beweegt. Voeg de variabelen `ball_y` en `ball_speed_y` toe.
````

````{attention} Toelichting
Regels uit de startcode die de bal horizontaal bewegen:
```python
ball_x = 0
ball_speed_x = 6

# move ball
ball_x = ball_x + ball_speed_x

# draw ball
screen.blit(ball_img, (ball_x, 0))
```
````

````{hint} Tips
:class: dropdown
-	Maak een variabele `ball_y` en geef die een waarde, bijvoorbeeld 100.
-	Gebruik de waarde van `ball_y` bij de functie die de bal op het scherm zet. Dit is de functie `screen.blit`. 
-	Maak een variabele `ball_speed_y` en geef die een waarde ongelijk aan 0, bijvoorbeeld 10.
-	Kopieer de regel code waarin steeds de waarde van `ball_x` wordt berekend. Pas de kopie aan, zodat de waarde van `ball_y` wordt berekend. Gebruik daarbij variabele `ball_speed_y`.
````

## Stap 3: Stuiter de bal tegen de onder- en bovenkant van het scherm

````{note} Opdracht
De bal verdwijnt nu uit het scherm als hij aan de bovenkant of de onderkant komt. Zorg dat de bal tegen de onderrand en bovenrand van het scherm stuitert, net zoals hij dat doet aan de zijkanten.
````

````{attention} Toelichting
Code die zorgt dat bal stuitert tegen zijkant van scherm:
```python
    if ball_x < 0 : # left edge
      ball_speed_x = abs(ball_speed_x) # positive x-speed = move right
    if ball_x + BALL_WIDTH > SCREEN_WIDTH: # right edge
      ball_speed_x = abs(ball_speed_x) * -1 # negative x-speed = move left
```

-	De functie `abs(getal)` geeft als resultaat een getal zonder min. Dus `abs(-2)` is 2 en `abs(2)` is ook 2. Dus `abs(ball_speed_x)` geeft de positieve waarde van de x-snelheid. `abs(ball_speed_x) * -1` geeft de negatieve waarde van de x-snelheid.
````

````{hint} Tips
:class: dropdown
-	Zoek de regels code die ervoor zorgen dat de bal tegen de zijkanten van het scherm kaatst. Kopieer dat stukje code en pas het aan zodat dat de bal ook tegen de bovenkant en onderkant van het scherm kaatst.
-	Gebruik `BALL_HEIGHT` om rekening te houden met de hoogte van de bal.
````
