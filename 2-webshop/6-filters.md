# Filters
In dit hoofdstuk ga je filters toevoegen aan je webshop. Met filters kun je selecteren welke artikelen getoond worden.

## Uitleg: REST-API

:::{note} Uitleg
### REST

API (Engels, spreek uit ee-pie-aai) staat voor Application Programming Interace. Een API is een stuk software dat computerprogramma op een gestandaardiseerde manier met elkaar verbindt. Een API tussen computerprogramma's die via het internet met elkaar zijn verbonden heet een webservice. Een webservice wordt aangeboden door een server en gebruikt door één of meerdere clients. Moderne webservices zijn RESTful (Engels, spreek uit als rest-foel). REST staat voor REpresentational State Transfer, maar meestal wordt alleen de afkorting gebruikt. REST is geen protocol maar een set ontwerp-richtlijnen.

Hier volgen enkele ontwerp-richtlijnen van REST.

Platform-onafhankelijk
: REST werkt via standaardprotocollen zoals HTTP en maakt gebruik van eenvoudige dataformaten zoals JSON. Daardoor kunnen verschillende systemen zoals Windows, Linux, iOS en Android probleemloos met elkaar communiceren.

Client-Server scheiding
: De client (zoals een app of website) en de server (waar de gegevens staan) werken onafhankelijk van elkaar. De client weet alleen wat hij nodig heeft, niet hoe de server dat regelt. Dit maakt onderhoud en ontwikkeling eenvoudiger: de client-zijde (frontend) en server-zijde (backend) kunnen apart worden aangepast.

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

## Opdracht: Toon filters voor soort en kleur
De front-end is al voorbereid voor het werken met filters, maar de API nog niet. In deze opdracht ga je zorgen dat de filters zichtbaar worden in de webshop. In de volgende opdracht zorg je dat alleen de artikelen worden getoond die in het filter zijn ingesteld.

:::{note}Opdracht
### Maak filters a)
De front-end vraagt via het endpoint `/api/filters` de lijst met filters op. In de API is het eindpoint al gemaakt, maar het geeft een lege lijst terug. De front-end geeft alleen filters weer als de lijst niet leeg is.

Maak een lijst met filters door onderstaande code op de juiste plaats in de API te zetten en test of het werkt.

Als je het goed gedaan hebt, dan zie je de filters in je webshop en kun je vinkjes zetten. De knop "Filter toepassen" werkt nog niet, dat komt in een volgende opdracht.

```{code} python
:caption: Python-code
:linenos:
    # Construct the response
    filters = {
        "soort": ["mooi","lelijk"],
        "kleur": ["rood","wit","blauw"]
    }
```

:::

```{hint} Tips (XXXXXX)
:class: dropdown
- De aanpassing moet je doen in de API, in het bestand `/app/main.py` bij de functie voor het endpoint `/api/products/`.
- Let op de commentaarregel om te zien naar welke plek je de code exact moet kopieren.
- Voeg aan de query een `SELECT` toe met één veld, namelijk de naam van de kleur.
- Voeg aan de query een `JOIN` toe tussen de tabellen `product_color` en `colors`.
- Controleer wat de API opstuurt naar de client. Zet in je browser achter de hostname van je webshop `/api/products/` en laadt die webpagina. Het antwoord is hetzelfde antwoord als wat de client van de API zou krijgen. Je ziet de artikelinformatie in JSON-formaat.
```

:::{note}Opdracht b)
### Maak filters automatisch
Bij opdracht a) heb je filters gemaakt. Maar als je een artikel met een nieuwe kleur aan je database toevoegt, dan moet je het filter aanpassen voordat je op die kleur kunt filteren. Voor nu is dat misschien okee, maar in een grote webshop is dat erg onhandig. In deze opdracht ga het filter zo maken dat hij de waarden van soort en kleur uit de database haalt.

Maak de twee queries in onderstaande code af. De eerts query moet alle soorten in de database geven en de tweede query alle kleuren.

Kopieer de code op de juiste plek in de API en test of hij het doet.

Als je het goed gedaan hebt, dan zie je de filters in je webshop en kun je vinkjes zetten. Als je op de knop "Filter toepassen" klik, dan zou de lijst met artikelen gefiltered moeten worden, maar dat ga je in de volgende opdracht doen.

```{code} python
:caption: Python-code
:linenos:
    # Fetch all distinct categories
    categories_query = "SELECT <maak af>"
    categories_result = db_connection.execute(categories_query).fetchall()
    categories = [row["name"] for row in categories_result]

    # Fetch all distinct colors
    colors_query = "SELECT <maak af>"
    colors_result = db_connection.execute(colors_query).fetchall()
    colors = [row["name"] for row in colors_result]

    # Construct the response
    filters = {
        "soort": categories,
        "kleur": colors
    }
```

:::

```{hint} Tips (XXXXXX)
:class: dropdown
- De aanpassing moet je doen in de API, in het bestand `/app/main.py` bij de functie voor het endpoint `/api/products/`.
- Let op de commentaarregel om te zien naar welke plek je de code exact moet kopieren.
- Voeg aan de query een `SELECT` toe met één veld, namelijk de naam van de kleur.
- Voeg aan de query een `JOIN` toe tussen de tabellen `product_color` en `colors`.
- Controleer wat de API opstuurt naar de client. Zet in je browser achter de hostname van je webshop `/api/products/` en laadt die webpagina. Het antwoord is hetzelfde antwoord als wat de client van de API zou krijgen. Je ziet de artikelinformatie in JSON-formaat.
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

## Opdracht: Laat filters op soort en kleur werken

De front-end in de webshop stuurt het filter als query-parameter mee naar het endpoint `/api/products` als op de knop `Filter toepassen` geklikt wordt. Om alleen de artikelen terug te sturen die aan het filter voldoen, moet je in de API een `WHERE`-clausule toe voegen aan het `SELECT`-commando dat de artikel-informatie uit de database ophaalt. Bekijk de tabel om te zien hoe het filter uiteindelijk moet gaan werken.

:::{table} Werking van filter

poppetje | huisje | rood | wit | blauw | getoonde artikelen | WHERE-clausule
:---: | :---: | :---: | :---: | :---: | --- | ---
☐ | ☐ | ☐ | ☐ | ☐ | alle artikelen | geen
☑ | ☐ | ☐ | ☐ | ☐ | artikelen met poppetje, de kleur maakt niet uit | `WHERE soort IN["poppetje"]`
☑ | ☑ | ☐ | ☐ | ☐ | artikelen met (poppetje of huisje), de kleur maakt niet uit | `WHERE soort IN["poppetje", "huisje"]`
☐ | ☐ | ☑ | ☐ | ☐ | artikelen met rood, de soort maakt niet uit | `WHERE kleur IN["rood"]`
☑ | ☐ | ☑ | ☐ | ☐ | artikelen met poppetje en rood | `WHERE soort IN["huisje"] AND kleur IN["rood"]`
☑ | ☑ | ☐ | ☑ | ☑ | artikelen met (poppetje of huisje) en (wit of blauw) | `WHERE soort IN["poppetje", "huisje"] AND kleur IN["wit", "blauw"]`

:::


Je gaat het filter stap voor stap maken in a) tot en met d) van deze opdracht. Je moet daarbij Python-code toevoegen aan de API.

:::{note}Opdracht a)
### filter op 0 of 1 soorten

0 of 1 soorten
```{code} pseudo 
:caption: Pseudo-code
:linenos:
    als aantal_soorten > 0
        plak ` WHERE ` aan query
        
    als aantal_soorten > 0
        plak `soorten IN [1e_soort ` aan query
        plak 1e_soort aan parameter-list
        plak `]` aan query         
```

xxxxxx code must be changed a little to make it fit 100% with pseudocode
```{code} python
:caption: Python-code
:linenos:
    # Filter soort (category in database)
    category_params = soort
    category_filters = []
    if len(category_params) > 0:
        placeholders = "?"
        for i in range(1, len(category_params)):
            placeholders = placeholders + ", ?"
        category_filters = ["cat.name IN (" + placeholders + ")"]
```
:::

:::{note}Opdracht b)
### filter op 0, 1 of meer soorten

0,1 of meer soorten
```{code} pseudo
:caption: Pseudo-code
:linenos:
:emphasize-lines: 7,8,9
    als aantal_soorten > 0
        plak ` WHERE ` aan query

    als aantal soorten > 0
        plak `soorten IN [1e_soort ` aan query
        plak 1e_soort aan parameter-list
    voor de 2e tot en met de laatste soort
        plak `, volgende_soort` aan query
        plak volgende_soort aan parameter-list 
    als aantal_soorten > 0
        plak `]` aan query       
```
:::

:::{note}Opdracht c)
### Voorbereiding voor filteren op kleuren


kleuren toevoegen met JOIN JOIN

dubbele artikelnummers voorkomen met GROUP BY

:::

:::{note}Opdracht d)
### filter op 0, 1 of meer soorten en 0, 1 of meer kleuren

```{code} pseudo
:caption: Pseudo-code
:linenos:
:emphasize-lines: 1,13,14,15,16,17,18,19,20,21,22
    als aantal_soorten > 0 of aantal_kleuren > 0
        plak ` WHERE ` aan query

    als aantal soorten > 0
        plak `soorten IN [1e_soort ` aan query
        plak 1e_soort aan parameter-list
    voor de 2e tot en met de laatste soort
        plak `, volgende_soort` aan query
        plak volgende_soort aan parameter-list 
    als aantal_soorten > 0
        plak `]` aan query

    als aantal_soorten > 0 en aantal_kleuren > 0
        plak ` AND ` aan query     
    als aantal kleuren > 0
        plak `kleuren IN [1e_kleur ` aan query
        plak 1e_kleur aan parameter-list
    voor de 2e tot en met de laatste kleur
        plak `, volgende_kleur` aan query
        plak volgende_kleur aan parameter-list 
    als aantal_kleuren > 0
        plak `]` aan query   
```
:::
