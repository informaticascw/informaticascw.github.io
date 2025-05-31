# Front-end
In dit hoofdstuk ga je aanpassingen doen aan de front-end van je webshop. De front-end is het statische gedeelte van de webshop, dat draait in de browser van de bezoekers van je webshop. 

## Pas kleuren aan (css)

## Maak aparte bestelpagina (html)

## DOM

:::{note} Uitleg

### Wat is het DOM?

De DOM (Document Object Model) is een boomstructuur die je browser maakt van een HTML-pagina.  
Elke tag in de HTML (zoals `<h1>`, `<div>`, `<p>`) wordt een object in die boom. 
JavaScript kan via de DOM elementen zoeken, toevoegen, of aanpassen.

JavaScript is een programmeertaal die elke browser begrijpt. Veel webpagina's bevatten JavaScript-code. Je kunt JavaScript-code vinden tussen de tag `<script>` in een `.html`-bestand of in een bestand met een naam die eindigt op `.js`.

### Objecten zoeken

Met JavaScript kun je bestaande elementen op verschillenden manieren in de DOM zoeken, bijvoorbeeld:

```javascript
element = document.getElementById("mijn-lijst");
anotherElement = document.querySelector(".knop");
```

### Objecten toevoegen

Je kunt nieuwe elementen maken en aan de DOM toevoegen:

```javascript
parent = document.getElementById("mijn-lijst");
let newChild = document.createElement("li");
newChild.textContent = "Hallo!";
parent.appendChild(newChild);
```

Hier maak je een nieuw list-item en voeg je die toe aan het einde van de lijst.

### Objecten wijzigen

Je kunt een DOM-element aanpassen door het in een variabele te stoppen en vervolgens de eigenschappen van het object te veranderen.

Voorbeeld:

```javascript
let knop = document.querySelector(".knop");
knop.textContent = "Klik hier!";
```

Dit verandert de echte knop op de pagina, want `knop` wijst naar het originele object. Niet de hele knop met alles erin is gekopieerd, maar alleen het geheugenadres dat wijst naar de knop is gekopieerd. De variabele `knop` noem je een variabele by reference.

:::

## Maak aparte pagina per product (javascript)
