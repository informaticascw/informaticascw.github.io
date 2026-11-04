---
numbering: false
---

(netwerken-les13)=
# Verdieping: DHCP en e-mail

Dit hoofdstuk is optioneel en valt buiten de kernplanning van twaalf lessen. Je onderzoekt twee extra toepassingsprotocollen.

## DHCP: wie stelt al die adressen in?

In de kernmodule kies je adressen met de hand. In een echt netwerk krijgt een {term}`client` zijn IPv4-instellingen vaak automatisch via {term}`DHCP`. De client zoekt een {term}`server`, krijgt een aanbod, vraagt een aangeboden configuratie aan en krijgt een bevestiging. De namen van de eerste berichten zijn Discover, Offer, Request en Acknowledge.

De configuratie kan naast het {term}`IP-adres` onder andere het {term}`masker <subnetmasker>`, een {term}`gateway` en DNS-serveradressen bevatten. Het adres wordt voor een bepaalde tijd uitgeleend: de lease. Een DHCP-server is geen DNS-server, al kan dezelfde machine beide diensten uitvoeren.

Een nieuwe client kent nog niet alle netwerkgegevens en gebruikt aanvankelijk broadcastcommunicatie. {term}`Routers <router>` sturen die niet vanzelf door naar andere netwerken. In grotere netwerken kan een speciaal ingestelde DHCP-relay helpen; dat configureren we hier niet.

::: {exercise} Filius: automatische instellingen
:label: nw13-o1

1. Werk in een kopie van het netwerk uit les 8. Installeer op de DNS-server ook de DHCP-serverdienst als die in jouw Filius-versie beschikbaar is.
2. Kies voor het server-LAN een pool `192.168.20.100` tot en met `192.168.20.120`, masker `255.255.255.0`, gateway `192.168.20.1` en {term}`DNS` `192.168.20.53`. Houd vaste serveradressen buiten de pool.
3. Voeg één nieuwe client toe op dezelfde {term}`switch` en stel deze in op automatische adresconfiguratie. Start de DHCP-dienst en vraag de configuratie aan.
4. Controleer de ontvangen instellingen en bezoek de oefenwebsite op naam. Welke {term}`functies <functie>` zijn door DHCP ingesteld en welke dienst levert nog steeds de pagina?
:::

::: {solution} nw13-o1
:class: dropdown

De client hoort een beschikbaar adres uit de pool en de ingestelde aanvullende gegevens te krijgen. DHCP levert de netwerkconfiguratie, DNS de naamkoppeling en de webserver de pagina. Automatische configuratie alleen bewijst dus nog niet dat iedere achterliggende dienst goed werkt. Menunamen en aanvullende opties kunnen per Filius-versie verschillen.
:::

## E-mail: verzenden is iets anders dan ophalen

Bij e-mail kunnen client en server meerdere rollen hebben. SMTP wordt gebruikt voor het aanbieden en doorsturen van mail. IMAP en POP worden gebruikt om ontvangen berichten via een client te benaderen. Bij webmail praat jouw browser via {term}`HTTP`(S) met de webmailtoepassing; de mailinfrastructuur erachter gebruikt andere {term}`afspraken <afspraak>`.

Een mailadres bevat een gebruikersdeel en domein, bijvoorbeeld `leerling@school.test`. Voor server-naar-serverbezorging kunnen MX-records in DNS aanwijzen welke mailservers bij een domein horen. Dat is iets anders dan een A-record voor een website.

::: {exercise} Zonder Filius: volg een e-mail
:label: nw13-o2

1. Is een browser die webmail toont bewijs dat alle mail met HTTP tussen mailservers reist?
2. Welke afspraak hoort bij mail aanbieden en doorsturen: SMTP of {term}`ARP`?
3. Waarom bewijst een werkende website op `school.test` nog niet dat mail naar dat domein bezorgd kan worden?
:::

::: {solution} nw13-o2
:class: dropdown

1. Nee. HTTP(S) kan de browserinterface verzorgen, terwijl mailservers met mailprotocollen communiceren.
2. SMTP. ARP lost een lokaal adresseringsprobleem op.
3. De webdienst en maildienst hebben verschillende configuraties en servers; ook de benodigde DNS-records kunnen verschillen.
:::
