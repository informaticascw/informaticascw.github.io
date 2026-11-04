(netwerken-les11)=
# Praktische eindopdracht: ontwerp en bouw

Een kleine organisatie heeft een werkruimte, een serverruimte en een tweede vestiging. Jij ontwerpt de adressering en maakt de onderlinge communicatie werkend in Filius.

Dit is de praktische beoordeling. Je werkt individueel, tenzij de docent anders aangeeft. Dit ene hoofdstuk beslaat les 11 en 12. Je levert een werkend netwerk én verklaringen in. Je hoeft niet werkelijk tientallen computers te tekenen: je adresplan moet daarvoor ruimte bieden.

## De opdracht

```{figure} images/eindopdracht.svg
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
