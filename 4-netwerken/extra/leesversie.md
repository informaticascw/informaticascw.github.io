# Computernetwerken — complete leesversie

Deze leesversie staat buiten de website-inhoudsopgave. De [begrippenlijst](../99-begrippenlijst.md) blijft één apart bronbestand. De MyST term-rollen worden vanuit het publicatieproject naar die lijst opgelost.

(netwerken-les01)=
# Bits versturen

## Inleiding

Je verstuurt een foto. De verbinding vervoert die foto niet als één herkenbaar plaatje, maar als signalen waaruit de ontvanger {term}`bits <bit>` moet afleiden. Daarvoor moeten zender en ontvanger dezelfde {term}`afspraken <afspraak>` gebruiken.

**Laag:** {term}`fysieke laag`. **Hoofdvraag:** hoe krijgt de ontvanger dezelfde reeks bits als de zender?

Je onderzoekt eerst hoe je een 0, een 1 en de grenzen ertussen herkenbaar maakt. Daarna vergelijk je overdrachtscapaciteit en {term}`vertraging`.

## Klassikaal: een bericht zonder woorden

Werk in teams van vier: een zender, ontvanger, tijdwaarnemer en controleur. De docent geeft alleen de zender een geheime reeks van acht bits. Tussen zender en ontvanger zit enkele meters afstand. Andere teams doen tegelijk mee.

In de eerste ronde mag de zender alleen een zaklamp of een omhooggehouden kaart gebruiken. Geen praten, schrijven of wijzen naar de bits. Spreek nog geen code af. De ontvanger schrijft op wat hij denkt te ontvangen.

Vergelijk de uitkomst. Spreek daarna een code, een startteken en een vast tempo af. Probeer een nieuwe reeks. Laat de ontvanger het bericht terugmelden, zodat de zender kan controleren of het klopt. Verhoog ten slotte het tempo totdat fouten optreden.

Bespreek welke afspraken het verschil maakten. De uitleg hieronder beschrijft deze ook zonder de oefening.

## Een bit is nog geen signaal

Een bit is een waarde: 0 of 1. Om die over te dragen heb je een fysiek verschijnsel nodig. Via koper kun je elektrische signalen gebruiken, via glasvezel licht en via {term}`wifi` radiogolven. Een zender zet bits om in signalen; de ontvanger leidt daar de bits weer uit af.

‘Licht aan is 1 en uit is 0’ lijkt voldoende. Maar is een lange periode licht één 1 of zijn het tien enen? Ontvangers hebben ook afspraken nodig over timing. Echte netwerkverbindingen gebruiken uitgebreidere coderingen dan dit eenvoudige voorbeeld.

Bij een {term}`protocol` spreken apparaten af hoe ze communiceren. De functie van de fysieke laag is het overdragen van bits. De concrete afspraken over signalen en timing vullen die {term}`functie` in.

### Voorbeeld

Je spreekt af: iedere seconde één bit, beginnen na twee korte flitsen. Vier seconden licht kan nu vier enen betekenen. Zonder de tijdafspraak blijft dat onduidelijk.

::: {exercise} Zonder Filius: ontbrekende afspraak
:label: nw01-o1

1. Een zender verstuurt `1001`. Waarom is alleen ‘aan is 1’ onvoldoende?
2. Noem twee afspraken die zender en ontvanger naast de bitbetekenis nodig hebben.
3. Waarom helpt harder of feller zenden niet altijd als berichten verkeerd worden begrepen?
:::

::: {solution} nw01-o1
:class: dropdown

1. Zonder timing weet de ontvanger niet waar de afzonderlijke bits beginnen en eindigen; ook het begin van het bericht moet herkenbaar zijn.
2. Bijvoorbeeld een startteken en een vaste bitduur.
3. Sterkte lost een ontbrekende code of tijdafspraak niet op; storing of te hoog tempo kan ook een rol spelen.
:::

## Snelheid en vertraging

De overdrachtssnelheid drukken we uit in {term}`bits per seconde`, bijvoorbeeld 100 Mbit/s. In deze module gebruiken we ‘{term}`bandbreedte`’ voor de beschikbare overdrachtscapaciteit. Eén {term}`byte` bestaat uit acht bits; MB en Mbit betekenen dus niet hetzelfde.

Vertraging is de tijd die overdracht en verwerking kosten. Een snelle verbinding kan toch een merkbare wachttijd hebben. Ook de route, afstand, wachtrijen en {term}`servers <server>` spelen mee. De langzaamste verbinding onderweg kan de doorvoer beperken.

### Voorbeeld

Een bestand van 20 MB bevat 160 Mbit, gerekend met decimale eenheden. Bij 40 Mbit/s duurt alleen het overbrengen theoretisch 4 seconden. Opstarttijd, protocolinformatie en ander verkeer zijn daarin niet meegerekend.

::: {exercise} Zonder Filius: sneller of eerder?
:label: nw01-o2

1. Bereken de minimale overdrachtstijd van 12 MB bij 24 Mbit/s.
2. Verbinding X heeft 1000 Mbit/s en 80 ms vertraging; Y heeft 100 Mbit/s en 10 ms. Welke is gunstiger voor heel korte interactieve berichten? Welke voor een groot bestand? Licht je aannames toe.
:::

::: {solution} nw01-o2
:class: dropdown

1. 12 × 8 / 24 = 4 seconden.
2. Voor korte berichten kan Y prettiger zijn door de lagere vertraging. Voor grote bestanden kan X meer doorvoer bieden. Dit geldt als de andere onderdelen van het pad en de server geen grotere beperking vormen.
:::

## In het echt en in Filius

Bekijk op je apparaat of je wifi of {term}`Ethernet` gebruikt. Bekijk een netwerkkabel en, als die beschikbaar is, een glasvezelaansluiting. Een kabel kan meerdere aders bevatten; één bit hoeft niet letterlijk één puls op één draad te zijn.

::: {exercise} Filius: je eerste verbinding
:label: nw01-o3

1. Maak in de ontwerpmodus twee computers en verbind ze met een kabel. Geef ze de namen A en B. Bewaar als `01-verbinding.fls`.
2. Klik een computer aan en zoek de instellingen voor {term}`IP-adres` en {term}`subnetmasker`. Je hoeft die nu nog niet te begrijpen of aan te passen.
3. Wijs aan welk onderdeel in je tekening de fysieke verbinding voorstelt.
4. Leg uit waarom de tekening nog niet bewijst dat A een webpagina van B kan ophalen.
:::

::: {solution} nw01-o3
:class: dropdown

De kabel stelt de fysieke verbinding voor. Een kabel alleen maakt nog geen werkende webdienst: ook adressering, protocolafspraken en de benodigde software moeten kloppen. Filius toont een model, geen echte elektrische of optische signalen.
:::


---

(netwerken-les02)=
# Een lokaal netwerk

## Inleiding

Twee computers kunnen met een kabel communiceren. Met twintig computers willen we niet voor ieder tweetal een eigen kabel aanleggen. We verbinden ze met een {term}`switch` en hebben dan adressen nodig om gericht te kunnen afleveren.

**Laag:** {term}`datalinklaag`. **Hoofdvraag:** hoe krijgt op een gedeeld lokaal netwerk het juiste apparaat het {term}`frame`?

Je leert welke informatie een frame bevat, hoe een switch uit verkeer leert en waarom sommige frames toch naar iedereen gaan.

## Klassikaal: de switch leert

Maak groepen van zes: vier apparaten, één switch en één waarnemer. Apparaten krijgen een unieke code; alleen de switch weet op welke genummerde ‘poort’ iedereen zit. Gebruik vier aparte stapeltjes papier als poorten. Een frame bevat broncode, bestemmingscode en bericht.

De switch begint met een lege tabel. Bij ieder frame schrijft hij broncode en binnenkomende poort op. Is de bestemming bekend, dan bezorgt hij alleen op die poort. Is de bestemming onbekend, dan maakt hij kopieën voor alle andere poorten. De bedoelde ontvanger antwoordt.

Laat eerst A naar B sturen, daarna B naar A en A opnieuw naar B. Laat vervolgens iemand een frame naar ‘iedereen’ sturen. De waarnemer telt per beurt de kopieën. Vergelijk waarom de eerste en latere beurten verschillen.

## Adressen op het lokale netwerk

De datalinklaag verpakt gegevens in frames. Een Ethernetframe bevat onder andere een bron-MAC-adres, een bestemmings-MAC-adres en de over te dragen gegevens. Aan het einde staat foutcontrole-informatie, de {term}`FCS` op basis van {term}`CRC`. Die kan veel overdrachtsfouten detecteren, maar herstelt de gegevens niet zelf.

Een {term}`MAC-adres` is een adres van een netwerkinterface, bijvoorbeeld `02:00:00:00:10:0a`. Een computer met twee interfaces kan verschillende MAC-adressen hebben. Apparaten kunnen ook aangepaste of private MAC-adressen gebruiken.

{term}`Unicast <unicast>` is gericht aan één ontvanger. Een Ethernetbroadcast gebruikt `ff:ff:ff:ff:ff:ff`: alle apparaten in het {term}`broadcastdomein` ontvangen het frame.

## Gericht doorsturen

Een switch verbindt aansluitingen. Hij leert uit het bronadres van binnenkomende frames welk MAC-adres via welke poort bereikbaar is. Bij een bekende bestemming stuurt hij gericht door. Bij een onbekende unicastbestemming verspreidt hij het frame over de andere geschikte poorten. Dat heet {term}`flooding`. Ook {term}`broadcasts <broadcast>` worden verspreid.

### Voorbeeld

A zit op poort 1 en B op poort 3. Zodra A een frame verstuurt, leert de switch ‘A via poort 1’. Zodra B antwoordt, leert hij ‘B via poort 3’. Voor een later frame van A naar B is poort 3 voldoende. De tabel is dus aangeleerd, niet vooraf een lijst van alle apparaten.

::: {exercise} Zonder Filius: vul de tabel
:label: nw02-o1

Een lege switch ontvangt achtereenvolgens A→B op poort 1, B→A op poort 3 en C→B op poort 2.

1. Geef na iedere ontvangst de geleerde tabel.
2. Over welke poorten wordt ieder frame verstuurd? De switch heeft vier poorten.
3. Wat verandert bij een broadcast van C?
:::

::: {solution} nw02-o1
:class: dropdown

1. Eerst A:1; daarna A:1 en B:3; ten slotte ook C:2.
2. A→B: poorten 2, 3 en 4. B→A: alleen 1. C→B: alleen 3.
3. De broadcast gaat via 1, 3 en 4 naar de andere aansluitingen, ook als alle gewone adressen bekend zijn.
:::

## Je lokale netwerk bouwen

In Filius gebruiken we alvast {term}`IP-adressen <IP-adres>` om met `ping` verkeer op te wekken. Het IP-adres is niet het adres waarop de switch zijn doorstuurkeuze baseert. Ping gebruikt {term}`ICMP`, geen {term}`TCP`; later onderscheiden we die {term}`protocollen <protocol>`.

::: {exercise} Filius: drie computers en een switch
:label: nw02-o2

1. Bouw A, B en D met één switch. Geef ze respectievelijk `192.168.10.10`, `.20` en `.30`, allemaal met {term}`masker <subnetmasker>` `255.255.255.0`. Laat de {term}`gateway` leeg.
2. Installeer in simulatiemodus de opdrachtregel op A en ping B.
3. Open de gegevensuitwisseling van A en B. Zoek bron- en bestemmingsadressen. Maak onderscheid tussen de velden met MAC-adressen en die met IP-adressen.
4. Bewaar als `02-lokaal.fls`. Noteer wat je in de simulatie wél kunt waarnemen en welke switchwerking je daarmee nog niet direct hebt aangetoond.
:::

::: {solution} nw02-o2
:class: dropdown

Een succesvolle ping laat communicatie tussen A en B zien. In de uitwisseling kun je de gebruikte adresvelden onderzoeken. Dat is op zichzelf geen bewijs van het volledige leerproces van een fysieke switch: Filius is een vereenvoudigd model. De theorie over leertabellen is daarom ook met de klassikale oefening en de papieren opdracht uitgewerkt.
:::

## In het echt: een apparaat met veel aansluitingen

Zoek in het lokaal een zichtbare wandcontactdoos voor {term}`Ethernet` of bekijk met de docent een beschikbare losse switch. Volg alleen zichtbare kabels: een wandcontactdoos is zelf geen switch. Een draadloos accesspoint koppelt wifi-apparaten aan het lokale netwerk; een thuisapparaat kan accesspoint, switch en {term}`router` in één behuizing combineren.

::: {exercise} Eigen omgeving: functie of behuizing?
:label: nw02-o3

1. Een thuisapparaat heeft vier LAN-poorten en {term}`wifi`. Waarom is ‘dit apparaat is alleen een router’ onvolledig?
2. Waarom bewijzen knipperende lampjes niet dat een website bereikbaar is?
:::

::: {solution} nw02-o3
:class: dropdown

1. De behuizing kan meerdere {term}`functies <functie>` bevatten: switch, accesspoint en router. Het aantal behuizingen is niet het aantal netwerkfuncties.
2. Lampjes kunnen een verbinding of verkeer aangeven, maar zeggen nog niet of adressering, {term}`routering`, {term}`DNS` en de webdienst werken.
:::


---

(netwerken-lagen)=
# Lagen en inkapseling

## Inleiding

Een {term}`Ethernetframe <frame>` brengt gegevens naar een volgende ontvanger op het lokale netwerk. Maar het bericht moet ook de juiste eindcomputer én het juiste programma bereiken. Soms liggen daar verschillende netwerken tussen. Eén soort adres lost al die vragen niet op.

We verdelen de communicatie daarom in {term}`functies <functie>`. Iedere laag gebruikt de dienst van de laag eronder. Je krijgt in dit hoofdstuk het overzicht; de afzonderlijke {term}`protocollen <protocol>` werk je daarna uit. Je hoeft hun details hier nog niet te kennen.

**Hoofdvraag:** hoe kunnen verschillende {term}`afspraken <afspraak>` samen één bericht bezorgen?

## Welke vraag hoort bij welke laag?

We gebruiken een internetmodel met vijf lagen. Een laag is geen aparte kast: één computer voert functies uit meerdere lagen uit.

| Laag | De vraag die deze laag oplost | Wat wordt toegevoegd of uitgevoerd? |
| --- | --- | --- |
| {term}`Toepassingslaag <toepassingslaag>` | Wat vraagt of levert het programma? | Een toepassingsbericht, bijvoorbeeld een verzoek om een webpagina |
| {term}`Transportlaag <transportlaag>` | Bij welke toepassing of verbinding horen de gegevens? Welke overdrachtsdienst is nodig? | Onder andere {term}`poortnummers <poortnummer>`; {term}`TCP` kan ook volgorde en hertransmissie verzorgen |
| {term}`Netwerklaag <netwerklaag>` | Naar welk eindapparaat moet het bericht over de gekoppelde netwerken? | Onder andere bron- en bestemmings-IP-adres |
| {term}`Datalinklaag <datalinklaag>` | Naar welke volgende ontvanger op deze lokale verbinding? | Onder andere bron- en bestemmings-MAC-adres bij {term}`Ethernet` |
| {term}`Fysieke laag <fysieke laag>` | Hoe dragen we de {term}`bits <bit>` over het {term}`medium`? | Signalen op koper, glasvezel of radio |

Een protocol is een verzameling concrete communicatieafspraken. {term}`IP` is bijvoorbeeld een protocol voor de netwerklaag. De functie is breder: die zegt welk probleem we oplossen, niet precies welke velden en berichten we gebruiken. {term}`HTTP` is een toepassingsprotocol voor webverkeer. TCP en {term}`UDP` zijn transportprotocollen. Hun werking komt later.

Dezelfde functie kan met verschillende protocollen of technieken worden ingevuld. Een browser kan webverkeer gebruiken via zowel een bekabelde als een draadloze aansluiting. De afspraak ‘vraag deze pagina op’ hoeft niet te veranderen alleen omdat het lokale medium verandert.

## Een bericht krijgt laag voor laag extra informatie

Een ontvangend apparaat moet kunnen herkennen wat het krijgt en voor wie het bedoeld is. De afzender voegt daarom bij iedere relevante laag besturingsinformatie toe, vaak als {term}`header` vóór de bestaande gegevens. Dat noemen we {term}`inkapseling` of encapsulation.

We volgen één klein HTTP-bericht dat boven TCP via IPv4 en Ethernet wordt verstuurd:

1. De toepassing maakt gegevens: bijvoorbeeld een verzoek om `/rooster.html`.
2. TCP voegt een TCP-header toe, onder andere met poort- en volgorde-informatie. Dit geheel heet een {term}`TCP-segment`.
3. IP behandelt dat segment als inhoud en voegt een IP-header toe. Dit geheel heet een {term}`IP-pakket`.
4. Ethernet behandelt het IP-pakket als inhoud en voegt een Ethernetheader én foutcontrole aan het einde toe. Dit geheel heet een frame. Het stukje achteraan heet een {term}`trailer`; de {term}`Ethernet-FCS <FCS>` bevat de foutcontrole.
5. De fysieke laag zet de bits van het frame om in signalen. Dit is geen extra papieren omslag met weer een nieuw adres.

```{figure} ../images/inkapseling.svg
:alt: Een Ethernetframe bevat een IP-pakket; dat bevat een TCP-segment met de toepassingsgegevens. De Ethernetheader en trailer staan buiten het IP-pakket.

Bij dit voorbeeld zit het segment in het pakket en het pakket in het frame. Iedere header hoort bij zijn eigen laag.
```

De inhoud van een laag heet ook wel de {term}`payload`. Voor Ethernet is dat in dit voorbeeld het hele IP-pakket, niet alleen de tekst van de webpagina. Eén toepassingbericht kan over meerdere TCP-segmenten verdeeld worden; de tekening toont bewust één klein stuk en geen algemene één-op-éénverhouding.

## Wat doet de ontvanger?

De ontvanger werkt in de omgekeerde richting. De netwerkinterface haalt bits uit signalen. De datalinklaag controleert het frame, verwerkt zijn eigen informatie en geeft de inhoud door aan de netwerklaag. IP verwerkt de IP-header en geeft de inhoud door aan TCP. TCP verwerkt zijn eigen informatie, voegt waar nodig ontvangen {term}`bytes <byte>` samen en levert de gegevens af bij de toepassing.

Dit heet {term}`ontkapseling`. Het is dus niet zo dat het ene apparaat alle headers tegelijk gebruikt voor één beslissing: iedere functie verwerkt de bijbehorende informatie.

::: {exercise} Zonder Filius: wat zit waarin?
:label: nw03-laag-o1

1. Orden van buiten naar binnen: toepassingsgegevens, Ethernetframe, TCP-segment en IP-pakket.
2. Hoort een bestemmings-MAC-adres bij dezelfde header als een bestemmings-IP-adres?
3. Een IP-pakket is 100 bytes groot. Er komt voor dit rekenvoorbeeld 18 bytes Ethernetheader en -trailer bij. Hoe groot is dit frame, zonder verdere fysieke overhead? Wordt het IP-pakket zelf hierdoor 118 bytes?
:::

::: {solution} nw03-laag-o1
:class: dropdown

1. Ethernetframe → IP-pakket → TCP-segment → toepassingsgegevens.
2. Nee. Het {term}`MAC-adres` hoort bij Ethernetinformatie en het {term}`IP-adres` bij IP-informatie. De ene header zit buiten de andere.
3. Het frame is 118 bytes. Het ingesloten IP-pakket blijft 100 bytes. De 18 bytes zijn informatie van de buitenste verpakking in dit vereenvoudigde voorbeeld.
:::

## En als er een router tussen zit?

Een {term}`router` ontvangt een lokaal frame, verwerkt die datalinkverpakking en bekijkt het IP-pakket. Hij bepaalt de volgende verbinding en maakt daarvoor een nieuw lokaal frame. Op een Ethernetverbinding krijgt dat frame de MAC-adressen voor die volgende stap. De router hoeft daarvoor niet de webpagina te begrijpen.

De IP-eindadressen blijven bij gewone {term}`routering` zonder {term}`NAT` gelijk. Het pakket is niet letterlijk byte voor byte onveranderd: bijvoorbeeld de IP-levensduur wordt aangepast. Die details zijn hier niet nodig voor het verschil tussen de twee soorten adressen.

Een {term}`switch` maakt zijn gewone Ethernetkeuze op basis van MAC-informatie. Een router maakt zijn doorstuurkeuze op basis van IP-informatie. Dat zijn verschillende vragen, ook als de functies in één behuizing zitten.

## Klassikaal: bouw samen de verpakkingen

Maak groepen van negen: vier zenderrollen, vier ontvangerrollen en één routerrol. Aan beide kanten zijn de rollen toepassing, transport, netwerk en datalink. De docent geeft iedere rol alleen de velden die die rol moet invullen. De toepassingsrol weet de boodschap; de netwerkrol kent het IP-eindadres; de datalinkrol kent de MAC-ontvanger voor het eerste kabelstuk.

Bouw met gevouwen kaarten een bericht: transportinformatie om toepassingsgegevens, IP-informatie om dat segment en een frame om dat pakket. Geef het geheel door. De ontvangers mogen ieder alleen hun eigen verpakking verwerken; alleen de toepassingsrol leest de tekst. Laat daarna de routerrol tussenbeide komen. Die verwijdert de lokale frameverpakking en maakt met andere MAC-adressen een nieuwe, zonder de toepassingsboodschap te openen.

Leg de oude en nieuwe buitenverpakking naast elkaar. Benoem wat veranderde en wat in de binnenste gegevens bleef staan. De fysieke overdracht van bits en echte foutcontrole worden hier niet nagespeeld.

::: {exercise} In het echt en in Filius: vind twee lagen
:label: nw03-laag-o2

1. Open de gegevensuitwisseling bij een ping tussen je twee bestaande Filius-computers. Zoek, voor zover jouw versie dit toont, Ethernet- en IPv4-velden in hetzelfde verzonden bericht. Noteer één MAC-adres en één IP-adres en benoem hun functie.
2. Als het venster de velden niet genest weergeeft, betekent dat dan dat er in een echt Ethernetframe geen IP-pakket kan zitten?
3. Waarom mag je bij deze ping niet automatisch een TCP-segment tekenen?
:::

::: {solution} nw03-laag-o2
:class: dropdown

1. Het MAC-adres hoort bij lokale aflevering; het IP-adres bij een IP-bron of -bestemming. De concrete waarden komen uit je eigen netwerk.
2. Nee. De weergave van een simulatie is niet de verpakking zelf. Gebruik de figuur om het verschil tussen de laagvelden te tekenen.
3. Ping gebruikt {term}`ICMP`, geen TCP. De uitlegfiguur laat één specifiek HTTP/TCP-voorbeeld zien, niet de inhoud van ieder IP-pakket.
:::


---

(netwerken-les04)=
# IP-netwerken en subnetten

## Inleiding

Een {term}`switch` houdt veel verkeer lokaal gericht. Toch moet ieder apparaat in het {term}`broadcastdomein` een {term}`broadcast` ontvangen. Hoe houden we dat beheersbaar als het netwerk groeit?

We onderzoeken eerst waarom je een lokaal netwerk zou splitsen. Daarna geven we ieder deel een eigen {term}`IP-subnet <subnet>` en rekenen we uit welke adressen daarin passen. Het herkennen van een lokaal of niet-lokaal adres is nodig om later een volgende ontvanger te kiezen.

**Laag:** {term}`netwerklaag`, met een grens aan de {term}`datalinklaag`. **Hoofdvraag:** hoe delen we het netwerk op in afzonderlijke delen die ieder een passende adresruimte hebben?

Je leert de netwerkgrens herkennen, netwerk- en broadcastadressen berekenen en een passend {term}`subnetmasker` kiezen. Dit hoofdstuk beslaat delen van twee lessen; de hoofdstukken zijn geen verplichte lesgrenzen.

## Klassikaal: eerst drukte, dan een grens

De docent geeft iedereen een kaart met een zichtbaar {term}`MAC-adres` en een verborgen {term}`IP-adres`. De helft heeft een uniek adres `192.168.10.…`, de andere helft `192.168.20.…`. Eén leerling observeert en wordt later {term}`router`. Je hoeft de maskers hieronder nog niet te kunnen berekenen: dat leer je na de oefening.

**Ronde 1 — één netwerk.** De hele klas is één netwerk met masker `255.255.0.0`. Enkele afzenders proberen tegelijk een klasgenoot op IP-adres te vinden. Zij vragen aan de hele klas: ‘Wie heeft …?’ Alleen de eigenaar antwoordt met zijn MAC-adres. De afzender bezorgt daarna een kort bericht. De waarnemer telt hoeveel mensen elke zoekvraag moeten aanhoren, ook als die niet voor hen is.

**Ronde 2 — twee gescheiden netwerken.** Vorm twee fysiek gescheiden groepen op basis van `192.168.10.…` en `192.168.20.…`. Beide krijgen masker `255.255.255.0`. Zoekvragen én bezorging mogen alleen binnen je eigen groep. Gebruik hetzelfde aantal afzenders en vergelijkbare lokale zoekvragen. Minder mensen hoeven iedere vraag te verwerken. Laat daarna iemand een bericht voor de andere groep bezorgen: dat mag nu niet.

**Ronde 3 — een verbinding tussen de groepen.** De routerleerling krijgt voor iedere groep een eigen adreskaart (`192.168.10.1` en `192.168.20.1`) en een eigen MAC-adres. Alleen die leerling mag tussen de groepen bemiddelen. Een afzender voor de andere groep zoekt de router in zijn eigen groep en geeft hem het bericht voor de eindontvanger. De router zoekt die ontvanger alleen in de andere groep en bezorgt het daar. Laat een antwoord terugsturen.

Bespreek samen: wat werd rustiger na het splitsen, welke mogelijkheid verdween en wat bracht de router terug? Wordt een zoekvraag van links in ronde 3 automatisch door iedereen rechts gehoord?

Het door elkaar praten maakt de gedeelde belasting voelbaar; echte {term}`wifi` gebruikt {term}`afspraken <afspraak>` voor kanaaltoegang. We vergelijken hier hoeveel apparaten een broadcast moeten verwerken, niet of de oefening gegarandeerd sneller verloopt. Alleen een ander subnetmasker instellen verdeelt één bestaand Ethernet- of wifinetwerk nog niet in twee broadcastdomeinen: de scheiding van de lokale netwerken hoort er ook bij.

## Waarom een lokaal netwerk begrenzen?

Een broadcastdomein is het deel van het netwerk waar een gewone lokale broadcast wordt verspreid. In onze voorbeelden vormen met elkaar verbonden gewone switches één broadcastdomein. Meer switches toevoegen maakt daarvan niet vanzelf verschillende domeinen.

Broadcast is nuttig: een apparaat kan iets vragen zonder het adres van de ontvanger al te kennen. Maar ieder ontvangen broadcastframe vraagt capaciteit en verwerking. Eén groot lokaal netwerk met steeds meer apparaten is daarom niet onbeperkt een goede oplossing.

### Voorbeeld

Vier switches verbinden samen 80 computers. Eén computer verstuurt een broadcast. Die wordt over de verbonden switches verspreid naar de overige geschikte aansluitingen. Het helpt niet om alleen een extra switch tussen twee bestaande switches te zetten: de broadcast blijft door die verbinding heen gaan.

::: {exercise} Zonder Filius: waar komt de broadcast?
:label: nw03-o1

Je hebt switch S1 verbonden met S2. A en B zitten op S1; C en D op S2.

1. Wie ontvangt een broadcast van A?
2. S2 wordt vervangen door twee achter elkaar gekoppelde switches. Beperkt dat de broadcast? Leg uit.
3. Welke kosten heeft een broadcast ook voor een apparaat dat geen antwoord geeft?
:::

::: {solution} nw03-o1
:class: dropdown

1. B, C en D, binnen deze eenvoudige opstelling.
2. Nee. De gewone switches verspreiden de broadcast verder.
3. Het {term}`frame` gebruikt capaciteit op relevante verbindingen en moet door ontvangende interfaces verwerkt worden, ook als geen antwoord volgt.
:::

## Hoe beschrijven we de afzonderlijke netwerken?

Een router verbindt verschillende IP-netwerken. Hij stuurt gewone Ethernetbroadcasts niet door zoals een switch dat doet. Apparaten aan de ene kant kunnen dus niet met een lokale broadcast alle apparaten aan de andere kant aanspreken.

Daarmee ontstaat een nieuwe vraag: hoe geven we aan in welk netwerk een bestemming ligt? Een IP-adres krijgt daarvoor een {term}`netwerkdeel` en een {term}`apparaatdeel`. Het subnetmasker bepaalt waar de grens ligt. Hieronder rekenen we uit waar die grens ligt.

De netwerklaag zorgt voor adressering en doorsturen tussen netwerken. {term}`IP` is een {term}`protocol` dat die {term}`functie` invult. {term}`Ethernet` blijft nodig voor afleveren op iedere afzonderlijke lokale verbinding.

### Voorbeeld

Links gebruiken we `192.168.10.…`, rechts `192.168.20.…`, beide met masker `255.255.255.0`. Een router heeft links adres `192.168.10.1` en rechts `192.168.20.1`. Een routeraansluiting hoort bij het netwerk waaraan die is verbonden.


## Vier keer acht bits

Een IPv4-adres heeft 32 {term}`bits <bit>`. We schrijven het als vier decimale getallen, bijvoorbeeld `192.168.10.37`. Ieder getal is een {term}`octet` van acht bits en ligt tussen 0 en 255.

In een octet hebben de bits van links naar rechts de waarden 128, 64, 32, 16, 8, 4, 2 en 1. Voor een decimaal getal tel je de waarden op waar een 1 staat. Zo is `01001101` gelijk aan 64 + 8 + 4 + 1 = 77. Bij `11111111` is de som 255.

Een subnetmasker heeft eerst aaneengesloten enen en daarna nullen. De enen wijzen de netwerkbits aan. `/24` betekent 24 enen: `255.255.255.0`. De laatste acht bits blijven beschikbaar voor adressen binnen het subnet.

Het {term}`netwerkadres` krijg je door de apparaatbits op 0 te zetten. Het {term}`broadcastadres` heeft alle apparaatbits op 1. In de gewone subnetten van deze module reserveren we beide: ze worden niet aan computers toegewezen.

### Voorbeeld: /24

`192.168.10.37/24` heeft netwerkadres `192.168.10.0`, broadcast `192.168.10.255` en bruikbare adressen `.1` tot en met `.254`. Voor een routerinterface gebruik je ook een bruikbaar adres. De gateway is niet automatisch `.1`; dat is een gekozen conventie.

## Een grens midden in een octet

Bij `/26` zijn zes bits beschikbaar voor het apparaatdeel. Er zijn 2⁶ = 64 adressen per blok, waarvan 62 bruikbaar. Het laatste maskeroctet is binair `11000000`, dus 192. Het masker wordt `255.255.255.192`.

In een /24-gebied liggen /26-blokken op `.0`, `.64`, `.128` en `.192`. Adres `.77` valt in blok `.64` tot en met `.127`.

| Onderdeel van 192.168.10.77/26 | Waarde |
| --- | --- |
| Netwerk | 192.168.10.64 |
| Broadcast | 192.168.10.127 |
| Bruikbaar | 192.168.10.65–192.168.10.126 |
| Aantal bruikbaar | 62 |

Bij een bitgewijze AND is de uitkomst alleen 1 als beide ingevoerde bits 1 zijn. Het masker bewaart zo de netwerkbits en zet de apparaatbits op 0. Je kunt het netwerkadres daarmee bit voor bit berekenen: `01001101` (77) AND `11000000` (192) wordt `01000000` (64). Broadcast ontstaat door de resterende zes bits op 1 te zetten.

### Van prefix naar masker en blok

Bij een prefix /n blijven `32 − n` apparaatbits over. Neem twee tot die macht voor het aantal adressen per blok. Bij de onderstaande prefixen liggen alle apparaatbits in het laatste octet:

| Prefix | Masker | Adressen per blok | Bruikbare adressen |
| --- | --- | --- | --- |
| /24 | 255.255.255.0 | 256 | 254 |
| /25 | 255.255.255.128 | 128 | 126 |
| /26 | 255.255.255.192 | 64 | 62 |
| /27 | 255.255.255.224 | 32 | 30 |
| /28 | 255.255.255.240 | 16 | 14 |
| /30 | 255.255.255.252 | 4 | 2 |

De blokken beginnen steeds op een veelvoud van de blokgrootte. Kies het blok waarin het adres valt; het eerste adres is het netwerkadres, het laatste is het broadcastadres. De overige adressen zijn in deze gewone LAN-voorbeelden bruikbaar.

::: {exercise} Zonder Filius: adressen berekenen
:label: nw04-o1

Bepaal voor ieder adres netwerkadres, broadcastadres, bruikbare reeks en aantal bruikbare adressen:

1. `192.168.20.145/27`.
2. `10.4.2.200/25`.
3. Kan `192.168.20.159/27` een computeradres zijn? Licht toe.
:::

::: {solution} nw04-o1
:class: dropdown

1. Masker `255.255.255.224`, blokgrootte 32: netwerk `.128`, broadcast `.159`, bruikbaar `.129–.158`, aantal 30.
2. Masker `255.255.255.128`: netwerk `10.4.2.128`, broadcast `10.4.2.255`, bruikbaar `.129–.254`, aantal 126.
3. Nee, dit is het broadcastadres van het subnet `.128/27`.
:::

## Hoe groot moet het subnet zijn?

Kies het kleinste aantal apparaatbits h waarvoor `2^h − 2` voldoende is. Reken alle benodigde interfaces mee: computers, {term}`servers <server>` én de routeraansluiting. In deze les behandelen we gewone LAN-subnetten, niet de bijzondere /31- en /32-toepassingen.

### Voorbeeld

Je hebt 26 computers, twee servers en één routerinterface: 29 adressen. Vijf apparaatbits geven 30 bruikbare adressen. `/27` past; `/28` met 14 bruikbare adressen is te klein. Met extra groeiruimte kan een groter subnet een betere ontwerpkeuze zijn.

::: {exercise} Zonder Filius: passend kiezen
:label: nw04-o2

1. Kies het kleinste subnet voor 45 computers, één server en één routerinterface. Geef prefix, masker en capaciteit.
2. Doe hetzelfde voor twaalf computers en één routerinterface.
3. In situatie 2 komen drie computers erbij. Welke consequentie heeft dat voor je eerdere keuze?
:::

::: {solution} nw04-o2
:class: dropdown

1. 47 adressen: /26, masker `255.255.255.192`, 62 bruikbaar.
2. 13 adressen: /28, masker `255.255.255.240`, 14 bruikbaar.
3. Nu zijn 16 adressen nodig; /28 is te klein. /27 biedt 30. Dit laat zien waarom je groei vooraf kunt meerekenen.
:::

### Dezelfde verbinding is niet altijd hetzelfde IP-subnet

Bereken met het masker van de afzender zowel het eigen netwerkadres als het netwerkadres van de bestemming. Zijn die gelijk, dan beschouwt de afzender de bestemming als lokaal. Zijn ze verschillend, dan heeft de afzender voor die bestemming een passende route nodig, meestal via de standaardgateway. Het volgende hoofdstuk werkt die aflevering uit.

Voorbeeld: `192.168.10.65/26` en `192.168.10.100/26` geven allebei netwerkadres `.64`. Adres `.130` geeft met hetzelfde masker netwerkadres `.128`. Dat laatste adres is voor de eerste afzender dus niet lokaal, ook als de apparaten aan dezelfde switch hangen.

::: {exercise} Filius: hetzelfde subnet of niet?
:label: nw04-o3

1. Maak twee computers op één switch: A `192.168.10.65/26` en B `192.168.10.100/26`. Vul in Filius het decimale masker in. Geen gateways.
2. Voorspel en test een ping van A naar B.
3. Geef B adres `192.168.10.130/26`. Voorspel en test opnieuw. Leg uit waarom alleen ‘ze zitten op dezelfde switch’ nu onvoldoende is.
4. Herstel het adres van B en bewaar als `04-subnetproef.fls`.
:::

::: {solution} nw04-o3
:class: dropdown

Eerst liggen beide adressen in subnet `.64/26` en kunnen ze rechtstreeks communiceren. Daarna ligt B in `.128/26`. A behandelt B dan niet als lokale IP-bestemming. Zonder geschikte router en route werkt de ping niet. De switch scheidt hiermee niet ineens broadcasts: de IP-keuze en de Ethernetstructuur zijn verschillende zaken.
:::

## In het echt

De netwerkdetails van je computer tonen een masker of prefix. Dat kan op school anders zijn dan thuis. Een adres dat begint met `10.` betekent niet dat het masker automatisch /8 is. Het ingestelde masker bepaalt de grens. In het hoofdstuk over {term}`ARP` zoek je deze gegevens zelf op.


---


(netwerken-arp-gateway)=
# ARP en de standaardgateway

## Inleiding

Je weet nu of twee {term}`IP-adressen <IP-adres>` in hetzelfde {term}`subnet` liggen. Je weet ook dat een {term}`Ethernetframe <frame>` een {term}`MAC-adres` als bestemming heeft. Daarmee ontbreekt nog één stap: een programma geeft een IP-bestemming op, maar de netwerkinterface moet een frame met een lokaal MAC-adres versturen.

**Hoofdvraag:** welk lokaal MAC-adres is nodig bij deze IP-bestemming, en hoe vindt de afzender dat adres?

We kiezen eerst de volgende ontvanger: het eindapparaat in het eigen subnet of de {term}`gateway` voor een ander subnet. Daarna gebruiken we {term}`ARP` om bij dat lokale IP-adres het MAC-adres te vinden. In de volgende voorbeelden zie je waarom het IP-eindadres en het lokale frameadres niet altijd naar hetzelfde apparaat wijzen.

## Rechtstreeks of via de gateway?

```{figure} ../images/twee-lans.svg
:alt: Twee lokale Ethernetnetwerken met ieder een eigen switch en een router ertussen.

Twee lokale Ethernetnetwerken met ieder een eigen switch en een router ertussen.
```

We gebruiken twee afzonderlijke Ethernetnetwerken. Ieder netwerk heeft een eigen {term}`switch`. Een {term}`router` verbindt de netwerken. De router heeft voor ieder netwerk een eigen netwerkaansluiting, met een eigen IP-adres en MAC-adres.

| Apparaat | Aansluiting | IP-adres | {term}`Subnetmasker <subnetmasker>` | Standaardgateway |
| --- | --- | --- | --- | --- |
| Computer A | Linker netwerk | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| Computer B | Linker netwerk | 192.168.10.20 | 255.255.255.0 | 192.168.10.1 |
| Router | Linker netwerk | 192.168.10.1 | 255.255.255.0 | — |
| Router | Rechter netwerk | 192.168.20.1 | 255.255.255.0 | — |
| Computer C | Rechter netwerk | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |

Computer A wil gegevens versturen. Eerst bepaalt A met zijn eigen subnetmasker of de bestemming in zijn eigen subnet ligt.

- **Binnen het eigen subnet:** A verstuurt rechtstreeks naar het apparaat.
- **Buiten het eigen subnet:** A verstuurt naar een router die de gegevens verder kan sturen. In dit netwerk gebruikt A daarvoor de standaardgateway.

De standaardgateway is dus het IP-adres van een routeraansluiting in het eigen subnet. We gebruiken in dit hoofdstuk geen extra routes op de computers.

### Voorbeeld: van A naar B

A heeft {term}`netwerkadres` `192.168.10.0`. Met het subnetmasker van A levert het adres van B hetzelfde netwerkadres op. A kan B rechtstreeks bereiken: de router is daarvoor niet nodig.

### Voorbeeld: van A naar C

Het adres van C levert met het subnetmasker van A netwerkadres `192.168.20.0` op. Dat is een ander subnet. A levert de gegevens daarom af bij gateway `192.168.10.1`.

::: {exercise} Zonder Filius: welke volgende stap?
:label: netwerken-arp-o1

Ga uit van de instellingen van computer A in de tabel.

1. Bepaal voor iedere bestemming of A rechtstreeks verstuurt of de gateway gebruikt: `192.168.10.50`, `192.168.20.10` en `192.168.11.10`.
2. Waarom kan A niet `192.168.20.1` als standaardgateway gebruiken in deze opstelling?
3. Een leerling zegt: ‘De eerste twee getallen van het IP-adres zijn gelijk, dus de computers zitten in hetzelfde subnet.’ Leg met een bestemming uit vraag 1 uit waarom dat hier niet klopt.
:::

::: {solution} netwerken-arp-o1
:class: dropdown

1. `192.168.10.50`: rechtstreeks; de twee andere bestemmingen: via `192.168.10.1`.
2. De gateway moet rechtstreeks bereikbaar zijn in het eigen subnet. `192.168.20.1` zit in deze opstelling op het andere Ethernetnetwerk.
3. Bijvoorbeeld `192.168.11.10`: de eerste twee getallen zijn gelijk, maar bij masker `255.255.255.0` hoort ook het derde getal bij het {term}`netwerkdeel`.
:::

::: {exercise} Filius: bouwen en voorspellen
:label: netwerken-arp-o2

1. Bouw de opstelling uit de tabel: A en B op de linker switch, C op de rechter switch en een router tussen de switches. Gebruik een gewone router met twee aansluitingen.
2. Stel de IP-adressen en subnetmaskers in. Laat de standaardgateway op de computers voorlopig leeg. Gebruik geen automatische adresuitgifte.
3. Voorspel of A met `ping` B en C kan bereiken. Schrijf bij beide een reden op.
4. Start de simulatie. Installeer op A de opdrachtregel en test `ping 192.168.10.20` en `ping 192.168.20.10`.
5. Vergelijk je waarnemingen met je voorspellingen.
6. Stel op A, B en C de gateways uit de tabel in. Test opnieuw. Verklaar wat er verandert.

Bewaar je netwerk. Je gebruikt het in de volgende opdrachten opnieuw.
:::

::: {solution} netwerken-arp-o2
:class: dropdown

Zonder gateway kan A B bereiken. C niet. Met juiste gateways kan de heenweg én terugweg tussen A en C worden afgelegd. De router kent beide netwerken via zijn eigen aansluitingen. Een gewone switch heeft voor dit werk geen IP-configuratie nodig.
:::

## Welk MAC-adres hoort bij dit IP-adres?

A weet nu dat B rechtstreeks bereikbaar is. Maar in een Ethernetframe moet een MAC-adres staan. A heeft het IP-adres van B; hoe vindt A het bijbehorende MAC-adres?

A kent zijn eigen MAC-adres al via zijn netwerkinterface. Wat ontbreekt is het MAC-adres van de volgende ontvanger. Daarvoor gebruikt A ARP, het Address Resolution Protocol.

1. A kijkt in zijn {term}`ARP-cache`: een tijdelijk bijgehouden tabel met IP-adressen en bijbehorende MAC-adressen.
2. Staat B er nog niet in? Dan verstuurt A een {term}`ARP-request`: ‘Wie heeft IP-adres 192.168.10.20? Geef je MAC-adres door aan 192.168.10.10.’
3. Dit request zit in een Ethernetframe met {term}`broadcastadres` `ff:ff:ff:ff:ff:ff`. De switch verspreidt het over de andere aansluitingen van het lokale netwerk.
4. B herkent zijn eigen IP-adres en stuurt een {term}`ARP-reply` rechtstreeks naar A, met daarin zijn MAC-adres.
5. A bewaart de koppeling tijdelijk en kan nu het {term}`IP-pakket` in een Ethernetframe naar B versturen.

Andere apparaten ontvangen het broadcastrequest ook, maar geven in deze opstelling geen antwoord op een vraag naar het IP-adres van B. De router stuurt dit ARP-broadcastrequest niet door naar het rechter netwerk.

::: {note} ARP en de lagen

{term}`IP` lost adressering tussen netwerken op. {term}`Ethernet` regelt de aflevering op het lokale netwerk. ARP verbindt die twee: voor een lokaal IP-adres zoekt het het bijbehorende MAC-adres. Een ARP-bericht zit rechtstreeks in een Ethernetframe, niet in een IP-pakket.
:::

### Voorbeeld: de adressen in een lokaal bericht

Voor de voorbeelden gebruiken we onderstaande MAC-adressen. De adressen die Filius toekent, kunnen anders zijn.

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
:label: netwerken-arp-o3

De ARP-cache van A is leeg. A wil een IP-pakket naar B versturen.

1. Schrijf de vraag uit het ARP-request op.
2. Geef het bron- en bestemmings-MAC-adres van het Ethernetframe met dat request.
3. Welke apparaten ontvangen het request: B, de linker routeraansluiting en/of C?
4. Wie antwoordt? Is dat antwoord een {term}`broadcast`? Licht toe.
5. Waarom is niet voor ieder volgend IP-pakket opnieuw een broadcast nodig?
:::

::: {solution} netwerken-arp-o3
:class: dropdown

1. Wie heeft `192.168.10.20`? Meld je bij `192.168.10.10`.
2. Bron `02:00:00:00:10:0a`; bestemming `ff:ff:ff:ff:ff:ff`.
3. B en de linker routeraansluiting ontvangen het request. C niet.
4. B antwoordt rechtstreeks aan het MAC-adres van A: {term}`unicast`.
5. A bewaart de koppeling tijdelijk in de ARP-cache.
:::

::: {exercise} Filius: ARP waarnemen
:label: netwerken-arp-o4

1. Begin met een nieuwe simulatiestart. Open bij A het venster met de gegevensuitwisseling. Dit venster kun je via het contextmenu van de computer openen; de precieze naam kan per taalversie verschillen.
2. Ping B en zoek in de gegevensuitwisseling naar ARP. Onderzoek zo nodig de eerste uitwisseling na het opnieuw starten van de simulatie.
3. Noteer uit het request het gezochte IP-adres en het bestemmings-MAC-adres. Noteer uit het reply het gevonden MAC-adres.
4. Ping B direct opnieuw. Vergelijk de nieuwe berichten met de eerste uitwisseling. Is er opnieuw ARP nodig? Onderbouw je antwoord met wat je ziet.
5. Leg uit waarom ‘bij iedere ping wordt altijd eerst een ARP-request verstuurd’ geen goede regel is.
:::

::: {solution} netwerken-arp-o4
:class: dropdown

Het request vraagt naar B en gebruikt het Ethernetbroadcastadres. Het reply vermeldt het MAC-adres van B. Bij onmiddellijke herhaling is normaal geen nieuwe ARP-uitwisseling nodig, omdat de koppeling nog bekend is. Vergelijk deze verklaring met de berichten die je zelf hebt vastgelegd.
:::

### In het echt: de adressen van jouw computer

Dezelfde soorten adressen die je in Filius gebruikt, staan ook ingesteld op je eigen computer. Zoek de gegevens van de verbinding waarmee je nu verbonden bent. Een computer kan meerdere netwerkadapters hebben, bijvoorbeeld voor {term}`wifi` en Ethernet.

::: {exercise} Eigen apparaat: vind je IP-adres, MAC-adres en gateway
:label: netwerken-arp-echt

1. Open de netwerkgegevens met de aanwijzingen hieronder.
2. Noteer van je actieve verbinding het IPv4-adres, subnetmasker (of {term}`prefixlengte <CIDR-prefix>`), MAC-adres en de standaardgateway. Die laatste kan ook ‘router’ heten.
3. Bepaal met het masker of je gateway in jouw eigen subnet ligt. Schrijf je berekening op. `/24` betekent bijvoorbeeld `255.255.255.0`; ga niet zonder controle van `/24` uit.
4. Vergelijk met een klasgenoot: hebben jullie hetzelfde IP-adres, MAC-adres en gateway? Wat verwacht je als jullie in hetzelfde subnet zitten?
5. Leg uit welke van de gevonden adressen jouw computer met ARP zou proberen te bereiken als je een website buiten het eigen subnet bezoekt en die koppeling nog niet bekend is.

**Chromebook:** open Instellingen → Netwerk → Wifi en selecteer je verbonden netwerk. Zoek de netwerkdetails; onder ‘Netwerk’ staan doorgaans de IP-configuratie en gateway. Zoek ook het wifi-MAC-adres in de details. Via het netwerkmenu rechtsonder en het informatiepictogram kun je ook IP- en MAC-gegevens bekijken. Op een beheerd apparaat kunnen sommige details verborgen zijn.

**Windows:** open de Opdrachtprompt en voer `ipconfig /all` uit. Zoek bij de actieve wifi- of Ethernetadapter naar IPv4-adres, subnetmasker, standaardgateway en fysiek adres. ‘Fysiek adres’ is hier het MAC-adres. Sla adapters over waarbij staat dat de verbinding is verbroken.

**Mac:** open Systeeminstellingen → Netwerk → de actieve verbinding → Details. Kijk bij {term}`TCP`/IP voor IPv4-adres, subnetmasker en router. Zoek bij Hardware of in de wifi-details naar het MAC-adres van de verbinding.

Verander geen instellingen. Kun je de gegevens niet bekijken, gebruik dan het demonstratievoorbeeld hieronder en vergelijk dat met een apparaat waarop de gegevens wel zichtbaar zijn.

**Demonstratievoorbeeld — geen screenshot of meting van het schoolnetwerk:**

```text
IPv4-adres        192.168.10.37
Subnetmasker      255.255.255.0
Standaardgateway  192.168.10.1
MAC-adres         02:00:00:00:10:25
```
:::

::: {solution} netwerken-arp-echt
:class: dropdown

Je eigen waarden hangen af van je verbinding. In het demonstratievoorbeeld leveren zowel `192.168.10.37` als gateway `192.168.10.1` met het masker netwerkadres `192.168.10.0` op. De gateway ligt dus in hetzelfde subnet.

Twee klasgenoten in hetzelfde subnet horen verschillende IPv4-adressen te hebben en normaal ook verschillende MAC-adressen. Ze gebruiken vaak dezelfde gateway. Dezelfde wifinaam bewijst op zichzelf niet dat jullie in hetzelfde subnet zitten.

Voor een website buiten het eigen subnet zoekt de computer met ARP het MAC-adres bij het IPv4-adres van de gateway, niet bij het IP-adres van de website. Het MAC-adres dat je apparaat gebruikt kan voor een wifinetwerk een privaat of willekeurig gekozen adres zijn. Noteer het adres van de actieve verbinding; beschouw een MAC-adres niet als een onveranderlijk serienummer van de hele computer.
:::

## Het eindadres en de volgende ontvanger

A wil nu een IP-pakket naar C sturen. C ligt buiten het eigen subnet. A moet het pakket daarom eerst afleveren bij zijn gateway.

**A zoekt met ARP het MAC-adres van de gateway op, niet het MAC-adres van C.** De gateway ligt immers op hetzelfde Ethernetnetwerk als A. C niet.

Het IP-pakket blijft gericht aan C. Alleen het Ethernetframe wordt gericht aan de router.

### Voorbeeld: van A via de router naar C

| Verbinding | Bron-MAC | Bestemmings-MAC | Bron-IP | Bestemmings-IP |
| --- | --- | --- | --- | --- |
| A naar router | A | Router links | 192.168.10.10 | 192.168.20.10 |
| Router naar C | Router rechts | C | 192.168.10.10 | 192.168.20.10 |

De router ontvangt het frame en haalt het IP-pakket eruit. Hij bepaalt via welke aansluiting de bestemming bereikbaar is. Op het rechter netwerk maakt hij een nieuw Ethernetframe. Als hij het MAC-adres van C nog niet kent, gebruikt hij daar eerst zelf ARP.

De bron- en bestemmings-IP-adressen blijven in dit voorbeeld gelijk. Er wordt geen {term}`NAT` gebruikt. Het Ethernetframe wordt voor de volgende verbinding vervangen; het IP-pakket gaat verder naar zijn eindbestemming.

::: {exercise} Zonder Filius: volg het antwoord
:label: netwerken-arp-o5

C stuurt een antwoord terug naar A. Ga ervan uit dat de benodigde ARP-koppelingen bekend zijn.

1. Maak voor de terugweg dezelfde tabel als in het voorbeeld. Gebruik de namen uit de MAC-adressentabel.
2. Een leerling zegt: ‘A zet het IP-adres van de gateway als bestemming in het IP-pakket, want daar moet het pakket eerst naartoe.’ Verbeter deze uitleg.
3. Naar welk IP-adres vraagt A met ARP voordat hij naar C kan versturen? Waarom vraagt A niet naar het IP-adres van C?
:::

::: {solution} netwerken-arp-o5
:class: dropdown

| Verbinding | Bron-MAC | Bestemmings-MAC | Bron-IP | Bestemmings-IP |
| --- | --- | --- | --- | --- |
| C naar router | C | Router rechts | 192.168.20.10 | 192.168.10.10 |
| Router naar A | Router links | A | 192.168.20.10 | 192.168.10.10 |

Het bestemmings-IP-adres blijft dat van de eindbestemming. Het bestemmings-MAC-adres is dat van de volgende ontvanger op het lokale netwerk. A vraagt met ARP naar `192.168.10.1`; C ligt buiten zijn lokale netwerk en ontvangt het ARP-request van A niet.
:::

::: {exercise} Filius: twee soorten adressen
:label: netwerken-arp-o6

1. Begin opnieuw met een nieuwe simulatiestart en open de gegevensuitwisseling bij A en de router.
2. Ping vanaf A naar C.
3. Zoek het ARP-request van A. Wordt gevraagd naar het adres van C of naar het adres van de gateway?
4. Zoek het IP-pakket dat A naar C stuurt. Noteer het bestemmings-IP-adres en het bestemmings-MAC-adres van het frame waarin het zit.
5. Bekijk hoe de router het pakket naar C verstuurt. Welke adressen veranderen? Welke blijven gelijk?
6. Gebruik je waarnemingen om uit te leggen waarom een IP-adres en een MAC-adres allebei nodig zijn.
:::

::: {solution} netwerken-arp-o6
:class: dropdown

A vraagt naar `192.168.10.1`. Het IP-pakket gaat naar `192.168.20.10`, in een frame naar de linker routeraansluiting. Op de volgende verbinding veranderen beide MAC-adressen; bron- en bestemmings-IP blijven gelijk. De router kan op het rechter netwerk zelf ARP gebruiken om C te vinden. Niet iedere herhaling hoeft nieuwe ARP-berichten op te leveren.
:::


---

(netwerken-les06)=
# Door meerdere netwerken

## Inleiding

Je computer kan een {term}`pakket <IP-pakket>` buiten het eigen {term}`subnet` aan de {term}`gateway` geven. Daarmee is de route nog niet compleet: ook die {term}`router` moet een volgende stap kiezen. We breiden ons netwerk uit met een tweede router en een derde lokaal netwerk.

**Laag:** {term}`netwerklaag`. **Hoofdvraag:** hoe kiest iedere router een bereikbare volgende stap voor het bestemmingsnetwerk?

Je leest en vult handmatige {term}`routeringstabellen <routeringstabel>`. Daarna controleer je niet alleen de heenweg, maar ook de terugweg.

## Klassikaal: iedere tussenpersoon kent alleen de volgende stap

Verdeel de klas over drie netwerken en twee routers. Geef iedere router alleen een lokale routetabel, geen volledige plattegrond. Leerlingen versturen kaartjes met een bestemmingsnetwerk. Iedere router moet een volgende stap kiezen en mag geen informatie bij de andere router opvragen.

Laat eerst een bericht van links naar rechts gaan terwijl de eerste router geen route naar rechts heeft. Het bericht blijft liggen. Voeg de ontbrekende route toe. Laat de ontvanger nu antwoorden terwijl de tweede router nog geen route terug heeft. Voeg die ook toe. Pas dan komt het antwoord aan.

Bespreek waarom één succesvolle heenweg nog geen geslaagd gesprek is. Gebruik voor de kaarten de netwerken en routes uit de tabellen hieronder.

## Een tabel met bestemmingsnetwerken

Een router zoekt het bestemmings-IP-adres op in zijn routeringstabel. Een regel bevat een bestemmingsnetwerk, een {term}`masker <subnetmasker>` en informatie over de volgende stap: rechtstreeks via een aansluiting of via een andere router, de {term}`next hop`.

De next hop moet rechtstreeks bereikbaar zijn. Een router stuurt niet zomaar naar een willekeurig verre router waarvan hij alleen het adres kent.

### Onze opstelling

```{figure} ../images/routering.svg
:alt: De drie LANs en het aparte verbindingsnetwerk tussen R1 en R2.

De drie LANs en het aparte verbindingsnetwerk tussen R1 en R2.
```

We breiden de router uit les 5 uit met een tweede router en een derde {term}`LAN`. Er zijn vier subnetten; het verbindingsnetwerk tussen de routers is er ook één.

| Netwerk | Aansluitingen |
| --- | --- |
| Links: 192.168.10.0/24 | A `.10`; R1 `.1` |
| Midden: 192.168.20.0/24 | C `.10`; R1 `.1` |
| Tussen routers: 10.0.0.0/30 | R1 `10.0.0.1`; R2 `10.0.0.2` |
| Rechts: 192.168.30.0/24 | D `.10`; R2 `.1` |

R1 heeft drie interfaces nodig. R2 heeft er twee. A gebruikt gateway `192.168.10.1`, C `192.168.20.1` en D `192.168.30.1`.

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

Rechtstreeks aangesloten netwerken zijn normaal vanuit de interfaceconfiguratie bekend; je hoeft daarvoor niet dezelfde handmatige next-hopregels toe te voegen.

::: {exercise} Zonder Filius: volg de route
:label: nw06-o1

1. A verstuurt naar D. Geef achtereenvolgens de volgende ontvangers vanaf A.
2. Welk bron- en bestemmings-IP-adres staan in het pakket tussen R1 en R2? Er is geen {term}`NAT`.
3. Welke handmatige regel heeft R2 nodig voor het antwoord aan A?
4. Waarom kan R1 voor netwerk `192.168.30.0/24` niet simpelweg D als next hop invullen?
:::

::: {solution} nw06-o1
:class: dropdown

1. Eerst R1, dan R2, dan D.
2. Bron `192.168.10.10`, bestemming `192.168.30.10`.
3. `192.168.10.0/24` via `10.0.0.1`.
4. D ligt niet op een rechtstreeks verbonden subnet van R1. R1 moet eerst een lokaal bereikbare volgende router aanspreken.
:::

## Specifiek of standaard?

Een router kan een {term}`standaardroute` hebben: `0.0.0.0/0`. Die wordt gebruikt als geen specifiekere route past. Passen meerdere regels, dan wint de meest specifieke: de langste passende prefix. Een /24 beschrijft minder adressen en is specifieker dan een /16.

Routers kunnen routes automatisch uitwisselen met routeringsprotocollen. In deze module stellen we enkele routes handmatig in. We behandelen de interne werking van zulke routeringsprotocollen niet.

::: {exercise} Zonder Filius: welke regel wint?
:label: nw06-o2

Een router heeft `10.0.0.0/8 via X`, `10.2.0.0/16 via Y` en `0.0.0.0/0 via Z`.

Bepaal de volgende stap voor `10.2.8.4`, `10.3.8.4` en `203.0.113.8`.
:::

::: {solution} nw06-o2
:class: dropdown

`10.2.8.4` via Y: /16 is het specifiekst. `10.3.8.4` via X: /8 past en /16 niet. `203.0.113.8` via Z: alleen de standaardroute past. De letters stellen hier rechtstreeks bereikbare next hops voor.
:::

::: {exercise} Filius: voeg een router toe
:label: nw06-o3

1. Open een kopie van je netwerk uit les 5. Bouw de uitbreiding uit de tabellen. Gebruik voor het verbindingsnetwerk masker `255.255.255.252`.
2. Schakel automatische {term}`routering` uit op de routers, als die aanstaat. Open de tabel voor handmatige routes.
3. Voeg eerst alleen op R1 de route naar `192.168.30.0` met masker `255.255.255.0` via `10.0.0.2` toe. Test A→D. Bekijk of het verzoek D kan bereiken en waarom een antwoord nog kan ontbreken.
4. Voeg op R2 de twee ontbrekende routes naar links en midden toe. Test A↔D en C↔D.
5. Bewaar als `06-routering.fls`. Noteer je ingestelde regels en leg van één ping heen- en terugweg uit.
:::

::: {solution} nw06-o3
:class: dropdown

Alleen de route op R1 geeft R2 nog geen route naar A. Na toevoegen van beide terugroutes kan het verkeer in beide richtingen door de opstelling. De interfaces en gateways moeten eveneens correct zijn. Noteer bij de handmatige regels de next-hopadressen van het verbindingsnetwerk, niet de LAN-adressen aan de verre kant.
:::

## In het echt: een route is geen rechte kabel

Op Windows kun je `tracert stanislas.informatica.nu` gebruiken, op een Mac in Terminal `traceroute stanislas.informatica.nu`. Op school kunnen deze opdrachten beperkt zijn; de docent kan ook een eigen resultaat laten zien. Je hoeft dit niet te installeren op een Chromebook.

De opdrachten proberen tussenliggende routers zichtbaar te maken met berichten waarvan de levensduur stapsgewijs toeneemt. Een sterretje is geen bewijs van een kapotte route: een router kan wel doorsturen maar niet op de meetberichten antwoorden. De heen- en terugroute kunnen bovendien verschillen. De wachttijd bij één hop is niet simpelweg de tijd van alleen dat kabelstuk.


---

(netwerken-les07)=
# Het juiste programma bereiken

## Inleiding

Een {term}`IP-adres` brengt gegevens bij een apparaat. Op dat apparaat kunnen tegelijk een browser, chat en spel actief zijn. Bovendien kunnen onderweg gegevens ontbreken of in een andere volgorde aankomen.

**Laag:** {term}`transportlaag`. **Hoofdvraag:** welke dienst is nodig om de gegevens bij de juiste toepassing af te leveren?

We lossen eerst het onderscheid tussen programma's en verbindingen op met poorten. Daarna bekijken we welke extra dienst {term}`TCP` biedt en wat {term}`UDP` daarvan juist niet zelf regelt.

## Klassikaal: een boodschap met ontbrekende delen

Werk met drie teams: zender, netwerk en ontvanger. De ontvanger heeft twee postvakken met de nummers 80 en 5000. De zender krijgt een tekst in zes genummerde delen, allemaal voor hetzelfde postvak. Het netwerkteam houdt één deel achter, verwisselt twee delen en bezorgt één deel dubbel. De ontvanger mag niet zien wat het netwerkteam achterhoudt.

Probeer eerst zonder terugmeldingen de tekst samen te stellen. Spreek daarna af dat de ontvanger meldt welk deel als volgende ontbreekt; de zender bewaart kopieën en stuurt zo nodig opnieuw. Kan de ontvanger nu de juiste tekst precies eenmaal in het juiste vak leggen?

Dit model gebruikt genummerde tekstdelen. TCP nummert in werkelijkheid {term}`bytes <byte>` en gebruikt uitgebreidere {term}`afspraken <afspraak>`. De oefening illustreert volgorde, ontbrekende gegevens, bevestigingen en het juiste ontvangende programma.

## Een adres voor het programma

Een transportbericht bevat een bron- en {term}`bestemmingspoort <poortnummer>`. Een poortnummer is hier geen fysieke aansluiting. Het helpt het besturingssysteem gegevens bij de juiste toepassing of verbinding af te leveren.

Een webserver luistert bij gewone {term}`HTTP` meestal op TCP-poort 80; {term}`HTTPS` gebruikt vaak TCP-poort 443. Een {term}`client` kiest doorgaans een tijdelijke bronpoort. Een TCP-verbinding is te onderscheiden aan beide IP-adressen en beide poortnummers.

### Voorbeeld

Client `192.168.10.10:51000` verbindt met {term}`server` `192.168.20.10:80`. Een tweede verbinding kan bronpoort `51001` gebruiken. Antwoorden gaan terug van serverpoort 80 naar de bijbehorende clientpoort. TCP en UDP hebben afzonderlijke poortnummer-ruimtes.

::: {exercise} Zonder Filius: naar welk programma?
:label: nw07-o1

1. Vul bron- en bestemmingspoort in voor het antwoord op de verbinding met clientpoort 51000.
2. Twee clients gebruiken allebei bronpoort 51000 naar dezelfde serverpoort. Waarom hoeven hun verbindingen niet door elkaar te raken?
3. Waarom is een TCP-poort iets anders dan poort 3 op een {term}`switch`?
:::

::: {solution} nw07-o1
:class: dropdown

1. Bronpoort 80, bestemmingspoort 51000.
2. Hun client-IP-adressen verschillen; beide IP-adressen en poorten onderscheiden de verbindingen.
3. De switchpoort is een aansluiting. De TCP-poort is een getal in transportinformatie waarmee software verbindingen en toepassingen onderscheidt.
:::

## Wat voegt TCP toe?

{term}`IP` biedt op zichzelf geen garantie dat ieder {term}`pakket <IP-pakket>` aankomt of dat pakketten op volgorde aankomen. TCP biedt een betrouwbare geordende {term}`bytestroom` tussen toepassingen. Het verdeelt gegevens in {term}`segmenten <TCP-segment>`, houdt volgnummers bij, verwerkt bevestigingen en verzendt ontbrekende gegevens opnieuw. Dubbele gegevens worden niet dubbel aan de toepassing afgegeven.

### Voorbeeld: een ontbrekend stuk

Stel dat de ontvanger bytes 1–4 en 9–12 heeft, maar 5–8 nog ontbreken. Hij kan de volledige reeks 1–12 nog niet op volgorde aan de toepassing geven. Met bevestigingen en volgnummers kan de zender vaststellen dat gegevens ontbreken en die opnieuw versturen, bijvoorbeeld na een wachttijd. Daarna levert TCP de bytes in de juiste volgorde af. Een dubbel ontvangen stuk wordt niet nogmaals als nieuwe inhoud afgegeven.

De nummers zijn hier vereenvoudigd; je hoeft geen echte {term}`TCP-header <header>` uit je hoofd te leren. Het belangrijke onderscheid is dat IP losse pakketten bezorgt, terwijl TCP daar voor de toepassing een geordende stroom van maakt.

Vooraf wordt een verbinding opgebouwd, herkenbaar aan SYN, SYN-ACK en ACK. Daarna kunnen gegevens stromen. TCP past de hoeveelheid uitstaand verkeer aan de ontvanger en de netwerksituatie aan. We rekenen niet aan die regelalgoritmen.

Betrouwbaar betekent niet dat iedere verbinding altijd slaagt. Als een kabel blijvend wegvalt, kan ook TCP de tekst niet bezorgen. De toepassing krijgt uiteindelijk een fout of merkt dat de verbinding stopt. TCP versleutelt gegevens niet automatisch.

## Wanneer UDP?

UDP verstuurt afzonderlijke datagrammen met poortinformatie, zonder zelf verbinding op te bouwen, ontvangst te bevestigen of de volgorde te herstellen. Een toepassing kan zulke {term}`functies <functie>` alsnog toevoegen. Bij live geluid kan een te laat opnieuw verstuurd stukje minder bruikbaar zijn dan het overslaan ervan.

| Vraag | TCP | UDP |
| --- | --- | --- |
| Verbinding vooraf | Ja | Niet door UDP zelf |
| Betrouwbare geordende stroom | Door TCP verzorgd | Niet door UDP verzorgd |
| Grenzen van toepassingbericht behouden | Nee, bytestroom | Ja, datagrammen |
| Versleuteling vanzelf | Nee | Nee |

HTTP/3 gebruikt QUIC boven UDP, met eigen betrouwbaarheid en beveiliging. Daarom is ‘websites gebruiken altijd TCP’ te absoluut. Onze Filius-voorbeelden gebruiken HTTP boven TCP.

::: {exercise} Zonder Filius: kies en onderbouw
:label: nw07-o2

1. Waarom is het belangrijk dat een download geen ontbrekende bytes bevat?
2. Waarom kan wachten op een oud geluidfragment vervelend zijn bij een live gesprek?
3. Iemand beweert: ‘UDP kan nooit betrouwbare communicatie opleveren.’ Verbeter die uitspraak.
:::

::: {solution} nw07-o2
:class: dropdown

1. Ontbrekende bytes kunnen het bestand onbruikbaar maken. Een betrouwbare overdracht moet de juiste bytes compleet afleveren.
2. Het wachten verhoogt de {term}`vertraging`; het gesprek is inmiddels verdergegaan.
3. UDP zelf biedt die dienst niet. Een {term}`protocol` of toepassing boven UDP kan betrouwbaarheid toevoegen.
:::

::: {exercise} Filius: TCP herkennen
:label: nw07-o3

1. Gebruik een computer als server op je bestaande netwerk. Installeer en start daar de webserver. Installeer op A een webbrowser.
2. Open de gegevensuitwisseling en bezoek vanaf A `http://192.168.20.10` als C je server is.
3. Zoek de opbouw van een TCP-verbinding en noteer de gebruikte poorten. Welke kant begon?
4. Vergelijk met een ping naar hetzelfde adres: zie je daar dezelfde TCP-opbouw? Bewaar als `07-transport.fls`.
:::

::: {solution} nw07-o3
:class: dropdown

De browser is de client en begint de verbinding. De HTTP-server gebruikt normaal TCP-poort 80; de client heeft een tijdelijke bronpoort. Bij een nieuwe verbinding zijn de TCP-opbouwberichten zichtbaar. Een ping gebruikt {term}`ICMP` en heeft geen TCP-handshake. Een reeds bestaande verbinding kan opnieuw gebruikt worden; start de simulatie opnieuw als je juist de eerste verbinding wilt onderzoeken.
:::

## In het echt: meerdere verbindingen

Bekijk in de browserontwikkeltools het tabblad Netwerk tijdens het laden van een pagina. Zoek, als beschikbaar, het externe adres en de protocolkolom. `h2` en `h3` verwijzen naar HTTP-versies, niet naar de fysieke aansluiting. Eén pagina kan veel verzoeken naar meerdere servers veroorzaken. De server kan meerdere verzoeken over één bestaande verbinding afhandelen.


---

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


---

(netwerken-les09)=
# Verbinden en beschermen

## Inleiding

Meerdere apparaten thuis delen vaak één publiek {term}`IPv4-adres <IP-adres>`. Tegelijk wil je niet dat iedere onbekende van buiten zomaar een verbinding naar je apparaten begint, of dat iemand onderweg de inhoud leest. Dat zijn drie verschillende problemen.

**Lagen:** netwerk, transport en toepassing. We behandelen daarom achtereenvolgens adresvertaling met {term}`NAT`, toelaten of blokkeren met een {term}`firewall` en bescherming van de inhoud met {term}`TLS` bij {term}`HTTPS`. Een werkende oplossing voor één probleem lost de andere twee niet vanzelf op.

## Klassikaal: één buitenadres voor meerdere bezoekers

Maak drie rollen: twee interne {term}`clients <client>`, een grensrouter en een externe {term}`server`. Clients krijgen allebei een bericht voor dezelfde server. Hun kaartjes hebben een intern IP-adres en {term}`bronpoort <poortnummer>`. De grensrouter heeft één buitenadres en een tabel met beschikbare buitenpoorten.

Laat eerst beide berichten naar buiten gaan onder precies hetzelfde buitenadres én dezelfde buitenpoort. Stuur het serverantwoord terug. De grensrouter kan nu niet bepalen welke client bedoeld is. Laat de {term}`router` vervolgens voor elke verbinding een eigen buitenpoort kiezen en de koppeling opschrijven. De antwoorden kunnen nu gericht terug.

Geef de router daarna een regelkaart: ‘nieuwe verbindingen van buiten alleen naar de gepubliceerde webdienst; antwoorden bij bestaande verbindingen wel toelaten’. Laat de externe server een ongevraagd nieuw bericht sturen. Bespreek welke beslissing over vertalen gaat en welke over toelaten.

## Private adressen

Voor intern gebruik zijn drie IPv4-reeksen gereserveerd:

| Reeks | Prefix |
| --- | --- |
| 10.0.0.0 tot 10.255.255.255 | 10.0.0.0/8 |
| 172.16.0.0 tot 172.31.255.255 | 172.16.0.0/12 |
| 192.168.0.0 tot 192.168.255.255 | 192.168.0.0/16 |

Verschillende organisaties mogen dezelfde {term}`private adressen <privaat IP-adres>` intern gebruiken. Die adressen zijn niet wereldwijd uniek en worden niet als gewone publieke bestemmingen over {term}`internet` gerouteerd. Niet ieder adres buiten deze drie reeksen is automatisch een bruikbaar publiek adres: er zijn ook andere bijzondere reeksen.

## NAT: adressen en poorten vertalen

Bij veel thuisnetwerken vertaalt de router bij uitgaand IPv4-verkeer het interne bronadres en meestal ook de bronpoort. We spreken vaak algemeen van NAT; deze variant heet ook {term}`NAPT` of PAT. De router onthoudt welke koppeling bij welke verbinding hoort en vertaalt de antwoorden terug.

### Voorbeeld — buitenadressen hieronder zijn documentatieadressen

| Intern | Naar buiten vertaald | Server |
| --- | --- | --- |
| 192.168.10.10:51000 | 203.0.113.5:40001 | 198.51.100.20:443 |
| 192.168.10.20:51000 | 203.0.113.5:40002 | 198.51.100.20:443 |

Beide clients kunnen dezelfde interne bronpoort gebruiken, maar krijgen hier verschillende buitenpoorten. Een antwoord naar buitenpoort 40002 wordt terugvertaald naar de tweede client.

NAT vervangt geen {term}`routering`: na het vertalen moet het {term}`pakket <IP-pakket>` nog steeds worden doorgestuurd. Ook is NAT geen versleuteling. Onze eerdere Filius-netwerken gebruiken private adressen zonder NAT: binnen die gesloten simulatie kan gewone routering voldoende zijn.

::: {exercise} Zonder Filius: volg de vertaling
:label: nw09-o1

1. Bij welke client hoort een antwoord naar `203.0.113.5:40001`?
2. Waarom zou dezelfde tabel buitenpoort 40001 niet ook voor de tweede verbinding naar dezelfde server moeten gebruiken?
3. Is `172.40.2.8` een RFC 1918-adres? En `172.20.2.8`?
:::

::: {solution} nw09-o1
:class: dropdown

1. `192.168.10.10:51000`.
2. De twee verbindingen zouden aan de buitenkant niet meer onderscheiden worden. In dit voorbeeld krijgt iedere verbinding een aparte buitenpoort.
3. `172.40.2.8` niet; `172.20.2.8` wel. De private 172-reeks loopt van 172.16 tot en met 172.31.
:::

## Firewall: wel of niet toelaten?

Een firewall beslist volgens regels welk verkeer wordt toegelaten. Regels kunnen kijken naar bron en bestemming, {term}`protocol`, poorten en de toestand van een verbinding. Een stateful firewall kan antwoorden bij een toegestane verbinding herkennen.

Een router kan doorsturen, NAT kan vertalen en een firewall kan filteren. Die {term}`functies <functie>` zitten vaak in één apparaat, maar lossen verschillende vragen op. Een firewall die ‘{term}`TCP` naar poort 443’ toestaat, beoordeelt daarmee niet automatisch of iedere website inhoudelijk veilig is.

::: {exercise} Zonder Filius: pas de regels toe
:label: nw09-o2

Een stateful firewall gebruikt deze volgorde: 1 antwoorden bij toegestane verbindingen toelaten; 2 interne clients nieuwe TCP-verbindingen naar externe poort 443 laten beginnen; 3 alle overige nieuwe verbindingen blokkeren.

1. Mag een interne browser een nieuwe verbinding naar externe poort 443 starten?
2. Mag het antwoord terug naar de tijdelijke clientpoort?
3. Mag een externe computer ongevraagd een nieuwe verbinding naar een interne client beginnen?
4. Voegt deze firewall automatisch versleuteling toe?
:::

::: {solution} nw09-o2
:class: dropdown

1. Ja, volgens regel 2.
2. Ja, als het bij de toegestane verbinding hoort, volgens regel 1.
3. Nee, volgens regel 3.
4. Nee, filteren en versleutelen zijn verschillende functies.
:::

## HTTPS: de verbinding beveiligen

HTTPS is {term}`HTTP` via een beveiligde verbinding. Bij HTTP/1.1 en HTTP/2 zorgt TLS boven TCP voor bescherming. De browser controleert onder andere of het certificaat past bij de domeinnaam en een vertrouwde certificaatketen heeft. De partijen spreken cryptografische sleutels af.

TLS beschermt de inhoud tegen meelezen en ongemerkt wijzigen onderweg en helpt de server te authenticeren. Het maakt een frauduleuze website niet eerlijk: ook een verkeerde website kan een geldig certificaat voor haar eigen domeinnaam hebben. Andere informatie, zoals IP-adressen en hoeveel verkeer er is, kan onderweg nog zichtbaar zijn. Moderne HTTP/3 gebruikt QUIC met TLS-beveiliging.

::: {exercise} In het echt: wat bewijst het certificaat?
:label: nw09-o3

1. Open de schoolwebsite via HTTPS. Open via de site-informatie bij de adresbalk de verbindings- of certificaatinformatie. Noteer de domeinnaam waarvoor het certificaat geldt en, indien zichtbaar, de geldigheidsperiode. De menunaam verschilt per browser.
2. Leg uit waarom een geldig certificaat geen kwaliteitskeurmerk voor de inhoud is.
3. Waarom kun je in je eigen ontwikkeltools toch de inhoud van HTTPS-antwoorden lezen?
:::

::: {solution} nw09-o3
:class: dropdown

1. De concrete gegevens verschillen; controleer de werkelijk bezochte naam en de getoonde certificaatnamen.
2. Het certificaat gaat over de identiteit bij een domeinnaam en de beveiligde verbinding, niet over de waarheid of goede bedoelingen van de inhoud.
3. Je browser is het eindpunt en ontsleutelt de gegevens. Een willekeurige tussenliggende router is dat niet.
:::

::: {exercise} Filius: wat laat het model zien?
:label: nw09-o4

1. Open je HTTP-website uit les 8 en lees een verzoek of antwoord in de gegevensuitwisseling. Zoek je eigen herkenbare paginatitel.
2. Vergelijk dit met de HTTPS-verbinding in de echte browser: wie kan daar de ontsleutelde inhoud bekijken?
3. Geef aan welke van de functies routering, NAT, firewall en TLS je tot nu toe daadwerkelijk in jouw Filius-opstelling hebt ingesteld en aangetoond.
:::

::: {solution} nw09-o4
:class: dropdown

Je hebt routering en een gewone HTTP-dienst ingesteld. De zichtbare paginatitel in die HTTP-uitwisseling toont geen TLS-beveiliging aan. Het configureren van private adressen is geen bewijs dat NAT actief is. Deze module vraagt geen onbevestigde TLS-simulatie of versieafhankelijke firewallconfiguratie in Filius; NAT en firewall beoordeel je hier met de uitgewerkte modellen en regels.
:::


---

(netwerken-les10)=
# Van URL naar webpagina

## Inleiding

Je kent nu de {term}`functies <functie>` van de verschillende lagen. In dit hoofdstuk gebruik je die kennis om één websitebezoek te volgen, van de tekst in de adresbalk tot de ontvangen inhoud.

**Hoofdvraag:** welke stappen zijn voor dit concrete bezoek nodig, en welke velden tonen aan wat er gebeurt?

Het [hoofdstuk over lagen en inkapseling](../03-lagen.md) geeft het verpakkingsmodel. Hier pas je dat toe op {term}`DNS`, {term}`TCP`, {term}`HTTP`, {term}`ARP` en {term}`routering`. Je legt je verklaring naast berichten die je zelf in de simulatie waarneemt.

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


---

(netwerken-les11)=
# Praktische eindopdracht: ontwerp en bouw

Een kleine organisatie heeft een werkruimte, een serverruimte en een tweede vestiging. Jij ontwerpt de adressering en maakt de onderlinge communicatie werkend in Filius.

Dit is de praktische beoordeling. Je werkt individueel, tenzij de docent anders aangeeft. Dit ene hoofdstuk beslaat les 11 en 12. Je levert een werkend netwerk én verklaringen in. Je hoeft niet werkelijk tientallen computers te tekenen: je adresplan moet daarvoor ruimte bieden.

## De opdracht

```{figure} ../images/eindopdracht.svg
:alt: De topologie ligt vast; de passende LAN-maskers kies je zelf.

De topologie ligt vast; de passende LAN-maskers kies je zelf.
```

Maak drie {term}`LAN's <LAN>` en een verbindingsnetwerk tussen twee gewone {term}`routers <router>`. R1 verbindt de werkruimte, serverruimte en het verbindingsnetwerk. R2 verbindt de tweede vestiging met het verbindingsnetwerk.

| Netwerk | Gewenste capaciteit, inclusief interfaces |
| --- | --- |
| Werkruimte | 45 werkplekken en één routerinterface |
| Serverruimte | Vier serverinterfaces en één routerinterface |
| Tweede vestiging | Twaalf werkplekken en één routerinterface |
| Verbinding R1–R2 | Twee routerinterfaces |

Gebruik als vaste beginadressen respectievelijk `192.168.40.0`, `192.168.50.0`, `192.168.60.0` en `10.0.0.0`. Kies voor ieder LAN het kleinste gewone {term}`subnet` dat voldoende adressen biedt. Gebruik /30 voor de verbinding tussen routers.

Je hoeft de adresruimte niet zelf in meerdere stukken te verdelen: ieder beginadres hoort bij het eigen subnet. Toon wel aan dat je subnetgrootte past. Reserveer waar je werkelijk meer apparaten toevoegt ook adressen daarvoor.

Teken minimaal twee {term}`clients <client>` in de werkruimte, twee in de tweede vestiging en twee {term}`servers <server>` in de serverruimte. Eén server biedt {term}`DNS` en één {term}`HTTP`. De vier geplande serverinterfaces zijn capaciteitseisen: de overige twee hoef je niet te tekenen. Gebruik per LAN een {term}`switch`.

## Adresplan vóór het bouwen

Maak per subnet een tabel met prefix, decimaal {term}`masker <subnetmasker>`, {term}`netwerkadres`, {term}`broadcastadres`, bruikbare reeks en capaciteit. Maak daarnaast een apparatentabel met alle getekende interfaces, hun {term}`IP-adres`, masker, {term}`gateway` en voor clients het DNS-serveradres.

Noteer vervolgens de handmatige routes voor R1 en R2. De rechtstreeks aangesloten netwerken moet je herkennen; daarvoor hoef je geen onnodige next-hopregels te schrijven. Gebruik geen automatische {term}`routering`, {term}`NAT`, {term}`DHCP` of Home Router in deze kernopdracht.

::: {note} Controlehulp bij het adresplan
:class: dropdown

Tel routerinterfaces mee, wijs geen netwerk- of broadcastadres toe en laat ieder {term}`next-hopadres <next hop>` op het lokale verbindingsnetwerk liggen. De docent beoordeelt je eigen keuze en berekening. De volledige voorbeeldconfiguratie staat in het docentmateriaal.
:::

## Diensten instellen

Maak op de DNS-server een record `www.project.test` dat naar je webserver verwijst. Maak op de webserver een pagina met:

- de naam van je organisatie en je eigen naam;
- een korte uitleg van het verschil tussen een IP-adres en een {term}`MAC-adres`;
- een korte uitleg waarom verkeer tussen de vestigingen een router nodig heeft.

De pagina moet vanaf beide LAN's op naam bereikbaar zijn. Je mag de bestaande Filius-startpagina aanpassen; een uitgebreid webontwerp is geen doel van deze opdracht.

## Werking aantonen

Voer deze tests uit en noteer per test de verwachte uitkomst, de feitelijke uitkomst en het bewijs. Bewijs kan bestaan uit een gerichte schermafbeelding of overgenomen relevante berichtvelden met toelichting.

| Test | Wat toon je aan? |
| --- | --- |
| Client naar tweede client in eigen LAN | Lokale bereikbaarheid |
| Werkruimte naar tweede vestiging en terug | Routering in beide richtingen |
| Website op IP-adres vanuit beide LAN's | Bereikbaarheid en webdienst |
| Website op naam vanuit beide LAN's | DNS plus webcommunicatie |
| Eerste verkeer buiten het eigen subnet volgen | {term}`ARP` voor de gateway en het behoud van het bestemmings-IP |

Een geslaagde ping is niet voldoende bewijs dat DNS of HTTP werkt. Kies bewijs dat bij de vraag past. Bewaar je definitieve bestand als `achternaam-netwerken.fls`.

## Verklaringen bij je eigen netwerk

Beantwoord met de werkelijk door jou gekozen adressen:

1. Waarom zijn netwerkfunctie en {term}`protocol` niet hetzelfde? Geef twee voorbeelden uit je opstelling.
2. Welke bestemming gebruikt een client in de werkruimte als Ethernetbestemming wanneer hij de webserver bezoekt? Welk IP-adres blijft de eindbestemming?
3. Welke handmatige routes zijn nodig voor een antwoord van de webserver naar een client in de tweede vestiging?
4. Welke rol hebben TCP-poorten bij het websitebezoek? Waarom gebruikt een ping die TCP-poorten niet?
5. Waarom bewijst jouw HTTP-website geen HTTPS-beveiliging? Wat zou {term}`TLS` toevoegen?
6. Zou je op het echte publieke {term}`internet` dezelfde private bronadressen rechtstreeks kunnen blijven gebruiken? Beschrijf wat {term}`NAPT` in een gebruikelijke IPv4-aansluiting verandert en wat een {term}`firewall` apart beslist.

::: {note} Waar letten we bij de verklaringen op?
:class: dropdown

Gebruik je eigen netwerk als bewijs. ‘De router stuurt het door’ is te algemeen: benoem de gekozen volgende stap en de adressen. Voor {term}`TCP` en {term}`HTTPS` zijn ook onderdelen nodig die je niet volledig uit de simulatie kunt aflezen. Leg daar de {term}`functie` uit en vermeld de grens van het model.
:::

## Inleveren en aantonen

Lever het Filius-bestand, het adres- en routeplan en je testverslag met verklaringen in. In les 12 rond je af en demonstreer je een door de docent gekozen communicatie. Je licht toe hoe je die hebt gecontroleerd.

De beoordelingscriteria staan verderop in dit hoofdstuk. Er zijn geen punten voor extra servers of extra protocollen als de gevraagde werking en uitleg nog niet kloppen.


## Bereid je demonstratie voor

Open je opgeslagen bestand en controleer dat je diensten na de simulatiestart actief zijn. Houd je adresplan en testverslag ernaast. De docent kiest een client en bestemming uit jouw opstelling. Je laat de communicatie zien en verklaart de betrokken lagen.

Tijdens de beoordeling horen volledige modelantwoorden niet op deze leerlingpagina. Bij gewone oefenopdrachten elders in de module blijven de antwoorden direct onder de vragen staan.

## Laat begrip zien

De docent kan bijvoorbeeld vragen:

- Waar komt het serveradres bij de naam vandaan?
- Naar welk IP-adres vraagt deze client met ARP, en waarom?
- Welke MAC-adressen veranderen bij deze router?
- Via welke tabelregel komt het antwoord terug?
- Welke functie zou blijven werken als je het lokale {term}`medium` vervangt?

Je hoeft geen vaste tekst op te zeggen. Gebruik je eigen adressen, routes en waarnemingen.

## Een bekende soort probleem onderzoeken

De docent wijzigt in een kopie één instelling uit een bekende categorie: een clientgateway, een DNS-verwijzing of een handmatige route. Je krijgt de waargenomen klacht, niet meteen de gewijzigde instelling.

1. Noem op basis van de klacht twee mogelijke oorzaken.
2. Kies zelf een controle waarmee je de mogelijkheden beter onderscheidt.
3. Voer de controle uit en leg uit wat de uitkomst wel en niet aantoont.
4. Herstel de oorzaak en toon de bedoelde werking opnieuw aan.

Dit is een kort individueel onderdeel van de beoordeling, geen extra hoofdstuk met nieuwe storingsstof. Het gaat om een beredeneerde keuze uit bekende controles, niet om willekeurig instellingen veranderen of steeds alles opnieuw bouwen.

## Beoordeling

| Onderdeel | Punten | Waar letten we op? |
| --- | --- | --- |
| Adressering en subnetten | 20 | Passende capaciteit, juiste grenzen, geldige en consistente interfaceadressen |
| Topologie en routering | 20 | Gescheiden LAN's, passende interfaces, next hops en heen- en terugroutes |
| DNS en HTTP | 15 | Correcte naamkoppeling, actieve webdienst en bereikbaarheid vanuit beide LAN's |
| Bewijs en testen | 15 | Gerichte tests met verwachting, uitkomst en bewijs voor de juiste functie |
| Begrip en verklaringen | 20 | Lagen, protocollen, ARP, adressen, TCP en beveiligingsfuncties in samenhang |
| Zelfstandig onderzoeken | 10 | Controle met reden, uitleg van de uitkomst, herstel en hertest |
| **Totaal** | **100** | |

Bij een deels werkend netwerk kun je punten verdienen voor onderdelen die aantoonbaar correct zijn. Een werkend bestand zonder verklaringen levert niet automatisch de punten voor begrip op.

## Afronding

Controleer of je ingeleverde bestand overeenkomt met je adresplan. Zorg dat iedere schermafbeelding een doel heeft en voorzien is van uitleg. Voeg geen complete lijst netwerkberichten toe zonder aan te geven welke regels het bewijs vormen.

De docent geeft aan hoe punten naar een cijfer worden omgerekend en hoe lang de individuele demonstratie duurt. Bij een grotere klas kan het korte onderzoek tijdens het zelfstandig werken in les 11 en 12 worden afgenomen.


---


(netwerken-les13)=
# Verdieping: DHCP en e-mail

Dit hoofdstuk is optioneel en valt buiten de kernplanning van twaalf lessen. Je onderzoekt twee extra toepassingsprotocollen.

## DHCP: wie stelt al die adressen in?

In de kernmodule kies je adressen met de hand. In een echt netwerk krijgt een {term}`client` zijn IPv4-instellingen vaak automatisch via {term}`DHCP`. De client zoekt een {term}`server`, krijgt een aanbod, vraagt een aangeboden configuratie aan en krijgt een bevestiging. De namen van de eerste berichten zijn Discover, Offer, Request en Acknowledge.

De configuratie kan naast het {term}`IP-adres` onder andere het {term}`masker <subnetmasker>`, een {term}`gateway` en DNS-serveradressen bevatten. Het adres wordt voor een bepaalde tijd uitgeleend: de lease. Een DHCP-server is geen DNS-server, al kan dezelfde machine beide diensten uitvoeren.

Een nieuwe client kent nog niet alle netwerkgegevens en gebruikt aanvankelijk broadcastcommunicatie. {term}`Routers <router>` sturen die niet vanzelf door naar andere netwerken. In grotere netwerken kan een speciaal ingestelde DHCP-relay helpen; dat configureren we hier niet.

::: {exercise} Filius: automatische instellingen
:label: nw13-o1

1. Werk in een kopie van het netwerk uit les 8. Installeer op de DNS-server ook de DHCP-serverdienst als die in jouw Filius-versie beschikbaar is.
2. Kies voor het server-LAN een pool `192.168.20.100` tot en met `192.168.20.120`, masker `255.255.255.0`, gateway `192.168.20.1` en {term}`DNS` `192.168.20.53`. Houd vaste serveradressen buiten de pool.
3. Voeg één nieuwe client toe op dezelfde {term}`switch` en stel deze in op automatische adresconfiguratie. Start de DHCP-dienst en vraag de configuratie aan.
4. Controleer de ontvangen instellingen en bezoek de oefenwebsite op naam. Welke {term}`functies <functie>` zijn door DHCP ingesteld en welke dienst levert nog steeds de pagina?
:::

::: {solution} nw13-o1
:class: dropdown

De client hoort een beschikbaar adres uit de pool en de ingestelde aanvullende gegevens te krijgen. DHCP levert de netwerkconfiguratie, DNS de naamkoppeling en de webserver de pagina. Automatische configuratie alleen bewijst dus nog niet dat iedere achterliggende dienst goed werkt. Menunamen en aanvullende opties kunnen per Filius-versie verschillen.
:::

## E-mail: verzenden is iets anders dan ophalen

Bij e-mail kunnen client en server meerdere rollen hebben. SMTP wordt gebruikt voor het aanbieden en doorsturen van mail. IMAP en POP worden gebruikt om ontvangen berichten via een client te benaderen. Bij webmail praat jouw browser via {term}`HTTP`(S) met de webmailtoepassing; de mailinfrastructuur erachter gebruikt andere {term}`afspraken <afspraak>`.

Een mailadres bevat een gebruikersdeel en domein, bijvoorbeeld `leerling@school.test`. Voor server-naar-serverbezorging kunnen MX-records in DNS aanwijzen welke mailservers bij een domein horen. Dat is iets anders dan een A-record voor een website.

::: {exercise} Zonder Filius: volg een e-mail
:label: nw13-o2

1. Is een browser die webmail toont bewijs dat alle mail met HTTP tussen mailservers reist?
2. Welke afspraak hoort bij mail aanbieden en doorsturen: SMTP of {term}`ARP`?
3. Waarom bewijst een werkende website op `school.test` nog niet dat mail naar dat domein bezorgd kan worden?
:::

::: {solution} nw13-o2
:class: dropdown

1. Nee. HTTP(S) kan de browserinterface verzorgen, terwijl mailservers met mailprotocollen communiceren.
2. SMTP. ARP lost een lokaal adresseringsprobleem op.
3. De webdienst en maildienst hebben verschillende configuraties en servers; ook de benodigde DNS-records kunnen verschillen.
:::
