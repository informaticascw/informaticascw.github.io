---
title: ARP en de standaardgateway
---

(netwerken-h05)=
# ARP en de standaardgateway

## Inleiding

Een programma geeft een IP-adres op als bestemming, maar een {term}`Ethernetframe <frame>` heeft een {term}`MAC-adres` als bestemming nodig. De computer moet dus twee dingen doen. Eerst bepaalt hij met het {term}`subnetmasker` welk apparaat op zijn eigen netwerk het pakket als eerste moet ontvangen: de bestemming zelf of de {term}`gateway`. Daarna zoekt hij met {term}`ARP` het MAC-adres van dat apparaat.

**Laag:** de overgang van netwerklaag naar datalinklaag. **Vraag:** naar welk apparaat stuurt een computer een pakket, en hoe vindt hij daarvan het MAC-adres?

## Rechtstreeks of via de gateway?

```{figure} images/twee-lans.svg
:alt: Twee lokale Ethernetnetwerken met ieder een eigen switch en een router ertussen.

Twee lokale Ethernetnetwerken met een router ertussen.
```

We gebruiken twee afzonderlijke Ethernetnetwerken, elk met een eigen {term}`switch`. Een {term}`router` verbindt ze. De router heeft op elk netwerk een eigen aansluiting met een eigen IP-adres en MAC-adres.

| Apparaat | Aansluiting | IP-adres | Subnetmasker | Standaardgateway |
| --- | --- | --- | --- | --- |
| Computer A | Linker netwerk | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| Computer B | Linker netwerk | 192.168.10.20 | 255.255.255.0 | 192.168.10.1 |
| Router | Linker netwerk | 192.168.10.1 | 255.255.255.0 | — |
| Router | Rechter netwerk | 192.168.20.1 | 255.255.255.0 | — |
| Computer C | Rechter netwerk | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |

Computer A wil gegevens versturen en bepaalt met zijn masker of de bestemming in zijn eigen subnet ligt.

- **Binnen het eigen subnet:** A stuurt rechtstreeks naar de bestemming.
- **Buiten het eigen subnet:** A stuurt naar een router. Daarvoor gebruikt A de standaardgateway.

De standaardgateway is dus het IP-adres van een routeraansluiting in het eigen subnet. In dit hoofdstuk stellen we geen extra routes in op de computers.

### Voorbeeld: van A naar B

A heeft {term}`netwerkadres` `192.168.10.0`. Met het masker van A heeft het adres van B hetzelfde netwerkadres. A kan B dus rechtstreeks bereiken, zonder router.

### Voorbeeld: van A naar C

Met het masker van A heeft het adres van C netwerkadres `192.168.20.0`. Dat is een ander subnet, dus A levert de gegevens af bij gateway `192.168.10.1`.

::: {exercise} Zonder Filius: welke volgende ontvanger?
:label: nw05-o1

Gebruik de instellingen van computer A uit de tabel.

1. Bepaal voor elke bestemming of A rechtstreeks verstuurt of de gateway gebruikt: `192.168.10.50`, `192.168.20.10` en `192.168.11.10`.
2. Waarom kan A niet `192.168.20.1` als standaardgateway gebruiken?
3. Een leerling zegt: ‘De eerste twee getallen van de IP-adressen zijn gelijk, dus de computers zitten in hetzelfde subnet.’ Weerleg dat met een bestemming uit vraag 1.
:::

::: {solution} nw05-o1
:class: dropdown

1. `192.168.10.50`: rechtstreeks. De andere twee: via `192.168.10.1`.
2. De gateway moet rechtstreeks bereikbaar zijn in het eigen subnet. `192.168.20.1` zit op het andere Ethernetnetwerk.
3. Bij `192.168.11.10` zijn de eerste twee getallen gelijk, maar bij masker `255.255.255.0` hoort ook het derde getal bij het {term}`netwerkdeel`. Dat adres ligt dus in een ander subnet.
:::

::: {exercise} Filius: bouwen en voorspellen
:label: nw05-o2

1. Bouw de opstelling uit de tabel: A en B op de linker switch, C op de rechter switch en een router tussen de switches. Gebruik een gewone router met twee aansluitingen.
2. Stel de IP-adressen en subnetmaskers in. Laat de standaardgateway op de computers voorlopig leeg en gebruik geen automatische adresuitgifte.
3. Voorspel of A met `ping` B en C kan bereiken en schrijf bij beide een reden op.
4. Start de simulatie, installeer op A de opdrachtregel en test `ping 192.168.10.20` en `ping 192.168.20.10`.
5. Vergelijk je waarnemingen met je voorspellingen.
6. Stel op A, B en C de gateways uit de tabel in en test opnieuw. Verklaar wat er verandert.

Bewaar je netwerk. Je gebruikt het in de volgende opdrachten opnieuw.
:::

::: {solution} nw05-o2
:class: dropdown

Zonder gateway kan A wel B bereiken, maar C niet. Met de juiste gateways kan het verkeer heen en terug tussen A en C lopen. De router kent beide netwerken via zijn eigen aansluitingen. Een switch heeft hiervoor geen IP-configuratie nodig.
:::

## ARP: het MAC-adres bij een IP-adres vinden

A weet nu dat B rechtstreeks bereikbaar is. In het Ethernetframe moet echter een MAC-adres staan, en A kent alleen het IP-adres van B. Het eigen MAC-adres kent A al via zijn netwerkinterface. Het MAC-adres van de ontvanger vindt hij met ARP, het Address Resolution Protocol:

1. A zoekt in zijn {term}`ARP-cache`: een tijdelijke tabel met IP-adressen en bijbehorende MAC-adressen.
2. Staat B er niet in, dan verstuurt A een {term}`ARP-request`: ‘Wie heeft IP-adres 192.168.10.20? Meld je bij 192.168.10.10.’
3. Dit request zit in een Ethernetframe met {term}`broadcastadres` `ff:ff:ff:ff:ff:ff`. De switch verspreidt het over alle andere aansluitingen van het lokale netwerk.
4. B herkent zijn eigen IP-adres en stuurt een {term}`ARP-reply` rechtstreeks naar A, met daarin zijn MAC-adres.
5. A bewaart de koppeling tijdelijk in zijn ARP-cache en kan het {term}`IP-pakket` in een frame naar B versturen.

Andere apparaten ontvangen het request ook, maar antwoorden niet. De router stuurt het ARP-request niet door naar het rechter netwerk.

::: {note} ARP en de lagen

IP regelt adressering tussen netwerken en Ethernet de aflevering op het lokale netwerk. ARP verbindt die twee: het zoekt bij een lokaal IP-adres het MAC-adres. Een ARP-bericht zit rechtstreeks in een Ethernetframe, niet in een IP-pakket.
:::

### Voorbeeld: de adressen in een lokaal bericht

In de voorbeelden gebruiken we deze MAC-adressen. Filius kent zelf andere adressen toe.

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
:label: nw05-o3

De ARP-cache van A is leeg. A wil een IP-pakket naar B sturen.

1. Schrijf de vraag uit het ARP-request op.
2. Geef het bron- en bestemmings-MAC-adres van het frame met dat request.
3. Welke apparaten ontvangen het request: B, de linker routeraansluiting en/of C?
4. Wie antwoordt? Is dat antwoord een {term}`broadcast`?
5. Waarom is niet voor elk volgend IP-pakket een nieuwe broadcast nodig?
:::

::: {solution} nw05-o3
:class: dropdown

1. Wie heeft `192.168.10.20`? Meld je bij `192.168.10.10`.
2. Bron `02:00:00:00:10:0a`, bestemming `ff:ff:ff:ff:ff:ff`.
3. B en de linker routeraansluiting. C niet.
4. B antwoordt rechtstreeks aan het MAC-adres van A. Dat is {term}`unicast`, geen broadcast.
5. A bewaart de koppeling tijdelijk in de ARP-cache.
:::

::: {exercise} Filius: ARP waarnemen
:label: nw05-o4

1. Start de simulatie opnieuw en open bij A het venster met de gegevensuitwisseling (via het contextmenu van de computer; de naam kan per taalversie verschillen).
2. Ping B en zoek in de gegevensuitwisseling naar ARP.
3. Noteer uit het request het gezochte IP-adres en het bestemmings-MAC-adres, en uit het reply het gevonden MAC-adres.
4. Ping B direct opnieuw. Is er weer ARP nodig? Onderbouw met wat je ziet.
5. Leg uit waarom ‘bij elke ping gaat eerst een ARP-request uit’ geen goede regel is.
:::

::: {solution} nw05-o4
:class: dropdown

Het request vraagt naar het IP-adres van B en gaat naar het Ethernetbroadcastadres. Het reply bevat het MAC-adres van B. Bij een directe herhaling is normaal geen nieuw ARP nodig, omdat de koppeling nog in de cache staat. Vergelijk deze verklaring met je eigen waarnemingen.
:::

## Via de gateway naar een ander netwerk

A wil een IP-pakket naar C sturen. C ligt buiten het eigen subnet, dus A levert het pakket eerst af bij zijn gateway.

**A zoekt met ARP het MAC-adres van de gateway, niet dat van C.** De gateway ligt op hetzelfde Ethernetnetwerk als A, C niet.

Het IP-pakket blijft aan C gericht. Alleen het Ethernetframe is aan de router gericht.

### Voorbeeld: van A via de router naar C

| Verbinding | Bron-MAC | Bestemmings-MAC | Bron-IP | Bestemmings-IP |
| --- | --- | --- | --- | --- |
| A naar router | A | Router links | 192.168.10.10 | 192.168.20.10 |
| Router naar C | Router rechts | C | 192.168.10.10 | 192.168.20.10 |

De router haalt het IP-pakket uit het frame en bepaalt via welke aansluiting de bestemming bereikbaar is. Op het rechter netwerk maakt hij een nieuw frame. Kent hij het MAC-adres van C nog niet, dan gebruikt hij daar zelf eerst ARP.

De IP-adressen blijven gelijk, omdat we hier geen {term}`NAT` gebruiken. Het frame wordt per verbinding vervangen; het IP-pakket gaat verder naar zijn bestemming.

::: {exercise} Zonder Filius: volg het antwoord
:label: nw05-o5

C stuurt een antwoord naar A. Ga ervan uit dat alle benodigde ARP-koppelingen bekend zijn.

1. Maak voor de terugweg dezelfde tabel als in het voorbeeld.
2. Een leerling zegt: ‘A zet het IP-adres van de gateway als bestemming in het IP-pakket, want daar moet het pakket eerst naartoe.’ Verbeter dat.
3. Naar welk IP-adres vraagt A met ARP voordat hij naar C kan versturen? Waarom niet naar het IP-adres van C?
:::

::: {solution} nw05-o5
:class: dropdown

1.

   | Verbinding | Bron-MAC | Bestemmings-MAC | Bron-IP | Bestemmings-IP |
   | --- | --- | --- | --- | --- |
   | C naar router | C | Router rechts | 192.168.20.10 | 192.168.10.10 |
   | Router naar A | Router links | A | 192.168.20.10 | 192.168.10.10 |

2. Het bestemmings-IP-adres blijft dat van de eindbestemming. Alleen het bestemmings-MAC-adres in het frame is dat van de gateway.
3. A vraagt naar `192.168.10.1`. C ligt buiten het lokale netwerk van A en ontvangt het ARP-request niet.
:::

::: {exercise} Filius: twee soorten adressen
:label: nw05-o6

1. Start de simulatie opnieuw en open de gegevensuitwisseling bij A en bij de router.
2. Ping vanaf A naar C.
3. Zoek het ARP-request van A. Vraagt A naar het adres van C of naar dat van de gateway?
4. Zoek het IP-pakket van A naar C. Noteer het bestemmings-IP-adres en het bestemmings-MAC-adres van het frame waarin het zit.
5. Bekijk hoe de router het pakket naar C verstuurt. Welke adressen veranderen en welke blijven gelijk?
6. Leg uit waarom zowel een IP-adres als een MAC-adres nodig is.
:::

::: {solution} nw05-o6
:class: dropdown

A vraagt naar `192.168.10.1`. Het IP-pakket gaat naar `192.168.20.10`, in een frame naar de linker routeraansluiting. Op de volgende verbinding veranderen beide MAC-adressen; bron- en bestemmings-IP blijven gelijk. De router kan op het rechter netwerk zelf ARP gebruiken om C te vinden. Bij een herhaling is niet altijd nieuw ARP nodig.
:::

## Eigen apparaat: IP-adres, MAC-adres en gateway

De soorten adressen uit Filius staan ook op je eigen computer. Een computer kan meerdere netwerkadapters hebben, bijvoorbeeld voor {term}`wifi` en voor Ethernet.

::: {exercise} Eigen apparaat: vind je IP-adres, MAC-adres en gateway
:label: nw05-o7

1. Open de netwerkgegevens met de aanwijzingen hieronder.
2. Noteer van je actieve verbinding het IPv4-adres, het subnetmasker (of de {term}`prefixlengte <CIDR-prefix>`), het MAC-adres en de standaardgateway. De gateway kan ook ‘router’ heten.
3. Bepaal met het masker of je gateway in jouw subnet ligt. Schrijf je berekening op. Ga niet zonder controle uit van `/24`.
4. Vergelijk met een klasgenoot: hebben jullie hetzelfde IP-adres, MAC-adres en dezelfde gateway? Wat verwacht je als jullie in hetzelfde subnet zitten?
5. Stel dat je een website buiten je subnet bezoekt en de benodigde ARP-koppeling nog niet bekend is. Naar welk adres vraagt je computer dan met ARP?

**Chromebook:** open Instellingen → Netwerk → Wifi en kies je verbonden netwerk. In de netwerkdetails staan de IP-configuratie en de gateway, en ook het MAC-adres van de wifi-adapter. Je kunt ook het netwerkmenu rechtsonder en het informatiepictogram gebruiken. Op een beheerd apparaat kunnen details verborgen zijn.

**Windows:** open de Opdrachtprompt en voer `ipconfig /all` uit. Zoek bij de actieve wifi- of Ethernetadapter het IPv4-adres, het subnetmasker, de standaardgateway en het fysieke adres. Het fysieke adres is het MAC-adres. Sla adapters over waarbij staat dat de verbinding is verbroken.

**Mac:** open Systeeminstellingen → Netwerk → de actieve verbinding → Details. Bij TCP/IP staan het IPv4-adres, het subnetmasker en de router. Het MAC-adres staat bij Hardware of in de wifi-details.

Verander geen instellingen. Kun je de gegevens niet zien, gebruik dan het voorbeeld hieronder en vergelijk dat met een apparaat waarop het wel kan.

**Voorbeeld (geen meting van het schoolnetwerk):**

```text
IPv4-adres        192.168.10.37
Subnetmasker      255.255.255.0
Standaardgateway  192.168.10.1
MAC-adres         02:00:00:00:10:25
```
:::

::: {solution} nw05-o7
:class: dropdown

Je waarden hangen af van je verbinding. In het voorbeeld hebben zowel `192.168.10.37` als de gateway `192.168.10.1` met het masker netwerkadres `192.168.10.0`, dus de gateway ligt in hetzelfde subnet.

Klasgenoten in hetzelfde subnet hebben verschillende IPv4-adressen en normaal ook verschillende MAC-adressen. Meestal hebben ze dezelfde gateway. Dezelfde wifinaam bewijst niet dat jullie in hetzelfde subnet zitten.

Voor een website buiten het eigen subnet zoekt de computer met ARP het MAC-adres van de gateway, niet dat van de website. Op wifi kan het MAC-adres privaat of willekeurig zijn. Een MAC-adres is dus niet altijd een vast serienummer van de computer.
:::
