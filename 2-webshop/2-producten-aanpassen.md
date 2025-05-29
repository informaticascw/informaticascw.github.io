# Producten aanpassen

## Uitleg: Architectuur
:::{note} Uitleg
```{figure} 2-architecture.svg
Architectuur van de webshop
```

Als je de webshop bezoekt dan laadt de browser eerst de een kale webpagina zonder producten. Daarna worden de artikelen geladen. Dat gaat zo snel, dat je het bijna niet ziet.

Het laden van de kale webpagina gebeurt in de volgende stappen.
1. Je opent een browser op je client en navigeert naar de webshop.
2. De browser downloadt het index.html bestand van de server. 
3. In het index.html bestand ziet de browser dat hij de bestanden style.css en script.js moet laden.
4. De bestanden index.html en style.css bevatten de startpagina van de webshop, zonder producten. De informatie uit die bestanden wordt door de browser opgeslagen in een Document Object Model (**DOM**). De DOM staat in het geheugen van de browser en bepaalt wat de browser op het scherm toont.

Het laden van de artikelen gebeurt in de volgende stappen.
1. In script.js staat een JavaScript-programma. De browser voert dat programma uit.
2. De JavaScript-code maakt via een link verbinding met de server. 
3. De link is gekoppeld aan een programma op de server. Dit programma is een Application Programming Interface (**API**). Onze API is geschreven in de programmeertaal Python. 
4. De API vraagt via het SQL-commando `select` informatie over artikelen op uit de database. 
5. Het antwoord van de database wordt door de API omgezet in **JSON**-formaat en teruggestuurd naar de client waarop de browser draait. 
6. Het JavaScript-programma in de browser leest het JSON-bestand en voegt elementen toe aan de DOM. Die elementen zijn stukjes HTML met informatie over de artikelen. In die informatie zit ook een link naar het plaatje van het artikel. De browser downloadt de afbeeldingen en toont alle elementen die aan de DOM zijn toegevoegd op het scherm.

Het geheel van linken, API, database en JSON dat op de server staat is een **REST**-interface. De REST-interface zorgt er dus voor dat de JavaScript-code in de browser informatie op kan vragen over artikelen in onze winkel. De REST-interface wint aan populariteit vanaf ongeveer 2010. Voor die tijd werd vaak gekozen voor een server die complete webpagina’s maakte, inclusief alle informatie over de artikelen. Een voordeel van REST ten opzichte van de traditionele aanpak is dat REST meer interactieve websites mogelijk maakt. Een ander voordeel is dat een REST-interface gemakkelijk door andere programma's dan browsers gebruikt kan worden. Zo kun je bijvoorbeeld zelf een Python-programma schrijven dat gebruik maakt van de REST-interface van chatgpt. Je leert meer over REST in volgende hoofdstukken.

:::

## Voeg een product toe (database)

## Uitleg: Een tabel maken in SQL
:::{note} Uitleg
### Een tabel maken in SQL

In een database staan gegevens in tabellen.
Een tabel bestaat uit kolommen.

Elke kolom heeft:
- een naam (zoals id of name)
- een gegevenstype (zoals tekst of een getal)

Veelgebruikte gegevenstypen:
- TEXT → een stuk tekst (zoals "Smurfin")
- REAL → een kommagetal (zoals 9.50 of 14.95)
- INTEGER → een heel getal (zoals 1, 25, 100)
- INTEGER PRIMARY KEY is een bijzonder vorm van een INTEGER, het is een heel getal en elke waarde in de kolom mag maar één keer gebruikt worden.

Voorbeeld om een tabel te maken in SQL:

```
CREATE TABLE products (
    id INTEGER PRIMARY KEY,
    name TEXT,
    price REAL
);
```

Deze tabel heet products.
Er staan drie kolommen in:
- id: een uniek nummer voor elk product
- name: de naam van het product, dit is een tekst
- price: de prijs van het product, dit is een kommagetal

```{tip} komma's en puntkomma's
De komma `,` wordt gebruikt als **scheiding** tussen kolommen. Na de laatste kolom komt dus geen komma meer. Als je een kolom aan het einde van de tabel toevoegt, dan moet je niet vergeten de komma toe te voegen achter de één na laatste kolom.

De puntkomma `;` wordt gebruikt als **afsluiting** van elk commando. Het maken van een tabel is een commando. Er staat een puntkomma na elke tabel die je maakt, dus ook na de laatste tabel.
```
:::

## Verander de naam van producten (database)
Gegevens aanpassen

## Verander de plaatjes van producten (database)
Bestand aanpassen

## Uitleg: Gegevens toevoegen
:::{note}
### Gegevens toevoegen

Als de tabel bestaat, kun je er gegevens in zetten.  
Dat doe je met de opdracht `INSERT INTO`.

Je geeft aan:
- aan welke tabel je iets toevoegt  
- welke kolommen je invult  
- welke waarden je opslaat  

Voorbeeld: één product toevoegen

```sql
INSERT INTO products (id, name, price)
VALUES (1, 'Smurfin', 9.50);
```

In dit voorbeeld:
- de gegevens gaan naar de tabel `products`  
- je vult drie kolommen in: `id`, `name`, `price`  
- de waarden zijn:
  - `1` voor `id` (een uniek nummer)  
  - `'Smurfin'` voor `name` (een tekst)  
  - `9.50` voor `price` (een kommagetal)

Voorbeeld: meerdere producten toevoegen

Je kunt meerdere regels toevoegen door meerdere `INSERT` commando's onder elkaar te zetten. 
Je kunt ook meerdere regels tegelijk toevoegen met één insert commando. Dit gaat als volgt.

```sql
INSERT INTO products (id, name, price) VALUES
  (2, 'Muzieksmurf', 14.95),
  (3, 'Grote smurf', 10.50);
```
:::

:::{note} Opdracht: Voeg regel toe aan de tabel products
:::

## Voeg een prijs toe (database)
Maak een extra veld `price`

## Voeg een beschrijving toe (database)
Maak een extra veld `description`
