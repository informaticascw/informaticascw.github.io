(netwerken-h11)=
# Praktische eindopdracht: ontwerp en bouw

Een kleine organisatie heeft een werkruimte, een serverruimte en een tweede vestiging. Jij ontwerpt de adressering en maakt de communicatie tussen de netwerken werkend in Filius.

Dit is de praktische beoordeling. Je werkt individueel, tenzij de docent anders aangeeft. Dit hoofdstuk beslaat les 11 en 12. Je levert een werkend netwerk én verklaringen in. Je hoeft niet tientallen computers te tekenen, maar je adresplan moet er wel ruimte voor bieden.

## De opdracht

```{figure} images/eindopdracht.svg
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

Lever het Filius-bestand, het adres- en routeplan en je testverslag met verklaringen in. In les 12 rond je af en demonstreer je een communicatie die de docent kiest. Je legt uit hoe je die hebt gecontroleerd.

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

Dit is een kort individueel onderdeel, geen nieuwe stof. Het gaat om een beredeneerde keuze uit bekende controles, niet om willekeurig instellingen veranderen of alles opnieuw bouwen. Bij een grote klas kan dit onderdeel tijdens het zelfstandig werken in les 11 en 12 worden afgenomen.

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
