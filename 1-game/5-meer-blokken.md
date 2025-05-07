# 5. Stap 15-19: meer blokken
```{pull-quote}
Eén blok is leuk, maar meer blokken is nog leuker! We gaan stap voor stap blokken toevoegen.
```

```{figure} scherm5.png
Schermafdruk van spelletje met basisstap 15 t/m 19.
```

## 5.1 Stap 15: Maak een tweede blok

````{note} Opdracht
Maak een tweede blok. Gebruik daarvoor de waarden van de variabelen `brick_x2` en `brick_y2`. In dit spel zien alle blokken er hetzelfde uit, daardoor kun je `brick_img`, `BRICK_WIDTH` en `BRICK-HEIGHT` gebruiken voor alle blokken.
````

````{attention} Toelichting
Om een tweede blok te maken, moet je drie stukken code kopiëren en aanpassen.

Code om plaats van blok te onthouden
```python
# define global variables
brick_x = 100
brick_y = 200
```

Code om botsing van bal met blok af te handelen
```python
if ... # ball collides with brick
    # print message in terminal
    # bounce
```

Code om blok te tekenen:   
```python
# draw bricks
screen.blit(brick_img, (brick_x, brick_y))
```
````

````{hint} Tips
:class: dropdown
-	Verander eerst overal in de code `brick_x` en `brick_y` door `brick_x1` en `brick_y1`. Als je dat goed doet, dan werkt je code nog hetzelfde. Dit helpt je om te zien waar je allemaal extra code moet toevoegen voor een tweede blok.  
-	Begin met het maken van variabelen `brick_x2` en `brick_y2`.
-	Voeg een regel toe om het nieuwe blok te tekenen
-	Kopieer de code die de botsing tussen bal en blok afhandelt. Pas de kopie aan zodat hij werkt met het tweede blok.
````

## 5.2 Stap 16: Zet blokken in genummerde lijsten

````{note} Opdracht
Gebruik een lijst met de naam bricks_x voor de variabelen `brick_x1` en `brick_x2`. Gebruik een genummerde lijst met de naam `bricks_y` voor de variabelen `brick_y1` en `brick_y2`. Deze stap is een voorbereiding op het gebruik van loops. Die ga je gebruiken in de volgende stap. Met loops verdwijnt de dubbele code die je in de vorige stap voor het tweede blok gemaakt hebt.
````

````{attention} Toelichting
Code om een lijst met twee elementen te definiëren:
```python
bricks_x = [96, 192]
```
Gebruik meervoud voor de naam van een lijst, dat maakt de code leesbaarder.

Code om een element uit een lijst te gebruiken:
```python
bricks_x[1] 
```
Het eerste element van de lijst `bricks_x` heeft als index het getal nul, het tweede element heeft als index één, het derde element heeft index twee enzovoort. Deze code geeft de waarde van het tweede element uit de lijst. Die waarde is 192.

Maak een lijst `bricks_y` op dezelfde manier als je `bricks_x` hebt gemaakt.
````

````{hint} Tips
:class: dropdown
-	Let op de index van de elementen uit de lijst. Het 1e element heeft index 0, het 2e element heeft index 1, het 3e element heeft index 2 enzovoort. 
````

## 5.3 Stap 17: Gebruik for-loop bij blokken tekenen

````{note} Opdracht
Maak met het commando `for` een loop die alle blokken tekent. 
````

````{attention} Toelichting
Eenvoudige code om met een loop alle elementen in de lijst af te drukken:
```python
for brick_x in bricks_x : 
    print(str(brick_x))
```
Omdat wij ook bricks_y gebruiken in de loop, heb je het nummer van het element in de lijst nodig binnen de for-loop.

Code die je in je game kunt gebruiken om met een loop alle elementen in de lijst af te drukken:
```python
for i in range(0, len(bricks_x)) : 
    print('bricks_x[' + str(i) + '] = ' + str(bricks_x[i]))
```
Deze code doorloopt de lijst van voor naar achter en slaat het nummer van het element uit de lijst op in de variabele i.
````

````{hint} Tips
:class: dropdown
-	Voeg bij code voor het tekenen van de blokken een for-loop toe die alle blokken tekent. Daarvoor heb je één teken-commando binnen de for-loop nodig.
-	Let op dat je de teken-commando inspringt.
-	Vergeet de oude regels die de blokken tekende niet te verwijderen.
````

## 5.4 Stap 18: Gebruik for-loop bij botsing tegen blokken

````{note} Opdracht
Maak met het commando for een loop die botsingen van de bal met alle blokken afhandelt.
````

````{hint} Tips
:class: dropdown
-	Kijk bij de vorige stap hoe je een for-loop maakt.
-	Let op dat je goed inspringt.
````

## 5.5 Stap 19: Maak een veld met 24 blokken

````{note} Opdracht
Voeg 22 nieuwe blokken toe, zodat je een veld krijgt met 24 blokken.
````

````{attention} Toelichting
In de vorige stap wordt het aantal elementen in de lijst berekend met `len(bricks_x)`. Daardoor hoef je nu maar heel weinig aan te passen om blokken toe te voegen. Je hoeft alleen elementen toe te voegen aan de definities van de lijsten.

````{hint} Tips
:class: dropdown
-	De lijsten `bricks_x` en `bricks_y` moeten evenveel elementen bevatten.
-	De definitie van lijsten kun je over meerdere regels verdelen. Op alle plaatsen waar een spatie is toegestaan, mag je op een nieuwe regel beginnen.
````
