(netwerken-les09)=
# Verbinden en beschermen

## Inleiding

Meerdere apparaten thuis delen vaak één publiek {term}`IPv4-adres <IP-adres>`. Tegelijk wil je niet dat iedere onbekende van buiten zomaar een verbinding naar je apparaten begint, of dat iemand onderweg de inhoud leest. Dat zijn drie verschillende problemen.

**Lagen:** netwerk, transport en toepassing. We behandelen daarom achtereenvolgens adresvertaling met {term}`NAT`, toelaten of blokkeren met een {term}`firewall` en bescherming van de inhoud met {term}`TLS` bij {term}`HTTPS`. Een werkende oplossing voor één probleem lost de andere twee niet vanzelf op.

## Klassikaal: één buitenadres voor meerdere bezoekers

Maak drie rollen: twee interne {term}`clients <client>`, een grensrouter en een externe {term}`server`. Clients krijgen allebei een bericht voor dezelfde server. Hun kaartjes hebben een intern IP-adres en {term}`bronpoort <poortnummer>`. De grensrouter heeft één buitenadres en een tabel met beschikbare buitenpoorten.

Laat eerst beide berichten naar buiten gaan onder precies hetzelfde buitenadres én dezelfde buitenpoort. Stuur het serverantwoord terug. De grensrouter kan nu niet bepalen welke client bedoeld is. Laat de {term}`router` vervolgens voor elke verbinding een eigen buitenpoort kiezen en de koppeling opschrijven. De antwoorden kunnen nu gericht terug.

Geef de router daarna een regelkaart: ‘nieuwe verbindingen van buiten alleen naar de gepubliceerde webdienst; antwoorden bij bestaande verbindingen wel toelaten’. Laat de externe server een ongevraagd nieuw bericht sturen. Bespreek welke beslissing over vertalen gaat en welke over toelaten.

## Private adressen

Voor intern gebruik zijn drie IPv4-reeksen gereserveerd:

| Reeks | Prefix |
| --- | --- |
| 10.0.0.0 tot 10.255.255.255 | 10.0.0.0/8 |
| 172.16.0.0 tot 172.31.255.255 | 172.16.0.0/12 |
| 192.168.0.0 tot 192.168.255.255 | 192.168.0.0/16 |

Verschillende organisaties mogen dezelfde {term}`private adressen <privaat IP-adres>` intern gebruiken. Die adressen zijn niet wereldwijd uniek en worden niet als gewone publieke bestemmingen over {term}`internet` gerouteerd. Niet ieder adres buiten deze drie reeksen is automatisch een bruikbaar publiek adres: er zijn ook andere bijzondere reeksen.

## NAT: adressen en poorten vertalen

Bij veel thuisnetwerken vertaalt de router bij uitgaand IPv4-verkeer het interne bronadres en meestal ook de bronpoort. We spreken vaak algemeen van NAT; deze variant heet ook {term}`NAPT` of PAT. De router onthoudt welke koppeling bij welke verbinding hoort en vertaalt de antwoorden terug.

### Voorbeeld — buitenadressen hieronder zijn documentatieadressen

| Intern | Naar buiten vertaald | Server |
| --- | --- | --- |
| 192.168.10.10:51000 | 203.0.113.5:40001 | 198.51.100.20:443 |
| 192.168.10.20:51000 | 203.0.113.5:40002 | 198.51.100.20:443 |

Beide clients kunnen dezelfde interne bronpoort gebruiken, maar krijgen hier verschillende buitenpoorten. Een antwoord naar buitenpoort 40002 wordt terugvertaald naar de tweede client.

NAT vervangt geen {term}`routering`: na het vertalen moet het {term}`pakket <IP-pakket>` nog steeds worden doorgestuurd. Ook is NAT geen versleuteling. Onze eerdere Filius-netwerken gebruiken private adressen zonder NAT: binnen die gesloten simulatie kan gewone routering voldoende zijn.

::: {exercise} Zonder Filius: volg de vertaling
:label: nw09-o1

1. Bij welke client hoort een antwoord naar `203.0.113.5:40001`?
2. Waarom zou dezelfde tabel buitenpoort 40001 niet ook voor de tweede verbinding naar dezelfde server moeten gebruiken?
3. Is `172.40.2.8` een RFC 1918-adres? En `172.20.2.8`?
:::

::: {solution} nw09-o1
:class: dropdown

1. `192.168.10.10:51000`.
2. De twee verbindingen zouden aan de buitenkant niet meer onderscheiden worden. In dit voorbeeld krijgt iedere verbinding een aparte buitenpoort.
3. `172.40.2.8` niet; `172.20.2.8` wel. De private 172-reeks loopt van 172.16 tot en met 172.31.
:::

## Firewall: wel of niet toelaten?

Een firewall beslist volgens regels welk verkeer wordt toegelaten. Regels kunnen kijken naar bron en bestemming, {term}`protocol`, poorten en de toestand van een verbinding. Een stateful firewall kan antwoorden bij een toegestane verbinding herkennen.

Een router kan doorsturen, NAT kan vertalen en een firewall kan filteren. Die {term}`functies <functie>` zitten vaak in één apparaat, maar lossen verschillende vragen op. Een firewall die ‘{term}`TCP` naar poort 443’ toestaat, beoordeelt daarmee niet automatisch of iedere website inhoudelijk veilig is.

::: {exercise} Zonder Filius: pas de regels toe
:label: nw09-o2

Een stateful firewall gebruikt deze volgorde: 1 antwoorden bij toegestane verbindingen toelaten; 2 interne clients nieuwe TCP-verbindingen naar externe poort 443 laten beginnen; 3 alle overige nieuwe verbindingen blokkeren.

1. Mag een interne browser een nieuwe verbinding naar externe poort 443 starten?
2. Mag het antwoord terug naar de tijdelijke clientpoort?
3. Mag een externe computer ongevraagd een nieuwe verbinding naar een interne client beginnen?
4. Voegt deze firewall automatisch versleuteling toe?
:::

::: {solution} nw09-o2
:class: dropdown

1. Ja, volgens regel 2.
2. Ja, als het bij de toegestane verbinding hoort, volgens regel 1.
3. Nee, volgens regel 3.
4. Nee, filteren en versleutelen zijn verschillende functies.
:::

## HTTPS: de verbinding beveiligen

HTTPS is {term}`HTTP` via een beveiligde verbinding. Bij HTTP/1.1 en HTTP/2 zorgt TLS boven TCP voor bescherming. De browser controleert onder andere of het certificaat past bij de domeinnaam en een vertrouwde certificaatketen heeft. De partijen spreken cryptografische sleutels af.

TLS beschermt de inhoud tegen meelezen en ongemerkt wijzigen onderweg en helpt de server te authenticeren. Het maakt een frauduleuze website niet eerlijk: ook een verkeerde website kan een geldig certificaat voor haar eigen domeinnaam hebben. Andere informatie, zoals IP-adressen en hoeveel verkeer er is, kan onderweg nog zichtbaar zijn. Moderne HTTP/3 gebruikt QUIC met TLS-beveiliging.

::: {exercise} In het echt: wat bewijst het certificaat?
:label: nw09-o3

1. Open de schoolwebsite via HTTPS. Open via de site-informatie bij de adresbalk de verbindings- of certificaatinformatie. Noteer de domeinnaam waarvoor het certificaat geldt en, indien zichtbaar, de geldigheidsperiode. De menunaam verschilt per browser.
2. Leg uit waarom een geldig certificaat geen kwaliteitskeurmerk voor de inhoud is.
3. Waarom kun je in je eigen ontwikkeltools toch de inhoud van HTTPS-antwoorden lezen?
:::

::: {solution} nw09-o3
:class: dropdown

1. De concrete gegevens verschillen; controleer de werkelijk bezochte naam en de getoonde certificaatnamen.
2. Het certificaat gaat over de identiteit bij een domeinnaam en de beveiligde verbinding, niet over de waarheid of goede bedoelingen van de inhoud.
3. Je browser is het eindpunt en ontsleutelt de gegevens. Een willekeurige tussenliggende router is dat niet.
:::

::: {exercise} Filius: wat laat het model zien?
:label: nw09-o4

1. Open je HTTP-website uit les 8 en lees een verzoek of antwoord in de gegevensuitwisseling. Zoek je eigen herkenbare paginatitel.
2. Vergelijk dit met de HTTPS-verbinding in de echte browser: wie kan daar de ontsleutelde inhoud bekijken?
3. Geef aan welke van de functies routering, NAT, firewall en TLS je tot nu toe daadwerkelijk in jouw Filius-opstelling hebt ingesteld en aangetoond.
:::

::: {solution} nw09-o4
:class: dropdown

Je hebt routering en een gewone HTTP-dienst ingesteld. De zichtbare paginatitel in die HTTP-uitwisseling toont geen TLS-beveiliging aan. Het configureren van private adressen is geen bewijs dat NAT actief is. Deze module vraagt geen onbevestigde TLS-simulatie of versieafhankelijke firewallconfiguratie in Filius; NAT en firewall beoordeel je hier met de uitgewerkte modellen en regels.
:::
