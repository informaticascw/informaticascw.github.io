(netwerken-h12)=
# Lagen en inkapseling

## Inleiding

In de vorige hoofdstukken heb je de lagen één voor één leren kennen: bits en signalen (hoofdstuk 1), frames en MAC-adressen (2), IP-adressen en subnetten (3), ARP (4), routeren (5), poorten, TCP en UDP (6), DNS (7), HTTP (8), e-mail (9), DHCP (10) en NAT en firewall (11). In dit hoofdstuk zet je ze naast elkaar. Eerst leer je hoe de lagen samen één bericht verpakken. Daarna volg je een volledig websitebezoek van de adresbalk tot de ontvangen pagina en leg je je verklaring naast berichten die je zelf in de simulatie ziet.

**Lagen:** alle vijf. **Vraag:** welke taak heeft elke laag, hoe wordt een bericht verpakt en welke stappen zijn voor een websitebezoek nodig?

## Vijf lagen, vijf vragen

We gebruiken een {term}`lagenmodel` met vijf lagen. Een laag is geen aparte kast: één computer voert taken uit meerdere lagen uit.

| Laag | Welke vraag lost de laag op? | Wat gebruikt de laag daarvoor? |
| --- | --- | --- |
| {term}`Toepassingslaag <toepassingslaag>` | Wat vraagt of levert het programma? | Een bericht van het programma, bijvoorbeeld een verzoek om een webpagina |
| {term}`Transportlaag <transportlaag>` | Voor welk programma zijn de gegevens bedoeld, en hoe betrouwbaar moeten ze aankomen? | {term}`Poortnummers <poortnummer>`; {term}`TCP` regelt ook volgorde en herhaling |
| {term}`Netwerklaag <netwerklaag>` | Naar welke computer moet het bericht, ook via andere netwerken? | Bron- en bestemmings-IP-adres |
| {term}`Datalinklaag <datalinklaag>` | Naar welk apparaat op deze lokale verbinding? | Bron- en bestemmings-MAC-adres bij {term}`Ethernet` |
| {term}`Fysieke laag <fysieke laag>` | Hoe gaan de {term}`bits <bit>` over het {term}`medium`? | Signalen op koper, glasvezel of radio |

Een protocol is een verzameling concrete afspraken. {term}`IP` is bijvoorbeeld het protocol van de netwerklaag, {term}`HTTP` een protocol van de toepassingslaag en TCP en {term}`UDP` zijn protocollen van de transportlaag. Dezelfde taak kan door verschillende protocollen worden uitgevoerd: een browser stuurt hetzelfde HTTP-verzoek via een kabel of via wifi. Alleen de onderste laag verandert.

## Inkapseling: elke laag voegt informatie toe

Een ontvanger moet kunnen herkennen wat hij krijgt en voor wie het bedoeld is. Daarom voegt de zender bij elke laag besturingsinformatie toe, meestal als {term}`header` vóór de gegevens. Dat heet {term}`inkapseling`.

We volgen één klein HTTP-bericht dat via TCP, IPv4 en Ethernet wordt verstuurd:

1. De toepassing maakt het bericht: een verzoek om `/rooster.html`.
2. TCP voegt een TCP-header toe met onder andere poortnummers en volgnummers. Dit geheel heet een {term}`TCP-segment`.
3. IP behandelt dat segment als inhoud en voegt een IP-header toe. Dit geheel heet een {term}`IP-pakket`.
4. Ethernet behandelt het IP-pakket als inhoud en voegt een header ervoor en een {term}`trailer` erachter toe. De trailer bevat de foutcontrole ({term}`FCS`). Dit geheel is het frame.
5. De fysieke laag zet de bits van het frame om in signalen. Zij voegt geen header toe.

```{figure} images/inkapseling.svg
:alt: Een Ethernetframe bevat een IP-pakket; dat bevat een TCP-segment met de toepassingsgegevens. De Ethernetheader en trailer staan buiten het IP-pakket.

Het segment zit in het pakket en het pakket in het frame. Elke header hoort bij zijn eigen laag.
```

De inhoud die een laag vervoert heet de {term}`payload`. Voor Ethernet is dat hier het hele IP-pakket, niet alleen de tekst van de webpagina. Eén bericht van een programma kan over meerdere TCP-segmenten worden verdeeld; de figuur toont bewust één klein bericht.

## Ontkapseling: de ontvanger pakt uit

De ontvanger werkt in omgekeerde richting. De netwerkinterface haalt de bits uit de signalen. De datalinklaag controleert het frame, verwerkt de Ethernetheader en geeft de inhoud door aan de netwerklaag. IP verwerkt de IP-header en geeft de inhoud door aan TCP. TCP verwerkt de TCP-header, voegt ontvangen {term}`bytes <byte>` in de goede volgorde samen en levert ze af bij het programma. Dit heet {term}`ontkapseling`. Elke laag gebruikt alleen zijn eigen header.

::: {exercise} Zonder Filius: wat zit waarin?
:label: nw12-l1

1. Orden van buiten naar binnen: toepassingsgegevens, Ethernetframe, TCP-segment, IP-pakket.
2. Staan een bestemmings-MAC-adres en een bestemmings-IP-adres in dezelfde header?
3. Een IP-pakket is 100 bytes. Ethernetheader en -trailer samen zijn in dit voorbeeld 18 bytes. Hoe groot is het frame? Is het IP-pakket zelf nu 118 bytes?
:::

::: {solution} nw12-l1
:class: dropdown

1. Ethernetframe → IP-pakket → TCP-segment → toepassingsgegevens.
2. Nee. Het MAC-adres staat in de Ethernetheader en het IP-adres in de IP-header. De Ethernetheader zit buiten het IP-pakket.
3. Het frame is 118 bytes. Het IP-pakket blijft 100 bytes: de 18 bytes zijn de buitenste verpakking.
:::

## Wat doet een router?

Een {term}`router` ontvangt een frame, haalt het IP-pakket eruit en kijkt naar het IP-adres van de bestemming. Daarmee kiest hij de volgende verbinding en verpakt hij het pakket in een nieuw frame. Op Ethernet krijgt dat frame de MAC-adressen voor de volgende stap. De router hoeft de inhoud van de webpagina niet te begrijpen.

Zonder {term}`NAT` blijven de IP-adressen van afzender en bestemming onderweg gelijk. Het IP-pakket verandert wel een klein beetje: de {term}`TTL`, een teller die bij elke router met 1 afneemt, wordt aangepast.

Een {term}`switch` kiest op basis van MAC-adressen, een router op basis van IP-adressen. Dat zijn twee verschillende beslissingen, ook als beide in één apparaat zitten.

## Klassikaal: een bericht inpakken en uitpakken

Maak groepen van negen: vier zenderrollen, vier ontvangerrollen en één routerrol. Aan beide kanten zijn de rollen toepassing, transport, netwerk en datalink. De docent geeft elke rol alleen de velden die die rol invult. De toepassingsrol kent de tekst, de netwerkrol het IP-adres van de bestemming en de datalinkrol het MAC-adres van de eerste ontvanger.

1. Bouw het bericht met gevouwen kaarten: transportinformatie om de toepassingsgegevens, IP-informatie om het segment en een frame om het pakket.
2. Geef het bericht door aan de ontvangers. Elke ontvangerrol haalt alleen zijn eigen verpakking weg. Alleen de toepassingsrol leest de tekst.
3. Laat nu de routerrol tussen zender en ontvanger staan. De router haalt het frame weg en verpakt het IP-pakket in een nieuw frame met andere MAC-adressen, zonder de toepassingsgegevens te openen.
4. Leg het oude en het nieuwe frame naast elkaar. Wat is veranderd en wat is gelijk gebleven?

De fysieke overdracht en de foutcontrole worden niet nagespeeld.

::: {exercise} Filius: twee lagen terugvinden
:label: nw12-l2

1. Open de gegevensuitwisseling bij een ping tussen twee computers uit je netwerk. Zoek, voor zover jouw versie dat toont, Ethernet- en IP-velden in hetzelfde bericht. Noteer één MAC-adres en één IP-adres en leg uit waarvoor elk adres dient.
2. Het venster toont de velden niet in elkaar genest. Betekent dat dat een frame geen IP-pakket bevat?
3. Waarom mag je bij deze ping geen TCP-segment tekenen?
:::

::: {solution} nw12-l2
:class: dropdown

1. Het MAC-adres dient voor aflevering op het lokale netwerk, het IP-adres voor de bron of bestemming van het pakket. De waarden komen uit je eigen netwerk.
2. Nee. Het venster is een weergave; de figuur laat zien hoe de verpakking in elkaar zit.
3. Ping gebruikt {term}`ICMP`, geen TCP. De figuur toont één HTTP/TCP-voorbeeld, niet de inhoud van elk IP-pakket.
:::

## Eén bezoek stap voor stap

Nu pas je het lagenmodel toe op {term}`DNS`, {term}`TCP`, {term}`HTTP`, {term}`ARP` en {term}`routering`. We nemen een vereenvoudigd HTTP-bezoek met {term}`IPv4`, {term}`Ethernet` en TCP. De {term}`client` is A (`192.168.10.10/24`) met {term}`gateway` `192.168.10.1`. De DNS-server is `192.168.20.53` en de webserver `192.168.20.10`. Er is geen {term}`NAT`, alle {term}`caches <cache>` zijn leeg en er is nog geen TCP-verbinding.

1. De browser haalt uit de {term}`URL` `http://nieuws.school.test/rooster.html` de hostnaam en het pad.
2. De client vraagt DNS naar het adres bij de hostnaam. De DNS-server ligt buiten het subnet van de client, dus dit verzoek gaat via de gateway. Is het MAC-adres van de gateway onbekend, dan gaat ARP aan de DNS-vraag vooraf.
3. DNS antwoordt met `192.168.20.10`. Vraag en antwoord zijn zelf ook netwerkverkeer, met transport-, IP- en Ethernetinformatie.
4. De client ziet dat de webserver ook buiten zijn subnet ligt en gebruikt opnieuw de gateway. Het MAC-adres van de gateway is inmiddels bekend.
5. TCP bouwt een verbinding op met serverpoort 80 en een tijdelijke clientpoort. De {term}`router` stuurt de {term}`pakketten <IP-pakket>` door. Op elke Ethernetverbinding staan andere {term}`MAC-adressen <MAC-adres>` in het frame.
6. De browser stuurt het HTTP-verzoek. Dat zit in {term}`TCP-segmenten <TCP-segment>`, die in IP-pakketten zitten, die op elke Ethernetverbinding in {term}`frames <frame>` zitten ({term}`inkapseling`).
7. De {term}`server` pakt de lagen uit en stuurt een HTTP-antwoord via dezelfde route terug. De browser ontvangt de HTML en kan daarna CSS en afbeeldingen opvragen.

Dit is een uitlegvolgorde. In de praktijk kunnen caches, hergebruikte verbindingen en nieuwere protocollen het verloop veranderen. Bij {term}`HTTPS` volgt na de TCP-handshake eerst een beveiligde verbindingsopbouw en pas daarna de HTTP-uitwisseling; HTTP/3 gebruikt een ander transport.

::: {exercise} Zonder Filius: één frame onderzoeken
:label: nw12-o1

1. A verstuurt het HTTP-verzoek. Geef op de verbinding van A naar de gateway het bron-IP, bestemmings-IP, de bestemmingspoort en het bestemmings-MAC-adres.
2. Welke adressen veranderen als de router het pakket naar de server verstuurt?
3. Waarom is ‘DNS komt altijd vóór ARP’ onjuist?
4. Waarom kan een browser dezelfde server blijven bereiken als de client van kabel naar {term}`wifi` overstapt?
:::

::: {solution} nw12-o1
:class: dropdown

1. Bron-IP `192.168.10.10`, bestemmings-IP `192.168.20.10`, TCP-bestemmingspoort 80 en het MAC-adres van de linker routeraansluiting (de gateway).
2. De MAC-adressen van bron en bestemming veranderen. Zonder NAT blijven de IP-adressen gelijk. De TTL in de IP-header verandert ook.
3. Ook de DNS-vraag moet bezorgd worden, en daarvoor kan eerst ARP nodig zijn.
4. HTTP beschrijft alleen de berichten van het programma. De lagen eronder kunnen een andere lokale verbinding gebruiken zonder dat HTTP verandert.
:::

::: {exercise} Filius: een onderbouwd verslag maken
:label: nw12-o2

1. Open `08-website.fls` en start een nieuwe simulatie.
2. Bezoek de website op naam. Leg maximaal zes berichten vast of noteer hun velden: ARP, DNS, TCP-opbouw, HTTP-verzoek, HTTP-antwoord en doorsturen door de router.
3. Schrijf bij elk bericht welk probleem het oplost en noteer bron, bestemming en het belangrijkste adres- of poortveld.
4. Bezoek de pagina nogmaals. Welke stappen worden herhaald en welke informatie wordt hergebruikt? Baseer je antwoord op wat je ziet.
:::

::: {solution} nw12-o2
:class: dropdown

Een goed verslag koppelt elk bericht aan zijn taak: ARP vindt lokaal een MAC-adres, DNS vindt een serveradres bij een naam, TCP bouwt een verbinding op, HTTP vraagt en levert de pagina en de router verzorgt de stap tussen de netwerken. Bij een herhaling kunnen caches en bestaande verbindingen stappen overbodig maken. Niet elke Filius-versie wist bij een nieuwe start alle informatie; schrijf op wat je werkelijk ziet.
:::

## Internet is een netwerk van netwerken

De router thuis of op school is niet ‘het {term}`internet`’. Hij geeft verkeer door aan het netwerk van een provider. Providers verbinden hun netwerken met elkaar en met netwerken van onder andere datacenters. Er is geen centrale router waar elk pakket langs moet. Organisaties maken afspraken over koppelingen en bereikbaarheid, en routers weten via welke buren welke bestemmingen bereikbaar zijn.

Ons Filius-model is kleiner en gebruikt handmatige routes. Op internet wisselen routers routes grotendeels automatisch uit. Ook DNS is verdeeld over organisaties. Het {term}`web` is één toepassing op internet; internet bestaat uit meer dan websites.

::: {exercise} Zonder Filius: dezelfde vraag op grotere schaal
:label: nw12-o3

1. Welke taak heeft de provider die in het kleine Filius-model niet als aparte organisatie voorkomt?
2. Moet jouw computer het MAC-adres van een server in een datacenter kennen? Leg uit.
3. Zijn internet, het web en wifi drie woorden voor hetzelfde?
:::

::: {solution} nw12-o3
:class: dropdown

1. De provider verzorgt de aansluiting op andere netwerken en daarmee de bereikbaarheid van de rest van het internet. De routers in het model beelden een klein stuk daarvan af.
2. Nee. Je computer heeft alleen het MAC-adres van de volgende ontvanger op zijn eigen verbinding nodig, meestal de gateway. MAC-adressen gelden niet als eindadres over het hele pad.
3. Nee. Internet is het geheel van gekoppelde netwerken, het web is een toepassing daarop met onder andere HTTP(S), en wifi is een techniek voor een draadloze lokale verbinding.
:::
