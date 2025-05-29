# Kleuren aan product toevoegen
In ons voorbeeld bestaat een product uit één of meer kleuren en een kleur wordt gebruikt in één of meerdere producten. Dat betekent dat er een n:m (spreek uit als "en op em") relatie tussen producten en kleuren. Andere voorbeelden van een n:m relatie zijn materialen of ingrediënten.

## Tabellen met N:M-relatie maken (uitleg)

:::{note} uitleg
Een _N:M-relatie_ (spreek uit als "en op em relatie") betekent:  
- één rij in de eerste tabel hoort bij nul, één of meer rijen in de tweede tabel **en**
- één rij in de tweede tabel hoort bij nul, één of meer rijen in de eerste tabel.

Voorbeeld: een N:M-relatie tussen product en kleur  
- één product kan meerdere kleuren hebben  
- één kleur kan bij meerdere producten horen

Hoe maak je deze relatie in SQL?
- Je maakt een **koppeltabel** (ook wel tussen-tabel genoemd)  
- In deze koppeltabel staan twee verwijzende sleutels:  
  - één die verwijst naar de eerste tabel  
  - één die verwijst naar de tweede tabel

Voorbeeld:

```sql
CREATE TABLE products (
  id INTEGER PRIMARY KEY,
  name TEXT
);

CREATE TABLE colors (
  id INTEGER PRIMARY KEY,
  name TEXT
);

CREATE TABLE product_colors (
  product_id INTEGER,
  color_id INTEGER,
  FOREIGN KEY(product_id) REFERENCES products(id),
  FOREIGN KEY(color_id) REFERENCES colors(id)
);
```

In dit voorbeeld:
- De tabel `product_colors` koppelt producten aan kleuren  
- `product_id` verwijst naar een rij in `products`  
- `color_id` verwijst naar een rij in `colors`  
- Zo kun je aangeven dat één product meerdere kleuren heeft, en één kleur bij meerdere producten hoort

:::

## Maak tabel met kleuren (database)
create table
insert

## Maak tabel die producten en kleuren koppelt (database)

## Beschrijf cardinaliteit (database)
voeg constraint toe

## Geef aan welke producten en kleuren bij elkaar horen (database)
vul verwijzingen in

## Json (uitleg)
api geeft resultaten in de vorm van json
- key value pairs
- dict
- list
voorbeeld

## Query met N:M-relatie maken (uitleg)
:::{note} uitleg
Bij een _N:M-relatie_ combineer je drie tabellen:
- de koppeltabel (bijv. `product_colors`)
- de eerste tabel (bijv. `products`)
- de tweede tabel (bijv. `colors`)

Het maakt in sql niet uit met welke tabel je begint. Wij beginnen met de **koppeltabel** en leggen van daaruit maak je verbinding met de andere twee tabellen.

Voorbeeld: producten met hun kleuren

```sql
SELECT colors.name, products.name
FROM product_colors
JOIN colors ON product_colors.color_id = colors.id
JOIN products ON product_colors.product_id = products.id;
```

Wat gebeurt er in deze query?
- `SELECT` kiest de kolommen die je wilt zien:
  - de naam van de kleur
  - de naam van het product
- `FROM product_colors` betekent dat je begint in de koppeltabel
- `JOIN colors` koppelt elke `color_id` aan een rij in `colors`
- `JOIN products` koppelt elke `product_id` aan een rij in `products`

Je krijgt dan een lijst van combinaties van kleur en product.

:::

## Maak query voor kleuren per product (api)
api aanpassing: query met join
juiste velden selecteren

## Voeg kleurinformatie toe aan producten (api)
