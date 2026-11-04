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
