# Stap 20-21: winnen
```{pull-quote}
Om het spel uit te kunnen spelen, moeten de blokken verdwijnen. Laten we dat gaan toevoegen.
```

```{figure} scherm6.png
Schermafdruk van spelletje met basisstap 20 t/m 21.
```

## Stap 20: Haal een blok weg als de bal een blok raakt

````{note} Opdracht
Verwijder een blok dat geraakt is uit de lijst, zodat het uit het veld verdwijnt. Stop de for-loop met `break`, zodra er een blok verwijderd is. 
````

````{attention} Toelichting
Code om het 1e element te verwijderen uit een lijst:
```python
  bricks_x.pop(0)
```

```python
Code om het 2e element te verwijderen uit een lijst:
  bricks_x.pop(1)
```
````

````{hint} Tips
:class: dropdown
-	Gebruik i om het nummer van het element dat je wilt verwijderen aan te geven.
-	Verwijder een element uit de lijst `bricks_x` en verwijder een element uit de lijst `bricks_y`. 
-	Als je nadat je een blok verwijderd hebt, het commando `break` gebruikt, dan wordt er maar één blok per frame verwijdert. De bal kan twee blokken tegelijk raken, maar elk frame gaat zo snel, dat je daar niks van ziet. Als je geen `break` gebruikt, dan krijg je een “index out of range” foutmelding, omdat je verderop in de for-loop probeert een element uit de lijst te gebruiken dat er niet meer is.
````

## Stap 21: Toon bericht als je wint

````{note} Opdracht
Als alle blokken weg zijn, dan heb je het level uitgespeeld. Stop de beweging van de bal en toon een bericht dat het level is uitgespeeld.
````

````{attention} Toelichting
De code len(bricks_x) geeft het aantal elementen in de lijst bricks_x. 
````

````{hint} Tips
:class: dropdown
-	Als je niet weet hoe je de bal stopt, kijk dan bij “Stap 8. Stop het spel als je af bent”
-	Als je niet weet hoe je een bericht op het scherm zet, kijk dan bij “Stap 9. Toon een bericht als je af bent”
-	Gebruik `if len(bricks_x) == 0 :` om te kijken of alle blokken weg zijn. 
-	Kun je in plaats van `if len(bricks_x) == 0 :` ook `if len(bricks_y) == 0 :` gebruiken?
````
