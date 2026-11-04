(netwerken-h08)=
# DNS en HTTP: een website opvragen

## Inleiding

Je typt een websiteadres in de browser. Daarin staan twee soorten informatie: de naam van een {term}`server` en de bron die je bij die server wilt opvragen. Het netwerk heeft eerst een {term}`IP-adres` nodig. Daarna heeft de server een duidelijk verzoek nodig.

**Laag:** {term}`toepassingslaag`. **Vraag:** hoe wordt een naam met een pad een verzoek aan de juiste webserver?

{term}`DNS` zoekt het IP-adres bij een naam. {term}`HTTP` vraagt de pagina op bij de server. Je stelt beide diensten apart in, zodat je ziet wat elk doet.

## Klassikaal: naam, adres en inhoud

Maak vier rollen: browserclients, een DNS-balie, webserver Noord en webserver Zuid. De DNS-balie heeft alleen een lijst met namen en serveradressen. Elke webserver heeft pagina’s met eigen paden. Alleen de servers hebben de inhoud.

Elke {term}`client` krijgt een {term}`URL`, bijvoorbeeld `http://nieuws.school.test/sport.html`. De client mag de DNS-balie alleen de hostnaam vragen en bezoekt daarna met het gevonden adres de juiste server om het pad op te vragen.

1. Laat clients eerst de hele URL aan de DNS-balie voorleggen. De balie heeft de pagina niet.
2. Spreek de twee aparte vragen af: eerst naar het adres, dan naar de pagina.
3. Verander alleen het serveradres op de DNS-lijst en verplaats de pagina naar die server. De URL blijft gelijk.

Bespreek welke rol welke informatie beheert. Het zijn twee diensten, ook als één echte computer beide uitvoert.

## DNS: een naam opzoeken

Het Domain Name System koppelt namen aan gegevens, waaronder IP-adressen. Een {term}`A-record` koppelt een naam aan een IPv4-adres; voor IPv6 is er het AAAA-record.

Je computer vraagt dit meestal aan een {term}`resolver <DNS-resolver>`. Die heeft het antwoord misschien al in een {term}`cache`. Zo niet, dan zoekt hij het op, eventueel via verwijzingen naar andere DNS-servers. DNS is wereldwijd verdeeld: geen enkele server kent alle namen. Rootservers en servers voor topleveldomeinen verwijzen door; gezaghebbende servers beheren de gegevens van hun eigen domeinen.

Een eenvoudige DNS-vraag gaat vaak via UDP-poort 53; DNS kan ook {term}`TCP` gebruiken. DNS is een ander protocol dan HTTP.

DNS levert geen webpagina en vertaalt niet de hele URL. Bij `http://nieuws.school.test/sport.html` zoekt DNS alleen de hostnaam `nieuws.school.test` op. Het pad `/sport.html` gaat pas naar de webserver. Namen met `.test` zijn bedoeld voor oefenomgevingen en bestaan niet op het publieke internet.

### Voorbeeld

DNS antwoordt dat `nieuws.school.test` bij `192.168.20.10` hoort. De browser kan nu verbinding maken met de webserver op dat adres. Bij een volgend bezoek kan het antwoord uit een cache komen, dus niet elk bezoek start een nieuwe zoekactie over de hele wereld.

::: {exercise} Zonder Filius: wie weet het?
:label: nw08-o1

1. Welke DNS-vraag hoort bij `http://nieuws.school.test/rooster.html`?
2. Waarom hoeven links niet te veranderen als een website naar een nieuw IP-adres verhuist?
3. Het DNS-antwoord is goed, maar de webserver staat uit. Is de naam dan toch goed opgezocht?
:::

::: {solution} nw08-o1
:class: dropdown

1. Vraag naar het adres van `nieuws.school.test`, niet naar `/rooster.html`.
2. Alleen de DNS-koppeling verandert; de naam blijft hetzelfde. Oude antwoorden kunnen nog tijdelijk in een cache staan.
3. Ja. DNS en de webserver zijn verschillende diensten. Een goed adres garandeert niet dat de webserver draait.
:::

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

::: {exercise} Zonder Filius: het antwoord lezen
:label: nw08-o2

1. Welke servernaam en welk pad staan in het voorbeeld?
2. Is een ontvangen 404 hetzelfde als geen netwerkverbinding? Leg uit.
3. Een pagina bevat twee afbeeldingen. Waarom veroorzaakt die pagina meer dan één verzoek?
:::

::: {solution} nw08-o2
:class: dropdown

1. Servernaam `nieuws.school.test`, pad `/rooster.html`.
2. Nee. Bij een 404 is er een antwoord van de server; alleen de gevraagde bron ontbreekt. Zonder verbinding komt er helemaal geen antwoord.
3. De browser haalt na de HTML ook de afbeeldingen op. Een cache kan het aantal nieuwe verzoeken beperken.
:::

::: {exercise} Filius: een website op naam
:label: nw08-o3

1. Open `07-transport.fls`. Gebruik C (`192.168.20.10`) als webserver. Pas de startpagina aan met een herkenbare titel en start de webserver.
2. Voeg aan het netwerk van C een DNS-server toe met adres `192.168.20.53`, masker `255.255.255.0` en {term}`gateway` `192.168.20.1`.
3. Installeer en start de DNS-server. Maak een adresrecord voor `nieuws.school.test` naar `192.168.20.10`.
4. Stel op A het DNS-serveradres `192.168.20.53` in. Laat de gateway goed staan.
5. Bezoek eerst `http://192.168.20.10` en daarna `http://nieuws.school.test`.
6. Zoek in de gegevensuitwisseling de DNS-vraag, het DNS-antwoord en het HTTP-verkeer. Noteer welke server bij welke dienst hoort.
7. Bewaar als `08-website.fls`.
:::

::: {solution} nw08-o3
:class: dropdown

De website is bereikbaar via het IP-adres én via de naam. De DNS-vraag gaat naar `.53` en levert het adres `.10`; het webverkeer gaat daarna naar `.10`. De DNS-server levert zelf niet de HTML. Ook als één computer beide diensten uitvoert, blijven het twee diensten. Dit voorbeeld heeft één lokale DNS-server en bootst de wereldwijde DNS-structuur niet na.
:::

## Eigen apparaat: webverkeer bekijken

Open de ontwikkeltools van je browser, kies Netwerk en laad de schoolwebsite opnieuw. Klik een verzoek aan en zoek de URL, de statuscode en het inhoudstype. Kies ook een CSS-bestand of afbeelding. Zijn de ontwikkeltools op school geblokkeerd, laat dan de docent het voordoen.

Bij {term}`HTTPS` toont je browser de leesbare inhoud, omdat hij die zelf ontsleutelt. Dat betekent niet dat iemand onderweg dezelfde inhoud kan lezen. HTTPS komt in hoofdstuk 9 aan bod.
