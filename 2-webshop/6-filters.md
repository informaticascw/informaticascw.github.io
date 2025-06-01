# Filters
In dit hoofdstuk ga je filters toevoegen aan je webshop. Met filters kun je selecteren welke artikelen getoond worden.

## REST-API (uitleg)

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

## Maak filters voor soort en kleur

:::{note}Opdracht
### Maak filters 
XXXXXXDe onderstaande code vraagt voor elk artikel de kleuren op uit de database en voegt deze toe aan de artikelinformatie (`product_rows`). De API stuurt `product_rows` in JSON-formaat naar de client. 

XXXXXXMaak de query in de code af door op de plekken met `<maak af>` de juiste stukje query in te vullen. De query eindigt met een vraagteken `?`. Op die plek wordt steeds het `product_id` ingevuld van het product waarvan we de kleuren opvragen.

```{code}python
    # Construct the response
    filters = {
        "soort": ["mooi","lelijk"],
        "kleur": ["rood","wit","blauw"]
    }
```

Kopieer de code op de juiste plek in de API en test of hij het doet.

Als je het goed gedaan hebt, dan zie je de filters in je webshop en kun je vinkjes zetten. Als je op de knop "Filter toepassen" klik, dan zou de lijst met artikelen gefiltered moeten worden, maar dat ga je in de volgende opdracht doen.

:::

```{hint} Tips (XXXXXX)
:class: dropdown
- De aanpassing moet je doen in de API, in het bestand `/app/main.py` bij de functie voor het endpoint `/api/products/`.
- Let op de commentaarregel om te zien naar welke plek je de code exact moet kopieren.
- Voeg aan de query een `SELECT` toe met één veld, namelijk de naam van de kleur.
- Voeg aan de query een `JOIN` toe tussen de tabellen `product_color` en `colors`.
- Controleer wat de API opstuurt naar de client. Zet in je browser achter de hostname van je webshop `/api/products/` en laadt die webpagina. Het antwoord is hetzelfde antwoord als wat de client van de API zou krijgen. Je ziet de artikelinformatie in JSON-formaat.
```

:::{note}Opdracht
### Maak filters automatisch
XXXXXXDe onderstaande code vraagt voor elk artikel de kleuren op uit de database en voegt deze toe aan de artikelinformatie (`product_rows`). De API stuurt `product_rows` in JSON-formaat naar de client. 

XXXXXXMaak de query in de code af door op de plekken met `<maak af>` de juiste stukje query in te vullen. De query eindigt met een vraagteken `?`. Op die plek wordt steeds het `product_id` ingevuld van het product waarvan we de kleuren opvragen.

```{code}python
    # Fetch all distinct categories
    categories_query = "SELECT name FROM categories"
    categories_result = db_connection.execute(categories_query).fetchall()
    categories = [row["name"] for row in categories_result]

    # Fetch all distinct colors
    colors_query = "SELECT name FROM colors"
    colors_result = db_connection.execute(colors_query).fetchall()
    colors = [row["name"] for row in colors_result]

    # Construct the response
    filters = {
        "soort": categories,
        "kleur": colors
    }
```

Kopieer de code op de juiste plek in de API en test of hij het doet.

Als je het goed gedaan hebt, dan zie je de filters in je webshop en kun je vinkjes zetten. Als je op de knop "Filter toepassen" klik, dan zou de lijst met artikelen gefiltered moeten worden, maar dat ga je in de volgende opdracht doen.

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

## Zorg dat filters werken (copy code)
