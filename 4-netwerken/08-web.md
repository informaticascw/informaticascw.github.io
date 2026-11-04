(netwerken-les08)=
# Een website opvragen

## Inleiding

Je typt een websiteadres in de browser. Daar staan twee verschillende soorten informatie in: de naam van een {term}`server` en de bron die je bij die server wilt opvragen. Het netwerk heeft eerst een {term}`IP-adres` nodig; de server heeft daarna een begrijpelijk verzoek nodig.

**Laag:** {term}`toepassingslaag`. **Hoofdvraag:** hoe wordt een naam plus pad een verzoek aan de juiste webserver?

{term}`DNS` en {term}`HTTP` lossen ieder een ander deel van dit probleem op. Je stelt beide diensten afzonderlijk in, zodat je hun werking kunt onderscheiden.

## Klassikaal: naam, adres en inhoud

Maak vier rollen: browserclients, een DNS-balie, webserver Noord en webserver Zuid. De DNS-balie krijgt alleen een lijst namen met serveradressen; de webservers krijgen elk pagina's met verschillende paden. Alleen de servers hebben de inhoud.

{term}`Clients <client>` krijgen een {term}`URL`, bijvoorbeeld `http://nieuws.school.test/sport.html`. Ze mogen de DNS-balie alleen de hostnaam vragen. Met het gevonden adres bezoeken ze de juiste server en vragen daar het pad. Laat eerst alles zonder uitleg in één vraag aan de DNS-balie proberen; die heeft de pagina niet. Spreek vervolgens de twee afzonderlijke vragen af.

Wijzig daarna alleen het serveradres op de DNS-lijst en verplaats de pagina naar die server. De URL kan gelijk blijven. Bespreek welke rol welke informatie beheert. Het zijn twee verschillende diensten, ook als één echte computer ze allebei uitvoert.

## DNS: een naam opzoeken

Het Domain Name System koppelt namen aan gegevens, waaronder IP-adressen. Een A-record koppelt een naam aan een IPv4-adres. Voor IPv6 bestaat het AAAA-record.

Je computer gebruikt meestal een {term}`resolver <DNS-resolver>`. Die kan een antwoord al tijdelijk hebben opgeslagen in een {term}`cache`. Anders zoekt de resolver het antwoord op, eventueel via verwijzingen naar andere DNS-servers. De wereldwijde DNS-structuur is verdeeld: geen enkele gewone DNS-server hoeft alle namen zelf te kennen. Rootservers en servers voor topleveldomeinen geven verwijzingen; gezaghebbende servers beheren de gegevens voor hun eigen zones.

Een eenvoudige DNS-opzoeking gebruikt vaak UDP-poort 53; DNS kan ook {term}`TCP` gebruiken. De naamdienst is dus niet hetzelfde {term}`protocol` als HTTP, ook al gebruiken beide de onderliggende netwerklagen.

DNS levert geen webpagina en vertaalt niet de hele URL. Bij `http://nieuws.school.test/sport.html` wordt de hostnaam `nieuws.school.test` opgezocht. `/sport.html` gaat pas naar de webserver. We gebruiken `.test` voor namen in de oefenomgeving, niet voor een publieke website.

### Voorbeeld

DNS antwoordt dat `nieuws.school.test` hoort bij `192.168.20.10`. De browser kan nu verbinding maken met de webdienst op die server. Bij herhaling kan een antwoord uit een cache komen: niet iedere paginabezoek start een nieuwe wereldwijde zoekactie.

::: {exercise} Zonder Filius: wie weet het?
:label: nw08-o1

1. Welke DNS-vraag past bij `http://nieuws.school.test/rooster.html`?
2. Waarom hoeft het verplaatsen van een website naar een nieuw IP-adres niet te betekenen dat alle links wijzigen?
3. Een DNS-antwoord is goed, maar de webserver staat uit. Kan de naam dan toch correct worden opgezocht?
:::

::: {solution} nw08-o1
:class: dropdown

1. Vraag naar het adres van `nieuws.school.test`, niet naar `/rooster.html`.
2. Je kunt de DNS-koppeling aanpassen en dezelfde naam blijven gebruiken. Oude antwoorden kunnen nog tijdelijk gecachet zijn.
3. Ja. DNS en de webdienst zijn verschillende diensten. Een correct adres garandeert geen actieve webserver.
:::

## HTTP: een verzoek en een antwoord

De browser is de client en verstuurt een HTTP-verzoek. De server stuurt een antwoord met een statuscode, {term}`headers <header>` en eventueel inhoud. HTML en CSS kennen jullie al: HTTP is de {term}`afspraak` voor het opvragen en afleveren daarvan.

Onderstaand voorbeeld is vereenvoudigd HTTP/1.1; sommige headers zijn weggelaten.

```http
GET /rooster.html HTTP/1.1
Host: nieuws.school.test
```

```http
HTTP/1.1 200 OK
Content-Type: text/html

<h1>Rooster</h1>
```

`GET` vraagt een bron op. `200` geeft een succesvol antwoord aan; `404` betekent dat de gevraagde bron niet gevonden is. Een 404 bewijst dus juist dat er een HTTP-antwoord van een server is gekomen. Headers geven extra informatie; de body bevat bijvoorbeeld HTML. Afbeeldingen en CSS kunnen aparte verzoeken veroorzaken.

::: {exercise} Zonder Filius: interpreteer het antwoord
:label: nw08-o2

1. Welke servernaam en welk pad staan in het voorbeeld?
2. Is een ontvangen 404 hetzelfde als geen netwerkverbinding? Leg uit.
3. Een pagina bevat twee plaatjes. Waarom kan één pagina meer dan één verzoek veroorzaken?
:::

::: {solution} nw08-o2
:class: dropdown

1. Host `nieuws.school.test`, pad `/rooster.html`.
2. Nee. Er is een serverantwoord ontvangen; de gevraagde bron ontbreekt daar. Dit is iets anders dan helemaal geen contact kunnen maken.
3. De browser kan na de HTML ook de genoemde afbeeldingen moeten ophalen. Caches kunnen het aantal nieuwe netwerkverzoeken beperken.
:::

::: {exercise} Filius: een website op naam
:label: nw08-o3

1. Open `07-transport.fls`. Gebruik C (`192.168.20.10`) als webserver. Pas de startpagina aan met een herkenbare titel. Start de webserver.
2. Voeg aan het netwerk van C een DNS-server toe met adres `192.168.20.53/24`, {term}`gateway` `192.168.20.1`.
3. Installeer en start de DNS-serverdienst. Maak een adresrecord voor `nieuws.school.test` naar `192.168.20.10`.
4. Stel op A het DNS-serveradres `192.168.20.53` in. Laat de gateway goed staan.
5. Bezoek eerst `http://192.168.20.10` en daarna `http://nieuws.school.test`.
6. Zoek in de gegevensuitwisseling de DNS-vraag, het antwoord en de HTTP-communicatie. Noteer welke server bij iedere dienst hoort. Bewaar als `08-website.fls`.
:::

::: {solution} nw08-o3
:class: dropdown

De website hoort via het IP-adres én de naam bereikbaar te zijn. DNS gaat naar `.53` en levert het adres `.10`; de webcommunicatie gaat daarna naar `.10`. De DNS-server levert zelf niet de HTML. Als je hetzelfde apparaat beide diensten laat uitvoeren, blijven de {term}`functies <functie>` toch verschillend. Het voorbeeld heeft één lokale DNS-server: het bootst niet de volledige wereldwijde DNS-hiërarchie na.
:::

## In het echt: kijk naar het webverkeer

Open de ontwikkeltools van je browser, kies Netwerk en laad de schoolwebsite opnieuw. Klik een verzoek aan en zoek de URL, statuscode en het inhoudstype. Kies daarnaast een CSS-bestand of afbeelding. Als ontwikkeltools op school geblokkeerd zijn, laat de docent één browser demonstreren.

De ontwikkeltools kunnen de inhoud van {term}`HTTPS` laten zien omdat je eigen browser die inhoud ontsleutelt. Dat betekent niet dat iemand onderweg dezelfde inhoud in leesbare vorm ziet. HTTPS behandelen we in de volgende les.
