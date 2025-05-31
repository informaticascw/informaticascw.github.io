
# 1:N-relatie
In dit hoofdstuk ga je een soort toevoegen aan elk product. Soort is een voorbeeld van een 1:N-relatie.


## Uitleg: Tabellen met 1:N-relatie maken

:::{note} uitleg
### Wat is een 1:N-relatie?

Een _1:N-relatie_ (spreek uit als "één op en relatie") betekent:  
- één rij in de eerste tabel hoort bij nul, één of meer rijen in de tweede tabel **en**
- één rij in de tweede tabel hoort bij nul of één rijen in de eerste tabel.

Voorbeeld: een 1:N-relatie tussen merk en product  
- één merk kan nul, één of meer producten hebben  
- elk product hoort bij nul of één merk

Hoe maak je deze relatie in SQL?
- Je zet een _verwijzende sleutel_ (Engels: foreign key) in de tweede tabel. De verwijzende sleutel staat dus in de tabel van de N.  
- Je geeft aan dat die verwijst naar de _primaire sleutel_ (Engels: primary key) van de eerste tabel.  

### SQL voorbeeld van tabellen met 1:N-relatie

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

## Opdracht: Voeg soort artikel toe aan de database

:::{note}Opdracht a)
### Tabel met soorten toevoegen
create table
:::

```{hint} Tips
:class: dropdown
- xxxxxx
```

:::{note}Opdracht b)
### Soorten toevoegen aan de tabel
insert
:::

```{hint} Tips
:class: dropdown
- xxxxxx
```

:::{note}Opdracht c)
### Koppel tabellen
verwijzende sleutel
laat de naam eindigen op _id, dan kan onze website er goed mee omgaan

voeg constraint toe
FOREIGN KEY
:::

```{hint} Tips
:class: dropdown
- xxxxxx
```

:::{note}Opdracht d)
### Voeg toe welke soort elk artikel is
INSERT
:::

```{hint} Tips
:class: dropdown
- xxxxxx
```

## Uitleg: Query met 1:N-relatie maken
:::{note} Uitleg

### Query met SELECT FROM JOIN voor 1:N-relatie
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

## Opdracht: Maak soort artikel zichtbaar in de webshop

:::{note}Opdracht a)
### Voeg soort toe aan query (api)
api aanpassing: query met join
:::

```{hint} Tips
:class: dropdown
- De aanpassing moet je doen in de API, in het bestand `/app/main.py`
- De query die je moet aanpassen is `SELECT * FROM Products;`
- Voeg aan de query een `JOIN` toe tussen de tabellen `Products` en `Categories`.
```

:::{note}Opdracht b)
### Verwijder overbodige velden
INSERT

speciale velden: name, price, description uit de tabel products worden herkend in de html en op speciale wijze getoond
het veld id de tabel products en velden die eindigen op _id worden herkend in de html en niet getoond, deze zijn wel handig om erin te houden

de website gebruikt de naam van de velden, meestal zijn die Engelstalig. Het is handig om die in de api aan te passen
AS gebruiken
:::

```{hint} Tips
:class: dropdown
- xxxxxx
```