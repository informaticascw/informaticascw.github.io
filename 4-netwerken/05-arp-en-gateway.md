---
title: ARP en de standaardgateway
---

(netwerken-arp-gateway)=
# ARP en de standaardgateway

## Inleiding

Je weet nu of twee {term}`IP-adressen <IP-adres>` in hetzelfde {term}`subnet` liggen. Je weet ook dat een {term}`Ethernetframe <frame>` een {term}`MAC-adres` als bestemming heeft. Daarmee ontbreekt nog één stap: een programma geeft een IP-bestemming op, maar de netwerkinterface moet een frame met een lokaal MAC-adres versturen.

**Hoofdvraag:** welk lokaal MAC-adres is nodig bij deze IP-bestemming, en hoe vindt de afzender dat adres?

We kiezen eerst de volgende ontvanger: het eindapparaat in het eigen subnet of de {term}`gateway` voor een ander subnet. Daarna gebruiken we {term}`ARP` om bij dat lokale IP-adres het MAC-adres te vinden. In de volgende voorbeelden zie je waarom het IP-eindadres en het lokale frameadres niet altijd naar hetzelfde apparaat wijzen.

## Rechtstreeks of via de gateway?

```{figure} images/twee-lans.svg
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
