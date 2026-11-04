---
numbering: false
---

(netwerken-verdieping)=
# Verdieping: DHCP en e-mail

Dit hoofdstuk is optioneel en valt buiten de twaalf lessen van de kern. Je onderzoekt twee extra protocollen van de toepassingslaag.

## DHCP: automatisch adressen instellen

In de kernmodule stel je adressen met de hand in. In een echt netwerk krijgt een {term}`client` zijn IPv4-instellingen meestal automatisch via {term}`DHCP`. De client zoekt een {term}`server`, krijgt een aanbod, vraagt dat aanbod aan en krijgt een bevestiging. De berichten heten Discover, Offer, Request en Acknowledge.

Behalve het {term}`IP-adres` kan de configuratie onder andere het {term}`masker <subnetmasker>`, de {term}`gateway` en DNS-serveradressen bevatten. Het adres wordt voor beperkte tijd uitgeleend: de {term}`lease`. Een DHCP-server is geen DNS-server, ook al kan één computer beide diensten uitvoeren.

Een nieuwe client kent nog geen netwerkgegevens en begint daarom met een broadcast. {term}`Routers <router>` sturen die niet vanzelf door naar andere netwerken. In grotere netwerken kan een speciaal ingestelde DHCP-relay dat oplossen; dat stel je hier niet in.

::: {exercise} Filius: automatische instellingen
:label: nw90-o1

1. Werk in een kopie van het netwerk uit hoofdstuk 8. Installeer op de DNS-server ook de DHCP-server, als jouw Filius-versie die heeft.
2. Kies voor het server-LAN een pool van `192.168.20.100` tot en met `192.168.20.120`, masker `255.255.255.0`, gateway `192.168.20.1` en {term}`DNS` `192.168.20.53`. Houd vaste serveradressen buiten de pool.
3. Voeg één nieuwe client toe op dezelfde {term}`switch` en stel die in op automatische adresconfiguratie. Start de DHCP-server en vraag de configuratie aan.
4. Controleer de ontvangen instellingen en bezoek de oefenwebsite op naam. Wat heeft DHCP ingesteld en welke dienst levert nog steeds de pagina?
:::

::: {solution} nw90-o1
:class: dropdown

De client krijgt een vrij adres uit de pool en de ingestelde extra gegevens. DHCP levert de netwerkconfiguratie, DNS de naamkoppeling en de webserver de pagina. Dat de automatische configuratie werkt, bewijst dus nog niet dat DNS en de webserver werken. Menunamen en opties kunnen per Filius-versie verschillen.
:::

## E-mail: verzenden is iets anders dan ophalen

Bij e-mail zijn meerdere protocollen betrokken. {term}`SMTP` dient om e-mail aan te bieden en door te sturen. IMAP en POP dienen om ontvangen berichten met een mailprogramma op te halen. Bij webmail praat je browser via HTTP(S) met de webmailtoepassing; de mailservers erachter gebruiken de mailprotocollen.

Een e-mailadres bestaat uit een gebruikersnaam en een domein, bijvoorbeeld `leerling@school.test`. Voor het bezorgen tussen mailservers wijst een {term}`MX-record` in DNS aan welke mailservers bij een domein horen. Dat is iets anders dan het A-record van een website.

::: {exercise} Zonder Filius: een e-mail volgen
:label: nw90-o2

1. Bewijst een browser die webmail toont dat alle mail tussen mailservers via HTTP reist?
2. Welk protocol hoort bij e-mail aanbieden en doorsturen: SMTP of {term}`ARP`?
3. Waarom bewijst een werkende website op `school.test` niet dat e-mail naar dat domein bezorgd kan worden?
:::

::: {solution} nw90-o2
:class: dropdown

1. Nee. HTTP(S) kan de webmailpagina in je browser verzorgen, terwijl mailservers onderling mailprotocollen gebruiken.
2. SMTP. ARP lost een lokaal adresseringsprobleem op.
3. De webserver en de mailserver zijn verschillende diensten met eigen instellingen, en ook de DNS-records verschillen.
:::
