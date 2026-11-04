(netwerken-h09)=
# SMTP en IMAP: e-mailen

## Inleiding

Een website vraag je op: jij begint en de server antwoordt. Bij e-mail werkt het anders. Een bericht gaat van jouw programma naar de mailserver van je school of provider, vandaar naar de mailserver van de ontvanger en wordt daar later opgehaald. Er zijn dus meerdere stappen en meerdere protocollen.

**Laag:** {term}`toepassingslaag`. **Vraag:** welke protocollen en servers zijn betrokken bij het versturen en ontvangen van e-mail?

## Verzenden en ophalen

Verzenden en ophalen zijn aparte taken met aparte protocollen:

- {term}`SMTP` dient om e-mail aan te bieden aan een mailserver en tussen mailservers door te sturen.
- IMAP en POP dienen om ontvangen berichten met een mailprogramma op te halen.
- Bij webmail praat je browser via HTTP met de webmailtoepassing. De mailservers erachter gebruiken onderling nog steeds SMTP.

Een e-mailadres bestaat uit een gebruikersnaam en een domein, bijvoorbeeld `leerling@school.test`. De mailserver van de afzender moet weten welke server mail voor `school.test` ontvangt. Dat staat in DNS, in een {term}`MX-record`. Dat is iets anders dan het A-record van een website.

### Voorbeeld

Je stuurt mail naar `leerling@school.test`:

1. Je mailprogramma biedt het bericht met SMTP aan bij jouw mailserver.
2. Jouw mailserver vraagt DNS naar het MX-record van `school.test` en krijgt de naam van de mailserver van de school.
3. Jouw mailserver stuurt het bericht met SMTP naar die server.
4. De ontvanger haalt het bericht later op met IMAP of POP, of leest het via webmail.

::: {exercise} Zonder Filius: een e-mail volgen
:label: nw09-o1

1. Bewijst een browser die webmail toont dat alle mail tussen mailservers via HTTP reist?
2. Welk protocol hoort bij e-mail aanbieden en doorsturen: SMTP of {term}`ARP`?
3. Waarom bewijst een werkende website op `school.test` niet dat e-mail naar dat domein bezorgd kan worden?
4. Waarom heeft de mailserver van de afzender DNS nodig om de mail te kunnen bezorgen?
:::

::: {solution} nw09-o1
:class: dropdown

1. Nee. HTTP kan de webmailpagina in je browser verzorgen, terwijl mailservers onderling SMTP gebruiken.
2. SMTP. ARP lost een lokaal adresseringsprobleem op.
3. De webserver en de mailserver zijn verschillende diensten met eigen instellingen, en ook de DNS-records verschillen (A-record voor de website, MX-record voor de mail).
4. Hij moet via het MX-record weten welke server de mail voor het domein ontvangt en daarna het IP-adres van die server opzoeken.
:::
