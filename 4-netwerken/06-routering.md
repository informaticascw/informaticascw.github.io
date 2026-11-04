(netwerken-les06)=
# Door meerdere netwerken

## Inleiding

Je computer kan een {term}`pakket <IP-pakket>` buiten het eigen {term}`subnet` aan de {term}`gateway` geven. Daarmee is de route nog niet compleet: ook die {term}`router` moet een volgende stap kiezen. We breiden ons netwerk uit met een tweede router en een derde lokaal netwerk.

**Laag:** {term}`netwerklaag`. **Hoofdvraag:** hoe kiest iedere router een bereikbare volgende stap voor het bestemmingsnetwerk?

Je leest en vult handmatige {term}`routeringstabellen <routeringstabel>`. Daarna controleer je niet alleen de heenweg, maar ook de terugweg.

## Klassikaal: iedere tussenpersoon kent alleen de volgende stap

Verdeel de klas over drie netwerken en twee routers. Geef iedere router alleen een lokale routetabel, geen volledige plattegrond. Leerlingen versturen kaartjes met een bestemmingsnetwerk. Iedere router moet een volgende stap kiezen en mag geen informatie bij de andere router opvragen.

Laat eerst een bericht van links naar rechts gaan terwijl de eerste router geen route naar rechts heeft. Het bericht blijft liggen. Voeg de ontbrekende route toe. Laat de ontvanger nu antwoorden terwijl de tweede router nog geen route terug heeft. Voeg die ook toe. Pas dan komt het antwoord aan.

Bespreek waarom één succesvolle heenweg nog geen geslaagd gesprek is. Gebruik voor de kaarten de netwerken en routes uit de tabellen hieronder.

## Een tabel met bestemmingsnetwerken

Een router zoekt het bestemmings-IP-adres op in zijn routeringstabel. Een regel bevat een bestemmingsnetwerk, een {term}`masker <subnetmasker>` en informatie over de volgende stap: rechtstreeks via een aansluiting of via een andere router, de {term}`next hop`.

De next hop moet rechtstreeks bereikbaar zijn. Een router stuurt niet zomaar naar een willekeurig verre router waarvan hij alleen het adres kent.

### Onze opstelling

```{figure} images/routering.svg
:alt: De drie LANs en het aparte verbindingsnetwerk tussen R1 en R2.

De drie LANs en het aparte verbindingsnetwerk tussen R1 en R2.
```

We breiden de router uit les 5 uit met een tweede router en een derde {term}`LAN`. Er zijn vier subnetten; het verbindingsnetwerk tussen de routers is er ook één.

| Netwerk | Aansluitingen |
| --- | --- |
| Links: 192.168.10.0/24 | A `.10`; R1 `.1` |
| Midden: 192.168.20.0/24 | C `.10`; R1 `.1` |
| Tussen routers: 10.0.0.0/30 | R1 `10.0.0.1`; R2 `10.0.0.2` |
| Rechts: 192.168.30.0/24 | D `.10`; R2 `.1` |

R1 heeft drie interfaces nodig. R2 heeft er twee. A gebruikt gateway `192.168.10.1`, C `192.168.20.1` en D `192.168.30.1`.

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

Rechtstreeks aangesloten netwerken zijn normaal vanuit de interfaceconfiguratie bekend; je hoeft daarvoor niet dezelfde handmatige next-hopregels toe te voegen.

::: {exercise} Zonder Filius: volg de route
:label: nw06-o1

1. A verstuurt naar D. Geef achtereenvolgens de volgende ontvangers vanaf A.
2. Welk bron- en bestemmings-IP-adres staan in het pakket tussen R1 en R2? Er is geen {term}`NAT`.
3. Welke handmatige regel heeft R2 nodig voor het antwoord aan A?
4. Waarom kan R1 voor netwerk `192.168.30.0/24` niet simpelweg D als next hop invullen?
:::

::: {solution} nw06-o1
:class: dropdown

1. Eerst R1, dan R2, dan D.
2. Bron `192.168.10.10`, bestemming `192.168.30.10`.
3. `192.168.10.0/24` via `10.0.0.1`.
4. D ligt niet op een rechtstreeks verbonden subnet van R1. R1 moet eerst een lokaal bereikbare volgende router aanspreken.
:::

## Specifiek of standaard?

Een router kan een {term}`standaardroute` hebben: `0.0.0.0/0`. Die wordt gebruikt als geen specifiekere route past. Passen meerdere regels, dan wint de meest specifieke: de langste passende prefix. Een /24 beschrijft minder adressen en is specifieker dan een /16.

Routers kunnen routes automatisch uitwisselen met routeringsprotocollen. In deze module stellen we enkele routes handmatig in. We behandelen de interne werking van zulke routeringsprotocollen niet.

::: {exercise} Zonder Filius: welke regel wint?
:label: nw06-o2

Een router heeft `10.0.0.0/8 via X`, `10.2.0.0/16 via Y` en `0.0.0.0/0 via Z`.

Bepaal de volgende stap voor `10.2.8.4`, `10.3.8.4` en `203.0.113.8`.
:::

::: {solution} nw06-o2
:class: dropdown

`10.2.8.4` via Y: /16 is het specifiekst. `10.3.8.4` via X: /8 past en /16 niet. `203.0.113.8` via Z: alleen de standaardroute past. De letters stellen hier rechtstreeks bereikbare next hops voor.
:::

::: {exercise} Filius: voeg een router toe
:label: nw06-o3

1. Open een kopie van je netwerk uit les 5. Bouw de uitbreiding uit de tabellen. Gebruik voor het verbindingsnetwerk masker `255.255.255.252`.
2. Schakel automatische {term}`routering` uit op de routers, als die aanstaat. Open de tabel voor handmatige routes.
3. Voeg eerst alleen op R1 de route naar `192.168.30.0` met masker `255.255.255.0` via `10.0.0.2` toe. Test A→D. Bekijk of het verzoek D kan bereiken en waarom een antwoord nog kan ontbreken.
4. Voeg op R2 de twee ontbrekende routes naar links en midden toe. Test A↔D en C↔D.
5. Bewaar als `06-routering.fls`. Noteer je ingestelde regels en leg van één ping heen- en terugweg uit.
:::

::: {solution} nw06-o3
:class: dropdown

Alleen de route op R1 geeft R2 nog geen route naar A. Na toevoegen van beide terugroutes kan het verkeer in beide richtingen door de opstelling. De interfaces en gateways moeten eveneens correct zijn. Noteer bij de handmatige regels de next-hopadressen van het verbindingsnetwerk, niet de LAN-adressen aan de verre kant.
:::

## In het echt: een route is geen rechte kabel

Op Windows kun je `tracert stanislas.informatica.nu` gebruiken, op een Mac in Terminal `traceroute stanislas.informatica.nu`. Op school kunnen deze opdrachten beperkt zijn; de docent kan ook een eigen resultaat laten zien. Je hoeft dit niet te installeren op een Chromebook.

De opdrachten proberen tussenliggende routers zichtbaar te maken met berichten waarvan de levensduur stapsgewijs toeneemt. Een sterretje is geen bewijs van een kapotte route: een router kan wel doorsturen maar niet op de meetberichten antwoorden. De heen- en terugroute kunnen bovendien verschillen. De wachttijd bij één hop is niet simpelweg de tijd van alleen dat kabelstuk.
