# n:m-relatie
In dit hoofdstuk ga je kleuren toevoegen aan elk product. Kleur en product hebben een n:m-relatie.

## Uitleg: Tabellen met n:m-relatie maken

:::{note} Uitleg

### Wat is een n:m-relatie?

Een _n:m-relatie_ (spreek uit: _en op em relatie_) wordt ook wel een _veel-op-veel-relatie_ (Engels: _many to many relationship_) genoemd. Twee tabellen hebben een een n:m relatie als:  
- één rij in de eerste tabel hoort bij nul, één of meer rijen in de tweede tabel **en**
- één rij in de tweede tabel hoort bij nul, één of meer rijen in de eerste tabel.

Voorbeeld: een n:m-relatie tussen product en kleur  
- één product kan meerdere kleuren hebben  
- één kleur kan bij meerdere producten horen

Hoe maak je deze relatie in SQL?
- Je maakt een **koppeltabel** (ook wel tussen-tabel genoemd)  
- In deze koppeltabel staan twee verwijzende sleutels:  
  - één die verwijst naar de eerste tabel  
  - één die verwijst naar de tweede tabel

(webshop-section4-uitleg-SQLvoorbeeldNMrelatie)=
### SQL voorbeeld van tabellen met n:m-relatie

```sql
CREATE TABLE products (
  id INTEGER PRIMARY KEY,
  name TEXT
);

CREATE TABLE colors (
  id INTEGER PRIMARY KEY,
  name TEXT
);

CREATE TABLE product_color (
  product_id INTEGER,
  color_id INTEGER,
  FOREIGN KEY(product_id) REFERENCES products(id),
  FOREIGN KEY(color_id) REFERENCES colors(id)
);
```

In dit voorbeeld:
- De tabel `product_color` koppelt producten aan kleuren  
- `product_id` verwijst naar een rij in `products`  
- `color_id` verwijst naar een rij in `colors`  
- Zo kun je aangeven dat één product meerdere kleuren heeft, en één kleur bij meerdere producten hoort

:::

## Opdracht: Voeg artikel-kleuren toe aan de database

In deze opdracht ga je kleuren (Engels: colors) toevoegen aan elk artikel in de database. Elk artikel heeft één of meer kleuren. Een kleur wordt gebruikt in één of meer artikelen.

De kleur wordt niet automatisch zichtbaar in je webshop, dat doen we in de volgende opdracht.

:::{note}Opdracht a)
### Kleuren-tabel toevoegen
Maak een nieuwe tabel waarin we de kleuren kunnen opslaan. Noem de tabel `colors`, noem het primaire sleutelveld `id` en maak een tekstveld `name` voor de naam van de kleur.
:::

```{hint} Tips
:class: dropdown
- Zie de [tips bij de opdracht soorten-tabel toevoegen](#webshop-section4-opdracht1a-tips) uit het vorige hoofdstuk.
```

:::{note}Opdracht b)
### Kleuren toevoegen aan de tabel
Voeg kleuren toe aan de tabel die je zojuist gemaakt hebt. Voorbeelden van kleuren zijn Blauw, Rood, Geel en Wit.
:::

```{hint} Tips
:class: dropdown
- Zie de [tips bij de opdracht soorten toevoegen aan de tabel](#webshop-section4-opdracht1b-tips) uit het vorige hoofdstuk.
```

:::{note}Opdracht c)
### Maak koppel-tabel
Omdat kleuren en artikelen een n:m-relatie (veel op veel) hebben, moeten we een extra tabel maken om de kleuren aan de artikelen te koppelen. Maak daarvoor de tabel `product_color`. Voeg aan de tabel een primaire sleutel, twee verwijzende sleutels en twee constraints toe. Gebruik `product_id` en `color_id` als namen voor je verwijzende sleutels. In de constraints zet je aan welke primaire sleutel elk van de verwijzende sleutels is gekoppeld.
:::

```{hint} Tips
:class: dropdown
- Voeg de verwijzende sleutels en de constraints toe aan de tabel `product_color`.
- De volgorde waarin je tabellen in je SQL-bestand zet doet ertoe. De tabel `product_color` moet je na de tabellen `products` en `colors` maken, anders dan kun je er niet naar verwijzen in je constraints in de tabel `product_color`.
- Als je niet meer weet hoe je een constraint toevoegt, bekijk dan [Uitleg SQL voorbeeld n:m-relatie](#webshop-section4-uitleg-SQLvoorbeeldNMrelatie)
```

:::{note}Opdracht d)
### Voeg toe welke kleuren elk artikel heeft
Voeg aan elk artikel toe welke kleuren erin zitten.
:::

```{hint} Tips
:class: dropdown
- Maak een `INSERT INTO`-opdracht die de `product_color`-tabel vult.
- Gebruik in de `INSERT INTO`-opdracht de velden `product_id` en `color_id`.
- Geef in je `INSERT INTO`-opdracht de nummers van de producten en kleuren die bij elkaar passen op. Elke conmbinatie is een nieuwe rij in de tabel.
````

## Uitleg: JSON

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
      "id": 1,
      "name": "Smurfin",
      "merk": "Smurf Mania",
      "kleur": [
        "Geel",
        "Blauw",
        "Wit"
      ]
    },
    {
      "id": 3,
      "name": "Grote smurf",
      "merk": "Smurf Mania",
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


## Uitleg: Query met n:m-relatie maken
:::{note} Uitleg

### Query met SELECT FROM JOIN JOIN voor n:m-relatie
Bij een _n:m-relatie_ combineer je drie tabellen:
- de koppeltabel (bijv. `product_color`)
- de eerste tabel (bijv. `products`)
- de tweede tabel (bijv. `colors`)

Het maakt in sql niet uit met welke tabel je begint. Wij beginnen met de **koppeltabel** en leggen van daaruit maak je verbinding met de andere twee tabellen.

Voorbeeld: producten met hun kleuren

```sql
SELECT colors.name, products.name
FROM product_color
JOIN colors ON product_color.color_id = colors.id
JOIN products ON product_color.product_id = products.id;
```

Wat gebeurt er in deze query?
- `SELECT` kiest de kolommen die je wilt zien:
  - de naam van de kleur
  - de naam van het product
- `FROM product_color` betekent dat je begint in de koppeltabel
- `JOIN colors` koppelt elke `color_id` aan een rij in `colors`
- `JOIN products` koppelt elke `product_id` aan een rij in `products`

Je krijgt dan een lijst van combinaties van kleur en product.

:::

## Opdracht: Maak kleuren per artikel zichtbaar in de webshop
Je hebt in de vorige opdracht kleur-informatie aan alle artikelen toegevoegd in de database. Maar deze informatie is nog niet te zien op de webshop. Dat komt omdat de API de kleuren niet opvraagt uit de database. Omdat er meerdere kleuren per product kunnen zijn, moeten we de kleuren in een aparte query opvragen. In deze opdracht ga je de API aanpassen, zodat de informatie over kleuren wordt toegevoegd aan de informatie over artikelen die wordt opgestuurd naar de client. De client is zo gemaakt dat hij deze extra informatie automatisch toont.

:::{note}Opdracht
### Maak kleuren-query en voeg die toe aan artikel-informatie in JSON-formaat
De onderstaande code vraagt voor elk artikel de kleuren op uit de database en voegt deze toe aan de artikelinformatie (`product_rows`). De API stuurt `product_rows` in JSON-formaat naar de client. 

Maak de query in de code af door op de plekken met `<maak af>` de juiste stukje query in te vullen. De query eindigt met een vraagteken `?`. Op die plek wordt steeds het `product_id` ingevuld van het product waarvan we de kleuren opvragen.

```{code}python
    # Add values for n:m property (e.g., colors) to products
    for product in product_rows:
        # Fetch colors for the product
        color_query = """
            SELECT <maak af>
            FROM <maak af>
            JOIN <maak af>
            WHERE product_id = ?
        """
        # Execute the query to fetch colors for the current product
        color_rows = db_connection.execute(color_query, (product["id"],)).fetchall()

        # Add fetched colors to product
        colors = []
        for row in color_rows:
            colors.append(row["name"])
        product["kleur"] = colors
```

Kopieer de code op de juiste plek in de API en test of hij het doet.

```{attention} Performance
:class: dropdown
We gebruiken voor elk product een aparte query om de kleuren uit de database op te vragen. Dit is niet heel efficient, maar wel eenvoudig. In een webshop met veel meer artikelen zouden programmeurs ervoor kiezen om de kleuren van alle producten tegelijk in één query op te vragen.
```

```{attention} SQL-injection
:class: dropdown
In onze code wordt de `execute` functie gebruikt om de query uit te voeren. De `execute`-functie vult ook de parameters in, zoals `product_id`. We hadden die parameter ook gewoon met `+` aan de query kunnen toevoegen,maar dat doen we bewust niet. 

Tijdens het invullen controleert de `execute`-functie of er geen rare dingen in het `product_id` staan. In deze code komt de waarde van `product_id` uit de database waar alleen ontwikkelaars bij kunnen. Bij het hoofdstuk over filters zul je zien dat parameters ook door de client (de computer van bezoekers) opgestuurd kunnen worden. Deze parameters zouden bezoekers kunnen veranderen voordat ze ze opsturen. 

Door de waarde van de parameter slim te kiezen kunnen gebruikers informatie uit de database halen die niet voor hen bedoeld is. Denk bijvoorbeeld aan een parameter `product_id` met de waarde `1; SELECT * FROM passwords;`. De database denkt dan dat hij twee opdrachten moet uitvoeren waarvan de laatste de wachtwoorden geeft. Deze truuk heet _SQL-injectie_. 

In de praktijk is het meestal niet zo gemakkelijk om een systeem te hacken met SQL-injectie, onder andere omdat wachtwoorden niet zomaar in een database worden gezet. Maar als je Googlet op SQL-injection, dan zie je dat het een veelvoorkomend probleem is. In onze database kan dit niet gebeuren, omdat we alle parameters door de `execute`-functie laten controlere.
```

:::

```{hint} Tips
:class: dropdown
- De aanpassing moet je doen in de API, in het bestand `/app/main.py` bij de functie voor het endpoint `/api/products/`.
- Let op de commentaarregel om te zien naar welke plek je de code exact moet kopieren.
- Voeg aan de query een `SELECT` toe met één veld, namelijk de naam van de kleur.
- Voeg aan de query een `JOIN` toe tussen de tabellen `product_color` en `colors`.
- Controleer wat de API opstuurt naar de client. Zet in je browser achter de hostname van je webshop `/api/products/` en laadt die webpagina. Het antwoord is hetzelfde antwoord als wat de client van de API zou krijgen. Je ziet de artikelinformatie in JSON-formaat.
```
