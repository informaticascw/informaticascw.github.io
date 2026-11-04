(netwerken-h08)=
# HTTP: een webpagina opvragen

## Inleiding

Met DNS heeft je browser het IP-adres van de webserver. Nu moet de browser nog aan de server duidelijk maken welke pagina hij wil. Daarvoor gebruikt hij {term}`HTTP`: een protocol waarmee een {term}`client` een verzoek doet en een {term}`server` antwoordt.

**Laag:** {term}`toepassingslaag`. **Vraag:** hoe vraagt een browser een pagina op bij een webserver en hoe antwoordt de server?

## Klassikaal: een pagina opvragen bij de juiste server

Maak drie rollen: browserclients, webserver Noord en webserver Zuid. Elke server heeft pagina’s op eigen paden. Clients krijgen een URL, zoals `http://nieuws.school.test/sport.html`, en een DNS-lijst die vertelt welke server bij welke naam hoort.

1. De client zoekt het adres van de server op de DNS-lijst en gaat naar die server.
2. De client vraagt het pad op. De server antwoordt met de pagina en een kaartje ‘200’, of met een kaartje ‘404’ als hij het pad niet heeft.
3. Verplaats een pagina naar de andere server, maar laat de DNS-lijst ongewijzigd. Wat gebeurt er als clients dezelfde URL gebruiken?
4. Pas nu de DNS-lijst aan. Werkt dezelfde URL weer?

Bespreek welke rol welke informatie beheert: DNS weet waar de server is, de server weet welke pagina’s er zijn.

## HTTP: een verzoek en een antwoord

De browser is de client en verstuurt een HTTP-verzoek. De server stuurt een antwoord met een statuscode, {term}`headers <header>` en eventueel inhoud, zoals HTML. HTTP is het protocol voor het opvragen en afleveren van webpagina’s en andere bestanden.

Het voorbeeld is vereenvoudigd HTTP/1.1; sommige headers zijn weggelaten.

```http
GET /rooster.html HTTP/1.1
Host: nieuws.school.test
```

```http
HTTP/1.1 200 OK
Content-Type: text/html

<h1>Rooster</h1>
```

`GET` vraagt een bron op. `200` betekent dat het gelukt is; `404` betekent dat de bron niet is gevonden. Bij een 404 is er dus wel een antwoord van een server gekomen. De headers geven extra informatie en de inhoud staat daarna. Afbeeldingen en CSS-bestanden in de pagina kunnen aparte verzoeken veroorzaken.

DNS en HTTP zijn verschillende diensten. Een goed DNS-antwoord garandeert niet dat de webserver draait, en een 404 betekent niet dat DNS faalde.

::: {note} HTTPS
HTTP-verkeer is leesbaar voor iedereen die het onderweg onderschept. {term}`HTTPS` is HTTP over een beveiligde verbinding met {term}`TLS`, die het verkeer versleutelt. Je herkent het aan `https://` en het slotje in de adresbalk. We werken HTTPS in deze module niet verder uit.
:::

::: {exercise} Zonder Filius: het antwoord lezen
:label: nw08-o1

1. Welke servernaam en welk pad staan in het voorbeeld?
2. Is een ontvangen 404 hetzelfde als geen netwerkverbinding? Leg uit.
3. Een pagina bevat twee afbeeldingen. Waarom veroorzaakt die pagina meer dan één verzoek?
4. Het DNS-antwoord is goed, maar de webserver staat uit. Wat merkt de browser?
:::

::: {solution} nw08-o1
:class: dropdown

1. Servernaam `nieuws.school.test`, pad `/rooster.html`.
2. Nee. Bij een 404 is er een antwoord van de server; alleen de gevraagde bron ontbreekt. Zonder verbinding komt er helemaal geen antwoord.
3. De browser haalt na de HTML ook de afbeeldingen op. Een cache kan het aantal nieuwe verzoeken beperken.
4. De browser krijgt geen verbinding met de server en dus geen HTTP-antwoord. De naam is wel goed opgezocht.
:::

::: {exercise} Filius: een website op naam
:label: nw08-o2

1. Open `07-dns.fls`. Gebruik C (`192.168.20.10`) als webserver. Installeer en start de webserver en pas de startpagina aan met een herkenbare titel. Installeer op A een webbrowser.
2. Bezoek eerst `http://192.168.20.10` en daarna `http://nieuws.school.test`.
3. Zoek in de gegevensuitwisseling de DNS-vraag, het DNS-antwoord en het HTTP-verkeer. Noteer welke server bij welke dienst hoort.
4. Zet de webserver uit en bezoek de pagina opnieuw. Wat merk je en wat zegt dat over DNS en HTTP?
5. Bewaar als `08-website.fls`.
:::

::: {solution} nw08-o2
:class: dropdown

De website is bereikbaar via het IP-adres én via de naam. De DNS-vraag gaat naar `.53` en levert het adres `.10`; het webverkeer gaat daarna naar `.10`. De DNS-server levert zelf niet de HTML. Met de webserver uit werkt DNS nog wel, maar de pagina komt niet meer.
:::

## Eigen apparaat: webverkeer bekijken

Open de ontwikkeltools van je browser, kies Netwerk en laad de schoolwebsite opnieuw. Klik een verzoek aan en zoek de URL, de statuscode en het inhoudstype. Kies ook een CSS-bestand of afbeelding. Zijn de ontwikkeltools op school geblokkeerd, laat dan de docent het voordoen.

Bij HTTPS toont je browser de leesbare inhoud, omdat hij die zelf ontsleutelt. Dat betekent niet dat iemand onderweg dezelfde inhoud kan lezen.
