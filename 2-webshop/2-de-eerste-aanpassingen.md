# De eerste aanpassingen

## Uitleg: Architectuur
:::{note} Uitleg
```{figure} 2-architecture.svg
Architectuur van de webshop
```

Als je de webshop bezoekt dan laadt de browser eerst de een kale webpagina zonder producten. Daarna worden de artikelen geladen. Dat gaat zo snel, dat je het bijna niet ziet.

Het laden van de kale webpagina gaat met de volgende stappen.
1. Je opent een browser op je client en navigeert naar de webshop.
2. De browser downloadt het index.html bestand van de server. 
3. In het index.html bestand ziet de browser dat hij de bestanden style.css en script.js moet laden.
4. De bestanden index.html en style.css bevatten de startpagina van de webshop, zonder producten. De informatie uit die bestanden wordt door de browser opgeslagen in een Document Object Model (_DOM_). De DOM staat in het geheugen van de browser en bepaalt wat de browser op het scherm toont.

Het laden van de artikelen gebeurt in de volgende stappen.
1. In script.js staat een JavaScript-programma. De browser voert dat programma uit.
2. De JavaScript-code maakt via een link verbinding met de server.
3. De link is gekoppeld aan een programma op de server. Dit programma is een Application Programming Interface (_API_, spreek uit als ee-pie-aai). De API in deze webshop is geschreven in de programmeertaal Python. 
4. De API vraagt via het SQL-commando `select` informatie over artikelen op uit de database. 
5. Het antwoord van de database wordt door de API omgezet in _JSON_-formaat (spreek uit als djee-sun-formaat) en teruggestuurd naar de client waarop de browser draait. 
6. Het JavaScript-programma in de browser leest het JSON-bestand en voegt elementen toe aan de DOM. Die elementen zijn stukjes HTML met informatie over de artikelen. In die informatie zit ook een link naar het plaatje van het artikel. De browser downloadt de plaatjes en toont alle elementen die aan de DOM zijn toegevoegd op het scherm.

```{seealso} REST 
Het geheel van linken, API, database en JSON dat op de server staat is een _REST_-API. De REST-API zorgt ervoor dat de JavaScript-code in de browser informatie op kan vragen over artikelen uit de webshop. De REST-API wint aan populariteit vanaf ongeveer 2010. Voor die tijd werd vaak gekozen voor een server die complete webpagina’s maakt, inclusief alle informatie over de artikelen. 

Een voordeel van REST ten opzichte van de traditionele aanpak is dat REST interactievere websites mogelijk maakt. Dat komt omdat het laden van extra informatie via een REST-API sneller gaat dan het herladen van de hele webpagina. Een ander voordeel is dat een REST-API gemakkelijk door andere programma's dan browsers gebruikt kan worden. Zo kun je bijvoorbeeld zelf een Python-programma schrijven dat gebruik maakt van de REST-interface van chatgpt. 

Je leert meer over REST in de volgende hoofdstukken.
```

:::

## Verander het onderwerp

```{hint} Tips
:class: dropdown
- Kijk in het bestand `/static/index.html`.
- Zoek naar de `h1` tag
```

## Verander de achtergrond-kleur

```{hint} Tips
:class: dropdown
- Kijk in het bestand `/static/style.css`.
```

## Verander de artikelnamen

```{hint} Tips
:class: dropdown
- Kijk in het bestand `/data/init.sql`.
- Start de webshop opnieuw.
```

## Verander een plaatje

```{hint} Tips
:class: dropdown
- Kijk in de map `/static/images`.
```
