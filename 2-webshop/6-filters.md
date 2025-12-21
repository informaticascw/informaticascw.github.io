(webshop-filters)=
# Filters

```{pull-quote}
De keuze is reuze.
```

```{figure} scherm5.png
Schermafdruk van webshop aan het einde van dit hoofdstuk.
```

In dit hoofdstuk ga je filters toevoegen aan je webshop. Met filters kun je selecteren welke artikelen getoond worden.

## Uitleg: REST-API

:::{note} Uitleg
### REST

API (Engels, spreek uit ee-pie-aai) staat voor Application Programming Interace. Een API is een stuk software dat computerprogramma op een gestandaardiseerde manier met elkaar verbindt. Een API tussen computerprogramma's die via het internet met elkaar zijn verbonden heet een webservice. Een webservice wordt aangeboden door een server en gebruikt door één of meerdere clients. Moderne webservices zijn RESTful (Engels, spreek uit als rest-foel). REST staat voor REpresentational State Transfer, maar meestal wordt alleen de afkorting gebruikt. REST is geen protocol maar een set ontwerp-richtlijnen.

Hier volgen enkele ontwerp-richtlijnen van REST.

Platform-onafhankelijk
: REST werkt via standaardprotocollen zoals HTTP en maakt gebruik van eenvoudige dataformaten zoals JSON. Daardoor kunnen verschillende systemen zoals Windows, Linux, iOS en Android probleemloos met elkaar communiceren.

Client-Server scheiding
: De client (zoals een app of website) en de server (waar de gegevens staan) werken onafhankelijk van elkaar. De client weet alleen wat hij nodig heeft, niet hoe de server dat regelt. Dit maakt onderhoud en ontwikkeling eenvoudiger: de client-zijde (wordt ook genoemd: front end) en server-zijde (wordt ook genoemd: back end) kunnen apart worden aangepast.

Statusloos
: Elke aanvraag (request) van de client bevat alle informatie die de server nodig heeft. De server bewaart geen gegevens over vorige aanvragen. Daardoor zijn REST API’s gemakkelijk uit te breiden en te beheren.

Clients en servers met REST API's communiceren met HTTP. Dit is hetzelfde protocol dat webbrowsers gebruiken om een webpagina van een server op te vragen. De client verstuurt een HTTP-request naar de server. De server antwoordt met een HTTP-response.

### HTTP-request

Een request is een bericht van de client (bijvoorbeeld een browser of app) naar de server (API). Hiermee vraag je iets op, voeg je iets toe, of verander/verwijder je iets.

Een request bestaat uit:

- Method (actie die je uitvoert – gebaseerd op CRUD):
  - GET – Gegevens opvragen (Read)
  - POST – Nieuwe gegevens aanmaken (Create)
  - PUT – Gegevens volledig bijwerken (Update)
  - DELETE – Gegevens verwijderen (Delete)
- Endpoint: De link naar de resource, zoals /gebruikers/42.
- Headers: bijvoorbeeld
 - Content-Type: Geeft aan in welk formaat je data stuurt (bijv. application/json)
 - Authorization: Bevat een token of API-key voor toegang tot beveiligde data
- Body (optioneel): De gegevens die je meestuurt, bijvoorbeeld een JSON-object bij POST of PUT.

### HTTP-response

Een response is het antwoord van de server op het verzoek van de client.

Een response bevat:

- Statuscode (resultaat van de aanvraag), bijvoorbeeld:
  - 200 OK – Alles is goed verlopen
  - 401 Unauthorized – Geen toegang (bijv. geen of fout token)
  - 404 Not Found – Gevraagde resource bestaat niet
  - 500 Internal Server Error – Fout aan serverzijde
- Headers: Extra info over het antwoord, zoals het dataformaat
- Body: De gegevens die teruggestuurd worden (bijv. een lijst, een bevestiging of een foutmelding)
:::

## Opdracht: Toon filters voor merk en kleur
De client is al voorbereid voor het werken met filters, maar de API nog niet. In deze opdracht ga je zorgen dat de filters zichtbaar worden in de webshop. In de volgende opdracht zorg je dat alleen de artikelen worden getoond die in het filter zijn ingesteld.

:::{note}Opdracht a)
### Maak filters
De client vraagt via het endpoint `/api/filters` de lijst met filters op. In de API is het eindpoint al gemaakt, maar het geeft een lege lijst terug. De client geeft alleen filters weer als de lijst niet leeg is.

Maak een lijst met filters door onderstaande code op de juiste plaats in de API te zetten en test of het werkt.

Als je het goed gedaan hebt, dan zie je de filters in je webshop en kun je vinkjes zetten. De knop "Filter toepassen" werkt nog niet, dat komt in een volgende opdracht.

```{code} python
:caption: Python-code
:linenos:
    # Construct the response
    filters = {
        "merk": ["Smurf Mania","Totally Smurf"],
        "kleur": ["rood","geel","blauw"]
    }
```

:::

```{hint} Tips
:class: dropdown
- De code moet worden ingevoegd in de functie `get_filters()` uit de API. 
- Let op het commentaar om de exacte plek te vinden waarnaar je de code moet kopieren.
```

:::{note}Opdracht b)
### Maak filters automatisch
Bij opdracht a) heb je filters gemaakt. Maar als je een artikel met een nieuwe kleur aan je database toevoegt, dan moet je het filter aanpassen voordat je op die kleur kunt filteren. Voor nu is dat misschien okee, maar in een grote webshop is dat erg onhandig. In deze opdracht ga het filter zo maken dat hij de waarden van merk en kleur uit de database haalt.

Maak de twee queries in onderstaande code af. De eerste query moet alle merken in de database geven en de tweede query alle kleuren.

Kopieer de code op de juiste plek in de API en test of hij het doet.

Als je het goed gedaan hebt, dan zie je de filters in je webshop en kun je vinkjes zetten. Als je op de knop "Filter toepassen" klik, dan gebeurt er niets. In de volgende opdracht ga je zorgen dat het filter wordt toegepast.

```{code} python
:caption: Python-code
:linenos:
    # Fetch all distinct brands
    brands_query = "SELECT <maak af>"
    brands_result = db_connection.execute(brands_query).fetchall()
    brands = [row["name"] for row in brands_result]

    # Fetch all distinct colors
    colors_query = "SELECT <maak af>"
    colors_result = db_connection.execute(colors_query).fetchall()
    colors = [row["name"] for row in colors_result]

    # Construct the response
    filters = {
        "merk": brands,
        "kleur": colors
    }
```

:::

```{hint} Tips
:class: dropdown
- De code moet worden ingevoegd in de functie `get_filters()` uit de API. 
- Let op het commentaar om de exacte plek te vinden waarnaar je de code moet kopieren.
- Maak beide SQL-queries in de code af.
```

## Uitleg: Extra gegevens in een request

:::{note} Uitleg
### Extra gegevens in een request

Bij het gebruiken van een REST API kun je informatie op verschillende manieren meegeven in een request. Hier zijn de drie meest gebruikte manieren:

Informatie in het endpoint zelf (path parameters)
: Je stopt informatie direct in de link, als onderdeel van het pad.
: Dit gebruik je voor het opvragen van een specifiek item.
: Voorbeeld: `/leerlingen/42` → vraag leerling met ID 42 op
: Voorbeeld: `/boeken/9783` → vraag boek met ISBN 9783 op
: Het getal of woord in de link wordt herkend als een parameter.

Informatie achter het endpoint met `?` (query parameters)
: Je zet parameters achter een vraagteken in de link.
: Dit wordt gebruikt om informatie mee te geven voor filteren, zoeken, sorteren of pagineren.
: Voorbeeld: `/leerlingen?klas=5V`
: Voorbeeld: `/producten?categorie=boeken&sort=prijs`
: Meerdere parameters worden gescheiden met een `&`, meerdere waarden voor dezelfde parameter worden gescheiden door een `,`.

Informatie in de body (bij POST en PUT)
: Stuur de gegevens mee in de body van de request, meestal in JSON-formaat.
: Dit gebruik je als je gegevens aanmaakt of bijwerkt.
: Dit zie bijvoorbeeld bij: `POST /leerlingen` → nieuwe leerling toevoegen
: en bij `PUT /gebruikers/42` → gebruiker met ID 42 aanpassen
: De data staat niet in de link, maar wordt meegestuurd in de inhoud van het verzoek.
:::

## Opdracht: Laat filters op merk en kleur werken

De client van de webshop stuurt het filter als query-parameter mee naar het endpoint `/api/products` als op de knop `Filter toepassen` geklikt wordt. Om alleen de artikelen terug te sturen die aan het filter voldoen, moet je in de API een `WHERE`-clausule toe voegen aan het `SELECT`-commando dat de artikel-informatie uit de database ophaalt. Bekijk de tabel om te zien hoe het filter uiteindelijk moet gaan werken.

:::{table} Werking van filter

Smurf Mania | Totally Smurf | rood | geel | blauw | getoonde artikelen | WHERE-clausule
:---: | :---: | :---: | :---: | :---: | --- | ---
☐ | ☐ | ☐ | ☐ | ☐ | alle artikelen | geen
☑ | ☐ | ☐ | ☐ | ☐ | artikelen van Smurf Mania, de kleur maakt niet uit | `WHERE merk IN ("Smurf Mania")`
☑ | ☑ | ☐ | ☐ | ☐ | artikelen van (Smurf Mania of Totally Smurf), de kleur maakt niet uit | `WHERE merk IN ("Smurf Mania", "Totally Smurf")`
☐ | ☐ | ☑ | ☐ | ☐ | artikelen met rood, het merk maakt niet uit | `WHERE kleur IN ("rood")`
☑ | ☐ | ☑ | ☐ | ☐ | artikelen van Smurf Mania met rood | `WHERE merk IN ("Smurf Mania") AND kleur IN ("rood")`
☑ | ☑ | ☐ | ☑ | ☑ | artikelen van (Smurf Mania of Totally Smurf) met (geel of blauw) | `WHERE merk IN ("Smurf Mania", "Totally Smurf") AND kleur IN ("geel", "blauw")`

:::

Je gaat het filter stap voor stap maken in a) tot en met d) van deze opdracht. Je moet daarbij SQL en Python-code toevoegen aan de API. Breidt je database uit als dat nodig is om alle combinaties te kunnen testen.

:::{note}Opdracht a)
### Filter op 0 of 1 merken

Onderstaande pseudo-code en bijpassende python-code zorgen ervoor dat het filter werkt als er nul, één of meerdere merken geselecteerd zijn. Bestudeer de pseudo-code en de Python-code. 

Knip en plak de Python-code op de juiste plek in de API en controleer of de eerste twee voorbeelden uit de tabel goed werken.

```{code} pseudo 
:caption: Pseudo-code
:linenos:
    als aantal_merken > 0
        plak ` WHERE ` aan query
        
    als aantal_merken > 0
        plak `merken IN (? ` aan query
        plak 1e_merk aan parameter-lijst
        plak `)` aan query         
```

```{code} python
:caption: Python-code
:linenos:
    # add WHERE to query if applicable
    if len(brand_filter_values) > 0 :
        query = query +  " WHERE "

    # add BRANDS IN to query if applicable
    if len(brand_filter_values) > 0:
        query = query +  "brands.name IN ( ?"
        query_params.append(brand_filter_values[0])
        query = query +  ")"
```
:::

```{hint} Tips
:class: dropdown
- De code moet worden ingevoegd in de functie `get_products()` uit de API.
- De exacte plek voor de code is nadat de basis query met `SELECT` wordt gemaakt en vóórdat de query wordt uitgevoerd (execute)
- Letop dat de query niet eindigt met `;` (puntkomma), want als je er dan `WHERE` aan vastplakt dan denkt de database dat je twee opdrachten tegelijk wilt uitvoeren. Dat geeft een foutmelding in de API waardoor de producten niet geladen kunnen worden.
```

:::{note}Opdracht b)
### Filter op 0, 1 of meer merken

Onderstaande pseudo-code is een uitbreiding op de pseudo-code uit onderdeel a). De nieuwe regels zijn gemarkeerd. 

Breidt de Python-code in de API uit, zodat het werkt zoals beschreven staat in de pseudo-code. Controleer of de eerste drie voorbeelden uit de tabel goed werken.

```{code} pseudo
:caption: Pseudo-code
:linenos:
:emphasize-lines: 7,8,9
    als aantal_merken > 0
        plak ` WHERE ` aan query

    als aantal merken > 0
        plak `merken IN (? ` aan query
        plak 1e_merk aan parameter-lijst
    voor de 2e tot en met de laatste merk
        plak `, ?` aan query
        plak volgende_merk aan parameter-lijst 
    als aantal_merken > 0
        plak `)` aan query       
```
:::

```{hint} Tips
:class: dropdown
- gebruik de volgende for-loop voor het tweede tot en met het laatste merk: \
`for i in range(1, len(brand_filter_values)):`
```

:::{note}Opdracht c)
### Voorbereiding voor filteren op kleuren

In onderdeel a) en b) heb je met `WHERE` gefilterd op het veld `brand`. Dat kon omdat in de query stond 
- `SELECT` ... `brands.name AS merk` en 
- `JOIN brands ON product.brand_id = brands.id`

Voeg de kleuren toe aan het resultaat van de query. Dit kan door de query aan te passen met de code hieronder. Voeg deze code toe na de basis query met `SELECT` en vóór de code met `WHERE` die je in de vorige opdracht hebt toegevoegd. Controleer of je webshop artikelen meerdere keren toont.
```{code} python
  # Add JOIN JOIN to query before filtering to ensure each product-color combination results in a line (e.q. multiple lines per product)
    query = query + """
        LEFT JOIN product_color ON products.id = product_color.product_id
        LEFT JOIN colors ON product_color.color_id = colors.id
    """
```

Omdat artikel een n:m-relatie met kleur heeft, wordt elk artikel zoveel keer in het resultaat opgenomen als er kleuren van dat artikel zijn. Dus als een artikel de kleuren `geel` en `blauw` heeft, dan wordt het artikel twee keer opgenomen in de ongefilterde lijst met artikelen. Dat is nodig om met `WHERE` op meerdere kleuren te kunnen filteren. In de artikelen-lijst die verzonden wordt mag elk artikel maximaal één keer voorkomen.

Voeg de volgende code toe om dubbele artikelen uit het resultaat te verwijderen. Deze code voeg je toe na de code met `WHERE` uit de vorige opdracht en vóór de code die de query uitvoert (execute). Controleer of je webshop alle artikelen één keer toont.
```{code} python
    # Add GROUP BY to query after filter to remove duplicate products (e.q. one line per product)
    query = query + " GROUP BY products.id"
```

```{hint} Tips
:class: dropdown
- `GROUP BY` komt na `WHERE`, voeg `GROUP BY` dus helemaal aan het einde van de query toe.
```
:::

:::{note}Opdracht d)
### Filter op 0, 1 of meer merken en 0, 1 of meer kleuren

Onderstaande pseudo-code is een uitbreiding op de pseudo-code uit onderdeel b). De gewijzigde en nieuwe regels zijn gemarkeerd. 

Breidt de Python-code in de API uit, zodat het werkt zoals beschreven staat in de pseudo-code. Controleer of alle voorbeelden uit de tabel goed werken.

```{code} pseudo
:caption: Pseudo-code
:linenos:
:emphasize-lines: 1,13,14,15,16,17,18,19,20,21,22,23
    als aantal_merken > 0 of aantal_kleuren > 0
        plak ` WHERE ` aan query

    als aantal merken > 0
        plak `merken IN (? ` aan query
        plak 1e_merk aan parameter-lijst
    voor de 2e tot en met de laatste merk
        plak `, ?` aan query
        plak volgende_merk aan parameter-lijst 
    als aantal_merken > 0
        plak `)` aan query

    als aantal_merken > 0 en aantal_kleuren > 0
        plak ` AND ` aan query

    als aantal kleuren > 0
        plak `kleuren IN (? ` aan query
        plak 1e_kleur aan parameter-lijst
    voor de 2e tot en met de laatste kleur
        plak `, ?` aan query
        plak volgende_kleur aan parameter-lijst 
    als aantal_kleuren > 0
        plak `)` aan query   
```
:::

```{hint} Tips
:class: dropdown
- kopieer de code voor merken en pas de variabelen aan, zodat het werkt voor kleuren.
- vergeet de aanpassing in regel 1 niet
- let op het verschil tussen regel 1 (`or`) en regel 13 (`and`)
```
