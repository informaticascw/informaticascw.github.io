(netwerken-les10)=
# Van URL naar webpagina

## Inleiding

Je kent nu de {term}`functies <functie>` van de verschillende lagen. In dit hoofdstuk gebruik je die kennis om één websitebezoek te volgen, van de tekst in de adresbalk tot de ontvangen inhoud.

**Hoofdvraag:** welke stappen zijn voor dit concrete bezoek nodig, en welke velden tonen aan wat er gebeurt?

Het [hoofdstuk over lagen en inkapseling](03-lagen.md) geeft het verpakkingsmodel. Hier pas je dat toe op {term}`DNS`, {term}`TCP`, {term}`HTTP`, {term}`ARP` en {term}`routering`. Je legt je verklaring naast berichten die je zelf in de simulatie waarneemt.

## Eén uitgewerkt bezoek

Neem een vereenvoudigd HTTP-bezoek met {term}`IPv4 <IP>`, {term}`Ethernet` en TCP. De {term}`client` is A `192.168.10.10/24`, {term}`gateway` `192.168.10.1`; DNS staat op `192.168.20.53`; de webserver is `192.168.20.10`. Er is geen {term}`NAT`. {term}`Caches <cache>` zijn leeg en er bestaat nog geen TCP-verbinding.

1. De browser haalt hostnaam en pad uit de {term}`URL` `http://nieuws.school.test/rooster.html`.
2. De client vraagt DNS naar de hostnaam. Omdat de DNS-server buiten zijn {term}`subnet` ligt, moet hij voor die vraag al de gateway gebruiken. Als het gateway-MAC-adres onbekend is, gaat aan die DNS-vraag eerst ARP vooraf.
3. DNS antwoordt met `192.168.20.10`. Vraag en antwoord zijn zelf ook netwerkcommunicatie met transport-, IP- en lokale afleverinformatie.
4. De client bepaalt voor de webserver opnieuw dat de bestemming buiten het eigen subnet ligt. De gatewaykoppeling kan inmiddels bekend zijn.
5. TCP bouwt een verbinding op met serverpoort 80 en een tijdelijke clientpoort. De {term}`router` stuurt de {term}`pakketten <IP-pakket>` door. Op iedere lokale Ethernetverbinding worden passende {term}`MAC-adressen <MAC-adres>` gebruikt.
6. De browser stuurt het HTTP-verzoek. In het TCP-model gaat HTTP-inhoud in {term}`TCP-segmenten <TCP-segment>`, die in IP-pakketten zitten, die op een lokale Ethernetverbinding in {term}`frames <frame>` zitten. Dit heet {term}`inkapseling`.
7. De {term}`server` verwerkt de lagen en stuurt een HTTP-antwoord via de terugweg. De browser ontvangt de HTML en kan daarna CSS en afbeeldingen opvragen.

Dit is een uitlegvolgorde, geen garantie op precies deze nieuwe berichten bij ieder bezoek. Caches, hergebruikte verbindingen en moderne webprotocollen kunnen de waarneming veranderen. Bij {term}`HTTPS` komt beveiligde verbindingsopbouw vóór de HTTP-uitwisseling; bij HTTP/3 is het transport anders.

::: {exercise} Zonder Filius: bekijk één frame
:label: nw10-o1

1. A verstuurt het HTTP-verzoek. Geef bron-IP, bestemmings-IP, {term}`bestemmingspoort <poortnummer>` en bestemmings-MAC op de verbinding A→gateway.
2. Welke adressen veranderen wanneer de router het pakket naar de server verstuurt?
3. Waarom is ‘DNS komt altijd vóór ARP’ onjuist?
4. Waarom mag een HTTP-programma bij dezelfde server blijven werken als de client van kabel naar {term}`wifi` overstapt?
:::

::: {solution} nw10-o1
:class: dropdown

1. Bron-IP `192.168.10.10`, bestemmings-IP `192.168.20.10`, TCP-bestemmingspoort 80; bestemmings-MAC van de lokale gatewayinterface.
2. De Ethernetbron en -bestemming veranderen. Zonder NAT blijven de IP-eindadressen gelijk. Andere IP-headervelden zoals TTL veranderen wel.
3. Ook de DNS-vraag moet bezorgd worden; daarvoor kan eerst ARP nodig zijn.
4. HTTP beschrijft toepassingsberichten. De lagere lagen kunnen een andere lokale verbinding verzorgen zonder die berichtafspraken te veranderen.
:::

::: {exercise} Filius: maak een bewijsverslag
:label: nw10-o2

1. Open `08-website.fls` en start een nieuwe simulatie.
2. Bezoek de website op naam. Leg maximaal zes relevante berichten vast of noteer hun velden: ARP, DNS, TCP-opbouw, HTTP-verzoek, HTTP-antwoord en doorsturen door de router.
3. Schrijf bij ieder gekozen bericht welke vraag het oplost. Noteer bron, bestemming en het relevante adres- of poortveld.
4. Bezoek de pagina nogmaals. Welke stappen worden opnieuw uitgevoerd en welke informatie kan hergebruikt worden? Baseer je antwoord op de waarneming, niet alleen op de lijst hierboven.
:::

::: {solution} nw10-o2
:class: dropdown

Een goed verslag verbindt waarnemingen aan functies: ARP vindt lokaal een MAC-adres, DNS vindt een serveradres bij een naam, TCP bouwt een verbinding op, HTTP vraagt inhoud en levert die terug. De router verzorgt de stap tussen netwerken. Herhaling kan verschillen door caches en bestaande verbindingen. Niet iedere start wist in iedere Filius-versie automatisch alle informatie; vermeld wat je daadwerkelijk ziet.
:::

## In het echt: internet is een netwerk van netwerken

De router thuis of op school is niet ‘het {term}`internet`’. Hij geeft verkeer door naar een netwerk van een provider. Providers verbinden hun netwerken met andere providers en met netwerken van bijvoorbeeld datacenters. Er is geen centrale router waar ieder pakket verplicht langs moet. Organisaties maken {term}`afspraken <afspraak>` over koppelingen en bereikbaarheid; routers hebben informatie over welke bestemmingen via welke buren bereikbaar zijn.

Ons Filius-model is kleiner en gebruikt handmatige routes. Op internet gebeurt route-uitwisseling grotendeels automatisch. Ook DNS is verdeeld over organisaties. Het {term}`web` is één toepassing die dat netwerk gebruikt; internet is dus meer dan websites.

::: {exercise} Zonder Filius: dezelfde vraag op grotere schaal
:label: nw10-o3

1. Welke functie heeft de provider die in het kleine Filius-model niet als aparte organisatie bestaat?
2. Moet jouw computer het MAC-adres kennen van de server in een datacenter? Licht toe.
3. Zijn internet, het web en wifi drie woorden voor hetzelfde?
:::

::: {solution} nw10-o3
:class: dropdown

1. De provider biedt onder andere aansluiting op andere netwerken en verdere bereikbaarheid. De modelrouters beelden een klein stukje van zulke doorstuurfuncties af.
2. Nee. Hij heeft op zijn lokale verbinding het adres van de volgende ontvanger nodig, meestal de gateway. MAC-adressen worden niet gebruikt als wereldwijd eindadres voor het hele pad.
3. Nee. Internet is het geheel van gekoppelde netwerken, het web een toepassing met onder andere HTTP(S), en wifi een techniek voor een lokale draadloze verbinding.
:::
