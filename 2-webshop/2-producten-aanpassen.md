# Producten aanpassen

## Uitleg: Architectuur
:::{note} Uitleg
```{figure} 2-architecture.jpg
Architectuur van de webshop
```
The basic idea is that a webpage of the shop is loaded by the browser and information on the articles in the shop are added to that depending on what the user selects.

1. You open a browser and navigate to the webshop.
2. The browser downloads the html and css files from the server. It also downloads a piece of javascript code.
3. The javascript code is being executed by the browser. The javascript code connects to a link on the server that is connected to the api. This is called a REST-interface. Through the REST interface, the javascript code in the browser request information on the articles it needs to display.
4. The api is a programm on the server which connects to the database. It requests information from the database and sends it back to the browser. The result is sent in json-format.
5. The javascript programm in the browser looks at the json-file and adds elements containing products in the shop to the DOM. The DOM is the model of the html files that the browser keeps in it memory and shows to the user. These elements added are displayed by the browser.
6. The browser downloads images for which a link was added to the product in the DOM.

An alternative approach would be to have the server build complete web-pages including all information on articles. This is the idea behind the php programming language. The REST-interface is gaining popularity. An advantage of REST above php is that REST allows for more responsive (interfactive) websites.

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
