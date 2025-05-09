# Stap 10-14: eerste blok
```{pull-quote}
Het spel bevat alleen nog maar een plank en een bal, maar geen blokken… Het wordt tijd om het eerste blok toe te voegen!
```

```{figure} scherm4.png
Schermafdruk van spelletje met basisstap 10 t/m 14.
```

## Stap 10: Teken een blok in het veld

````{note} Opdracht
Teken een blok op het scherm. Gebruik de variabele `brick_img` om het plaatje van het blok op te slaan. Maak en gebruik de constanten `BRICK_WIDTH` en `BRICK_HEIGHT` voor de breedte en hoogte van het blok. Het blok is 96 pixels breed en 32 pixels hoog. Maak en gebruik de variabelen `brick_x` en `brick_y` voor de linkerbovenhoek van het blok. Kies zelf op welke plaats je het blok op het scherm wilt zetten.
````

````{hint} Tips
:class: dropdown
-	Bekijk “Stap 4. Teken de plank” als je er niet uitkomt.
````

## Stap 11: Detecteer als de bal het blok raakt

````{note} Opdracht
Druk een tekst af in de terminal als de bal het blok raakt.
````

````{attention} Toelichting
Een tekst in de terminal afdrukken doe je zo:
```python
print('brick touched at ball_x = ' + str(ball_x) + ' and ball_y = ' + str(ball_y))
```
````

````{hint} Tips
:class: dropdown
-	Bekijk “Stap 7. Stuiter de bal tegen de plank” als je niet meer weet hoe je kunt zien dat twee voorwerpen elkaar raken.
-	Python plakt teksten aan elkaar als je ze optelt. De functie `str` zet een getal om in een string. Deze functie heb je nodig, omdat Python getallen en strings niet automatisch bij elkaar optelt; je krijgt dan een foutmelding.
-	Meer informatie over het printen van tekst vind je op\
  https://www.freecodecamp.org/news/python-print-variable-how-to-print-a-string-and-variable/
-	Je vraagt je misschien af hoe je het blok weghaalt. Dat leer je in “Stap 20, Haal een blok weg als de bal een blok raakt”.
````

## Stap 12: Stuiter de bal omhoog als hij het blok raakt

````{note} Opdracht
Stuiter de bal omhoog als hij van boven aankomt en een blok raakt. Ga ervan uit dat de beweging van de bal in de x- en y-richting minder pixels per frame is dan de breedte en hoogte van de bal. Dat betekent dat er altijd een stukje van de bal buiten het blok is. De stuiter vanaf beneden, links en rechts ga je in de volgende stappen toevoegen.
````

````{attention} Toelichting
Pseudo-code
```pseudo
als de bal het blok raakt :
    druk een tekst af
    als ( de bal naar onder beweegt en 
          de bovenkant van de bal zit boven de bovenkant van het blok ) :
        maak snelheid_y omhoog
```

De schuingedrukte regels heb je al gemaakt in de vorige stap. De rest moet je nog toevoegen.

Er zit twee keer “als” in de pseudo-code. De tweede “als” wordt alleen uitgevoerd als de eerste “als” waar is. Je kunt deze code combineren in één “als”, door de condities uit beide “als”-en aan elkaar te knopen met “and”. In de volgende stappen ga je zien dat dat in dit geval minder duidelijk is, omdat er dan dubbele code ontstaat.
````

````{hint} Tips
:class: dropdown
-	Met `if ball_speed_y > 0 :` kun je kijken of de bal naar onder beweegt.
-	De bovenkant van de bal is `ball_y`.
-	De bovenkant van het blok is `brick_`y.
-	`maak snelheid_y omhoog` betekent dat snelheid_y een negatief getal (een getal kleiner dan 0) moet zijn. Gebruik daarvoor de functie `abs()`. Kijk in stap 7 en stap 3 als je niet meer weet hoe je `abs()` kunt gebruiken
-	Kun je uitleggen waarom de code bij de tweede “als” kijkt of er een stukje bal buiten het blok zit, in plaats van te kijken of er een stukje bal binnen het blok zit?
````

## Stap 13: Stuiter de bal omlaag als hij het blok raakt

````{note} Opdracht
Voeg code toe die de bal omlaag stuitert als hij van beneden aankomt en een blok raakt. 
````

````{attention} Toelichting
Pseudo-code
```pseudo
als de bal het blok raakt :
    druk een tekst af
    als ( de bal naar onder beweegt en 
          de bovenkant van de bal zit boven de bovenkant van het blok ) :
        maak snelheid_y omhoog
    anders als ( de bal naar boven beweegt en 
          de onderkant van de bal zit onder de onderkant van het blok ) :
        maak snelheid_y omlaag
```

De schuingedrukte regels heb je al gemaakt in de vorige stap. De rest moet je nog toevoegen. Bij de vorige stap checkt je code of er een stuk van de bal binnen het blok zat. De code die je in deze stap toevoegt checkt welk stuk van de bal buiten het blok zit.
````

````{hint} Tips
:class: dropdown
-	Met `elif ball_speed_y < 0 :` kun je kijken of de bal naar boven beweegt.
-	De onderkant van de bal is `ball_y + BALL_HEIGHT`.
-	De onderkant van het blok is `brick_y + BRICK_HEIGHT`.
-	`maak snelheid_y omlaag` betekent dat snelheid_y een positief getal (een getal groter dan 0) moet zijn. Gebruik daarvoor de functie `abs()`. Kijk in stap 7 en stap 3 als je niet meer weet hoe je `abs()` kunt gebruiken
````

## Stap 14: Stuiter de bal links of rechts als hij het blok raakt

````{note} Opdracht
Voeg code toe die de bal stuitert als hij van links of rechts aankomt en een blok raakt. 
````

````{attention} Toelichting
Pseudo-code
```pseudo
als de bal het blok raakt :
    druk een tekst af
    als ( de bal naar onder beweegt en 
          de bovenkant van de bal zit boven de bovenkant van het blok ) :
        maak snelheid_y omhoog
    anders als ( de bal naar boven beweegt en 
          de onderkant van de bal zit onder de onderkant van het blok ) :
        maak snelheid_y omlaag
    anders als ( de bal naar rechts beweegt en 
          de linkerkant van de bal zit links van de linkerkant van het blok ) :
        maak snelheid_x naar links
    anders als ( de bal naar links beweegt en 
          de rechterkant van de bal zit rechts van de rechterkant van het blok ) :
        maak snelheid_x naar rechts
```

De schuingedrukte regels heb je al gemaakt in de vorige stap. De rest moet je nog toevoegen. {xxx-check-xxx}
````

````{hint} Tips
:class: dropdown
-	Kijk naar de vorige 2 stappen, kopieer de code en pas hem aan zodat hij voor x werkt in plaats van voor y.
-	`maak snelheid_x` links betekent dat snelheid_x een negatief getal (een getal kleiner dan 0) moet zijn. `maak snelheid_x rechts` betekent dat snelheid_x een postief getal (een getal groter dan 0) moet zijn. Gebruik daarvoor de functie `abs()`. Kijk in de vorige stap als je niet meer weet hoe je deze functie gebruikt.
-	Er zijn andere pseudo-codes mogelijk die een bal die ergens tegenaan botst laten stuiteren. Kun jij er eentje bedenken? Wat zijn de voor- en nadelen ten opzichte van de code uit deze stap?
````
