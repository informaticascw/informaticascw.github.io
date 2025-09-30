
# 1:n-relatie
In dit hoofdstuk ga je een merk toevoegen aan elk product. Merk en product hebben een 1:n-relatie.


## Uitleg: Tabellen met 1:n-relatie maken

:::{note} uitleg
### Wat is een 1:n-relatie?

Een _1:n-relatie_ (spreek uit: _één op en relatie_) wordt ook wel een _één-op-veel-relatie_ (Engels: _one to many relationship_) genoemd. Twee tabellen hebben een 1:n-relatie als:  
- één rij in de eerste tabel hoort bij nul, één of meer rijen in de tweede tabel **en**
- één rij in de tweede tabel hoort bij nul of één rijen in de eerste tabel.

Voorbeeld: een 1:n-relatie tussen merk en product  
- één merk kan nul, één of meer producten hebben  
- elk product hoort bij nul of één merk

Hoe maak je deze relatie in SQL?
- Je zet een _verwijzende sleutel_ (Engels: foreign key) in de tweede tabel. De verwijzende sleutel staat dus in de tabel van de N.  
- Je geeft aan dat die verwijst naar de _primaire sleutel_ (Engels: primary key) van de eerste tabel.  

(webshop-section4-uitleg-SQLvoorbeeld1Nrelatie)=
### SQL voorbeeld van tabellen met 1:n-relatie

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
- `products.brand_id` is een foreign key (n-kant)  
- Bij een product dat niet aan een merk gekoppeld is, heeft de verwijzende sleutel de waarde `NULL`
- Een merk **kan** aan een product gekoppeld zijn, maar dat **hoeft niet**

:::

## Opdracht: Voeg merk toe aan de database

In deze opdracht ga je een merk (Engels: brand) toevoegen aan elk artikel in de database. Elk artikel is van één merk. Een merk heeft één of meer artikelen.

Her merk wordt niet automatisch zichtbaar in je webshop, dat doen we in de volgende opdracht.

:::{note}Opdracht a)
### Merken-tabel toevoegen
Maak een nieuwe tabel waarin we de merken kunnen opslaan. Noem de tabel `brands`, noem het primaire sleutelveld `id` en maak een tekstveld `name` voor de naam van het merk.
:::

(webshop-section4-opdracht1a-tips)=
```{hint} Tips
:class: dropdown
- Gebruik de SQL-opdracht `CREATE TABLE`
- Na een aanpassing moet je de database opnieuw maken met het terminal-commando `bash start.sh`. Let op of er foutmeldingen in de terminal verschijnen.
- Als je geen producten meer ziet in je shop, dan heb je waarschijnlijk een fout gemaakt waardoor de webshop de database niet opnieuw kan maken. Bekijk de foutmeldingen in de terminal.
```

:::{note}Opdracht b)
### Merken toevoegen aan de tabel
Voeg de merken die je in je winkel verkoopt toe aan de tabel die je zojuist gemaakt hebt. Gebruik de merken `Smurf Mania` en `Totally Smurf`.
:::

(webshop-section4-opdracht1b-tips)=
```{hint} Tips
:class: dropdown
- gebruik de SQL-opdracht `INSERT INTO`
```

:::{note}Opdracht c)
### Koppel tabellen
Koppel de tabellen door het toevoegen van een verwijzende sleutel en een constraint. Gebruik `brand_id` als naam voor je verwijzende sleutel. In de constraint zet je aan welke primaire sleutel de verwijzende sleutel is gekoppeld.
:::

(webshop-section4-opdracht1c-tips)=
```{hint} Tips
:class: dropdown
- Voeg de verwijzende sleutel en de constraint toe aan de tabel `products`.
- De verwijzende sleutel heeft het datatype `INTEGER`.
- De contraint is van de vorm met `FOREIGN KEY(`_verwijzende_sleutel_`) REFERENCES(`_tabel_`.`_primaire_sleutel_`)`
- De volgorde waarin je tabellen in je SQL-bestand zet doet ertoe. De tabel `brandss` moet je eerder maken dan de tabel `products`, anders dan kent de computer de tabel `brands` nog niet als je ernaar wilt verwijzen in je constraint.
```

:::{note}Opdracht d)
### Voeg toe van welk melk elk artikel is
Voeg aan elk artikel toe welke soort erbij hoort.
:::

(webshop-section4-opdracht1d-tips)=
```{hint} Tips
:class: dropdown
- Pas de `INSERT INTO`-opdracht die de `products`-tabel vult aan. 
- Voeg het veld `brand_id` toe aan `INSERT INTO products` en geef voor elk product het nummer van de soort op.
```

## Uitleg: Query met 1:n-relatie maken
:::{note} Uitleg

### Query met SELECT FROM JOIN voor 1:n-relatie
Bij een _1:n-relatie_ kun je een query maken om gegevens uit beide tabellen te combineren.  
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

## Opdracht: Maak merk zichtbaar in de webshop
Je hebt in de vorige opdracht het merk aan alle artikelen in de database toegevoegd. Maar de naamm van het merk is nog niet te zien op de webshop. Dat komt omdat de API niks doet met de merken-tabel de database. In deze opdracht ga je de API aanpassen, zodat de informatie uit de merken-tabel wordt doorgeven aan de client. De client is zo gemaakt dat hij deze extra informatie automatisch toont.

:::{note}Opdracht a)
### Voeg merk toe aan query
Zoek in de API de query die de artikelen (`products`) opvraagt. Voeg hier een `JOIN` aan toe, zodat de informatie uit de merken-tabel wordt toegevoegd.
:::

```{hint} Tips
:class: dropdown
- De aanpassing moet je doen in de API, in het bestand `/app/main.py`
- De query die je moet aanpassen is `SELECT * FROM products;`
- Voeg aan de query een `JOIN` toe tussen de tabellen `products` en `brands`.
- Als je op de plaats van de naam van je product de naam van het merk ziet, dan komt dat omdat onze client `products.name` met `brands.name` overschrijft. Laat dat voor nu even zo, in de volgende opdracht leer je hoe je dit oplost.
```

:::{note}Opdracht b)
### Veldnamen opschonen
De website gebruikt de namen van de velden uit de database. Dit geeft twee schoonheidsproblemen in de website.

1. De webpagina toont alle velden uit de database. De velden met verwijzende sleutels worden getoond, maar die zijn niet nuttig voor gebruikers.
2. De veldnamen in de database zijn Engelstalig. Dat is handig voor programmeurs, maar onze gebruikers zijn vaak Nederlandstalig. 

Pas de query in de api aan op de volgende punten.

1. Vervang `*` (dit betekent: alle velden) uit de query door de namen van de velden die je nodig hebt.
2. Gebruik `AS` om velden een Nederlandse naam te geven.
3. Velden met de naam `name`, `image_link` en `price` uit de tabel products moet je in je query opnemen zonder de naam te veranderen. Deze veldnamen worden door de website herkent en speciaal behandeld.
:::

```{hint} Tips
:class: dropdown
- De query die je moet aanpassen is `SELECT * FROM products JOIN ...`
- In de query moet je `SELECT * FROM` vervangen door `SELECT products.name, products.image_link, products.price ... FROM`. Op de puntjes vul je de overige veldnamen in.
- Je kunt velden een andere naam in de website geven met `AS`. Bijvoorbeeld `SELECT description` vervangen door `SELECT description AS beschrijving`.
- In de database kun je dezelfde veldnamen in meerdere tabellen gebruiken. Onze api stuurt de namen van de velden zonder tabelnaam naar de client. De client ziet daardoor het verschil niet tussen velden met dezelfde naam uit verschillende tabellen. Je kunt dat oplossen in de query die je in de api gebruikt. Daar kun je de velden met dezelfde naam een unieke naam geven.
Bijvoorbeeld: `SELECT products.name, brands.name` wordt `SELECT products.name, brands.name AS merk`
```