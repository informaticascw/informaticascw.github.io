(netwerken-h05)=
# Routeren: doorsturen naar het juiste netwerk

## Inleiding

In hoofdstuk 4 gaf je computer een {term}`pakket <IP-pakket>` voor een ander netwerk aan de {term}`gateway`. Daarmee is het pakket er nog niet: ook die {term}`router` moet kiezen waar het naartoe gaat, eventueel naar een volgende router. Elke router beslist alleen over de eerstvolgende stap, met behulp van een {term}`routeringstabel`.

**Laag:** {term}`netwerklaag`. **Vraag:** hoe kiest een router de volgende stap naar een bestemmingsnetwerk, en wat is nodig om ook het antwoord terug te laten komen?

Je breidt je netwerk uit met een tweede router en een derde {term}`LAN`, vult handmatig routeringstabellen in en controleert zowel de heenweg als de terugweg.

## Klassikaal: routers die alleen de volgende stap kennen

Verdeel de klas over drie netwerken en twee routers. Elke router krijgt alleen een eigen routeringstabel, geen plattegrond van het hele netwerk. Leerlingen sturen kaartjes met een bestemmingsnetwerk. De router kiest een volgende stap en mag niets bij de andere router navragen.

1. Stuur een bericht van links naar rechts terwijl de eerste router nog geen route naar rechts heeft. Het bericht blijft liggen.
2. Voeg de ontbrekende route toe. Laat de ontvanger nu antwoorden terwijl de tweede router nog geen route terug heeft. Ook het antwoord blijft liggen.
3. Voeg die route ook toe. Nu komt het antwoord aan.

Bespreek waarom een geslaagde heenweg nog geen geslaagde communicatie is. Gebruik voor de kaartjes de netwerken en routes uit de tabellen hieronder.

## Een tabel met bestemmingsnetwerken

Een router zoekt het IP-adres van de bestemming op in zijn routeringstabel. Een regel bevat een bestemmingsnetwerk, een {term}`masker <subnetmasker>` en de volgende stap: een rechtstreeks aangesloten netwerk of een andere router, de {term}`next hop`. De next hop moet rechtstreeks bereikbaar zijn. Een router stuurt niet naar een router waarvan hij alleen het adres kent maar die ergens ver weg staat.

### Een tweede router en een derde LAN

```{figure} images/routering.svg
:alt: De drie LANs en het aparte verbindingsnetwerk tussen R1 en R2.

De drie LANs en het aparte verbindingsnetwerk tussen R1 en R2.
```

We breiden het netwerk uit hoofdstuk 4 uit met een tweede router en een derde LAN. Er zijn vier subnetten, want ook het verbindingsnetwerk tussen de routers is een subnet.

| Netwerk | Aansluitingen |
| --- | --- |
| Links: 192.168.10.0/24 | A `.10`; R1 `.1` |
| Midden: 192.168.20.0/24 | C `.10`; R1 `.1` |
| Tussen routers: 10.0.0.0/30 | R1 `10.0.0.1`; R2 `10.0.0.2` |
| Rechts: 192.168.30.0/24 | D `.10`; R2 `.1` |

R1 heeft drie aansluitingen en R2 twee. A gebruikt gateway `192.168.10.1`, C `192.168.20.1` en D `192.168.30.1`.

| Router | Bestemming | Volgende stap |
| --- | --- | --- |
| R1 | 192.168.10.0/24 | Rechtstreeks aangesloten |
| R1 | 192.168.20.0/24 | Rechtstreeks aangesloten |
| R1 | 10.0.0.0/30 | Rechtstreeks aangesloten |
| R1 | 192.168.30.0/24 | Via 10.0.0.2 |
| R2 | 192.168.30.0/24 | Rechtstreeks aangesloten |
| R2 | 10.0.0.0/30 | Rechtstreeks aangesloten |
| R2 | 192.168.10.0/24 | Via 10.0.0.1 |
| R2 | 192.168.20.0/24 | Via 10.0.0.1 |

Rechtstreeks aangesloten netwerken kent een router uit de instellingen van zijn aansluitingen. Daarvoor hoef je geen next-hopregels toe te voegen.

::: {exercise} Zonder Filius: volg de route
:label: nw05-o1

1. A verstuurt naar D. Geef de opeenvolgende ontvangers vanaf A.
2. Welk bron- en bestemmings-IP-adres staan in het pakket tussen R1 en R2? Er is geen {term}`NAT`.
3. Welke handmatige regel heeft R2 nodig voor het antwoord aan A?
4. Waarom kan R1 voor netwerk `192.168.30.0/24` niet D als next hop invullen?
:::

::: {solution} nw05-o1
:class: dropdown

1. Eerst R1, dan R2, dan D.
2. Bron `192.168.10.10`, bestemming `192.168.30.10`.
3. `192.168.10.0/24` via `10.0.0.1`.
4. D ligt niet in een subnet waarop R1 rechtstreeks is aangesloten. R1 moet eerst een router sturen die hij wel rechtstreeks kan bereiken.
:::

## Meest specifieke route en standaardroute

Een router kan een {term}`standaardroute` hebben: `0.0.0.0/0`. Die wordt gebruikt als geen specifiekere route past. Passen meerdere regels, dan wint de meest specifieke, dus die met de langste prefix. Een /24 beschrijft minder adressen dan een /16 en is dus specifieker.

Routers kunnen routes automatisch uitwisselen met routeringsprotocollen. In deze module stel je routes handmatig in en behandelen we die protocollen niet.

::: {exercise} Zonder Filius: welke regel wint?
:label: nw05-o2

Een router heeft `10.0.0.0/8 via X`, `10.2.0.0/16 via Y` en `0.0.0.0/0 via Z`. Bepaal de volgende stap voor `10.2.8.4`, `10.3.8.4` en `203.0.113.8`.
:::

::: {solution} nw05-o2
:class: dropdown

`10.2.8.4` gaat via Y: /16 is het meest specifiek. `10.3.8.4` gaat via X: /8 past en /16 niet. `203.0.113.8` gaat via Z: alleen de standaardroute past. X, Y en Z zijn hier rechtstreeks bereikbare next hops.
:::

::: {exercise} Filius: een tweede router toevoegen
:label: nw05-o3

1. Open een kopie van je netwerk uit hoofdstuk 4 en bouw de uitbreiding uit de tabellen. Gebruik voor het verbindingsnetwerk masker `255.255.255.252`.
2. Schakel automatische {term}`routering` op de routers uit, als die aanstaat. Open de tabel voor handmatige routes.
3. Voeg eerst alleen op R1 de route naar `192.168.30.0` met masker `255.255.255.0` via `10.0.0.2` toe. Test A→D. Bereikt het verzoek D? Waarom ontbreekt het antwoord nog?
4. Voeg op R2 de twee ontbrekende routes naar links en midden toe. Test A↔D en C↔D.
5. Bewaar als `05-routering.fls`. Noteer je ingestelde regels en leg van één ping de heen- en terugweg uit.
:::

::: {solution} nw05-o3
:class: dropdown

Met alleen de route op R1 kan het verzoek D bereiken, maar R2 weet niet hoe het antwoord bij A komt. Na het toevoegen van beide terugroutes werkt het verkeer in beide richtingen. De aansluitingen en gateways moeten ook kloppen. Gebruik als next hop het adres van de router op het verbindingsnetwerk, niet een adres aan de andere kant van die router.
:::

## Eigen netwerk: een route is geen rechte kabel

Op Windows gebruik je `tracert stanislas.informatica.nu` en op een Mac in Terminal `traceroute stanislas.informatica.nu`. Op school kunnen deze opdrachten geblokkeerd zijn; de docent kan dan een eigen resultaat laten zien. Op een Chromebook hoef je niets te installeren.

Deze opdrachten sturen berichten waarvan de {term}`TTL` stap voor stap oploopt, waardoor de tussenliggende routers zich melden. Een sterretje bewijst niet dat de route kapot is: een router kan doorsturen zonder op meetberichten te antwoorden. De heen- en terugroute kunnen verschillen. De wachttijd bij één stap is bovendien niet de tijd van alleen dat stuk kabel.
