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
