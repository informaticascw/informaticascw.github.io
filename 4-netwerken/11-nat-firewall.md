(netwerken-h11)=
# NAT en firewall

## Inleiding

Thuis delen meerdere apparaten vaak één publiek IPv4-adres. Je wilt ook niet dat onbekenden van buiten zomaar een verbinding met je apparaten beginnen. Dat zijn twee verschillende problemen met twee verschillende oplossingen: adresvertaling met {term}`NAT` en filteren met een {term}`firewall`. Een oplossing voor één probleem lost het andere niet op.

**Lagen:** netwerk en transport. **Vraag:** hoe kunnen meerdere apparaten één publiek adres delen, en wie bepaalt welk verkeer binnenkomt?

## Klassikaal: één buitenadres voor meerdere clients

Maak drie rollen: twee interne {term}`clients <client>`, een grensrouter en een externe {term}`server`. Beide clients sturen een bericht naar dezelfde server. Op hun kaartjes staan een intern IP-adres en een {term}`bronpoort <poortnummer>`. De grensrouter heeft één buitenadres en een lijst met beschikbare buitenpoorten.

1. Laat beide berichten naar buiten gaan met hetzelfde buitenadres én dezelfde buitenpoort. Stuur de antwoorden van de server terug. De router kan niet bepalen voor welke client een antwoord is.
2. Laat de {term}`router` nu bij elke verbinding een eigen buitenpoort kiezen en de koppeling opschrijven. De antwoorden kunnen nu bij de juiste client komen.
3. Geef de router een regelkaart: ‘nieuwe verbindingen van buiten alleen naar de gepubliceerde webserver; antwoorden bij bestaande verbindingen wel doorlaten’. Laat de externe server een ongevraagd nieuw bericht sturen.

Bespreek welke beslissing over vertalen gaat en welke over toelaten.

## Private adressen

Voor intern gebruik zijn drie IPv4-reeksen gereserveerd:

| Reeks | Prefix |
| --- | --- |
| 10.0.0.0 tot 10.255.255.255 | 10.0.0.0/8 |
| 172.16.0.0 tot 172.31.255.255 | 172.16.0.0/12 |
| 192.168.0.0 tot 192.168.255.255 | 192.168.0.0/16 |

Organisaties mogen dezelfde {term}`private adressen <privaat IP-adres>` intern gebruiken. Die adressen zijn niet wereldwijd uniek en worden op het {term}`internet` niet doorgestuurd. Niet elk adres buiten deze reeksen is automatisch een bruikbaar {term}`publiek adres <publiek IP-adres>`: er zijn nog andere gereserveerde reeksen.

## NAT: adressen en poorten vertalen

Bij veel thuisnetwerken vervangt de router bij uitgaand verkeer het interne bronadres en meestal ook de bronpoort. Dat heet NAT; deze variant heet precies {term}`NAPT` of PAT. De router onthoudt welke koppeling bij welke verbinding hoort en vertaalt de antwoorden terug.

### Voorbeeld

De buitenadressen hieronder zijn documentatieadressen.

| Intern | Naar buiten vertaald | Server |
| --- | --- | --- |
| 192.168.10.10:51000 | 203.0.113.5:40001 | 198.51.100.20:443 |
| 192.168.10.20:51000 | 203.0.113.5:40002 | 198.51.100.20:443 |

Beide clients gebruiken dezelfde interne bronpoort, maar krijgen een andere buitenpoort. Een antwoord naar buitenpoort 40002 gaat terug naar de tweede client.

NAT vervangt {term}`routering` niet: na het vertalen moet het {term}`pakket <IP-pakket>` nog steeds worden doorgestuurd. NAT versleutelt ook niets. Onze Filius-netwerken gebruiken private adressen zonder NAT; in zo’n afgesloten netwerk is gewone routering genoeg.

::: {exercise} Zonder Filius: de vertaling volgen
:label: nw11-o1

1. Bij welke client hoort een antwoord naar `203.0.113.5:40001`?
2. Waarom zou de router buitenpoort 40001 niet ook voor de tweede verbinding naar dezelfde server gebruiken?
3. Is `172.40.2.8` een privaat adres? En `172.20.2.8`?
:::

::: {solution} nw11-o1
:class: dropdown

1. `192.168.10.10:51000`.
2. Dan zijn de twee verbindingen aan de buitenkant niet meer te onderscheiden. Elke verbinding krijgt daarom een eigen buitenpoort.
3. `172.40.2.8` niet; `172.20.2.8` wel. De private 172-reeks loopt van 172.16 tot en met 172.31.
:::

## Firewall: wel of niet toelaten?

Een firewall bepaalt aan de hand van regels welk verkeer wordt doorgelaten. De regels kunnen kijken naar bron en bestemming, {term}`protocol`, poorten en de toestand van een verbinding. Een stateful firewall herkent antwoorden bij een toegestane verbinding.

Een router stuurt door, NAT vertaalt en een firewall filtert. Die taken zitten vaak in één apparaat, maar het blijven verschillende beslissingen. Een firewall die {term}`TCP` naar poort 443 toestaat, beoordeelt daarmee niet of een website betrouwbaar is.

::: {exercise} Zonder Filius: de regels toepassen
:label: nw11-o2

Een stateful firewall past deze regels in volgorde toe: (1) antwoorden bij toegestane verbindingen toelaten; (2) interne clients nieuwe TCP-verbindingen naar externe poort 443 laten beginnen; (3) alle andere nieuwe verbindingen blokkeren.

1. Mag een interne browser een nieuwe verbinding naar externe poort 443 starten?
2. Mag het antwoord terug naar de tijdelijke clientpoort?
3. Mag een externe computer ongevraagd een nieuwe verbinding naar een interne client beginnen?
4. Versleutelt deze firewall het verkeer?
:::

::: {solution} nw11-o2
:class: dropdown

1. Ja, volgens regel 2.
2. Ja, omdat het bij de toegestane verbinding hoort (regel 1).
3. Nee, volgens regel 3.
4. Nee. Filteren en versleutelen zijn verschillende taken.
:::

::: {exercise} Filius: wat laat het model zien?
:label: nw11-o3

1. Open je HTTP-website uit hoofdstuk 8 en lees een verzoek of antwoord in de gegevensuitwisseling. Zoek je eigen paginatitel.
2. Waaraan zie je dat dit verkeer niet versleuteld is?
3. Welke van routering, NAT en firewall heb je in je eigen Filius-netwerk daadwerkelijk ingesteld en aangetoond?
:::

::: {solution} nw11-o3
:class: dropdown

Je hebt routering en een gewone HTTP-dienst ingesteld. De leesbare paginatitel in de HTTP-uitwisseling laat zien dat dit verkeer niet versleuteld is. Private adressen gebruiken is geen bewijs dat NAT actief is. In deze module stel je NAT en firewall niet in Filius in; je beoordeelt ze met de uitgewerkte modellen en regels.
:::
