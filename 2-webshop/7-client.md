# Client
In de vorige hoofdstukken heb je aanpassingen gedaan aan de server-zijde van je webshop. Dit zijn de database en de api. In dit hoofdstuk ga je aanpassingen doen aan de client-zijde van je webshop. De client is het gedeelte van de webshop dat wordt uitgevoerd in de browser van de bezoekers van je webshop. Dit bevat html, css en javascript. Deze bestanden vind je in de map `static`.

## Opdracht: Maak aparte bestelpagina
In deze opdracht ga je een HTML-pagina toevoegen.

## Uitleg: DOM

:::{note} Uitleg

### Wat is het DOM?

De DOM (Document Object Model) is een boomstructuur die je browser maakt van een HTML-pagina.
Elke tag in de HTML (zoals `<h1>`, `<div>`, `<p>`) wordt een object in die boom. 
JavaScript kan via de DOM elementen zoeken, toevoegen, of aanpassen.

JavaScript is een programmeertaal die elke browser begrijpt. Veel webpagina's bevatten JavaScript-code. Je kunt JavaScript-code vinden tussen de tag `<script>` in een `.html`-bestand of in een bestand met een naam die eindigt op `.js`.

### Objecten zoeken

Met JavaScript kun je bestaande elementen op verschillenden manieren in de DOM zoeken, bijvoorbeeld:

```{code} javascript
element = document.getElementById("mijn-lijst");
anotherElement = document.querySelector(".knop");
```

### Objecten toevoegen

Je kunt nieuwe elementen maken en aan de DOM toevoegen:

```{code} javascript
parent = document.getElementById("mijn-lijst");
let newChild = document.createElement("li");
newChild.textContent = "Hallo!";
parent.appendChild(newChild);
```

Hier maak je een nieuw list-item en voeg je die toe aan het einde van de lijst.

### Objecten wijzigen

Je kunt een DOM-element aanpassen door het in een variabele te stoppen en vervolgens de eigenschappen van het object te veranderen.

Voorbeeld:

```{code} javascript
let knop = document.querySelector(".knop");
knop.textContent = "Klik hier!";
```

Dit verandert de echte knop op de pagina, want `knop` wijst naar het originele object. Niet de hele knop met alles erin is gekopieerd, maar alleen het geheugenadres dat wijst naar de knop is gekopieerd. De variabele `knop` noem je een variabele by reference.

:::

## Opdracht: Maak aparte pagina per product
In deze opdracht ga je een HTML-pagina met JavaScript toevoegen en een nieuw entry-point aan de API toevoegen.
