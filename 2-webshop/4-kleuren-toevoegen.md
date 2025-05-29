# Kleuren aan product toevoegen
In ons voorbeeld bestaat een product uit één of meer kleuren en een kleur wordt gebruikt in één of meerdere producten. Dat betekent dat er een n:m (spreek uit als "en op em") relatie tussen producten en kleuren. Andere voorbeelden van een n:m relatie zijn materialen of ingrediënten.

## Tabellen met N:M-relatie maken (uitleg)

:::{note} Uitleg

### Wat is een N:M-relatie?

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

### SQL voorbeeld:

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

## JSON (uitleg)

:::{note} Uitleg
### Wat is JSON?

_JSON_ (Spreek uit als djee-sun) is een formaat om gegevens op te slaan of door te geven tussen systemen. JSON is gemakkelijk te lezen voor mensen en gemakkelijk te gebruiken in veel programmeertalen zoals Python en JavaScript. Het wordt veel gebruikt bij informatieuitwisseling tussen systemen die via het het internet met elkaar zijn verbonden. De schrijfwijze van JSON lijkt een beetje op Python, maar is bedoeld voor uitwisseling van gegevens in plaats van code.

### Structuur van JSON

JSON kent dictionaries, lists en key-value pairs.
- Een _dictionary_ (_woordenboek_) is een set key-value pairs. Elke key is uniek binnen de dictionary en de volgorde van de keys maakt niet uit. Een dict begint met `{` en eindigt met `}` (spreek uit als krulhaken of curly brackets), daartussen staan de key-value pairs. Key-value pairs worden gescheiden door `,` (spreek uit als komma of comma).
- Een _key-value pair_ bestaat uit een sleutel en een waarde, gescheiden door `:` (spreek uit als dubbele punt of collon).
- Een _key_ (_sleutel_) is een stukje tekst. Sleutels worden geschreven tussen `"` en `"` (spreek uit als dubbele quotes of double quotes). De dubbele quotes zijn één karakter, dus niet twee enkele quotes achter elkaar. Verder zijn de quotes recht, daardoor is er geen verschil tussen de quotes aan het begin en het einde van een tekst.
- Een _value_ (_waarde_) kan true of false, een enkel getal of stuk tekst zijn. Maar op de plek van een waarde kan ook weer een nieuwe dictionary of list staan.
- Een _list_ (_lijst_) is een geordende lijst met waarden. Elke waarde mag meer dan één keer voorkomen en de volgorde van de waarden doet er toe. Een list begint met `[` en eindigt met `]` (spreek uit als vierkante haken of square brackets), daartussen staan de waarden. Waarden worden gescheiden door `,` (komma of comma).

```{note} JSON in JavaScript
In JavaScript is de notatie van JSON exact gelijk aan de notatie van JSON in Python. De terminologie is wel anders. In Python worden de termen dictionary en list gebruikt, terwijl in JavaScript de termen object en array worden gebruikt. Keys met meerdere woorden worden in JavaScript vaak geschreven als firstSecond (camelCase) en in Python als first_second (snake_case). Maar beide manieren werken in beide talen. Wij kiezen voor snake_case.
```

### Voorbeeld van JSON

Hieronder zie je een voorbeeld van JSON:

```json
{
  "products": [
    {
      "id": 3,
      "name": "Smurfin",
      "merk": "Smurf Toys Inc.",
      "kleur": [
        "Geel",
        "Blauw",
        "Wit"
      ]
    },
    {
      "id": 4,
      "name": "Grote smurf",
      "merk": "Smurf Toys Inc.",
      "kleur": [
        "Rood",
        "Blauw",
        "Wit"
      ]
    }
  ]
}
```

Dit voorbeeld bevat een lijst met producten. 
- Het hoogste niveau is een list met één key `"products"`.
- De waarde van `"products"` is een **list** van producten.
- Elk product is een **dict** met key values pairs:
  - een `id` met als waarde een getal
  - een `name` met als waarde een tekst
  - een `merk` met as waarde een tekst
  - een `kleur` met als waarde een list

:::


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
