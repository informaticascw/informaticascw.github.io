# Computernetwerken — complete leesversie

Deze leesversie staat buiten de website-inhoudsopgave. De [begrippenlijst](../99-begrippenlijst.md) blijft één apart bronbestand.


---

(netwerken-h01)=
# Bits versturen

## Inleiding

Je verstuurt een foto. Over de verbinding gaan geen plaatjes maar signalen, zoals lichtpulsen of spanningsverschillen. De ontvanger moet daaruit dezelfde {term}`bits <bit>` afleiden als de zender verstuurde. Dat lukt alleen als beide kanten van tevoren afspreken hoe een 0, een 1 en het tempo eruitzien.

**Laag:** {term}`fysieke laag`. **Vraag:** hoe herkent de ontvanger dezelfde bitreeks als de zender verstuurde, en hoe snel kan dat?

## Klassikaal: een bitreeks overseinen

Werk in teams van vier: zender, ontvanger, tijdwaarnemer en controleur. De docent geeft alleen de zender een geheime reeks van acht bits. Zender en ontvanger staan enkele meters uit elkaar. Alle teams doen tegelijk mee.

1. **Ronde 1, zonder afspraken.** De zender gebruikt alleen een zaklamp of een omhooggehouden kaart. Praten, schrijven en wijzen zijn niet toegestaan. De ontvanger schrijft op wat hij denkt te ontvangen.
2. **Ronde 2, met afspraken.** Spreek een code, een startteken en een vast tempo af. Verstuur een nieuwe reeks. De ontvanger meldt het resultaat terug, zodat de zender kan controleren of het klopt.
3. **Ronde 3, sneller.** Verhoog het tempo tot er fouten optreden.

Bespreek welke afspraken het verschil maakten. De uitleg hieronder beschrijft die afspraken ook zonder de oefening.

## Van bit naar signaal

Een bit is een waarde: 0 of 1. Om die over te dragen is een fysiek verschijnsel nodig. Via koper gebruik je elektrische signalen, via glasvezel licht en via {term}`wifi` radiogolven. De zender zet bits om in signalen; de ontvanger leidt de bits daar weer uit af.

‘Licht aan is 1, licht uit is 0’ lijkt voldoende, maar is een lange periode licht één 1 of tien enen? De ontvanger moet dus ook weten hoe lang één bit duurt en waar een bericht begint. Echte verbindingen gebruiken uitgebreidere codes dan dit voorbeeld.

Afspraken over hoe apparaten communiceren heten een {term}`protocol`. De fysieke laag heeft één taak: bits als signalen over een {term}`medium` overbrengen. Protocollen voor die laag leggen onder andere de bitduur en de signaalvorm vast.

### Voorbeeld

Je spreekt af: één bit per seconde, beginnen na twee korte flitsen. Vier seconden licht betekent nu vier enen. Zonder de afspraak over de bitduur is dat niet te bepalen.

::: {exercise} Zonder Filius: ontbrekende afspraken
:label: nw01-o1

1. Een zender verstuurt `1001`. Waarom is alleen ‘licht aan is 1’ onvoldoende voor de ontvanger?
2. Noem twee afspraken die zender en ontvanger naast de betekenis van 0 en 1 nodig hebben.
3. De zender verkort de bitduur zonder de ontvanger te waarschuwen. Wat gaat er mis?
:::

::: {solution} nw01-o1
:class: dropdown

1. De ontvanger weet niet waar het ene bit eindigt en het volgende begint, en ook niet waar het bericht start.
2. Bijvoorbeeld een startteken en een vaste bitduur.
3. De ontvanger blijft met de oude bitduur lezen. Daardoor worden bits samengevoegd of overgeslagen en klopt de ontvangen reeks niet meer.
:::

## Snelheid en vertraging

De snelheid van een verbinding geef je aan in {term}`bits per seconde`, bijvoorbeeld 100 Mbit/s. In deze module noemen we die beschikbare overdrachtscapaciteit de {term}`bandbreedte`. Een {term}`byte` is acht bits, dus MB en Mbit zijn niet hetzelfde.

De {term}`vertraging` is de tijd tussen verzenden en aankomen. Een verbinding met veel capaciteit kan toch een merkbare vertraging hebben, bijvoorbeeld door een lange route of wachtrijen. De traagste schakel op de route bepaalt hoe snel gegevens maximaal aankomen.

### Voorbeeld

Een bestand van 20 MB is 160 Mbit (decimale eenheden). Bij 40 Mbit/s kost het overbrengen minstens 4 seconden. Opstarttijd, extra protocolinformatie en ander verkeer zijn daarbij niet meegerekend.

::: {exercise} Zonder Filius: sneller of eerder?
:label: nw01-o2

1. Bereken de minimale overdrachtstijd van 12 MB bij 24 Mbit/s.
2. Verbinding X heeft 1000 Mbit/s en 80 ms vertraging; verbinding Y heeft 100 Mbit/s en 10 ms vertraging. Welke is gunstiger voor korte interactieve berichten en welke voor een groot bestand? Geef je aanname erbij.
:::

::: {solution} nw01-o2
:class: dropdown

1. 12 × 8 / 24 = 4 seconden.
2. Voor korte berichten is Y gunstiger vanwege de lagere vertraging. Voor een groot bestand is X gunstiger vanwege de hogere capaciteit. Dat geldt als de rest van de route en de server geen grotere beperking vormen.
:::

## Fysieke verbindingen in de praktijk

Kijk op je apparaat of je verbonden bent met wifi of met {term}`Ethernet`. Bekijk een netwerkkabel en, als die er is, een glasvezelaansluiting. Een kabel bevat meestal meerdere aders; één bit hoeft dus niet letterlijk één puls op één draad te zijn.

::: {exercise} Filius: je eerste verbinding
:label: nw01-o3

1. Maak in de ontwerpmodus twee computers en verbind ze met een kabel. Geef ze de namen A en B. Bewaar als `01-verbinding.fls`.
2. Wijs aan welk onderdeel in je tekening de fysieke verbinding voorstelt.
3. Leg uit waarom deze tekening nog niet bewijst dat A een webpagina van B kan ophalen.
:::

::: {solution} nw01-o3
:class: dropdown

De kabel stelt de fysieke verbinding voor. Voor een werkende webdienst zijn ook adressering, protocolafspraken en software op beide computers nodig. Filius laat een model zien, geen echte elektrische of optische signalen.
:::

---

(netwerken-h02)=
# Een lokaal netwerk

## Inleiding

Twee computers verbind je met één kabel. Voor twintig computers is een kabel per paar onwerkbaar: je sluit ze aan op een {term}`switch`. Dan moet elk bericht wel aanwijzen voor wie het bedoeld is. Daarvoor gebruikt een lokaal netwerk adressen.

**Laag:** {term}`datalinklaag`. **Vraag:** hoe komt een {term}`frame` op een lokaal netwerk bij precies het juiste apparaat?

Je leert welke gegevens een frame bevat, hoe een switch uit verkeer leert waar apparaten zitten en waarom sommige frames toch naar alle apparaten gaan.

## Klassikaal: de leertabel van een switch naspelen

Maak groepen van zes: vier apparaten, één switch en één waarnemer. Elk apparaat krijgt een unieke code. Alleen de switch weet op welke poort wie zit; gebruik vier stapeltjes papier als poorten. Een frame bevat een broncode, een bestemmingscode en een bericht.

De switch begint met een lege tabel. Bij elk frame schrijft hij de broncode en de poort van binnenkomst op. Kent hij de bestemming, dan levert hij het frame alleen op die poort af. Kent hij de bestemming niet, dan maakt hij kopieën voor alle andere poorten. De bedoelde ontvanger antwoordt.

Laat A naar B sturen, daarna B naar A en daarna A weer naar B. Laat vervolgens iemand een frame naar ‘iedereen’ sturen. De waarnemer telt per beurt de kopieën. Verklaar waarom de eerste beurt anders verloopt dan de latere.

## Adressen en frames

De datalinklaag verpakt gegevens in frames. Een Ethernetframe bevat onder andere een bron-MAC-adres, een bestemmings-MAC-adres en de gegevens die het vervoert. Achteraan staat een controlegetal, de {term}`FCS`, berekend met {term}`CRC`. De ontvanger kan daarmee veel overdrachtsfouten opsporen, maar de FCS herstelt de gegevens niet.

Een {term}`MAC-adres` hoort bij een {term}`netwerkinterface`, bijvoorbeeld `02:00:00:00:10:0a`. Een computer met een bekabelde en een draadloze interface heeft dus twee MAC-adressen. Apparaten kunnen ook een aangepast of willekeurig MAC-adres gebruiken.

Een frame kan aan één ontvanger gericht zijn ({term}`unicast`) of aan alle apparaten op het lokale netwerk ({term}`broadcast`). Het Ethernetbroadcastadres is `ff:ff:ff:ff:ff:ff`. Alle apparaten in het {term}`broadcastdomein` ontvangen zo’n frame.

## Hoe een switch leert

Een switch leert uit het bronadres van binnenkomende frames via welke poort een MAC-adres bereikbaar is. Kent hij de bestemming, dan stuurt hij het frame alleen via die poort door. Kent hij de bestemming niet, dan stuurt hij het frame via alle andere poorten door. Dat heet {term}`flooding`. Broadcasts worden altijd zo verspreid.

### Voorbeeld

A zit op poort 1 en B op poort 3. Zodra A een frame verstuurt, leert de switch ‘A zit op poort 1’. Zodra B antwoordt, leert hij ‘B zit op poort 3’. Een volgend frame van A naar B gaat alleen via poort 3. De tabel wordt dus tijdens het gebruik opgebouwd en is niet vooraf ingesteld.

::: {exercise} Zonder Filius: vul de leertabel in
:label: nw02-o1

Een switch met vier poorten heeft een lege tabel en ontvangt achtereenvolgens: A→B op poort 1, B→A op poort 3 en C→B op poort 2.

1. Geef na elk frame de leertabel.
2. Via welke poorten verstuurt de switch elk frame door?
3. Wat verandert als C daarna een broadcast verstuurt?
:::

::: {solution} nw02-o1
:class: dropdown

1. Eerst A:1; daarna A:1 en B:3; ten slotte ook C:2.
2. A→B: poorten 2, 3 en 4 (B is nog onbekend). B→A: alleen poort 1. C→B: alleen poort 3.
3. De broadcast gaat via poorten 1, 3 en 4. Een broadcast wordt altijd naar alle andere poorten gestuurd, ook als alle adressen bekend zijn.
:::

## Een lokaal netwerk bouwen

In Filius gebruik je alvast {term}`IP-adressen <IP-adres>` om met `ping` verkeer te maken. De switch kiest zijn doorstuurpoort niet op basis van het IP-adres, maar op basis van het MAC-adres. Ping gebruikt {term}`ICMP`, niet {term}`TCP`. Hoe een computer het MAC-adres van de ontvanger te weten komt, behandelen we in hoofdstuk 4.

::: {exercise} Filius: drie computers en een switch
:label: nw02-o2

1. Bouw A, B en D met één switch. Geef ze de adressen `192.168.10.10`, `192.168.10.20` en `192.168.10.30`, allemaal met {term}`subnetmasker` `255.255.255.0`. Laat de {term}`gateway` leeg.
2. Installeer in de simulatiemodus de opdrachtregel op A en ping B.
3. Open de gegevensuitwisseling van A en B. Zoek de velden met bron en bestemming. Welke velden bevatten MAC-adressen en welke IP-adressen?
4. Bekijk, als jouw Filius-versie dat toont, de leertabel van de switch.
5. Bewaar als `02-lokaal.fls`.
:::

::: {solution} nw02-o2
:class: dropdown

Een geslaagde ping toont dat A en B kunnen communiceren. In de gegevensuitwisseling staan MAC-adressen in de Ethernetvelden en IP-adressen in de IP-velden. Of je de leertabel van de switch kunt bekijken, hangt af van je Filius-versie. Filius is een vereenvoudigd model; de klassikale oefening en de papieren opdracht laten het leerproces van de switch beter zien.
:::

## Eigen omgeving: switch, accesspoint en router

Zoek in het lokaal een Ethernetwandcontactdoos of bekijk samen met de docent een losse switch. Een wandcontactdoos is zelf geen switch: volg de kabel tot het apparaat. Een draadloos accesspoint verbindt wifiapparaten met het lokale netwerk. Een thuisapparaat combineert vaak accesspoint, switch en {term}`router` in één behuizing.

::: {exercise} Eigen omgeving: taak of apparaat?
:label: nw02-o3

1. Een thuisapparaat heeft vier LAN-poorten en wifi. Waarom is ‘dit apparaat is alleen een router’ onvolledig?
2. Waarom bewijzen knipperende lampjes niet dat een website bereikbaar is?
:::

::: {solution} nw02-o3
:class: dropdown

1. Het apparaat voert meerdere taken uit: switch, accesspoint en router. Eén behuizing kan dus meerdere netwerkfuncties bevatten.
2. Lampjes tonen dat er een verbinding of verkeer is, maar niet of adressering, {term}`routering`, {term}`DNS` en de webserver werken.
:::

---

(netwerken-h03)=
# Een wereldwijd netwerk

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

---

(netwerken-h04)=
# Lokale netwerken en wereldwijde netwerken verbinden

## Inleiding

Een programma geeft een IP-adres op als bestemming, maar een {term}`Ethernetframe <frame>` heeft een {term}`MAC-adres` als bestemming nodig. De computer moet dus twee dingen doen. Eerst bepaalt hij met het {term}`subnetmasker` welk apparaat op zijn eigen netwerk het pakket als eerste moet ontvangen: de bestemming zelf of de {term}`gateway`. Daarna zoekt hij met {term}`ARP` het MAC-adres van dat apparaat.

**Laag:** de overgang van netwerklaag naar datalinklaag. **Vraag:** naar welk apparaat stuurt een computer een pakket, en hoe vindt hij daarvan het MAC-adres?

## Rechtstreeks of via de gateway?

```{figure} ../images/twee-lans.svg
:alt: Twee lokale Ethernetnetwerken met ieder een eigen switch en een router ertussen.

Twee lokale Ethernetnetwerken met een router ertussen.
```

We gebruiken twee afzonderlijke Ethernetnetwerken, elk met een eigen {term}`switch`. Een {term}`router` verbindt ze. De router heeft op elk netwerk een eigen aansluiting met een eigen IP-adres en MAC-adres.

| Apparaat | Aansluiting | IP-adres | Subnetmasker | Standaardgateway |
| --- | --- | --- | --- | --- |
| Computer A | Linker netwerk | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| Computer B | Linker netwerk | 192.168.10.20 | 255.255.255.0 | 192.168.10.1 |
| Router | Linker netwerk | 192.168.10.1 | 255.255.255.0 | — |
| Router | Rechter netwerk | 192.168.20.1 | 255.255.255.0 | — |
| Computer C | Rechter netwerk | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |

Computer A wil gegevens versturen en bepaalt met zijn masker of de bestemming in zijn eigen subnet ligt.

- **Binnen het eigen subnet:** A stuurt rechtstreeks naar de bestemming.
- **Buiten het eigen subnet:** A stuurt naar een router. Daarvoor gebruikt A de standaardgateway.

De standaardgateway is dus het IP-adres van een routeraansluiting in het eigen subnet. In dit hoofdstuk stellen we geen extra routes in op de computers.

### Voorbeeld: van A naar B

A heeft {term}`netwerkadres` `192.168.10.0`. Met het masker van A heeft het adres van B hetzelfde netwerkadres. A kan B dus rechtstreeks bereiken, zonder router.

### Voorbeeld: van A naar C

Met het masker van A heeft het adres van C netwerkadres `192.168.20.0`. Dat is een ander subnet, dus A levert de gegevens af bij gateway `192.168.10.1`.

::: {exercise} Zonder Filius: welke volgende ontvanger?
:label: nw04-o1

Gebruik de instellingen van computer A uit de tabel.

1. Bepaal voor elke bestemming of A rechtstreeks verstuurt of de gateway gebruikt: `192.168.10.50`, `192.168.20.10` en `192.168.11.10`.
2. Waarom kan A niet `192.168.20.1` als standaardgateway gebruiken?
3. Een leerling zegt: ‘De eerste twee getallen van de IP-adressen zijn gelijk, dus de computers zitten in hetzelfde subnet.’ Weerleg dat met een bestemming uit vraag 1.
:::

::: {solution} nw04-o1
:class: dropdown

1. `192.168.10.50`: rechtstreeks. De andere twee: via `192.168.10.1`.
2. De gateway moet rechtstreeks bereikbaar zijn in het eigen subnet. `192.168.20.1` zit op het andere Ethernetnetwerk.
3. Bij `192.168.11.10` zijn de eerste twee getallen gelijk, maar bij masker `255.255.255.0` hoort ook het derde getal bij het {term}`netwerkdeel`. Dat adres ligt dus in een ander subnet.
:::

::: {exercise} Filius: bouwen en voorspellen
:label: nw04-o2

1. Bouw de opstelling uit de tabel: A en B op de linker switch, C op de rechter switch en een router tussen de switches. Gebruik een gewone router met twee aansluitingen.
2. Stel de IP-adressen en subnetmaskers in. Laat de standaardgateway op de computers voorlopig leeg en gebruik geen automatische adresuitgifte.
3. Voorspel of A met `ping` B en C kan bereiken en schrijf bij beide een reden op.
4. Start de simulatie, installeer op A de opdrachtregel en test `ping 192.168.10.20` en `ping 192.168.20.10`.
5. Vergelijk je waarnemingen met je voorspellingen.
6. Stel op A, B en C de gateways uit de tabel in en test opnieuw. Verklaar wat er verandert.

Bewaar je netwerk. Je gebruikt het in de volgende opdrachten opnieuw.
:::

::: {solution} nw04-o2
:class: dropdown

Zonder gateway kan A wel B bereiken, maar C niet. Met de juiste gateways kan het verkeer heen en terug tussen A en C lopen. De router kent beide netwerken via zijn eigen aansluitingen. Een switch heeft hiervoor geen IP-configuratie nodig.
:::

## ARP: het MAC-adres bij een IP-adres vinden

A weet nu dat B rechtstreeks bereikbaar is. In het Ethernetframe moet echter een MAC-adres staan, en A kent alleen het IP-adres van B. Het eigen MAC-adres kent A al via zijn netwerkinterface. Het MAC-adres van de ontvanger vindt hij met ARP, het Address Resolution Protocol:

1. A zoekt in zijn {term}`ARP-cache`: een tijdelijke tabel met IP-adressen en bijbehorende MAC-adressen.
2. Staat B er niet in, dan verstuurt A een {term}`ARP-request`: ‘Wie heeft IP-adres 192.168.10.20? Meld je bij 192.168.10.10.’
3. Dit request zit in een Ethernetframe met {term}`broadcastadres` `ff:ff:ff:ff:ff:ff`. De switch verspreidt het over alle andere aansluitingen van het lokale netwerk.
4. B herkent zijn eigen IP-adres en stuurt een {term}`ARP-reply` rechtstreeks naar A, met daarin zijn MAC-adres.
5. A bewaart de koppeling tijdelijk in zijn ARP-cache en kan het {term}`IP-pakket` in een frame naar B versturen.

Andere apparaten ontvangen het request ook, maar antwoorden niet. De router stuurt het ARP-request niet door naar het rechter netwerk.

::: {note} ARP en de lagen

IP regelt adressering tussen netwerken en Ethernet de aflevering op het lokale netwerk. ARP verbindt die twee: het zoekt bij een lokaal IP-adres het MAC-adres. Een ARP-bericht zit rechtstreeks in een Ethernetframe, niet in een IP-pakket.
:::

### Voorbeeld: de adressen in een lokaal bericht

In de voorbeelden gebruiken we deze MAC-adressen. Filius kent zelf andere adressen toe.

| Aansluiting | MAC-adres |
| --- | --- |
| A | 02:00:00:00:10:0a |
| B | 02:00:00:00:10:14 |
| Router links | 02:00:00:00:10:01 |
| Router rechts | 02:00:00:00:20:01 |
| C | 02:00:00:00:20:0a |

Na de ARP-uitwisseling verstuurt A een IP-pakket naar B:

| Onderdeel | Bron | Bestemming |
| --- | --- | --- |
| Ethernetframe | MAC-adres A | MAC-adres B |
| IP-pakket in dat frame | 192.168.10.10 | 192.168.10.20 |

::: {exercise} Zonder Filius: wie krijgt welk bericht?
:label: nw04-o3

De ARP-cache van A is leeg. A wil een IP-pakket naar B sturen.

1. Schrijf de vraag uit het ARP-request op.
2. Geef het bron- en bestemmings-MAC-adres van het frame met dat request.
3. Welke apparaten ontvangen het request: B, de linker routeraansluiting en/of C?
4. Wie antwoordt? Is dat antwoord een {term}`broadcast`?
5. Waarom is niet voor elk volgend IP-pakket een nieuwe broadcast nodig?
:::

::: {solution} nw04-o3
:class: dropdown

1. Wie heeft `192.168.10.20`? Meld je bij `192.168.10.10`.
2. Bron `02:00:00:00:10:0a`, bestemming `ff:ff:ff:ff:ff:ff`.
3. B en de linker routeraansluiting. C niet.
4. B antwoordt rechtstreeks aan het MAC-adres van A. Dat is {term}`unicast`, geen broadcast.
5. A bewaart de koppeling tijdelijk in de ARP-cache.
:::

::: {exercise} Filius: ARP waarnemen
:label: nw04-o4

1. Start de simulatie opnieuw en open bij A het venster met de gegevensuitwisseling (via het contextmenu van de computer; de naam kan per taalversie verschillen).
2. Ping B en zoek in de gegevensuitwisseling naar ARP.
3. Noteer uit het request het gezochte IP-adres en het bestemmings-MAC-adres, en uit het reply het gevonden MAC-adres.
4. Ping B direct opnieuw. Is er weer ARP nodig? Onderbouw met wat je ziet.
5. Leg uit waarom ‘bij elke ping gaat eerst een ARP-request uit’ geen goede regel is.
:::

::: {solution} nw04-o4
:class: dropdown

Het request vraagt naar het IP-adres van B en gaat naar het Ethernetbroadcastadres. Het reply bevat het MAC-adres van B. Bij een directe herhaling is normaal geen nieuw ARP nodig, omdat de koppeling nog in de cache staat. Vergelijk deze verklaring met je eigen waarnemingen.
:::

## Via de gateway naar een ander netwerk

A wil een IP-pakket naar C sturen. C ligt buiten het eigen subnet, dus A levert het pakket eerst af bij zijn gateway.

**A zoekt met ARP het MAC-adres van de gateway, niet dat van C.** De gateway ligt op hetzelfde Ethernetnetwerk als A, C niet.

Het IP-pakket blijft aan C gericht. Alleen het Ethernetframe is aan de router gericht.

### Voorbeeld: van A via de router naar C

| Verbinding | Bron-MAC | Bestemmings-MAC | Bron-IP | Bestemmings-IP |
| --- | --- | --- | --- | --- |
| A naar router | A | Router links | 192.168.10.10 | 192.168.20.10 |
| Router naar C | Router rechts | C | 192.168.10.10 | 192.168.20.10 |

De router haalt het IP-pakket uit het frame en bepaalt via welke aansluiting de bestemming bereikbaar is. Op het rechter netwerk maakt hij een nieuw frame. Kent hij het MAC-adres van C nog niet, dan gebruikt hij daar zelf eerst ARP.

De IP-adressen blijven gelijk, omdat we hier geen {term}`NAT` gebruiken. Het frame wordt per verbinding vervangen; het IP-pakket gaat verder naar zijn bestemming.

::: {exercise} Zonder Filius: volg het antwoord
:label: nw04-o5

C stuurt een antwoord naar A. Ga ervan uit dat alle benodigde ARP-koppelingen bekend zijn.

1. Maak voor de terugweg dezelfde tabel als in het voorbeeld.
2. Een leerling zegt: ‘A zet het IP-adres van de gateway als bestemming in het IP-pakket, want daar moet het pakket eerst naartoe.’ Verbeter dat.
3. Naar welk IP-adres vraagt A met ARP voordat hij naar C kan versturen? Waarom niet naar het IP-adres van C?
:::

::: {solution} nw04-o5
:class: dropdown

1.

   | Verbinding | Bron-MAC | Bestemmings-MAC | Bron-IP | Bestemmings-IP |
   | --- | --- | --- | --- | --- |
   | C naar router | C | Router rechts | 192.168.20.10 | 192.168.10.10 |
   | Router naar A | Router links | A | 192.168.20.10 | 192.168.10.10 |

2. Het bestemmings-IP-adres blijft dat van de eindbestemming. Alleen het bestemmings-MAC-adres in het frame is dat van de gateway.
3. A vraagt naar `192.168.10.1`. C ligt buiten het lokale netwerk van A en ontvangt het ARP-request niet.
:::

::: {exercise} Filius: twee soorten adressen
:label: nw04-o6

1. Start de simulatie opnieuw en open de gegevensuitwisseling bij A en bij de router.
2. Ping vanaf A naar C.
3. Zoek het ARP-request van A. Vraagt A naar het adres van C of naar dat van de gateway?
4. Zoek het IP-pakket van A naar C. Noteer het bestemmings-IP-adres en het bestemmings-MAC-adres van het frame waarin het zit.
5. Bekijk hoe de router het pakket naar C verstuurt. Welke adressen veranderen en welke blijven gelijk?
6. Leg uit waarom zowel een IP-adres als een MAC-adres nodig is.
:::

::: {solution} nw04-o6
:class: dropdown

A vraagt naar `192.168.10.1`. Het IP-pakket gaat naar `192.168.20.10`, in een frame naar de linker routeraansluiting. Op de volgende verbinding veranderen beide MAC-adressen; bron- en bestemmings-IP blijven gelijk. De router kan op het rechter netwerk zelf ARP gebruiken om C te vinden. Bij een herhaling is niet altijd nieuw ARP nodig.
:::

## Eigen apparaat: IP-adres, MAC-adres en gateway

De soorten adressen uit Filius staan ook op je eigen computer. Een computer kan meerdere netwerkadapters hebben, bijvoorbeeld voor {term}`wifi` en voor Ethernet.

::: {exercise} Eigen apparaat: vind je IP-adres, MAC-adres en gateway
:label: nw04-o7

1. Open de netwerkgegevens met de aanwijzingen hieronder.
2. Noteer van je actieve verbinding het IPv4-adres, het subnetmasker (of de {term}`prefixlengte <CIDR-prefix>`), het MAC-adres en de standaardgateway. De gateway kan ook ‘router’ heten.
3. Bepaal met het masker of je gateway in jouw subnet ligt. Schrijf je berekening op. Ga niet zonder controle uit van `/24`.
4. Vergelijk met een klasgenoot: hebben jullie hetzelfde IP-adres, MAC-adres en dezelfde gateway? Wat verwacht je als jullie in hetzelfde subnet zitten?
5. Stel dat je een website buiten je subnet bezoekt en de benodigde ARP-koppeling nog niet bekend is. Naar welk adres vraagt je computer dan met ARP?

**Chromebook:** open Instellingen → Netwerk → Wifi en kies je verbonden netwerk. In de netwerkdetails staan de IP-configuratie en de gateway, en ook het MAC-adres van de wifi-adapter. Je kunt ook het netwerkmenu rechtsonder en het informatiepictogram gebruiken. Op een beheerd apparaat kunnen details verborgen zijn.

**Windows:** open de Opdrachtprompt en voer `ipconfig /all` uit. Zoek bij de actieve wifi- of Ethernetadapter het IPv4-adres, het subnetmasker, de standaardgateway en het fysieke adres. Het fysieke adres is het MAC-adres. Sla adapters over waarbij staat dat de verbinding is verbroken.

**Mac:** open Systeeminstellingen → Netwerk → de actieve verbinding → Details. Bij TCP/IP staan het IPv4-adres, het subnetmasker en de router. Het MAC-adres staat bij Hardware of in de wifi-details.

Verander geen instellingen. Kun je de gegevens niet zien, gebruik dan het voorbeeld hieronder en vergelijk dat met een apparaat waarop het wel kan.

**Voorbeeld (geen meting van het schoolnetwerk):**

```text
IPv4-adres        192.168.10.37
Subnetmasker      255.255.255.0
Standaardgateway  192.168.10.1
MAC-adres         02:00:00:00:10:25
```
:::

::: {solution} nw04-o7
:class: dropdown

Je waarden hangen af van je verbinding. In het voorbeeld hebben zowel `192.168.10.37` als de gateway `192.168.10.1` met het masker netwerkadres `192.168.10.0`, dus de gateway ligt in hetzelfde subnet.

Klasgenoten in hetzelfde subnet hebben verschillende IPv4-adressen en normaal ook verschillende MAC-adressen. Meestal hebben ze dezelfde gateway. Dezelfde wifinaam bewijst niet dat jullie in hetzelfde subnet zitten.

Voor een website buiten het eigen subnet zoekt de computer met ARP het MAC-adres van de gateway, niet dat van de website. Op wifi kan het MAC-adres privaat of willekeurig zijn. Een MAC-adres is dus niet altijd een vast serienummer van de computer.
:::

---

(netwerken-h05)=
# Routeren

## Inleiding

In hoofdstuk 4 gaf je computer een {term}`pakket <IP-pakket>` voor een ander netwerk aan de {term}`gateway`. Daarmee is het pakket er nog niet: ook die {term}`router` moet kiezen waar het naartoe gaat, eventueel naar een volgende router. Elke router beslist alleen over de eerstvolgende stap, met behulp van een {term}`routeringstabel`.

**Laag:** {term}`netwerklaag`. **Vraag:** hoe kiest een router de volgende stap naar een bestemmingsnetwerk, en wat is nodig om ook het antwoord terug te laten komen?

Je breidt je netwerk uit met een tweede router en een derde {term}`LAN`, vult handmatig routeringstabellen in en controleert zowel de heenweg als de terugweg.

## Klassikaal: routers die alleen de volgende stap kennen

Verdeel de klas over drie netwerken en twee routers. Elke router krijgt alleen een eigen routeringstabel, geen plattegrond van het hele netwerk. Leerlingen sturen kaartjes met een bestemmingsnetwerk. De router kiest een volgende stap en mag niets bij de andere router navragen.

1. Stuur een bericht van links naar rechts terwijl de eerste router nog geen route naar rechts heeft. Het bericht blijft liggen.
2. Voeg de ontbrekende route toe. Laat de ontvanger nu antwoorden terwijl de tweede router nog geen route terug heeft. Ook het antwoord blijft liggen.
3. Voeg die route ook toe. Nu komt het antwoord aan.

Bespreek waarom een geslaagde heenweg nog geen geslaagde communicatie is. Gebruik voor de kaartjes de netwerken en routes uit de tabellen hieronder.

## Een tabel met bestemmingsnetwerken

Een router zoekt het IP-adres van de bestemming op in zijn routeringstabel. Een regel bevat een bestemmingsnetwerk, een {term}`masker <subnetmasker>` en de volgende stap: een rechtstreeks aangesloten netwerk of een andere router, de {term}`next hop`. De next hop moet rechtstreeks bereikbaar zijn. Een router stuurt niet naar een router waarvan hij alleen het adres kent maar die ergens ver weg staat.

### Een tweede router en een derde LAN

```{figure} ../images/routering.svg
:alt: De drie LANs en het aparte verbindingsnetwerk tussen R1 en R2.

De drie LANs en het aparte verbindingsnetwerk tussen R1 en R2.
```

We breiden het netwerk uit hoofdstuk 4 uit met een tweede router en een derde LAN. Er zijn vier subnetten, want ook het verbindingsnetwerk tussen de routers is een subnet.

| Netwerk | Aansluitingen |
| --- | --- |
| Links: 192.168.10.0/24 | A `.10`; R1 `.1` |
| Midden: 192.168.20.0/24 | C `.10`; R1 `.1` |
| Tussen routers: 10.0.0.0/30 | R1 `10.0.0.1`; R2 `10.0.0.2` |
| Rechts: 192.168.30.0/24 | D `.10`; R2 `.1` |

R1 heeft drie aansluitingen en R2 twee. A gebruikt gateway `192.168.10.1`, C `192.168.20.1` en D `192.168.30.1`.

| Router | Bestemming | Volgende stap |
| --- | --- | --- |
| R1 | 192.168.10.0/24 | Rechtstreeks aangesloten |
| R1 | 192.168.20.0/24 | Rechtstreeks aangesloten |
| R1 | 10.0.0.0/30 | Rechtstreeks aangesloten |
| R1 | 192.168.30.0/24 | Via 10.0.0.2 |
| R2 | 192.168.30.0/24 | Rechtstreeks aangesloten |
| R2 | 10.0.0.0/30 | Rechtstreeks aangesloten |
| R2 | 192.168.10.0/24 | Via 10.0.0.1 |
| R2 | 192.168.20.0/24 | Via 10.0.0.1 |

Rechtstreeks aangesloten netwerken kent een router uit de instellingen van zijn aansluitingen. Daarvoor hoef je geen next-hopregels toe te voegen.

::: {exercise} Zonder Filius: volg de route
:label: nw05-o1

1. A verstuurt naar D. Geef de opeenvolgende ontvangers vanaf A.
2. Welk bron- en bestemmings-IP-adres staan in het pakket tussen R1 en R2? Er is geen {term}`NAT`.
3. Welke handmatige regel heeft R2 nodig voor het antwoord aan A?
4. Waarom kan R1 voor netwerk `192.168.30.0/24` niet D als next hop invullen?
:::

::: {solution} nw05-o1
:class: dropdown

1. Eerst R1, dan R2, dan D.
2. Bron `192.168.10.10`, bestemming `192.168.30.10`.
3. `192.168.10.0/24` via `10.0.0.1`.
4. D ligt niet in een subnet waarop R1 rechtstreeks is aangesloten. R1 moet eerst een router sturen die hij wel rechtstreeks kan bereiken.
:::

## Meest specifieke route en standaardroute

Een router kan een {term}`standaardroute` hebben: `0.0.0.0/0`. Die wordt gebruikt als geen specifiekere route past. Passen meerdere regels, dan wint de meest specifieke, dus die met de langste prefix. Een /24 beschrijft minder adressen dan een /16 en is dus specifieker.

Routers kunnen routes automatisch uitwisselen met routeringsprotocollen. In deze module stel je routes handmatig in en behandelen we die protocollen niet.

::: {exercise} Zonder Filius: welke regel wint?
:label: nw05-o2

Een router heeft `10.0.0.0/8 via X`, `10.2.0.0/16 via Y` en `0.0.0.0/0 via Z`. Bepaal de volgende stap voor `10.2.8.4`, `10.3.8.4` en `203.0.113.8`.
:::

::: {solution} nw05-o2
:class: dropdown

`10.2.8.4` gaat via Y: /16 is het meest specifiek. `10.3.8.4` gaat via X: /8 past en /16 niet. `203.0.113.8` gaat via Z: alleen de standaardroute past. X, Y en Z zijn hier rechtstreeks bereikbare next hops.
:::

::: {exercise} Filius: een tweede router toevoegen
:label: nw05-o3

1. Open een kopie van je netwerk uit hoofdstuk 4 en bouw de uitbreiding uit de tabellen. Gebruik voor het verbindingsnetwerk masker `255.255.255.252`.
2. Schakel automatische {term}`routering` op de routers uit, als die aanstaat. Open de tabel voor handmatige routes.
3. Voeg eerst alleen op R1 de route naar `192.168.30.0` met masker `255.255.255.0` via `10.0.0.2` toe. Test A→D. Bereikt het verzoek D? Waarom ontbreekt het antwoord nog?
4. Voeg op R2 de twee ontbrekende routes naar links en midden toe. Test A↔D en C↔D.
5. Bewaar als `05-routering.fls`. Noteer je ingestelde regels en leg van één ping de heen- en terugweg uit.
:::

::: {solution} nw05-o3
:class: dropdown

Met alleen de route op R1 kan het verzoek D bereiken, maar R2 weet niet hoe het antwoord bij A komt. Na het toevoegen van beide terugroutes werkt het verkeer in beide richtingen. De aansluitingen en gateways moeten ook kloppen. Gebruik als next hop het adres van de router op het verbindingsnetwerk, niet een adres aan de andere kant van die router.
:::

## Eigen netwerk: een route is geen rechte kabel

Op Windows gebruik je `tracert stanislas.informatica.nu` en op een Mac in Terminal `traceroute stanislas.informatica.nu`. Op school kunnen deze opdrachten geblokkeerd zijn; de docent kan dan een eigen resultaat laten zien. Op een Chromebook hoef je niets te installeren.

Deze opdrachten sturen berichten waarvan de {term}`TTL` stap voor stap oploopt, waardoor de tussenliggende routers zich melden. Een sterretje bewijst niet dat de route kapot is: een router kan doorsturen zonder op meetberichten te antwoorden. De heen- en terugroute kunnen verschillen. De wachttijd bij één stap is bovendien niet de tijd van alleen dat stuk kabel.

---

(netwerken-h06)=
# Poorten, TCP en UDP

## Inleiding

Een {term}`IP-adres` brengt gegevens bij een computer. Daarop draaien tegelijk een browser, een chatprogramma en een spel. Bovendien kunnen onderweg gegevens verloren gaan, dubbel aankomen of in een andere volgorde binnenkomen. De transportlaag lost beide problemen op.

**Laag:** {term}`transportlaag`. **Vraag:** hoe komen gegevens bij het juiste programma terecht, en hoe zorg je dat ze volledig en in de goede volgorde aankomen?

Je leert eerst hoe poorten programma’s en verbindingen onderscheiden. Daarna bekijk je wat {term}`TCP` extra biedt en wat {term}`UDP` juist niet zelf regelt.

## Klassikaal: een boodschap met ontbrekende delen

Werk met drie teams: zender, netwerk en ontvanger. De ontvanger heeft twee postvakken, genummerd 80 en 5000. De zender krijgt een tekst in zes genummerde delen, allemaal voor hetzelfde postvak. Het netwerkteam houdt één deel achter, verwisselt twee delen en levert één deel dubbel af. De ontvanger kan niet zien wat het netwerk achterhoudt.

1. Probeer eerst zonder terugmeldingen de tekst samen te stellen.
2. Spreek daarna af dat de ontvanger meldt welk deel hij als volgende mist. De zender bewaart kopieën en stuurt zo nodig opnieuw.
3. Kan de ontvanger nu de juiste tekst precies één keer in het juiste postvak leggen?

TCP nummert in werkelijkheid {term}`bytes <byte>` in plaats van tekstdelen. De oefening laat wel volgorde, ontbrekende gegevens, bevestigingen en het juiste ontvangende programma zien.

## Poorten: een adres voor het programma

Een transportbericht bevat een bron- en een bestemmingspoort ({term}`poortnummer`). Een poortnummer is geen fysieke aansluiting: het helpt het besturingssysteem de gegevens bij het juiste programma of de juiste verbinding af te leveren.

Een webserver luistert bij gewoon {term}`HTTP` meestal op TCP-poort 80 en bij {term}`HTTPS` meestal op TCP-poort 443. Een {term}`client` kiest doorgaans een tijdelijke bronpoort. Een TCP-verbinding wordt herkend aan beide IP-adressen en beide poortnummers. TCP en UDP hebben elk hun eigen poortnummers.

### Voorbeeld

Client `192.168.10.10:51000` maakt verbinding met {term}`server` `192.168.20.10:80`. Een tweede verbinding kan bronpoort `51001` gebruiken. Antwoorden gaan van serverpoort 80 terug naar de bijbehorende clientpoort.

::: {exercise} Zonder Filius: naar welk programma?
:label: nw06-o1

1. Geef de bron- en bestemmingspoort van het antwoord van de server op de verbinding met clientpoort 51000.
2. Twee clients gebruiken allebei bronpoort 51000 naar dezelfde serverpoort. Waarom raken hun verbindingen niet door elkaar?
3. Waarom is een TCP-poort iets anders dan poort 3 op een {term}`switch`?
:::

::: {solution} nw06-o1
:class: dropdown

1. Bronpoort 80, bestemmingspoort 51000.
2. De IP-adressen van de clients verschillen. Een verbinding wordt herkend aan beide IP-adressen en beide poorten samen.
3. Een switchpoort is een fysieke aansluiting. Een TCP-poort is een getal in de transportinformatie waarmee software verbindingen en programma’s onderscheidt.
:::

## Wat voegt TCP toe?

{term}`IP` garandeert niet dat elk {term}`pakket <IP-pakket>` aankomt of dat pakketten in volgorde aankomen. TCP biedt de toepassing een betrouwbare, geordende {term}`bytestroom`. TCP verdeelt de gegevens in {term}`segmenten <TCP-segment>`, houdt volgnummers bij, verwerkt bevestigingen en verstuurt ontbrekende gegevens opnieuw. Dubbele gegevens geeft TCP niet dubbel aan het programma.

### Voorbeeld: een ontbrekend stuk

De ontvanger heeft bytes 1–4 en 9–12, maar 5–8 ontbreken. Hij kan 1–12 nog niet in volgorde aan het programma geven. Aan de volgnummers en bevestigingen merkt de zender dat er iets ontbreekt en stuurt dat opnieuw, bijvoorbeeld na een wachttijd. Daarna levert TCP alle bytes in de goede volgorde af. Een dubbel ontvangen stuk geeft TCP niet nogmaals af.

De nummers zijn hier vereenvoudigd; je hoeft de echte {term}`TCP-header <header>` niet te kennen. Het gaat om het verschil: IP bezorgt losse pakketten en TCP maakt daar voor het programma een geordende stroom van.

Voordat gegevens stromen, bouwen client en server een verbinding op met een {term}`handshake`: de berichten SYN, SYN-ACK en ACK. TCP past ook de hoeveelheid gegevens die tegelijk onderweg is aan op de ontvanger en het netwerk. Die regelalgoritmen behandelen we niet.

Betrouwbaar betekent niet dat een verbinding altijd slaagt. Valt een kabel blijvend uit, dan kan ook TCP niets bezorgen en krijgt het programma uiteindelijk een foutmelding. TCP versleutelt gegevens niet.

## Wanneer UDP?

UDP verstuurt afzonderlijke {term}`datagrammen <datagram>` met poortnummers. UDP bouwt zelf geen verbinding op, bevestigt de ontvangst niet en herstelt de volgorde niet. Een programma kan die taken zelf toevoegen. Bij live geluid is een stukje dat te laat opnieuw wordt verstuurd minder bruikbaar dan een stukje dat wordt overgeslagen.

| Eigenschap | TCP | UDP |
| --- | --- | --- |
| Verbinding vooraf | Ja | Niet door UDP zelf |
| Betrouwbare, geordende stroom | Door TCP verzorgd | Niet door UDP verzorgd |
| Grenzen tussen berichten van het programma behouden | Nee (bytestroom) | Ja (datagrammen) |
| Versleuteling | Nee | Nee |

HTTP/3 gebruikt QUIC boven UDP; QUIC zorgt zelf voor betrouwbaarheid en beveiliging. ‘Websites gebruiken altijd TCP’ is dus te stellig. In onze Filius-voorbeelden gebruikt HTTP wel TCP.

::: {exercise} Zonder Filius: kies en onderbouw
:label: nw06-o2

1. Waarom is het belangrijk dat bij een download geen bytes ontbreken?
2. Waarom is wachten op een oud geluidsfragment vervelend bij een live gesprek?
3. Iemand zegt: ‘UDP kan nooit betrouwbare communicatie opleveren.’ Verbeter die uitspraak.
:::

::: {solution} nw06-o2
:class: dropdown

1. Ontbrekende bytes kunnen het bestand onbruikbaar maken. De download moet alle bytes in de goede volgorde afleveren.
2. Wachten vergroot de {term}`vertraging`, terwijl het gesprek al verder is.
3. UDP zelf biedt dat niet, maar een protocol of programma boven UDP kan betrouwbaarheid toevoegen.
:::

::: {exercise} Filius: TCP herkennen
:label: nw06-o3

1. Gebruik C als webserver in je bestaande netwerk: installeer en start de webserver. Installeer op A een webbrowser.
2. Open de gegevensuitwisseling en bezoek vanaf A `http://192.168.20.10`.
3. Zoek de opbouw van de TCP-verbinding en noteer de gebruikte poorten. Welke kant begon?
4. Vergelijk met een ping naar hetzelfde adres. Zie je daar ook een TCP-opbouw?
5. Bewaar als `06-transport.fls`.
:::

::: {solution} nw06-o3
:class: dropdown

De browser is de client en begint de verbinding. De webserver gebruikt normaal TCP-poort 80 en de client een tijdelijke bronpoort. Bij een nieuwe verbinding zijn de opbouwberichten zichtbaar. Ping gebruikt {term}`ICMP` en heeft geen handshake. Een bestaande verbinding kan hergebruikt worden: start de simulatie opnieuw als je juist de eerste verbinding wilt zien.
:::

## Eigen apparaat: meerdere verbindingen

Open in de ontwikkeltools van je browser het tabblad Netwerk en laad een pagina. Zoek, als beschikbaar, het externe adres en de kolom met het protocol. `h2` en `h3` zijn versies van HTTP. Eén pagina kan veel verzoeken aan meerdere servers veroorzaken, en een server kan meerdere verzoeken over één bestaande verbinding afhandelen.

---

(netwerken-h07)=
# DNS: een naam opzoeken

## Inleiding

Je typt een websiteadres in de browser, bijvoorbeeld `http://nieuws.school.test/rooster.html`. Zo’n adres heet een {term}`URL`. Het bevat een protocol (`http`), de naam van een computer (de hostnaam `nieuws.school.test`) en een pad (`/rooster.html`). Het netwerk kan niets met een naam: het heeft een {term}`IP-adres` nodig. Het {term}`DNS` zoekt dat IP-adres bij de hostnaam.

**Laag:** {term}`toepassingslaag`. **Vraag:** hoe vindt een computer het IP-adres dat bij een naam hoort?

## Klassikaal: een naam omzetten in een adres

Maak twee rollen: clients en een DNS-balie. De DNS-balie heeft alleen een lijst met namen en bijbehorende adressen. Alle clients krijgen een URL, zoals `http://nieuws.school.test/sport.html`.

1. Laat de clients eerst de hele URL aan de DNS-balie voorleggen. De balie kent alleen namen en kan niets met het pad.
2. Spreek af dat clients alleen de hostnaam vragen. De balie antwoordt met een adres.
3. Verander op de lijst alleen het adres dat bij een naam hoort. De URL van de clients blijft gelijk, maar ze komen nu bij een ander adres uit.

Bespreek wat de DNS-balie wel en niet weet.

## DNS: namen en adressen koppelen

Het Domain Name System koppelt namen aan gegevens, waaronder IP-adressen. Een {term}`A-record` koppelt een naam aan een IPv4-adres; voor IPv6 is er het AAAA-record.

Je computer vraagt dit meestal aan een {term}`resolver <DNS-resolver>`. Die heeft het antwoord misschien al in een {term}`cache`. Zo niet, dan zoekt hij het op, eventueel via verwijzingen naar andere DNS-servers. DNS is wereldwijd verdeeld: geen enkele server kent alle namen. Rootservers en servers voor topleveldomeinen verwijzen door; gezaghebbende servers beheren de gegevens van hun eigen domeinen.

Een eenvoudige DNS-vraag gaat vaak via UDP-poort 53; DNS kan ook {term}`TCP` gebruiken.

DNS levert geen webpagina en vertaalt niet de hele URL. Bij `http://nieuws.school.test/sport.html` zoekt DNS alleen de hostnaam `nieuws.school.test` op. Het pad `/sport.html` gaat pas later naar de webserver. Namen met `.test` zijn bedoeld voor oefenomgevingen en bestaan niet op het publieke internet.

### Voorbeeld

DNS antwoordt dat `nieuws.school.test` bij `192.168.20.10` hoort. Je computer kan nu verkeer naar dat adres sturen. Bij een volgende vraag kan het antwoord uit een cache komen, dus niet elke vraag start een nieuwe zoekactie over de hele wereld.

::: {exercise} Zonder Filius: wie weet het?
:label: nw07-o1

1. Welke DNS-vraag hoort bij `http://nieuws.school.test/rooster.html`?
2. Waarom hoeven links niet te veranderen als een website naar een nieuw IP-adres verhuist?
3. Een computer vraagt kort na elkaar twee keer naar dezelfde naam. Waarom kan het tweede antwoord sneller komen?
:::

::: {solution} nw07-o1
:class: dropdown

1. Vraag naar het adres van `nieuws.school.test`, niet naar `/rooster.html`.
2. Alleen de DNS-koppeling verandert; de naam blijft hetzelfde. Oude antwoorden kunnen nog tijdelijk in een cache staan.
3. Het eerste antwoord is bewaard in een cache, dus de resolver hoeft het niet opnieuw op te zoeken.
:::

::: {exercise} Filius: een DNS-server instellen
:label: nw07-o2

1. Open `06-transport.fls`. Computer C heeft adres `192.168.20.10`.
2. Voeg aan het netwerk van C een DNS-server toe met adres `192.168.20.53`, masker `255.255.255.0` en {term}`gateway` `192.168.20.1`.
3. Installeer en start de DNS-server. Maak een adresrecord voor `nieuws.school.test` naar `192.168.20.10`.
4. Stel op A het DNS-serveradres `192.168.20.53` in. Laat de gateway goed staan.
5. Ping vanaf A eerst `192.168.20.10` en daarna `nieuws.school.test`.
6. Zoek in de gegevensuitwisseling de DNS-vraag, het DNS-antwoord en de daaropvolgende ping. Welke computer geeft het DNS-antwoord?
7. Bewaar als `07-dns.fls`.
:::

::: {solution} nw07-o2
:class: dropdown

Beide pings werken. Bij de ping op naam gaat eerst een DNS-vraag naar `192.168.20.53`, die het adres `192.168.20.10` teruggeeft. Daarna gaat de ping naar `192.168.20.10`. De DNS-server levert alleen het adres en doet zelf niets met de ping. Dit voorbeeld heeft één lokale DNS-server en bootst de wereldwijde DNS-structuur niet na.
:::

---

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

---

(netwerken-h09)=
# E-mail

## Inleiding

Een website vraag je op: jij begint en de server antwoordt. Bij e-mail werkt het anders. Een bericht gaat van jouw programma naar de mailserver van je school of provider, vandaar naar de mailserver van de ontvanger en wordt daar later opgehaald. Er zijn dus meerdere stappen en meerdere protocollen.

**Laag:** {term}`toepassingslaag`. **Vraag:** welke protocollen en servers zijn betrokken bij het versturen en ontvangen van e-mail?

## Verzenden en ophalen

Verzenden en ophalen zijn aparte taken met aparte protocollen:

- {term}`SMTP` dient om e-mail aan te bieden aan een mailserver en tussen mailservers door te sturen.
- IMAP en POP dienen om ontvangen berichten met een mailprogramma op te halen.
- Bij webmail praat je browser via HTTP met de webmailtoepassing. De mailservers erachter gebruiken onderling nog steeds SMTP.

Een e-mailadres bestaat uit een gebruikersnaam en een domein, bijvoorbeeld `leerling@school.test`. De mailserver van de afzender moet weten welke server mail voor `school.test` ontvangt. Dat staat in DNS, in een {term}`MX-record`. Dat is iets anders dan het A-record van een website.

### Voorbeeld

Je stuurt mail naar `leerling@school.test`:

1. Je mailprogramma biedt het bericht met SMTP aan bij jouw mailserver.
2. Jouw mailserver vraagt DNS naar het MX-record van `school.test` en krijgt de naam van de mailserver van de school.
3. Jouw mailserver stuurt het bericht met SMTP naar die server.
4. De ontvanger haalt het bericht later op met IMAP of POP, of leest het via webmail.

::: {exercise} Zonder Filius: een e-mail volgen
:label: nw09-o1

1. Bewijst een browser die webmail toont dat alle mail tussen mailservers via HTTP reist?
2. Welk protocol hoort bij e-mail aanbieden en doorsturen: SMTP of {term}`ARP`?
3. Waarom bewijst een werkende website op `school.test` niet dat e-mail naar dat domein bezorgd kan worden?
4. Waarom heeft de mailserver van de afzender DNS nodig om de mail te kunnen bezorgen?
:::

::: {solution} nw09-o1
:class: dropdown

1. Nee. HTTP kan de webmailpagina in je browser verzorgen, terwijl mailservers onderling SMTP gebruiken.
2. SMTP. ARP lost een lokaal adresseringsprobleem op.
3. De webserver en de mailserver zijn verschillende diensten met eigen instellingen, en ook de DNS-records verschillen (A-record voor de website, MX-record voor de mail).
4. Hij moet via het MX-record weten welke server de mail voor het domein ontvangt en daarna het IP-adres van die server opzoeken.
:::

---

(netwerken-h10)=
# DHCP: automatisch instellen

## Inleiding

Tot nu toe stelde je IP-adressen, maskers en gateways met de hand in. Dat is onwerkbaar als er elke dag nieuwe apparaten bij komen, zoals telefoons en laptops. Met {term}`DHCP` krijgt een apparaat die instellingen automatisch van een server.

**Laag:** {term}`toepassingslaag`. **Vraag:** hoe krijgt een apparaat zonder instellingen toch een IP-adres, masker, gateway en DNS-server?

## DHCP: wie stelt al die adressen in?

Een {term}`client` die op een netwerk wordt aangesloten, kent nog geen netwerkgegevens. Hij zoekt een {term}`server` met vier berichten:

1. **Discover:** de client roept naar iedereen dat hij een configuratie zoekt.
2. **Offer:** een DHCP-server biedt een adres en andere instellingen aan.
3. **Request:** de client vraagt dat aanbod aan.
4. **Acknowledge:** de server bevestigt.

Behalve het {term}`IP-adres` kan de configuratie onder andere het {term}`masker <subnetmasker>`, de {term}`gateway` en DNS-serveradressen bevatten. Het adres wordt voor beperkte tijd uitgeleend: de {term}`lease`. Een DHCP-server is geen DNS-server, ook al kan één computer beide diensten uitvoeren.

De eerste berichten zijn broadcasts, want de client heeft nog geen adres en kent de server niet. {term}`Routers <router>` sturen broadcasts niet vanzelf door naar andere netwerken. In grotere netwerken kan een speciaal ingestelde DHCP-relay dat oplossen; dat stel je hier niet in.

::: {exercise} Zonder Filius: DHCP volgen
:label: nw10-o1

1. Waarom kan een nieuwe client zijn DHCP-vraag niet rechtstreeks aan één server richten?
2. Welke vier instellingen kan een client via DHCP krijgen?
3. Waarom bewijst een geslaagde DHCP-configuratie niet dat DNS en de webserver werken?
:::

::: {solution} nw10-o1
:class: dropdown

1. Hij heeft nog geen IP-adres en kent het adres van de server niet. Daarom begint hij met een broadcast.
2. IP-adres, subnetmasker, gateway en DNS-serveradres.
3. DHCP stelt alleen de netwerkinstellingen in. DNS en de webserver zijn aparte diensten.
:::

::: {exercise} Filius: automatische instellingen
:label: nw10-o2

1. Werk in een kopie van `08-website.fls`. Installeer op de DNS-server ook de DHCP-server, als jouw Filius-versie die heeft.
2. Kies voor het server-LAN een pool van `192.168.20.100` tot en met `192.168.20.120`, masker `255.255.255.0`, gateway `192.168.20.1` en DNS `192.168.20.53`. Houd vaste serveradressen buiten de pool.
3. Voeg één nieuwe client toe op dezelfde {term}`switch` en stel die in op automatische adresconfiguratie. Start de DHCP-server en vraag de configuratie aan.
4. Controleer de ontvangen instellingen en bezoek de oefenwebsite op naam. Wat heeft DHCP ingesteld en welke dienst levert nog steeds de pagina?
5. Bewaar als `10-dhcp.fls`.
:::

::: {solution} nw10-o2
:class: dropdown

De client krijgt een vrij adres uit de pool en de ingestelde extra gegevens. DHCP levert de netwerkconfiguratie, DNS de naamkoppeling en de webserver de pagina. Menunamen en opties kunnen per Filius-versie verschillen.
:::

---

(netwerken-h11)=
# NAT en firewall

## Inleiding

Thuis delen meerdere apparaten vaak één publiek IPv4-adres. Je wilt ook niet dat onbekenden van buiten zomaar een verbinding met je apparaten beginnen. Dat zijn twee verschillende problemen met twee verschillende oplossingen: adresvertaling met {term}`NAT` en filteren met een {term}`firewall`. Een oplossing voor één probleem lost het andere niet op.

**Lagen:** netwerk en transport. **Vraag:** hoe kunnen meerdere apparaten één publiek adres delen, en wie bepaalt welk verkeer binnenkomt?

## Klassikaal: één buitenadres voor meerdere clients

Maak drie rollen: twee interne {term}`clients <client>`, een grensrouter en een externe {term}`server`. Beide clients sturen een bericht naar dezelfde server. Op hun kaartjes staan een intern IP-adres en een {term}`bronpoort <poortnummer>`. De grensrouter heeft één buitenadres en een lijst met beschikbare buitenpoorten.

1. Laat beide berichten naar buiten gaan met hetzelfde buitenadres én dezelfde buitenpoort. Stuur de antwoorden van de server terug. De router kan niet bepalen voor welke client een antwoord is.
2. Laat de {term}`router` nu bij elke verbinding een eigen buitenpoort kiezen en de koppeling opschrijven. De antwoorden kunnen nu bij de juiste client komen.
3. Geef de router een regelkaart: ‘nieuwe verbindingen van buiten alleen naar de gepubliceerde webserver; antwoorden bij bestaande verbindingen wel doorlaten’. Laat de externe server een ongevraagd nieuw bericht sturen.

Bespreek welke beslissing over vertalen gaat en welke over toelaten.

## Private adressen

Voor intern gebruik zijn drie IPv4-reeksen gereserveerd:

| Reeks | Prefix |
| --- | --- |
| 10.0.0.0 tot 10.255.255.255 | 10.0.0.0/8 |
| 172.16.0.0 tot 172.31.255.255 | 172.16.0.0/12 |
| 192.168.0.0 tot 192.168.255.255 | 192.168.0.0/16 |

Organisaties mogen dezelfde {term}`private adressen <privaat IP-adres>` intern gebruiken. Die adressen zijn niet wereldwijd uniek en worden op het {term}`internet` niet doorgestuurd. Niet elk adres buiten deze reeksen is automatisch een bruikbaar {term}`publiek adres <publiek IP-adres>`: er zijn nog andere gereserveerde reeksen.

## NAT: adressen en poorten vertalen

Bij veel thuisnetwerken vervangt de router bij uitgaand verkeer het interne bronadres en meestal ook de bronpoort. Dat heet NAT; deze variant heet precies {term}`NAPT` of PAT. De router onthoudt welke koppeling bij welke verbinding hoort en vertaalt de antwoorden terug.

### Voorbeeld

De buitenadressen hieronder zijn documentatieadressen.

| Intern | Naar buiten vertaald | Server |
| --- | --- | --- |
| 192.168.10.10:51000 | 203.0.113.5:40001 | 198.51.100.20:443 |
| 192.168.10.20:51000 | 203.0.113.5:40002 | 198.51.100.20:443 |

Beide clients gebruiken dezelfde interne bronpoort, maar krijgen een andere buitenpoort. Een antwoord naar buitenpoort 40002 gaat terug naar de tweede client.

NAT vervangt {term}`routering` niet: na het vertalen moet het {term}`pakket <IP-pakket>` nog steeds worden doorgestuurd. NAT versleutelt ook niets. Onze Filius-netwerken gebruiken private adressen zonder NAT; in zo’n afgesloten netwerk is gewone routering genoeg.

::: {exercise} Zonder Filius: de vertaling volgen
:label: nw11-o1

1. Bij welke client hoort een antwoord naar `203.0.113.5:40001`?
2. Waarom zou de router buitenpoort 40001 niet ook voor de tweede verbinding naar dezelfde server gebruiken?
3. Is `172.40.2.8` een privaat adres? En `172.20.2.8`?
:::

::: {solution} nw11-o1
:class: dropdown

1. `192.168.10.10:51000`.
2. Dan zijn de twee verbindingen aan de buitenkant niet meer te onderscheiden. Elke verbinding krijgt daarom een eigen buitenpoort.
3. `172.40.2.8` niet; `172.20.2.8` wel. De private 172-reeks loopt van 172.16 tot en met 172.31.
:::

## Firewall: wel of niet toelaten?

Een firewall bepaalt aan de hand van regels welk verkeer wordt doorgelaten. De regels kunnen kijken naar bron en bestemming, {term}`protocol`, poorten en de toestand van een verbinding. Een stateful firewall herkent antwoorden bij een toegestane verbinding.

Een router stuurt door, NAT vertaalt en een firewall filtert. Die taken zitten vaak in één apparaat, maar het blijven verschillende beslissingen. Een firewall die {term}`TCP` naar poort 443 toestaat, beoordeelt daarmee niet of een website betrouwbaar is.

::: {exercise} Zonder Filius: de regels toepassen
:label: nw11-o2

Een stateful firewall past deze regels in volgorde toe: (1) antwoorden bij toegestane verbindingen toelaten; (2) interne clients nieuwe TCP-verbindingen naar externe poort 443 laten beginnen; (3) alle andere nieuwe verbindingen blokkeren.

1. Mag een interne browser een nieuwe verbinding naar externe poort 443 starten?
2. Mag het antwoord terug naar de tijdelijke clientpoort?
3. Mag een externe computer ongevraagd een nieuwe verbinding naar een interne client beginnen?
4. Versleutelt deze firewall het verkeer?
:::

::: {solution} nw11-o2
:class: dropdown

1. Ja, volgens regel 2.
2. Ja, omdat het bij de toegestane verbinding hoort (regel 1).
3. Nee, volgens regel 3.
4. Nee. Filteren en versleutelen zijn verschillende taken.
:::

::: {exercise} Filius: wat laat het model zien?
:label: nw11-o3

1. Open je HTTP-website uit hoofdstuk 8 en lees een verzoek of antwoord in de gegevensuitwisseling. Zoek je eigen paginatitel.
2. Waaraan zie je dat dit verkeer niet versleuteld is?
3. Welke van routering, NAT en firewall heb je in je eigen Filius-netwerk daadwerkelijk ingesteld en aangetoond?
:::

::: {solution} nw11-o3
:class: dropdown

Je hebt routering en een gewone HTTP-dienst ingesteld. De leesbare paginatitel in de HTTP-uitwisseling laat zien dat dit verkeer niet versleuteld is. Private adressen gebruiken is geen bewijs dat NAT actief is. In deze module stel je NAT en firewall niet in Filius in; je beoordeelt ze met de uitgewerkte modellen en regels.
:::

---

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

```{figure} ../images/inkapseling.svg
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

---

(netwerken-h13)=
# Praktische eindopdracht: ontwerp en bouw

Een kleine organisatie heeft een werkruimte, een serverruimte en een tweede vestiging. Jij ontwerpt de adressering en maakt de communicatie tussen de netwerken werkend in Filius.

Dit is de praktische beoordeling. Je werkt individueel, tenzij de docent anders aangeeft. Dit hoofdstuk beslaat les 15 en 16. Je levert een werkend netwerk én verklaringen in. Je hoeft niet tientallen computers te tekenen, maar je adresplan moet er wel ruimte voor bieden.

## De opdracht

```{figure} ../images/eindopdracht.svg
:alt: De topologie ligt vast; de passende LAN-maskers kies je zelf.

De topologie ligt vast; de passende maskers kies je zelf.
```

Maak drie {term}`LAN's <LAN>` en een verbindingsnetwerk tussen twee gewone {term}`routers <router>`. R1 verbindt de werkruimte, de serverruimte en het verbindingsnetwerk. R2 verbindt de tweede vestiging met het verbindingsnetwerk.

| Netwerk | Gewenste capaciteit, inclusief interfaces |
| --- | --- |
| Werkruimte | 45 werkplekken en één routeraansluiting |
| Serverruimte | Vier serveraansluitingen en één routeraansluiting |
| Tweede vestiging | Twaalf werkplekken en één routeraansluiting |
| Verbinding R1–R2 | Twee routeraansluitingen |

De beginadressen liggen vast: `192.168.40.0`, `192.168.50.0`, `192.168.60.0` en `10.0.0.0`, in de volgorde van de tabel. Kies voor elk LAN het kleinste gewone {term}`subnet` met genoeg adressen. Gebruik /30 voor de verbinding tussen de routers. Toon aan dat je gekozen grootte past.

Teken minimaal twee {term}`clients <client>` in de werkruimte, twee in de tweede vestiging en twee {term}`servers <server>` in de serverruimte. Eén server biedt {term}`DNS`, de andere {term}`HTTP`. De overige geplande aansluitingen hoef je niet te tekenen, maar ze moeten wel in je adresplan passen. Gebruik per LAN een {term}`switch`.

## Adresplan vóór het bouwen

Maak per subnet een tabel met prefix, decimaal {term}`masker <subnetmasker>`, {term}`netwerkadres`, {term}`broadcastadres`, bruikbare reeks en capaciteit. Maak ook een tabel met alle getekende aansluitingen en hun {term}`IP-adres`, masker, {term}`gateway` en, voor clients, het DNS-serveradres.

Noteer daarna de handmatige routes voor R1 en R2. Rechtstreeks aangesloten netwerken hoef je niet als route toe te voegen. Gebruik in deze opdracht geen automatische {term}`routering`, {term}`NAT`, {term}`DHCP` of Home Router.

::: {note} Controlehulp bij het adresplan
:class: dropdown

Tel routeraansluitingen mee, wijs geen netwerk- of broadcastadres toe aan een apparaat en kies elk {term}`next hop`-adres in het verbindingsnetwerk. De docent beoordeelt je eigen keuzes en berekeningen. De volledige voorbeeldconfiguratie staat in het docentmateriaal.
:::

## Diensten instellen

Maak op de DNS-server een record `www.project.test` dat naar je webserver wijst. Maak op de webserver een pagina met:

- de naam van je organisatie en je eigen naam;
- een korte uitleg van het verschil tussen een IP-adres en een {term}`MAC-adres`;
- een korte uitleg waarom verkeer tussen de vestigingen een router nodig heeft.

De pagina moet vanuit beide LAN’s op naam bereikbaar zijn. Je mag de standaardpagina van Filius aanpassen; een uitgebreid webontwerp is niet de bedoeling.

## Werking aantonen

Voer de tests uit en noteer per test de verwachte uitkomst, de werkelijke uitkomst en je bewijs. Bewijs kan een gerichte schermafbeelding zijn of overgenomen berichtvelden met uitleg.

| Test | Wat toon je aan? |
| --- | --- |
| Client naar tweede client in het eigen LAN | Lokale bereikbaarheid |
| Werkruimte naar tweede vestiging en terug | Routering in beide richtingen |
| Website op IP-adres vanuit beide LAN’s | Bereikbaarheid en webserver |
| Website op naam vanuit beide LAN’s | DNS plus webverkeer |
| Eerste verkeer buiten het eigen subnet volgen | {term}`ARP` voor de gateway en behoud van het bestemmings-IP-adres |

Een geslaagde ping bewijst niet dat DNS of HTTP werkt. Kies bewijs dat bij de vraag past. Bewaar je definitieve bestand als `achternaam-netwerken.fls`.

## Verklaringen bij je eigen netwerk

Beantwoord met de adressen die je zelf hebt gekozen:

1. Waarom zijn een netwerkfunctie en een {term}`protocol` niet hetzelfde? Geef twee voorbeelden uit je opstelling.
2. Welk Ethernetbestemmingsadres gebruikt een client in de werkruimte bij een bezoek aan de webserver? Welk IP-adres blijft de eindbestemming?
3. Welke handmatige routes zijn nodig voor het antwoord van de webserver aan een client in de tweede vestiging?
4. Welke rol spelen TCP-poorten bij het websitebezoek? Waarom gebruikt een ping geen TCP-poorten?
5. Waarom bewijst jouw HTTP-website geen HTTPS-beveiliging? Wat zou {term}`TLS` toevoegen?
6. Kun je op het publieke {term}`internet` dezelfde private bronadressen rechtstreeks blijven gebruiken? Beschrijf wat {term}`NAPT` in een gebruikelijke IPv4-aansluiting verandert en wat een {term}`firewall` apart beslist.

::: {note} Waar letten we bij de verklaringen op?
:class: dropdown

Gebruik je eigen netwerk als bewijs. ‘De router stuurt het door’ is te algemeen: noem de gekozen volgende stap en de adressen. TCP en HTTPS kun je niet volledig uit de simulatie aflezen. Leg daar de werking uit en geef aan wat het model niet laat zien.
:::

## Inleveren en demonstreren

Lever het Filius-bestand, het adres- en routeplan en je testverslag met verklaringen in. In les 16 rond je af en demonstreer je een communicatie die de docent kiest. Je legt uit hoe je die hebt gecontroleerd.

Open je opgeslagen bestand vooraf en controleer dat je diensten na het starten van de simulatie actief zijn. Houd je adresplan en testverslag bij de hand. De docent kiest een client en een bestemming uit jouw opstelling. Je toont de communicatie en verklaart de betrokken lagen. Voor extra servers of protocollen zijn geen punten te halen als de gevraagde werking en uitleg nog niet kloppen.

De docent kan bijvoorbeeld vragen:

- Waar komt het serveradres bij de naam vandaan?
- Naar welk IP-adres vraagt deze client met ARP, en waarom?
- Welke MAC-adressen veranderen bij deze router?
- Via welke tabelregel komt het antwoord terug?
- Welke taak blijft werken als je het lokale {term}`medium` vervangt?

Je hoeft geen vaste tekst op te zeggen. Gebruik je eigen adressen, routes en waarnemingen.

## Een storing onderzoeken

De docent wijzigt in een kopie van je netwerk één instelling uit een bekende categorie: een clientgateway, een DNS-adres of een handmatige route. Je krijgt de klacht te horen, niet de wijziging.

1. Noem op basis van de klacht twee mogelijke oorzaken.
2. Kies een controle waarmee je de mogelijkheden van elkaar onderscheidt.
3. Voer de controle uit en leg uit wat de uitkomst wel en niet aantoont.
4. Herstel de oorzaak en toon de bedoelde werking opnieuw aan.

Dit is een kort individueel onderdeel, geen nieuwe stof. Het gaat om een beredeneerde keuze uit bekende controles, niet om willekeurig instellingen veranderen of alles opnieuw bouwen. Bij een grote klas kan dit onderdeel tijdens het zelfstandig werken in les 15 en 16 worden afgenomen.

## Beoordeling

| Onderdeel | Punten | Waar letten we op? |
| --- | --- | --- |
| Adressering en subnetten | 20 | Passende capaciteit, juiste grenzen, geldige en consistente adressen |
| Topologie en routering | 20 | Gescheiden LAN’s, passende aansluitingen, next hops en heen- en terugroutes |
| DNS en HTTP | 15 | Juiste naamkoppeling, werkende webserver en bereikbaarheid vanuit beide LAN’s |
| Bewijs en testen | 15 | Gerichte tests met verwachting, uitkomst en bewijs |
| Begrip en verklaringen | 20 | Lagen, protocollen, ARP, adressen, TCP en beveiliging in samenhang |
| Zelfstandig onderzoeken | 10 | Controle met reden, uitleg van de uitkomst, herstel en hertest |
| **Totaal** | **100** | |

Bij een deels werkend netwerk verdien je punten voor de onderdelen die aantoonbaar kloppen. Een werkend bestand zonder verklaringen levert niet automatisch de punten voor begrip op. Zorg dat elke schermafbeelding een doel en een uitleg heeft en voeg geen complete lijst netwerkberichten toe zonder aan te geven welke regels het bewijs vormen.

De docent vertelt hoe punten naar een cijfer worden omgerekend en hoe lang de individuele demonstratie duurt.
