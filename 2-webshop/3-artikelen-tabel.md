# Artikelen-tabel
```{pull-quote}
We maken vriendjes en een plek om te wonen.
```

```{figure} scherm2.png
Schermafdruk van webshop aan het einde van dit hoofdstuk.
```

In dit hoofdstuk ga je meer artikelen toevoegen en krijgen je artikelen meer velden, zoals een beschrijving en een prijs.

## Uitleg: Gegevens toevoegen
:::{note} Uitleg
### Gegevens toevoegen met INSERT INTO

Als de tabel bestaat, kun je er gegevens in zetten.  
Dat doe je met de opdracht `INSERT INTO`.

Je geeft aan:
- aan welke tabel je iets toevoegt  
- welke kolommen je invult  
- welke waarden je opslaat  

### Voorbeeld: één product toevoegen

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

### Voorbeeld: meerdere producten toevoegen

Je kunt meerdere regels toevoegen door meerdere `INSERT` commando's onder elkaar te zetten. 
Je kunt ook meerdere regels tegelijk toevoegen met één insert commando. Dit gaat als volgt.

```sql
INSERT INTO products (id, name, price) VALUES
  (2, 'Muzieksmurf', 14.95),
  (3, 'Grote smurf', 10.50);
```
:::

## Opdracht: Voeg artikelen toe

:::{note} Opdracht
Voeg twee artikelen toe aan de database.

Je hoeft hiervoor alleen de database aan te passen.
:::

```{hint} Tips
:class: dropdown
- Aanpassingen in de database doe je in het bestand `/data/init.sql`. Na een aanpassing moet je de database opnieuw maken met het terminal-commando `bash start.sh`.
- Als je helemaal geen artikelen meer ziet, dan heb je waarschijnlijk een fout gemaakt in de SQL. Foutmeldingen verschijnen in de terminal als je de database opnieuw aanmaakt.
- Voeg elk artikel toe met een apart INSERT INTO commando. 
- Als de artikelen zichtbaar zijn, probeer dan de leesbaarheid van je code te verbeteren door alle artikelen in één INSERT INTO commando te zetten.
- Er staat een komma tussen elke artikel in een INSERT INTO commando, er staat geen komma na het laatste artikel in INSERT INTO.
```

## Uitleg: Een tabel maken in SQL
:::{note} Uitleg
### Wat zit er in een tabel?

In een database staan gegevens in tabellen.
Een tabel bestaat uit kolommen.

Elke kolom heeft:
- een naam (zoals id of name)
- een gegevenstype (zoals tekst of een getal)

Veelgebruikte gegevenstypen:
- TEXT → een stuk tekst (zoals "Smurfin")
- REAL → een kommagetal (zoals 9.50 of 14.95)
- INTEGER → een heel getal (zoals 1, 25, 100)
- INTEGER PRIMARY KEY is een bijzondere soort INTEGER, het is een heel getal en elke waarde in de kolom mag maar één keer gebruikt worden.

### Voorbeeld om een tabel te maken in SQL

```sql
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

:::

```{tip} komma's, punten en puntkomma's
De komma `,` wordt gebruikt als **scheiding** tussen kolommen. Na de laatste kolom komt dus geen komma meer. Als je een kolom aan het einde van de tabel toevoegt, dan moet je niet vergeten de komma toe te voegen achter de één na laatste kolom.

De punt `.` wordt gebruikt als **decimaalteken**. Dus een prijs van 4 euro en 99 cent wordt genoteerd als `4.99`. Als je per ongeluk een komma gebruikt in plaats van een punt, dan denkt de computer dat het twee gehele getallen zijn.

De puntkomma `;` wordt gebruikt als **afsluiting** van elk commando. Het maken van een tabel is een commando. Er staat een puntkomma na elke tabel die je maakt, dus ook na de laatste tabel.
```

## Opdracht: Voeg artikel-beschrijvingen toe

:::{note} Opdracht
Voeg aan elk artikel een beschrijving toe.

Maak in de database een extra veld in de tabel product. Geef het veld de naam `beschrijving` en geef aan dat er tekst in staat. Voeg de beschrijvingen toe aan de database door het `INSERT INTO` commando aan te passen.

Je hoeft alleen de database aan te passen. De API en de front-end (het static-deel) zijn zo gemaakt, dat alle extra velden die je maakt automatisch worden getoond.
:::

```{hint} Tips
:class: dropdown
- Aanpassingen in de database doe je in het bestand `/data/init.sql`. Na een aanpassing moet je de database opnieuw maken met het terminal-commando `bash start.sh`.
- Let op foutmeldingen in de terminal als je de database opnieuw aanmaakt.
```

## Opdracht: Voeg artikel-prijzen toe

:::{note} Opdracht
Voeg aan elk artikel een beschrijving toe.

Maak in de database een extra veld met de naam `price`. Geef aan dat er een kommagetal in staat. Voeg de prijzen toe aan de database door het `INSERT INTO` commando aan te passen.

De front-end is zo gemaakt dat een veld met de naam `price` speciaal wordt behandeld. De prijzen worden automatisch voorzien van een euro-teken en afgerond op twee cijfers achter de komma.
:::

```{hint} Tips
:class: dropdown
- Denk aan het juiste gebruik van komma en punt, zie de uitleg hierboven.
- Als je in je webshop het bedrag ziet zonder euro-teken ervoor, kijk dan of je het veld de goede naam (`price`) hebt gegeven.
- Zie tips bij de vorige exercise.
```
