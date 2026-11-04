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

In Filius gebruik je alvast {term}`IP-adressen <IP-adres>` om met `ping` verkeer te maken. De switch kiest zijn doorstuurpoort niet op basis van het IP-adres, maar op basis van het MAC-adres. Ping gebruikt {term}`ICMP`, niet {term}`TCP`. Hoe een computer het MAC-adres van de ontvanger te weten komt, behandelen we in hoofdstuk 5.

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
