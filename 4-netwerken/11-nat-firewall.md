(netwerken-h09)=
# NAT, firewall en HTTPS

## Inleiding

Thuis delen meerdere apparaten vaak één publiek IPv4-adres. Je wilt ook niet dat onbekenden van buiten zomaar een verbinding met je apparaten beginnen, of dat iemand onderweg de inhoud van je verkeer meeleest. Dat zijn drie verschillende problemen met drie verschillende oplossingen: adresvertaling met {term}`NAT`, filteren met een {term}`firewall` en versleutelen met {term}`TLS` bij {term}`HTTPS`. Een oplossing voor één probleem lost de andere twee niet op.

**Lagen:** netwerk, transport en toepassing. **Vraag:** hoe kunnen meerdere apparaten één publiek adres delen, wie bepaalt welk verkeer binnenkomt, en hoe blijft de inhoud van webverkeer geheim?

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
:label: nw09-o1

1. Bij welke client hoort een antwoord naar `203.0.113.5:40001`?
2. Waarom zou de router buitenpoort 40001 niet ook voor de tweede verbinding naar dezelfde server gebruiken?
3. Is `172.40.2.8` een privaat adres? En `172.20.2.8`?
:::

::: {solution} nw09-o1
:class: dropdown

1. `192.168.10.10:51000`.
2. Dan zijn de twee verbindingen aan de buitenkant niet meer te onderscheiden. Elke verbinding krijgt daarom een eigen buitenpoort.
3. `172.40.2.8` niet; `172.20.2.8` wel. De private 172-reeks loopt van 172.16 tot en met 172.31.
:::

## Firewall: wel of niet toelaten?

Een firewall bepaalt aan de hand van regels welk verkeer wordt doorgelaten. De regels kunnen kijken naar bron en bestemming, {term}`protocol`, poorten en de toestand van een verbinding. Een stateful firewall herkent antwoorden bij een toegestane verbinding.

Een router stuurt door, NAT vertaalt en een firewall filtert. Die taken zitten vaak in één apparaat, maar het blijven verschillende beslissingen. Een firewall die {term}`TCP` naar poort 443 toestaat, beoordeelt daarmee niet of een website betrouwbaar is.

::: {exercise} Zonder Filius: de regels toepassen
:label: nw09-o2

Een stateful firewall past deze regels in volgorde toe: (1) antwoorden bij toegestane verbindingen toelaten; (2) interne clients nieuwe TCP-verbindingen naar externe poort 443 laten beginnen; (3) alle andere nieuwe verbindingen blokkeren.

1. Mag een interne browser een nieuwe verbinding naar externe poort 443 starten?
2. Mag het antwoord terug naar de tijdelijke clientpoort?
3. Mag een externe computer ongevraagd een nieuwe verbinding naar een interne client beginnen?
4. Versleutelt deze firewall het verkeer?
:::

::: {solution} nw09-o2
:class: dropdown

1. Ja, volgens regel 2.
2. Ja, omdat het bij de toegestane verbinding hoort (regel 1).
3. Nee, volgens regel 3.
4. Nee. Filteren en versleutelen zijn verschillende taken.
:::

## HTTPS: de verbinding beveiligen

HTTPS is {term}`HTTP` over een beveiligde verbinding. Bij HTTP/1.1 en HTTP/2 doet TLS dat boven TCP. De browser controleert onder andere of het {term}`certificaat` bij de domeinnaam past en door een vertrouwde partij is uitgegeven. Beide kanten spreken daarna cryptografische sleutels af.

TLS beschermt de inhoud tegen meelezen en ongemerkt aanpassen onderweg en helpt de identiteit van de server vast te stellen. Een frauduleuze website wordt daardoor niet eerlijk: ook een verkeerde website kan een geldig certificaat voor haar eigen domeinnaam hebben. Andere gegevens, zoals IP-adressen en de hoeveelheid verkeer, kunnen onderweg zichtbaar blijven. HTTP/3 gebruikt QUIC met TLS-beveiliging.

::: {exercise} Eigen apparaat: wat bewijst een certificaat?
:label: nw09-o3

1. Open de schoolwebsite via HTTPS. Open via de sloticoon bij de adresbalk de verbindings- of certificaatinformatie (de menunamen verschillen per browser). Noteer voor welke domeinnaam het certificaat geldt en, als dat zichtbaar is, de geldigheidsperiode.
2. Leg uit waarom een geldig certificaat geen kwaliteitskeurmerk voor de inhoud is.
3. Waarom kun je in je eigen ontwikkeltools de inhoud van HTTPS-antwoorden wel lezen?
:::

::: {solution} nw09-o3
:class: dropdown

1. De waarden verschillen; controleer de bezochte naam en de namen in het certificaat.
2. Een certificaat zegt iets over de identiteit bij een domeinnaam en over de beveiligde verbinding, niet over de waarheid of de bedoelingen van de inhoud.
3. Je browser is het eindpunt en ontsleutelt de gegevens. Een tussenliggende router is dat niet.
:::

::: {exercise} Filius: wat laat het model zien?
:label: nw09-o4

1. Open je HTTP-website uit hoofdstuk 8 en lees een verzoek of antwoord in de gegevensuitwisseling. Zoek je eigen paginatitel.
2. Vergelijk dit met HTTPS in een echte browser: wie kan daar de ontsleutelde inhoud bekijken?
3. Welke van routering, NAT, firewall en TLS heb je in je eigen Filius-netwerk daadwerkelijk ingesteld en aangetoond?
:::

::: {solution} nw09-o4
:class: dropdown

Je hebt routering en een gewone HTTP-dienst ingesteld. De leesbare paginatitel in de HTTP-uitwisseling laat zien dat dit verkeer niet versleuteld is. Private adressen gebruiken is geen bewijs dat NAT actief is. In deze module stel je TLS, NAT en firewall niet in Filius in; je beoordeelt ze met de uitgewerkte modellen en regels.
:::
