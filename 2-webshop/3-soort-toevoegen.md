
# Soort aan product toevoegen
1:n relaties toevoegen


## Tabellen met 1:N-relatie maken (uitleg)

:::{note} uitleg
Een _1:N-relatie_ (spreek uit als "één op en relatie") betekent:  
- één rij in de eerste tabel hoort bij nul, één of meer rijen in de tweede tabel **en**
- één rij in de tweede tabel hoort bij nul of één rijen in de eerste tabel.

Voorbeeld: een 1:N-relatie tussen merk en product  
- één merk kan nul, één of meer producten hebben  
- elk product hoort bij nul of één merk

Hoe maak je deze relatie in SQL?
- Je zet een _verwijzende sleutel_ (Engels: foreign key) in de tweede tabel. De verwijzende sleutel staat dus in de tabel van de N.  
- Je geeft aan dat die verwijst naar de _primaire sleutel_ (Engels: primary key) van de eerste tabel.  

Voorbeeld:

```sql
CREATE TABLE brands (
  id INTEGER PRIMARY KEY,
  name TEXT
);

CREATE TABLE products (
  id INTEGER PRIMARY KEY,
  name TEXT,
  price REAL,
  brand_id INTEGER,
  FOREIGN KEY(brand_id) REFERENCES brands(id)
);
```

In dit voorbeeld:
- `brands.id` is de primaire sleutel (1-kant)  
- `products.brand_id` is een foreign key (N-kant)  
- Bij een product dat niet aan een merk gekoppeld is, heeft de verwijzende sleutel de waarde `NULL`
- Een merk **kan** aan een product gekoppeld zijn, maar dat **hoeft niet**

:::

## maak tabel met soorten (database)
create table
insert

## maak veld dat product aan soort koppelt (database)
voeg verwijzende sleutel toe
laat de naam eindigen op _id, dan kan onze website er goed mee omgaan

## beschrijf cardinaliteit (database)
voeg constraint toe

## koppel producten aan soort (database)
vul verwijzingen in

## api (uitleg)
api verbindt de database met de website

back end: api en database
front end: website

webserver voor static files, bij ons in de api, bij grotere projecten vaak op aparte servers. Database draait ook vaak op één of meerdere aparte servers.

## Query met 1:N-relatie maken (uitleg)
:::{note} uitleg
Bij een _1:N-relatie_ kun je een query maken om gegevens uit beide tabellen te combineren.  
Je gebruikt dan het sleutelveld waarop ze gekoppeld zijn.

Voorbeeld: producten met hun merknaam

```sql
SELECT products.name, brands.name
FROM products
JOIN brands ON products.brand_id = brands.id;
```

Wat gebeurt er in deze query?
- `SELECT` kiest de kolommen die je wilt zien:  
  - de naam van het product  
  - de naam van het merk
- `FROM products` betekent dat je begint bij de tabel `products`
- `JOIN brands ON products.brand_id = brands.id` zegt:  
  combineer elke rij uit `products` met een rij uit `brands`  
  waar de waarde van `brand_id` hetzelfde is als de `id` van het merk

Je krijgt dan een lijst van producten, met daarbij het merk waar ze bij horen.

:::

## voeg soort toe aan query (api)
api aanpassing: query met join

## niet benodigde velden verwijderen (niet nodig, verwijderen) / namen van velden aanpassen (api)
speciale velden: name, price, description uit de tabel products worden herkend in de html en op speciale wijze getoond
het veld id de tabel products en velden die eindigen op _id worden herkend in de html en niet getoond, deze zijn wel handig om erin te houden

de website gebruikt de naam van de velden, meestal zijn die Engelstalig. Het is handig om die in de api aan te passen
AS gebruiken
