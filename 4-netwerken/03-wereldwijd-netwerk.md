(netwerken-h03)=
# IP: wereldwijd netwerk

## Inleiding

Het internet is een wereldwijd netwerk van netwerken. Dat kan alleen als elk netwerk beperkt van omvang is en je van elk adres kunt zien in welk netwerk het ligt. Een {term}`switch` stuurt gewone frames gericht door, maar een {term}`broadcast` bereikt elk apparaat in het {term}`broadcastdomein`. Hoe groter het netwerk, hoe meer capaciteit en verwerking dat kost. Daarom splits je een groot netwerk in kleinere IP-netwerken ({term}`subnetten <subnet>`) en verbind je die met een {term}`router`. Daarvoor moet je met IP-adressen en subnetmaskers kunnen rekenen.

**Laag:** {term}`netwerklaag`. **Vraag:** hoe deel je een netwerk op in subnetten, en hoe bepaal je met een IP-adres en een masker in welk subnet een apparaat zit?

Je leert de netwerkgrens herkennen, netwerk- en broadcastadressen berekenen en een passend {term}`subnetmasker` kiezen.

## Klassikaal: zoekvragen tellen in één groot en in twee kleine netwerken

Elke leerling krijgt een kaart met een zichtbaar {term}`MAC-adres` en een verborgen {term}`IP-adres`. De helft heeft een adres `192.168.10.…`, de andere helft `192.168.20.…`. Eén leerling observeert en wordt in ronde 3 de router. De maskers hoef je nu nog niet zelf te kunnen berekenen; dat leer je hierna.

**Ronde 1: één netwerk.** De hele klas vormt één netwerk met masker `255.255.0.0`. Enkele afzenders zoeken tegelijk een klasgenoot op IP-adres. Ze roepen naar de hele klas: ‘Wie heeft …?’ Alleen de eigenaar antwoordt met zijn MAC-adres. Daarna bezorgt de afzender een kort bericht. De waarnemer telt hoeveel mensen elke zoekvraag moeten aanhoren.

**Ronde 2: twee gescheiden netwerken.** Vorm twee losse groepen, `192.168.10.…` en `192.168.20.…`, elk met masker `255.255.255.0`. Zoekvragen en berichten blijven binnen de eigen groep. Gebruik evenveel afzenders als in ronde 1. Probeer daarna een bericht aan iemand in de andere groep te bezorgen: dat lukt nu niet.

**Ronde 3: een router ertussen.** De routerleerling krijgt een kaart per groep (`192.168.10.1` en `192.168.20.1`) met een eigen MAC-adres per kaart. Alleen de router mag tussen de groepen bemiddelen. Een afzender zoekt de router in zijn eigen groep en geeft hem het bericht. De router zoekt de ontvanger alleen in de andere groep en bezorgt het daar. Laat ook een antwoord terugsturen.

Bespreek: wat werd rustiger na het splitsen, wat kon niet meer en wat bracht de router terug? Hoort iedereen rechts een zoekvraag van links?

Let op de grenzen van deze nabootsing: je telt hoeveel mensen een vraag moeten verwerken, niet of het sneller gaat. Ook is een ander masker instellen niet genoeg om in het echt twee broadcastdomeinen te krijgen. De netwerken moeten ook echt gescheiden zijn, bijvoorbeeld door een router.

## Waarom een lokaal netwerk begrenzen?

Een broadcastdomein is het deel van het netwerk waar een gewone broadcast wordt verspreid. Gewone switches die met elkaar verbonden zijn, vormen samen één broadcastdomein. Meer switches maken dus geen aparte domeinen.

Broadcast is nuttig: een apparaat kan iets vragen zonder het adres van de ontvanger te kennen. Maar elke broadcast kost capaciteit en moet door elk apparaat worden verwerkt. Eén groot netwerk met steeds meer apparaten schaalt daarom niet onbeperkt.

### Voorbeeld

Vier switches verbinden samen 80 computers. Eén computer verstuurt een broadcast en alle 79 andere computers ontvangen die. Een extra switch ertussen verandert dat niet.

::: {exercise} Zonder Filius: wie ontvangt de broadcast?
:label: nw03-o1

Switch S1 is verbonden met S2. A en B zitten op S1; C en D op S2.

1. Wie ontvangt een broadcast van A?
2. S2 wordt vervangen door twee achter elkaar geschakelde switches. Beperkt dat de broadcast? Leg uit.
3. Welke kosten heeft een broadcast voor een apparaat dat er niet op antwoordt?
:::

::: {solution} nw03-o1
:class: dropdown

1. B, C en D.
2. Nee. Gewone switches sturen de broadcast door naar alle andere aansluitingen.
3. Het {term}`frame` gebruikt capaciteit op de verbindingen en elk ontvangend apparaat moet het verwerken, ook zonder antwoord.
:::

## Netwerkdeel en apparaatdeel

Een router verbindt verschillende IP-netwerken en stuurt gewone Ethernetbroadcasts niet door. Een broadcast blijft dus binnen zijn eigen netwerk.

Daardoor moet een apparaat kunnen bepalen in welk netwerk een bestemming ligt. Een IP-adres bestaat daarom uit twee delen: het {term}`netwerkdeel` wijst het netwerk aan en het {term}`apparaatdeel` wijst het apparaat in dat netwerk aan. Het subnetmasker bepaalt waar de grens tussen beide ligt.

De netwerklaag verzorgt adressering en doorsturen tussen netwerken. {term}`IP` is het protocol van deze laag. {term}`Ethernet` blijft nodig om op elke afzonderlijke lokale verbinding af te leveren.

### Voorbeeld

Links gebruiken we `192.168.10.…`, rechts `192.168.20.…`, beide met masker `255.255.255.0`. De router heeft links adres `192.168.10.1` en rechts `192.168.20.1`. Elke routeraansluiting hoort bij het netwerk waarop hij is aangesloten.

## Een IP-adres is vier keer acht bits

Een IPv4-adres bestaat uit 32 {term}`bits <bit>`, geschreven als vier decimale getallen, bijvoorbeeld `192.168.10.37`. Elk getal is een {term}`octet` van acht bits en ligt tussen 0 en 255.

In een octet hebben de bits van links naar rechts de waarden 128, 64, 32, 16, 8, 4, 2 en 1. Het decimale getal is de som van de waarden waar een 1 staat. Zo is `01001101` gelijk aan 64 + 8 + 4 + 1 = 77 en `11111111` gelijk aan 255.

Een subnetmasker bestaat uit aaneengesloten enen gevolgd door nullen. De enen horen bij het netwerkdeel. `/24` betekent 24 enen, dus `255.255.255.0`; de laatste acht bits vormen het apparaatdeel.

Het {term}`netwerkadres` ontstaat door alle apparaatbits op 0 te zetten. Het {term}`broadcastadres` heeft alle apparaatbits op 1. In de gewone subnetten van deze module krijgt geen enkel apparaat een van deze twee adressen.

### Voorbeeld: /24

`192.168.10.37/24` heeft netwerkadres `192.168.10.0`, broadcastadres `192.168.10.255` en bruikbare adressen `.1` tot en met `.254`. Ook een routeraansluiting gebruikt een bruikbaar adres. Dat de gateway meestal `.1` is, is een gewoonte en geen regel.

## Een grens midden in een octet

Bij `/26` zijn zes bits beschikbaar voor het apparaatdeel. Dat geeft 2⁶ = 64 adressen per blok, waarvan 62 bruikbaar. Het laatste octet van het masker is binair `11000000`, dus 192. Het masker is `255.255.255.192`.

In een /24-gebied beginnen de /26-blokken op `.0`, `.64`, `.128` en `.192`. Adres `.77` valt in het blok `.64` tot en met `.127`.

| Onderdeel van 192.168.10.77/26 | Waarde |
| --- | --- |
| Netwerkadres | 192.168.10.64 |
| Broadcastadres | 192.168.10.127 |
| Bruikbaar | 192.168.10.65 tot en met 192.168.10.126 |
| Aantal bruikbaar | 62 |

Je kunt het netwerkadres ook bitsgewijs berekenen met een AND: de uitkomst is alleen 1 als beide bits 1 zijn. Het masker houdt zo de netwerkbits over en maakt de apparaatbits 0: `01001101` (77) AND `11000000` (192) geeft `01000000` (64). Het broadcastadres krijg je door de zes apparaatbits op 1 te zetten.

### Van prefix naar masker en blok

Bij prefix /n blijven `32 − n` apparaatbits over. Het aantal adressen per blok is 2 tot die macht. In de tabel liggen alle apparaatbits in het laatste octet:

| Prefix | Masker | Adressen per blok | Bruikbare adressen |
| --- | --- | --- | --- |
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /30 | 255.255.255.252 | 4 | 2 |

Blokken beginnen steeds op een veelvoud van de blokgrootte. Zoek het blok waarin het adres valt: het eerste adres is het netwerkadres, het laatste het broadcastadres en alle adressen daartussen zijn bruikbaar.

::: {exercise} Zonder Filius: adressen berekenen
:label: nw03-o2

Bepaal voor elk adres het netwerkadres, het broadcastadres, de bruikbare reeks en het aantal bruikbare adressen:

1. `192.168.20.145/27`
2. `10.4.2.200/25`
3. Kan `192.168.20.159/27` het adres van een computer zijn? Leg uit.
:::

::: {solution} nw03-o2
:class: dropdown

1. Masker `255.255.255.224`, blokgrootte 32: netwerkadres `192.168.20.128`, broadcastadres `192.168.20.159`, bruikbaar `.129` tot en met `.158`, 30 adressen.
2. Masker `255.255.255.128`: netwerkadres `10.4.2.128`, broadcastadres `10.4.2.255`, bruikbaar `.129` tot en met `.254`, 126 adressen.
3. Nee. Dit is het broadcastadres van het subnet `192.168.20.128/27`.
:::

## Hoe groot moet het subnet zijn?

Zoek het kleinste aantal apparaatbits h waarvoor `2^h − 2` groot genoeg is. Tel alle interfaces mee: computers, {term}`servers <server>` en de routeraansluiting. We behandelen alleen gewone LAN-subnetten, niet de bijzondere /31 en /32.

### Voorbeeld

Je hebt 26 computers, twee servers en één routeraansluiting: 29 adressen. Met vijf apparaatbits zijn er 30 bruikbare adressen, dus `/27` past. `/28` heeft er maar 14. Wil je ruimte voor groei, dan is een groter subnet een betere keuze.

::: {exercise} Zonder Filius: een passend subnet kiezen
:label: nw03-o3

1. Kies het kleinste subnet voor 45 computers, één server en één routeraansluiting. Geef prefix, masker en aantal bruikbare adressen.
2. Doe hetzelfde voor twaalf computers en één routeraansluiting.
3. In situatie 2 komen drie computers bij. Wat betekent dat voor je keuze?
:::

::: {solution} nw03-o3
:class: dropdown

1. 47 adressen: /26, masker `255.255.255.192`, 62 bruikbaar.
2. 13 adressen: /28, masker `255.255.255.240`, 14 bruikbaar.
3. Nu zijn 16 adressen nodig en is /28 te klein. /27 biedt 30. Reken dus groei vooraf mee.
:::

## Zit de bestemming in mijn subnet?

Een afzender berekent met zijn eigen masker het netwerkadres van zichzelf en van de bestemming. Zijn die gelijk, dan is de bestemming lokaal. Zijn ze verschillend, dan heeft de afzender een router nodig, meestal de standaardgateway. Hoofdstuk 4 werkt dat verder uit.

Voorbeeld: `192.168.10.65/26` en `192.168.10.100/26` hebben allebei netwerkadres `.64`. Adres `.130` heeft met hetzelfde masker netwerkadres `.128`. Voor de eerste afzender is `.130` dus niet lokaal, ook als beide apparaten op dezelfde switch zitten.

::: {exercise} Filius: hetzelfde subnet of niet?
:label: nw03-o4

1. Maak twee computers op één switch: A `192.168.10.65` en B `192.168.10.100`, beide met masker `255.255.255.192`. Stel geen gateways in.
2. Voorspel en test een ping van A naar B.
3. Geef B het adres `192.168.10.130` (masker blijft `255.255.255.192`). Voorspel en test opnieuw. Leg uit waarom ‘ze zitten op dezelfde switch’ nu niet genoeg is.
4. Zet het adres van B terug en bewaar als `03-subnetproef.fls`.
:::

::: {solution} nw03-o4
:class: dropdown

Eerst liggen beide adressen in subnet `192.168.10.64/26` en kunnen ze rechtstreeks communiceren. Daarna ligt B in `192.168.10.128/26`. A beschouwt B dan niet als lokaal en heeft een router nodig. Die is er niet, dus de ping mislukt. De fysieke aansluiting op één switch verandert dat niet: IP-subnetten en de Ethernetstructuur zijn verschillende dingen.
:::

## Eigen apparaat: let op het masker

Het masker op je computer kan op school anders zijn dan thuis. Een adres dat met `10.` begint, heeft niet automatisch masker /8: het ingestelde masker bepaalt de grens. In hoofdstuk 4 zoek je de netwerkgegevens van je eigen apparaat op.
