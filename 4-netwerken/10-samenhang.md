(netwerken-h10)=
# Van URL naar webpagina

## Inleiding

Je kent nu de taken van alle lagen. In dit hoofdstuk volg je één websitebezoek van de tekst in de adresbalk tot de ontvangen pagina en gebruik je daarvoor alles uit de vorige hoofdstukken.

**Vraag:** welke stappen zijn voor dit bezoek nodig, en welke velden in de berichten laten dat zien?

Het [hoofdstuk over lagen en inkapseling](03-lagen.md) beschrijft hoe berichten worden verpakt. Hier pas je dat toe op {term}`DNS`, {term}`TCP`, {term}`HTTP`, {term}`ARP` en {term}`routering`. Je vergelijkt je verklaring met berichten die je zelf in de simulatie ziet.

## Eén bezoek stap voor stap

We nemen een vereenvoudigd HTTP-bezoek met {term}`IPv4`, {term}`Ethernet` en TCP. De {term}`client` is A (`192.168.10.10/24`) met {term}`gateway` `192.168.10.1`. De DNS-server is `192.168.20.53` en de webserver `192.168.20.10`. Er is geen {term}`NAT`, alle {term}`caches <cache>` zijn leeg en er is nog geen TCP-verbinding.

1. De browser haalt uit de {term}`URL` `http://nieuws.school.test/rooster.html` de hostnaam en het pad.
2. De client vraagt DNS naar het adres bij de hostnaam. De DNS-server ligt buiten het subnet van de client, dus dit verzoek gaat via de gateway. Is het MAC-adres van de gateway onbekend, dan gaat ARP aan de DNS-vraag vooraf.
3. DNS antwoordt met `192.168.20.10`. Vraag en antwoord zijn zelf ook netwerkverkeer, met transport-, IP- en Ethernetinformatie.
4. De client ziet dat de webserver ook buiten zijn subnet ligt en gebruikt opnieuw de gateway. Het MAC-adres van de gateway is inmiddels bekend.
5. TCP bouwt een verbinding op met serverpoort 80 en een tijdelijke clientpoort. De {term}`router` stuurt de {term}`pakketten <IP-pakket>` door. Op elke Ethernetverbinding staan andere {term}`MAC-adressen <MAC-adres>` in het frame.
6. De browser stuurt het HTTP-verzoek. Dat zit in {term}`TCP-segmenten <TCP-segment>`, die in IP-pakketten zitten, die op elke Ethernetverbinding in {term}`frames <frame>` zitten ({term}`inkapseling`).
7. De {term}`server` pakt de lagen uit en stuurt een HTTP-antwoord via dezelfde route terug. De browser ontvangt de HTML en kan daarna CSS en afbeeldingen opvragen.

Dit is een uitlegvolgorde. In de praktijk kunnen caches, hergebruikte verbindingen en nieuwere protocollen het verloop veranderen. Bij {term}`HTTPS` volgt na de TCP-handshake eerst een beveiligde verbindingsopbouw en pas daarna de HTTP-uitwisseling; HTTP/3 gebruikt een ander transport.

::: {exercise} Zonder Filius: één frame onderzoeken
:label: nw10-o1

1. A verstuurt het HTTP-verzoek. Geef op de verbinding van A naar de gateway het bron-IP, bestemmings-IP, de bestemmingspoort en het bestemmings-MAC-adres.
2. Welke adressen veranderen als de router het pakket naar de server verstuurt?
3. Waarom is ‘DNS komt altijd vóór ARP’ onjuist?
4. Waarom kan een browser dezelfde server blijven bereiken als de client van kabel naar {term}`wifi` overstapt?
:::

::: {solution} nw10-o1
:class: dropdown

1. Bron-IP `192.168.10.10`, bestemmings-IP `192.168.20.10`, TCP-bestemmingspoort 80 en het MAC-adres van de linker routeraansluiting (de gateway).
2. De MAC-adressen van bron en bestemming veranderen. Zonder NAT blijven de IP-adressen gelijk. De TTL in de IP-header verandert ook.
3. Ook de DNS-vraag moet bezorgd worden, en daarvoor kan eerst ARP nodig zijn.
4. HTTP beschrijft alleen de berichten van het programma. De lagen eronder kunnen een andere lokale verbinding gebruiken zonder dat HTTP verandert.
:::

::: {exercise} Filius: een onderbouwd verslag maken
:label: nw10-o2

1. Open `08-website.fls` en start een nieuwe simulatie.
2. Bezoek de website op naam. Leg maximaal zes berichten vast of noteer hun velden: ARP, DNS, TCP-opbouw, HTTP-verzoek, HTTP-antwoord en doorsturen door de router.
3. Schrijf bij elk bericht welk probleem het oplost en noteer bron, bestemming en het belangrijkste adres- of poortveld.
4. Bezoek de pagina nogmaals. Welke stappen worden herhaald en welke informatie wordt hergebruikt? Baseer je antwoord op wat je ziet.
:::

::: {solution} nw10-o2
:class: dropdown

Een goed verslag koppelt elk bericht aan zijn taak: ARP vindt lokaal een MAC-adres, DNS vindt een serveradres bij een naam, TCP bouwt een verbinding op, HTTP vraagt en levert de pagina en de router verzorgt de stap tussen de netwerken. Bij een herhaling kunnen caches en bestaande verbindingen stappen overbodig maken. Niet elke Filius-versie wist bij een nieuwe start alle informatie; schrijf op wat je werkelijk ziet.
:::

## Internet is een netwerk van netwerken

De router thuis of op school is niet ‘het {term}`internet`’. Hij geeft verkeer door aan het netwerk van een provider. Providers verbinden hun netwerken met elkaar en met netwerken van onder andere datacenters. Er is geen centrale router waar elk pakket langs moet. Organisaties maken afspraken over koppelingen en bereikbaarheid, en routers weten via welke buren welke bestemmingen bereikbaar zijn.

Ons Filius-model is kleiner en gebruikt handmatige routes. Op internet wisselen routers routes grotendeels automatisch uit. Ook DNS is verdeeld over organisaties. Het {term}`web` is één toepassing op internet; internet bestaat uit meer dan websites.

::: {exercise} Zonder Filius: dezelfde vraag op grotere schaal
:label: nw10-o3

1. Welke taak heeft de provider die in het kleine Filius-model niet als aparte organisatie voorkomt?
2. Moet jouw computer het MAC-adres van een server in een datacenter kennen? Leg uit.
3. Zijn internet, het web en wifi drie woorden voor hetzelfde?
:::

::: {solution} nw10-o3
:class: dropdown

1. De provider verzorgt de aansluiting op andere netwerken en daarmee de bereikbaarheid van de rest van het internet. De routers in het model beelden een klein stuk daarvan af.
2. Nee. Je computer heeft alleen het MAC-adres van de volgende ontvanger op zijn eigen verbinding nodig, meestal de gateway. MAC-adressen gelden niet als eindadres over het hele pad.
3. Nee. Internet is het geheel van gekoppelde netwerken, het web is een toepassing daarop met onder andere HTTP(S), en wifi is een techniek voor een draadloze lokale verbinding.
:::
