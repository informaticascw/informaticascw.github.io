---
numbering: false
---
(netwerken-begrippen)=
# Begrippenlijst

Deze lijst bevat de centrale definities van de module. Begrippen in de hoofdstukken verwijzen met MyST-termen naar deze ene lijst. De uitleg en voorbeelden in de hoofdstukken laten zien hoe je de begrippen toepast.

::: {glossary}

afspraak
: Regel die zender en ontvanger allebei gebruiken om communicatie op dezelfde manier uit te voeren of te begrijpen.

apparaatdeel
: Bits van een IPv4-adres die binnen het gekozen subnet beschikbaar zijn voor adressen. In een gewoon LAN reserveren we alle nullen en alle enen voor netwerk- en broadcastadres.

ARP
: Protocol om op een lokaal IPv4-netwerk het MAC-adres bij het IP-adres van een volgende ontvanger te vinden.

ARP-cache
: Tijdelijke tabel met lokaal bekende koppelingen tussen IP-adressen en MAC-adressen.

ARP-reply
: ARP-antwoord dat de gezochte adreskoppeling meedeelt, in de voorbeelden rechtstreeks aan de vrager.

ARP-request
: ARP-vraag naar het MAC-adres bij een lokaal IP-adres; in de voorbeelden als Ethernetbroadcast verstuurd.

bandbreedte
: In deze module: de beschikbare overdrachtscapaciteit van een verbinding, meestal uitgedrukt in bits per seconde.

bit
: Binaire waarde: 0 of 1. Een fysiek signaal kan een of meer bits voorstellen.

bits per seconde
: Eenheid voor overdrachtssnelheid: hoeveel bits per seconde worden overgedragen. Mbit/s betekent miljoen bits per seconde.

broadcast
: Bericht voor alle apparaten binnen het betreffende lokale broadcastdomein, in plaats van één geselecteerde ontvanger.

broadcastadres
: Adres om alle ontvangers binnen een bereik aan te spreken. Ethernet gebruikt ff:ff:ff:ff:ff:ff. Het IPv4-broadcastadres van een gewoon subnet heeft alle apparaatbits op 1.

broadcastdomein
: Deel van een netwerk waar een gewone lokale broadcast wordt verspreid. Gewone routering verbindt netwerken zonder hun Ethernetbroadcasts door te zetten.

byte
: Groep van acht bits. Eén MB en één Mbit zijn daarom verschillende hoeveelheden gegevens.

bytestroom
: Reeks bytes zonder door TCP bewaarde grenzen tussen de oorspronkelijke toepassingsberichten. TCP levert ontvangen bytes geordend aan de toepassing.

cache
: Tijdelijke opslag van eerder verkregen informatie om die opnieuw te kunnen gebruiken zonder alles opnieuw op te vragen.

CIDR-prefix
: Notatie zoals /26 die aangeeft hoeveel van de 32 IPv4-bits bij het netwerkdeel horen.

client
: Programma of apparaat dat een dienst van een server aanvraagt, bijvoorbeeld een browser die een webpagina opvraagt.

CRC
: Methode voor het berekenen van foutcontrole-informatie uit bits. De ontvanger kan ermee veel overdrachtsfouten detecteren; CRC herstelt de gegevens niet zelf.

datalinklaag
: Laag die gegevens in frames over een lokale verbinding aflevert. Bij Ethernet worden daarvoor onder andere MAC-adressen gebruikt.

DHCP
: Toepassingsprotocol waarmee een client automatisch netwerkconfiguratie kan verkrijgen, zoals IPv4-adres, masker, gateway en DNS-server.

DNS
: Verdeeld systeem voor naamgegevens. Een DNS-opzoeking kan bijvoorbeeld het IP-adres bij een hostnaam opleveren; DNS levert niet de webpagina zelf.

DNS-resolver
: Dienst die DNS-vragen voor een client beantwoordt, vanuit een cache of door de benodigde naamgegevens op te zoeken.

Ethernet
: Familie van technieken en afspraken voor lokale netwerkcommunicatie, met frames en MAC-adressen. In deze module vooral bekabeld, geschakeld Ethernet.

FCS
: Frame Check Sequence: foutcontroleveld aan het einde van een Ethernetframe, berekend met CRC.

firewall
: Functie die volgens regels communicatie toelaat of blokkeert. Kan onder andere adressen, protocollen, poorten en verbindingstoestand gebruiken.

flooding
: Doorsturen van een frame naar alle andere geschikte switchpoorten, bijvoorbeeld bij een onbekende unicastbestemming.

frame
: Datalinkverpakking. Een Ethernetframe bevat een header, inhoud en een trailer met foutcontrole. De inhoud kan een heel IP-pakket zijn.

functie
: Het probleem of de taak die een netwerkonderdeel of laag oplost. Een protocol legt de concrete communicatieafspraken vast waarmee zo een functie wordt uitgevoerd.

fysieke laag
: Laag die bits als signalen over een medium overdraagt, bijvoorbeeld via koper, glasvezel of radio.

gateway
: Volgende router waar een apparaat verkeer naartoe kan sturen. De standaardgateway wordt gebruikt als voor een bestemming geen specifiekere route beschikbaar is.

header
: Besturingsinformatie vóór de inhoud van een protocolbericht. Iedere laag verwerkt zijn eigen headervelden; verschillende headers kunnen in elkaar verpakt zijn.

HTTP
: Toepassingsprotocol voor verzoeken en antwoorden rond bronnen zoals webpagina’s. De inhoud kan onder andere HTML, CSS of een afbeelding zijn.

HTTPS
: HTTP over een beveiligde verbinding. TLS beschermt onder andere de inhoud en ondersteunt controle van de serveridentiteit; HTTPS is geen keurmerk voor de juistheid van een website.

ICMP
: Protocol voor controle- en foutmeldingen bij IP. Ping gebruikt ICMP-echoverzoeken en -antwoorden, geen TCP-poorten.

inkapseling
: Toevoegen van protocolinformatie rond gegevens van een hogere laag. Bijvoorbeeld: TCP-segment in IP-pakket in Ethernetframe.

internet
: Geheel van gekoppelde netwerken die met gemeenschappelijke afspraken gegevens kunnen uitwisselen. Het web is één toepassing op internet.

IP
: Internet Protocol: protocol voor adressering en aflevering van pakketten tussen netwerken. IPv4 gebruikt adressen van 32 bits en biedt op zichzelf geen betrouwbare geordende bytestroom.

IP-adres
: Logisch adres van een netwerkinterface. Met het subnetmasker bepaalt een IPv4-afzender welk deel het subnet aanwijst.

IP-pakket
: Verpakking van de netwerklaag: een IP-header plus inhoud, bijvoorbeeld een TCP-segment of ICMP-bericht.

lagenmodel
: Indeling van communicatiefuncties in lagen. Een laag gebruikt diensten van de laag eronder; de module gebruikt vijf lagen.

LAN
: Local Area Network: lokaal netwerk, bijvoorbeeld computers op een geschakeld Ethernetnetwerk. Een fysieke locatie kan meerdere logisch gescheiden LAN’s bevatten.

MAC-adres
: Adres van een netwerkinterface voor lokale datalinkaflevering. Het is niet automatisch een onveranderlijk serienummer van de hele computer.

medium
: Fysieke drager voor signalen, zoals een koperkabel, glasvezel of radioverbinding.

NAPT
: Variant van NAT die bij verbindingen zowel adres- als poortinformatie vertaalt, zodat meerdere interne apparaten een buitenadres kunnen delen.

NAT
: Network Address Translation: vertalen van IP-adresinformatie bij een netwerkgrens. De gebruikelijke thuisvariant vertaalt ook poorten en heet NAPT of PAT.

netwerkadres
: Eerste adres van een gewoon IPv4-subnet, met alle apparaatbits op 0. Het benoemt het subnet en wordt in deze LAN-voorbeelden niet aan een apparaat toegewezen.

netwerkdeel
: Bits van een IP-adres die volgens het subnetmasker het subnet aanwijzen.

netwerklaag
: Laag voor adressering en doorsturen tussen netwerken. IP is een protocol dat deze functie invult.

next hop
: Rechtstreeks bereikbare volgende router waar een pakket volgens een route naartoe wordt gestuurd.

octet
: Groep van acht bits. Ieder getal in de gebruikelijke IPv4-notatie stelt een octet voor en ligt tussen 0 en 255.

ontkapseling
: Verwerken en wegnemen van protocolverpakkingen aan de ontvangende kant, waarbij inhoud aan de volgende hogere laag wordt doorgegeven.

payload
: Inhoud die een protocol vervoert. Voor Ethernet kan dat een heel IP-pakket zijn; voor IP bijvoorbeeld een heel TCP-segment.

poortnummer
: Getal in transportinformatie dat helpt gegevens bij de juiste toepassing of verbinding af te leveren. Dit is iets anders dan een fysieke switchaansluiting.

privaat IP-adres
: IPv4-adres uit een voor intern gebruik gereserveerde reeks. Het is niet wereldwijd uniek; organisaties kunnen dezelfde adressen intern hergebruiken.

protocol
: Verzameling concrete afspraken over de vorm, betekenis en uitwisseling van communicatie tussen deelnemers.

publiek IP-adres
: IP-adres dat voor publieke bereikbaarheid wordt gebruikt. Niet elk adres buiten de private reeksen is automatisch een publiek bruikbaar adres.

router
: Netwerkfunctie die IP-pakketten op basis van routes naar een volgende verbinding doorstuurt. Een router scheidt in onze voorbeelden lokale broadcastdomeinen.

routering
: Kiezen en gebruiken van stappen om pakketten door gekoppelde netwerken naar een bestemming te sturen.

routeringstabel
: Tabel met bestemmingsnetwerken en de bijbehorende volgende stap of rechtstreeks aangesloten interface.

server
: Programma of apparaat dat een dienst aanbiedt, bijvoorbeeld HTTP-verzoeken beantwoordt. Eén apparaat kan meerdere serverdiensten uitvoeren.

standaardroute
: Route die gebruikt wordt als geen specifiekere route past. Bij IPv4 wordt zij als 0.0.0.0/0 geschreven.

subnet
: Verzameling IP-adressen met hetzelfde netwerkdeel volgens een gekozen masker. Alleen andere subnetten instellen scheidt nog geen Ethernetbroadcasts.

subnetmasker
: Patroon met aaneengesloten enen voor het netwerkdeel en daarna nullen voor het apparaatdeel van een IPv4-adres.

switch
: Netwerkfunctie die Ethernetframes tussen aansluitingen doorstuurt. Leert normaal uit bron-MAC-adressen via welke aansluiting apparaten bereikbaar zijn.

TCP
: Transportprotocol dat toepassingen een betrouwbare geordende bytestroom biedt, met verbindingen, volgnummers, bevestigingen en hertransmissie. Biedt niet vanzelf versleuteling.

TCP-segment
: TCP-header met eventueel gegevens; wordt als inhoud van een IP-pakket verstuurd.

TLS
: Beveiligingsprotocol voor onder andere vertrouwelijkheid, integriteit en controle van de serveridentiteit. Wordt bij HTTPS gebruikt.

toepassingslaag
: Laag voor berichten en diensten van toepassingen, zoals naamopzoeking met DNS en webverkeer met HTTP.

trailer
: Protocolinformatie achter de inhoud. Ethernet gebruikt aan het einde van een frame een foutcontroleveld.

transportlaag
: Laag die communicatie tussen toepassingen ondersteunt, onder andere met poorten. TCP en UDP bieden verschillende transportdiensten.

UDP
: Transportprotocol voor afzonderlijke datagrammen met poorten. Verzorgt zelf geen verbindingsopbouw, geordende stroom of hertransmissie; een toepassing kan zulke functies toevoegen.

unicast
: Gerichte aflevering aan één ontvanger, in tegenstelling tot bijvoorbeeld broadcast aan alle lokale ontvangers.

URL
: Aanduiding van een bron, met onder andere protocol, hostnaam en eventueel pad, bijvoorbeeld http://nieuws.school.test/rooster.html.

vertraging
: Tijd die verstrijkt door transport, verwerking en wachten. Een verbinding met veel capaciteit kan toch merkbare vertraging hebben.

web
: Toepassing op internet voor gekoppelde bronnen en pagina’s, benaderd met onder andere HTTP(S). Internet als geheel omvat meer toepassingen.

wifi
: Techniek voor draadloze lokale netwerkcommunicatie via radiogolven. Een wifinaam alleen bepaalt niet welk IP-subnet of broadcastdomein wordt gebruikt.

:::
