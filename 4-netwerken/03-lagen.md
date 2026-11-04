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

```{figure} images/inkapseling.svg
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
