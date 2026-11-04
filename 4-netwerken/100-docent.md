---
numbering: false
---
(netwerken-docent)=
# Voor de docent

## Opbouw

Hoofdstuknummers en lesnummers zijn niet hetzelfde. De module heeft twaalf inhoudelijke hoofdstukken en één beoordelingshoofdstuk. De startpagina, begrippenlijst en deze docentpagina worden niet meegeteld.

Hoofdstuk 12 vat de lagen samen en introduceert inkapseling: toepassingsgegevens in een TCP-segment, in een IP-pakket, in een Ethernetframe met header en trailer. De fysieke laag zet bits om in signalen en voegt geen header toe. Het hoofdstuk past dat model daarna toe op één websitebezoek.

Hoofdstuk 3 bevat de klassikale oefening met één druk netwerk, splitsen en weer koppelen. Die motiveert de overgang naar afzonderlijke IP-netwerken. Hoofdstuk 4 behandelt daarna alleen nog hoe een computer het MAC-adres bij de gekozen lokale ontvanger vindt; daar is geen tweede broadcastspel.

De begrippenlijst bevat vaktermen die leerlingen moeten kunnen uitleggen en die op meer dan één plek voorkomen. De hoofdstukken linken de eerste vermelding van een term.

## Planning van zestien lessen

| Les | Hoofdstuk | Activiteiten en richttijden | Huiswerk/voorbereiding |
| --- | --- | --- | --- |
| 1 | 1 Bits | 15 min signalenspel, 15 min uitleg, 30 min rekenen en eerste verbinding | Rekenen afronden |
| 2 | 2 Een lokaal netwerk | 15 min switchspel, 15 min uitleg, 30 min lokaal netwerk en frames | Leertabel verklaren |
| 3 | 3 Een wereldwijd netwerk | 15 min broadcastspel, 15 min netwerkgrens, 30 min uitleg en berekeningen | Eerste berekeningen afronden |
| 4 | 3 Een wereldwijd netwerk | 20 min uitgewerkte berekeningen, 25 min oefenen, 15 min subnetproef | Subnetberekeningen afronden |
| 5 | 4 Netwerken verbinden | 10 min keuze volgende ontvanger, 15 min ARP, 20 min routerpad en Filius, 15 min eigen apparaat | Schriftelijke verklaringen afronden |
| 6 | 5 Routeren | 10 min lokale routekaarten, 15 min uitleg, 35 min handmatige routes | Heen- en terugweg verklaren |
| 7 | 6 Poorten, TCP en UDP | 10 min ontbrekende delen, 20 min poorten en TCP/UDP, 30 min vragen en waarneming | Begripsvragen afronden |
| 8 | 7 DNS | 10 min DNS-balie, 15 min uitleg, 35 min DNS-server instellen | Vragen over naam en adres afronden |
| 9 | 8 HTTP | 10 min pagina opvragen, 15 min uitleg, 35 min website op naam | Verzoek en antwoord verklaren |
| 10 | 9 E-mail | 20 min uitleg, 25 min vragen, 15 min eigen mailprogramma of webmail bekijken | Vragen afronden |
| 11 | 10 DHCP | 20 min uitleg, 30 min DHCP instellen, 10 min nabespreken | Instellingen vergelijken met handmatige configuratie |
| 12 | 11 NAT en firewall | 10 min vertaaltabelspel, 30 min uitleg, 20 min regels toepassen | Verschil NAT en firewall verklaren |
| 13 | 12 Lagen en inkapseling | 20 min lagen en inkapseling, 15 min verpakkingen in groepen, 25 min uitgewerkt bezoek | Uitgewerkt bezoek nalopen |
| 14 | 12 en 13 | 25 min bewijsverslag, 10 min introductie beoordeling, 25 min start eindopdracht | Adresplan eindopdracht voorbereiden |
| 15 | 13 Eindopdracht | 5 min afspraken, 55 min bouwen en testen | Verslag volgens schoolafspraak afronden |
| 16 | 13 Eindopdracht | 5 min afspraken, 55 min afronden en individueel aantonen | Inleveren |

Dit zijn richttijden, geen gemeten uitvoertijden. Hoofdstuk 3 vraagt flink oefenen; gebruik huiswerk voor aanvullende berekeningen en stel de kern boven verdieping. Een correct startbestand kan helpen als Filius-bediening de conceptuele leertijd verdringt. Er zijn nog geen praktisch geteste .fls-startbestanden meegeleverd.

## Klassikale voorbereiding

### Hoofdstuk 1 en 2

Voor het signalenspel: per vier leerlingen een zender, ontvanger, tijdwaarnemer en controleur; geheime 8-bitreeksen, kaart of lampje en klok. Eerst zonder code, daarna afspraken over begin en tempo. Het leert signaalafspraken, geen echte Ethernetcodering.

Voor de switch: vier apparaatcodes, vier poortstapels, frames en een lege leertabel. Laat de switch uit de bronadressen leren en onbekende bestemmingen kopiëren. De waarnemer telt kopieën; doel is gericht doorsturen begrijpen, niet zo snel mogelijk papier verplaatsen.

### Hoofdstuk 12: lagen en verpakkingen

Werk per groep van negen met vier zenderrollen, vier ontvangerrollen en één routerrol. Gebruik bij een andere groepsgrootte een waarnemer of combineer zender- en ontvangerrollen na elkaar. Geef iedere rol alleen de benodigde informatie:

| Rol | Kaart voor de eerste verzending |
| --- | --- |
| Toepassing | Vraag de tekst ‘Rooster voor morgen’ op |
| Transport | Clientpoort 51000, serverpoort 80; voeg deze velden toe |
| Netwerk | Bron 192.168.10.10, eindbestemming 192.168.20.10 |
| Datalink | Bron-MAC A, volgende ontvanger router-links; maak de buitenste omslag |
| Router | Nieuwe buitenste omslag: bron router-rechts, bestemming C; IP-eindadressen behouden |

Gebruik drie groottes gevouwen kaarten: transport, IP en Ethernet. De toepassingsgegevens staan op het binnenste kaartje. De Ethernetverpakking heeft een apart gemarkeerde trailer; er wordt geen echte CRC berekend. Laat de ontvanger eerst zonder router ontkapselen; laat daarna met nieuwe MAC-adressen dezelfde inhoud door een router gaan. Bespreek dat echte TCP-verdeling en de fysieke signalen niet worden nagespeeld.

### Hoofdstuk 3: broadcastbelasting en netwerkgrenzen

Gebruik de hele klas. Geef de helft unieke IP-adressen 192.168.10.10 en verder; de andere helft 192.168.20.10 en verder. Reserveer .1 voor de twee routerinterfaces en geef iedere kaart een eigen fictief MAC-adres. Eén waarnemer wordt in de derde ronde router.

Eerst is de hele klas één /16-netwerk. Daarna maak je twee daadwerkelijk gescheiden lokale groepen met /24. De maskers staan op het bord; berekenen hoeft op dat moment nog niet. Laat per helft bijvoorbeeld drie afzenders tegelijk een lokale bestemming zoeken. Houd het aantal afzenders bij vergelijking gelijk en maak na ronde 1 de tijdelijk bekende koppelingen leeg. Laat iedereen normaal verstaanbaar praten; maximaal lawaai is niet nodig.

Tel hoeveel leerlingen zoekvragen moeten verwerken. De winst hoeft niet als snellere stopwatchtijd zichtbaar te zijn: de oefening heeft ook uitvoeringskosten. Eerst belast iedere vraag beide groepen, daarna alleen de eigen groep. Geef pas dan een bestemming buiten de groep en introduceer de router als oplossing. De router zoekt lokaal aan beide kanten; de oorspronkelijke broadcast gaat niet automatisch door.

Benadruk de grenzen van de vergelijking: alleen andere IP-instellingen scheiden geen Ethernetbroadcasts; hetzelfde wifi-SSID zegt niet genoeg over subnetten; radio-interferentie is niet hetzelfde als een broadcastdomein. Deze oefening richt zich alleen op netwerkgrenzen; het inpakken van berichten komt in hoofdstuk 12 aan bod.

### Hoofdstuk 4: geen tweede klassikale introductie

De inleiding benoemt de resterende adreskoppeling. Gebruik het bestaande lokale netwerk en de nieuwe tweede LAN-opstelling. Laat de leerling eerst het IP-adres van de volgende ontvanger kiezen, en pas daarna met ARP het MAC-adres daarvan zoeken. Controleer vooraf waar de netwerkgegevens van het eigen schoolapparaat zichtbaar zijn. Demonstreer anders op een docentcomputer.

### Hoofdstuk 5 tot en met 12

| Hoofdstuk | Voorbereiding | Didactische focus |
| --- | --- | --- |
| 5 Routeren | Lokale tabellen voor R1 en R2 uit het hoofdstuk | Eerst ontbreekt de heenroute, dan de terugroute; geen centraal inzicht voor iedere routerrol |
| 6 Poorten, TCP en UDP | Zes genummerde tekstdelen, kopieën en twee poortpostvakken | Volgorde, ontbrekende gegevens en doublures; TCP nummert bytes, niet deze papieren berichtdelen |
| 7 DNS | Namenlijst met adressen en clients met URL-kaarten | DNS kent alleen hostnamen en adressen, niet het pad |
| 8 HTTP | URL-kaarten, DNS-lijst en twee servers met pagina’s | De server bepaalt of een pad bestaat (200 of 404); verplaatsen vraagt ook een aangepaste DNS-lijst |
| 9 E-mail en 10 DHCP | Geen | Verzenden en ophalen zijn aparte taken; DHCP stelt alleen netwerkinstellingen in |
| 11 NAT en firewall | Twee clients, één buitenadres, poortkaartjes, vertaaltabel en filterregel | Eerst een ambigu antwoord; daarna onderscheid door buitenpoorten; filteren blijft een aparte beslissing |
| 12 Lagen en inkapseling | Verpakkingskaarten (zie hierboven), werkende DNS/HTTP-opstelling en berichtvensters | Eerst verpakken en uitpakken met kaarten; daarna verbinden leerlingen bestaande waarnemingen met de verklaringen |

Voor e-mail en DHCP is geen klassikale oefening toegevoegd; beide hoofdstukken werken met uitleg en vragen, en DHCP daarnaast met een Filius-opdracht.

## Praktijk en beoordeling

De doorlopende opstelling ontstaat in hoofdstuk 1–2. Hoofdstuk 3 gebruikt een aparte subnetproef; overschrijf de basisopstelling daarmee niet. Hoofdstuk 4 bouwt de twee LAN’s met één router, hoofdstuk 5 voegt een tweede router toe, en hoofdstuk 7–8 voegen DNS en web toe.

Controleer in de schoolversie vooraf: lokale ping, gerouteerde ping, twee routers met handmatige routes, HTTP op IP en naam, en de zichtbaarheid van ARP/TCP/HTTP. Exacte menunamen en cachegedrag zijn nog niet praktisch getest. Een verloren eerste ping kan door adresresolutie komen; kies geen conclusie op basis van één losse meting.

Gebruik de rubric uit hoofdstuk 13. De fysieke laag, TCP-dienst en beveiligingsfuncties zijn niet allemaal aan een werkend bestand af te lezen: neem de verklaringen mee. Bij een grote klas zijn dertig mondelinge gesprekken van vijf minuten niet in één les haalbaar. Laat het korte foutonderzoek zo nodig schriftelijk doen in individuele kopieën en controleer mondeling één gekozen stap tijdens les 15 of 16.

## Begrippenlijst onderhouden

Alle definities staan één keer in `99-begrippenlijst.md`, binnen een MyST-glossary. De hoofdstukken gebruiken de term-rol, met weergavetekst waar nodig, en linken een term bij de eerste vermelding in een hoofdstuk. Nieuwe vaktermen horen op de begrippenpagina; gewone woorden niet. Kopieer de glossary niet naar andere hoofdstukken of naar de leesversie. De begrippenpagina blijft in de inhoudsopgave, zodat MyST de termverwijzingen kan oplossen.


## Voorbeeldconfiguratie en beoordeling

Dit bestand hoort bij de docent. Het is één geldige uitwerking; andere consistente keuzes voor interfaceadressen zijn mogelijk. De vereiste kleinste maskers en de vastgelegde netwerkbeginadressen beperken de subnetkeuze.

### Adresplan

| Netwerk | Nodig | Prefix en masker | Netwerk | Broadcast | Bruikbaar | Capaciteit |
| --- | --- | --- | --- | --- | --- | --- |
| Werkruimte | 46 | /26, 255.255.255.192 | 192.168.40.0 | 192.168.40.63 | .1–.62 | 62 |
| Serverruimte | 5 | /29, 255.255.255.248 | 192.168.50.0 | 192.168.50.7 | .1–.6 | 6 |
| Tweede vestiging | 13 | /28, 255.255.255.240 | 192.168.60.0 | 192.168.60.15 | .1–.14 | 14 |
| Routerverbinding | 2 | /30, 255.255.255.252 | 10.0.0.0 | 10.0.0.3 | .1–.2 | 2 |

De 45 en twaalf werkplekken worden niet allemaal getekend. Alle vier geplande serverinterfaces zijn in de capaciteit meegerekend. Deze taak vraagt geen VLSM-verdeling van één grotere pool.

### Interfaces en diensten

| Interface | IP-adres | Masker | Gateway | DNS |
| --- | --- | --- | --- | --- |
| R1 werkruimte | 192.168.40.1 | /26 | — | — |
| R1 servers | 192.168.50.1 | /29 | — | — |
| R1 tussen routers | 10.0.0.1 | /30 | — | — |
| R2 tussen routers | 10.0.0.2 | /30 | — | — |
| R2 tweede vestiging | 192.168.60.1 | /28 | — | — |
| Client W1 | 192.168.40.10 | /26 | 192.168.40.1 | 192.168.50.3 |
| Client W2 | 192.168.40.11 | /26 | 192.168.40.1 | 192.168.50.3 |
| Client V1 | 192.168.60.10 | /28 | 192.168.60.1 | 192.168.50.3 |
| Client V2 | 192.168.60.11 | /28 | 192.168.60.1 | 192.168.50.3 |
| Webserver | 192.168.50.2 | /29 | 192.168.50.1 | Optioneel voor deze dienst |
| DNS-server | 192.168.50.3 | /29 | 192.168.50.1 | — |

DNS-record: `www.project.test` → `192.168.50.2`. HTTP-service gestart; clientbrowsers gebruiken `http://www.project.test`.

### Handmatige routes

| Router | Bestemming | Masker | Next hop |
| --- | --- | --- | --- |
| R1 | 192.168.60.0 | 255.255.255.240 | 10.0.0.2 |
| R2 | 192.168.40.0 | 255.255.255.192 | 10.0.0.1 |
| R2 | 192.168.50.0 | 255.255.255.248 | 10.0.0.1 |

Automatische route-uitwisseling staat uit. Rechtstreeks aangesloten netwerken horen uit de interfaceconfiguratie bekend te zijn. Een passende standaardroute kan technisch werken, maar laat de leerling ook de gevraagde specifieke routes verklaren.

### Kern van de verklaringen

1. Bijvoorbeeld: de netwerklaag lost bereikbaarheid tussen netwerken op; IP bevat daarvoor adresinformatie en afspraken. De toepassingslaag verzorgt een dienst; HTTP bevat verzoek/antwoordafspraken voor webbronnen.
2. W1 adresseert het frame aan de MAC van `192.168.40.1`; het pakket blijft bestemd voor `192.168.50.2`.
3. De webserver gebruikt gateway `192.168.50.1`; R1 gebruikt voor `192.168.60.0/28` next hop `10.0.0.2`; R2 levert rechtstreeks in de vestiging af.
4. TCP-bestemmingspoort 80 en een tijdelijke clientpoort onderscheiden de webverbinding. Ping gebruikt ICMP, geen TCP-poorten.
5. HTTP is geen bewijs van TLS. TLS zou onder andere vertrouwelijkheid, integriteit en controle van de serveridentiteit toevoegen. Een certificaat is geen inhoudelijk keurmerk.
6. Private adressen worden niet rechtstreeks als publieke eindadressen gerouteerd. Gebruikelijke NAPT vertaalt intern bron-IP en bronpoort naar buitenadres en buitenpoort. Een firewall beslist apart welke communicatie mag plaatsvinden.

### Foutvarianten voor de individuele controle

Kies precies één verandering per kopie. Zorg eerst dat de ongewijzigde versie aantoonbaar werkt. Vertel alleen de klacht, niet de wijziging.

| Wijziging | Klacht | Passende onderscheidende controle | Herstel |
| --- | --- | --- | --- |
| Gateway van V1 naar onbestaande 192.168.60.14 | Lokale buren werken, verre bestemmingen niet | Eigen gatewayconfiguratie vergelijken; lokale bereikbaarheid aantonen; ARP voor .14 onderzoeken | Gateway terug naar .1 |
| DNS op W1 naar onbestaande 192.168.50.6 | Website op IP wel, op naam niet | IP versus naam vergelijken en DNS-doel controleren | DNS terug naar .3 |
| Route op R1 naar 192.168.60.0 verwijderen | W1 en V1 kunnen niet heen en weer, lokale diensten werken | Route naar vestiging onderzoeken, heen- en terugweg onderscheiden | Specifieke route via 10.0.0.2 herstellen |

Als een leerling een geldige alternatieve controle kiest, beoordeel de redenering. Beloon geen verplichte volgorde om de volgorde zelf. Laat niet een hele klas tegelijk aan hetzelfde gedeelde foutbestand werken: gebruik afzonderlijke kopieën.

### Scoringshouvast

Gebruik de zes categorieën van de leerlingrubric. Per categorie: volledig wanneer gevraagde werking én onderbouwing kloppen; ongeveer de helft wanneer een belangrijk deel correct is maar er nog een inhoudelijke fout of ontbrekend bewijs is; nul wanneer relevant werk ontbreekt of de kern niet klopt. Verdeel binnen de categorie naar de omvang van de aantoonbare prestatie.

Bij adressering kun je 8 punten voor subnetkeuze/grenzen, 8 voor interfaces en 4 voor consistentie reserveren. Routering: 8 voor topologie, 8 voor handmatige regels en 4 voor terugweg. Diensten: 5 voor DNS, 5 voor HTTP, 5 voor beide LAN's. Bewijs: 5 voor gerichte verwachtingen, 5 voor waarneming en 5 voor verklaring van wat die aantoont. Begrip: 4 per onderwerp lagen, ARP/adressen, routeverklaring, transport en beveiliging. Onderzoek: 3 voor hypotheses, 3 voor gekozen controle, 2 voor conclusie en 2 voor herstel/hertest.

Voorkom dubbele aftrek zonder onderscheid: een fout masker kan zowel een berekening als een werkende verbinding raken, maar geef nog punten voor een correct beredeneerde controle en juiste overige concepten. De school bepaalt de cijferomrekening en eventuele cesuur.

---


## Bronnen en inhoudelijke verantwoording

De uitleg is nieuw geschreven voor deze doelgroep. Bronnen dienen voor controle en verdere verdieping; de leerling hoeft deze technische documenten niet zelfstandig te lezen. Geen complete hoofdstukken uit externe boeken zijn overgenomen.

| Onderwerp | Primaire bron of officiële documentatie |
| --- | --- |
| Bestaande schrijfvorm en project | [Bronrepository van de website](https://github.com/informaticascw/informaticascw.github.io), met name de game-, webshop- en netwerkbestanden |
| MyST-opdrachten en antwoorden | [Exercises and Solutions](https://mystmd.org/guide/exercises) |
| Filius en beschikbare materialen | [Officiële downloadpagina](https://www.lernsoftware-filius.de/Herunterladen), [begeleidend materiaal](https://www.lernsoftware-filius.de/Begleitmaterial), [broncode](https://gitlab.com/filius1/filius) |
| IPv4 | [RFC 791](https://www.rfc-editor.org/rfc/rfc791) |
| CIDR/adresprefixen | [RFC 4632](https://www.rfc-editor.org/rfc/rfc4632) |
| ARP | [RFC 826](https://www.rfc-editor.org/rfc/rfc826) |
| Private adressen | [RFC 1918](https://www.rfc-editor.org/rfc/rfc1918) |
| Documentatieadressen | [RFC 5737](https://www.rfc-editor.org/rfc/rfc5737) |
| TCP | [RFC 9293](https://www.rfc-editor.org/rfc/rfc9293) |
| UDP | [RFC 768](https://www.rfc-editor.org/rfc/rfc768) |
| DNS | [RFC 1034](https://www.rfc-editor.org/rfc/rfc1034), [RFC 1035](https://www.rfc-editor.org/rfc/rfc1035) |
| HTTP-werking | [MDN: Overview of HTTP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Overview), [HTTP semantics, RFC 9110](https://www.rfc-editor.org/rfc/rfc9110) |
| NAT en NAPT | [RFC 3022](https://www.rfc-editor.org/rfc/rfc3022) |
| TLS | [TLS 1.3, RFC 8446](https://www.rfc-editor.org/rfc/rfc8446), inclusief verwijzingen naar updates op de bronpagina |
| QUIC en HTTP/3 | [RFC 9000](https://www.rfc-editor.org/rfc/rfc9000), [RFC 9114](https://www.rfc-editor.org/rfc/rfc9114) |
| DHCP | [RFC 2131](https://www.rfc-editor.org/rfc/rfc2131) |
| SMTP | [RFC 5321](https://www.rfc-editor.org/rfc/rfc5321) |
| Apparaatgegevens Chromebook | [Google Chromebook Help](https://support.google.com/chromebook/answer/1047420) |
| Apparaatgegevens Windows | [Microsoft ipconfig](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/ipconfig) |
| Apparaatgegevens Mac | [Apple netwerkinstellingen](https://support.apple.com/en-gb/guide/mac-help/mh11939/mac) |

### Grenzen van de module

Ethernet wordt uitgelegd als geschakeld lokaal netwerk; wifi is geen ‘Ethernet zonder kabel’ met identieke kanaaltoegang. Subnetten en broadcastdomeinen worden niet gelijkgesteld zonder de fysieke/logische scheiding te benoemen. MAC-adressen worden niet voorgesteld als onveranderlijke serienummers. Betrouwbaarheid van TCP is geen garantie bij een permanent verbroken verbinding en geen automatische versleuteling. Webverkeer wordt voor het model boven TCP uitgewerkt, met de uitzondering HTTP/3 expliciet benoemd.

Filius is een onderwijsmodel. De auteurswebsite en enkele broncodeonderdelen zijn geraadpleegd, maar de opstellingen zijn niet in deze omgeving daadwerkelijk in de GUI uitgevoerd. Broncode-inzage vervangt die praktische test niet. De relevante klassen voor verdere controle zijn onder andere `JWeiterleitungsTabelle`, `GUIApplicationWebServerWindow` en de netwerkstack in het Filius-project.

---


## Status

- De Filius-opstellingen en lestijden zijn nog niet praktisch getest. Er zijn geen geteste .fls-startbestanden bijgevoegd.
- De subnetberekeningen in de hoofdstukken en in de voorbeeldconfiguratie zijn met Python `ipaddress` gecontroleerd.
