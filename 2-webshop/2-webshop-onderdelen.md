# Webshop-onderdelen

```{pull-quote}
We beginnen met drie smurfen.
```

```{figure} scherm1.png
Schermafdruk van webshop aan het begin van dit hoofdstuk.
```

In dit hoofdstuk ga je kleine aanpassingen doen in je webshop, zoals teksten, kleuren en plaatjes aanpassen. Je maakt kennis met alle onderdelen van de webshop en leert hoe die samenwerken.

## Uitleg: Architectuur
:::{note} Uitleg

### Onderdelen van de webshop
```{figure} 2-architecture.svg
Architectuur van de webshop
```

Als je de webshop bezoekt dan laadt de browser eerst een kale webpagina zonder producten. Daarna worden de artikelen geladen. Dat gaat zo snel, dat je het bijna niet ziet.

### Webpagina laden
Het laden van de kale webpagina gaat met de volgende stappen.
1. Je opent een browser op je client en navigeert naar de webshop.
2. De browser downloadt het index.html bestand van de server. 
3. In het index.html bestand ziet de browser dat hij de bestanden style.css en script.js moet laden.
4. De bestanden index.html en style.css bevatten de startpagina van de webshop, zonder producten. De informatie uit die bestanden wordt door de browser opgeslagen in een Document Object Model (_DOM_). De DOM staat in het geheugen van de browser en bepaalt wat de browser op het scherm toont.

### Producten laden
Het laden van de artikelen gebeurt in de volgende stappen.
1. In script.js staat een JavaScript-programma. De browser voert dat programma uit.
2. De JavaScript-code maakt via een link verbinding met de server.
3. De link is gekoppeld aan een programma op de server. Dit programma is een Application Programming Interface (_API_, spreek uit als ee-pie-aai). De API in deze webshop is geschreven in de programmeertaal Python. 
4. De API vraagt via het SQL-commando `select` informatie over artikelen op uit de database. 
5. Het antwoord van de database wordt door de API omgezet in _JSON_-formaat (spreek uit als djee-sun-formaat) en teruggestuurd naar de client waarop de browser draait. 
6. Het JavaScript-programma in de browser leest het JSON-bestand en voegt elementen toe aan de DOM. Die elementen zijn stukjes HTML met informatie over de artikelen. In die informatie zit ook een link naar het plaatje van het artikel. De browser downloadt de plaatjes en toont alle elementen die aan de DOM zijn toegevoegd op het scherm.

:::

```{seealso} REST 
Het geheel van linken, API, database en JSON dat op de server staat is een _REST_-API. De REST-API zorgt ervoor dat de JavaScript-code in de browser informatie op kan vragen over artikelen uit de webshop. De REST-API wint aan populariteit vanaf ongeveer 2010. Voor die tijd werd vaak gekozen voor een server die complete webpagina’s maakt, inclusief alle informatie over de artikelen. 

Een voordeel van REST ten opzichte van de traditionele aanpak is dat REST interactievere websites mogelijk maakt. Dat komt omdat het laden van extra informatie via een REST-API sneller gaat dan het herladen van de hele webpagina. Een ander voordeel is dat een REST-API gemakkelijk door andere programma's dan browsers gebruikt kan worden. Zo kun je bijvoorbeeld zelf een Python-programma schrijven dat gebruik maakt van de REST-interface van chatgpt. 

Je leert meer over REST in de volgende hoofdstukken.
```

## Opdracht: Je eerste wijzigingen in de startcode 

```{attention} Toelichting
Voor deze opdracht krijg je startcode. De startcode moet je aanpassen in een ontwikkelomgeving. Je docent vertelt hoe je aan de startcode komt en welke ontwikkelomgeving je mag gebruiken.
```

Deze opdracht bestaat uit onderdeel a), b), c), d) en e). Begin bij het eerste onderdeel, sla geen onderdelen over. Onder ‘Opdracht x)’ staat steeds wat je code moet doen. Lees dit aandachtig door, voordat je begint te coderen. De tips kun je bekijken als je er niet uitkomt.

:::{note} Opdracht a)
### Run de startcode 

- Start de server (database en api) van je webshop. Gebruikt daarvoor het commando `bash start.sh`.
- Open een client van je webshop. Doe dat door een webpagina te openen op poort 8000 van je webserver.

Als het gelukt is, dan zie je een webshop met drie smurfen.
:::

```{hint} Tips
:class: dropdown
- Bij de startcode zit een `README.md` bestand. Hierin staat hoe je code kunt starten, stoppen, wijzigingen en opslaan.
- Meer informatie over de ontwikkelomgeving GitHub Codespaces vind je op\
  https://stanislas.informatica.nu/help/codespaces/
```

:::{note} Opdracht b)
### Verander het onderwerp

Start de webshop met het commando `bash start.sh` in de terminal
De webshop verschijnt op je scherm.
Bovenaan de webshoppagina staat de naam van de webshop (Smurfsjop). 

Verzin zelf een naam voor jouw webshop en pas de code aan, zodat jouw naam getoond wordt.
:::

```{hint} Tips
:class: dropdown
- Kijk in het bestand `/static/index.html`.
- Zoek naar de `h1` tag
```

:::{note} Opdracht c)
### Verander de kleur

De webshop gebruikt zwarte letters op een bijna witte achtergrond en witte letters op een smurfblauwe achtergrond. 

Verander de smurfblauwe kleur in een kleur die past bij jouw webshop.
:::

```{hint} Tips
:class: dropdown
- Kijk in het bestand `/static/style.css`.
```

:::{note} Opdracht d)
### Verander de artikelnamen

Bovenaan de plaatjes staan de namen van de artikelen die je verkoopt. 

Verander de namen van artikelen in artikelen die jij wilt verkopen.
:::

```{hint} Tips
:class: dropdown
- Kijk in het bestand `/data/init.sql` en pas daar de inhoud van de juiste velden aan.
- Start de webshop opnieuw met het terminal-commando `bash start.sh`. Tijdens het starten wordt de database opnieuw gemaakt met de commando's in het bestand init.sql
```

:::{note} Opdracht e)
### Verander een plaatje

Voeg een nieuw plaatje toe en geef het een naam die past bij het artikel.
:::

```{hint} Tips
:class: dropdown
- Er is [meer uitleg over de ontwikkelomgeving Codespaces](#webshop-codespaces), daarin staat hoe je bestanden kunt uploaden. 
- De bestanden met plaatjes staan in de map `/static/images`.
- De namen van de bestanden staan in de database `/data/init.sql`.
- Na aanpassen van het bestand `/data/init.sql` moet je de database opnieuw maken met het terminal-commando `bash start.sh`.
```
