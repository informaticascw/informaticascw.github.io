(netwerken-les07)=
# Het juiste programma bereiken

## Inleiding

Een {term}`IP-adres` brengt gegevens bij een apparaat. Op dat apparaat kunnen tegelijk een browser, chat en spel actief zijn. Bovendien kunnen onderweg gegevens ontbreken of in een andere volgorde aankomen.

**Laag:** {term}`transportlaag`. **Hoofdvraag:** welke dienst is nodig om de gegevens bij de juiste toepassing af te leveren?

We lossen eerst het onderscheid tussen programma's en verbindingen op met poorten. Daarna bekijken we welke extra dienst {term}`TCP` biedt en wat {term}`UDP` daarvan juist niet zelf regelt.

## Klassikaal: een boodschap met ontbrekende delen

Werk met drie teams: zender, netwerk en ontvanger. De ontvanger heeft twee postvakken met de nummers 80 en 5000. De zender krijgt een tekst in zes genummerde delen, allemaal voor hetzelfde postvak. Het netwerkteam houdt één deel achter, verwisselt twee delen en bezorgt één deel dubbel. De ontvanger mag niet zien wat het netwerkteam achterhoudt.

Probeer eerst zonder terugmeldingen de tekst samen te stellen. Spreek daarna af dat de ontvanger meldt welk deel als volgende ontbreekt; de zender bewaart kopieën en stuurt zo nodig opnieuw. Kan de ontvanger nu de juiste tekst precies eenmaal in het juiste vak leggen?

Dit model gebruikt genummerde tekstdelen. TCP nummert in werkelijkheid {term}`bytes <byte>` en gebruikt uitgebreidere {term}`afspraken <afspraak>`. De oefening illustreert volgorde, ontbrekende gegevens, bevestigingen en het juiste ontvangende programma.

## Een adres voor het programma

Een transportbericht bevat een bron- en {term}`bestemmingspoort <poortnummer>`. Een poortnummer is hier geen fysieke aansluiting. Het helpt het besturingssysteem gegevens bij de juiste toepassing of verbinding af te leveren.

Een webserver luistert bij gewone {term}`HTTP` meestal op TCP-poort 80; {term}`HTTPS` gebruikt vaak TCP-poort 443. Een {term}`client` kiest doorgaans een tijdelijke bronpoort. Een TCP-verbinding is te onderscheiden aan beide IP-adressen en beide poortnummers.

### Voorbeeld

Client `192.168.10.10:51000` verbindt met {term}`server` `192.168.20.10:80`. Een tweede verbinding kan bronpoort `51001` gebruiken. Antwoorden gaan terug van serverpoort 80 naar de bijbehorende clientpoort. TCP en UDP hebben afzonderlijke poortnummer-ruimtes.

::: {exercise} Zonder Filius: naar welk programma?
:label: nw07-o1

1. Vul bron- en bestemmingspoort in voor het antwoord op de verbinding met clientpoort 51000.
2. Twee clients gebruiken allebei bronpoort 51000 naar dezelfde serverpoort. Waarom hoeven hun verbindingen niet door elkaar te raken?
3. Waarom is een TCP-poort iets anders dan poort 3 op een {term}`switch`?
:::

::: {solution} nw07-o1
:class: dropdown

1. Bronpoort 80, bestemmingspoort 51000.
2. Hun client-IP-adressen verschillen; beide IP-adressen en poorten onderscheiden de verbindingen.
3. De switchpoort is een aansluiting. De TCP-poort is een getal in transportinformatie waarmee software verbindingen en toepassingen onderscheidt.
:::

## Wat voegt TCP toe?

{term}`IP` biedt op zichzelf geen garantie dat ieder {term}`pakket <IP-pakket>` aankomt of dat pakketten op volgorde aankomen. TCP biedt een betrouwbare geordende {term}`bytestroom` tussen toepassingen. Het verdeelt gegevens in {term}`segmenten <TCP-segment>`, houdt volgnummers bij, verwerkt bevestigingen en verzendt ontbrekende gegevens opnieuw. Dubbele gegevens worden niet dubbel aan de toepassing afgegeven.

### Voorbeeld: een ontbrekend stuk

Stel dat de ontvanger bytes 1–4 en 9–12 heeft, maar 5–8 nog ontbreken. Hij kan de volledige reeks 1–12 nog niet op volgorde aan de toepassing geven. Met bevestigingen en volgnummers kan de zender vaststellen dat gegevens ontbreken en die opnieuw versturen, bijvoorbeeld na een wachttijd. Daarna levert TCP de bytes in de juiste volgorde af. Een dubbel ontvangen stuk wordt niet nogmaals als nieuwe inhoud afgegeven.

De nummers zijn hier vereenvoudigd; je hoeft geen echte {term}`TCP-header <header>` uit je hoofd te leren. Het belangrijke onderscheid is dat IP losse pakketten bezorgt, terwijl TCP daar voor de toepassing een geordende stroom van maakt.

Vooraf wordt een verbinding opgebouwd, herkenbaar aan SYN, SYN-ACK en ACK. Daarna kunnen gegevens stromen. TCP past de hoeveelheid uitstaand verkeer aan de ontvanger en de netwerksituatie aan. We rekenen niet aan die regelalgoritmen.

Betrouwbaar betekent niet dat iedere verbinding altijd slaagt. Als een kabel blijvend wegvalt, kan ook TCP de tekst niet bezorgen. De toepassing krijgt uiteindelijk een fout of merkt dat de verbinding stopt. TCP versleutelt gegevens niet automatisch.

## Wanneer UDP?

UDP verstuurt afzonderlijke datagrammen met poortinformatie, zonder zelf verbinding op te bouwen, ontvangst te bevestigen of de volgorde te herstellen. Een toepassing kan zulke {term}`functies <functie>` alsnog toevoegen. Bij live geluid kan een te laat opnieuw verstuurd stukje minder bruikbaar zijn dan het overslaan ervan.

| Vraag | TCP | UDP |
| --- | --- | --- |
| Verbinding vooraf | Ja | Niet door UDP zelf |
| Betrouwbare geordende stroom | Door TCP verzorgd | Niet door UDP verzorgd |
| Grenzen van toepassingbericht behouden | Nee, bytestroom | Ja, datagrammen |
| Versleuteling vanzelf | Nee | Nee |

HTTP/3 gebruikt QUIC boven UDP, met eigen betrouwbaarheid en beveiliging. Daarom is ‘websites gebruiken altijd TCP’ te absoluut. Onze Filius-voorbeelden gebruiken HTTP boven TCP.

::: {exercise} Zonder Filius: kies en onderbouw
:label: nw07-o2

1. Waarom is het belangrijk dat een download geen ontbrekende bytes bevat?
2. Waarom kan wachten op een oud geluidfragment vervelend zijn bij een live gesprek?
3. Iemand beweert: ‘UDP kan nooit betrouwbare communicatie opleveren.’ Verbeter die uitspraak.
:::

::: {solution} nw07-o2
:class: dropdown

1. Ontbrekende bytes kunnen het bestand onbruikbaar maken. Een betrouwbare overdracht moet de juiste bytes compleet afleveren.
2. Het wachten verhoogt de {term}`vertraging`; het gesprek is inmiddels verdergegaan.
3. UDP zelf biedt die dienst niet. Een {term}`protocol` of toepassing boven UDP kan betrouwbaarheid toevoegen.
:::

::: {exercise} Filius: TCP herkennen
:label: nw07-o3

1. Gebruik een computer als server op je bestaande netwerk. Installeer en start daar de webserver. Installeer op A een webbrowser.
2. Open de gegevensuitwisseling en bezoek vanaf A `http://192.168.20.10` als C je server is.
3. Zoek de opbouw van een TCP-verbinding en noteer de gebruikte poorten. Welke kant begon?
4. Vergelijk met een ping naar hetzelfde adres: zie je daar dezelfde TCP-opbouw? Bewaar als `07-transport.fls`.
:::

::: {solution} nw07-o3
:class: dropdown

De browser is de client en begint de verbinding. De HTTP-server gebruikt normaal TCP-poort 80; de client heeft een tijdelijke bronpoort. Bij een nieuwe verbinding zijn de TCP-opbouwberichten zichtbaar. Een ping gebruikt {term}`ICMP` en heeft geen TCP-handshake. Een reeds bestaande verbinding kan opnieuw gebruikt worden; start de simulatie opnieuw als je juist de eerste verbinding wilt onderzoeken.
:::

## In het echt: meerdere verbindingen

Bekijk in de browserontwikkeltools het tabblad Netwerk tijdens het laden van een pagina. Zoek, als beschikbaar, het externe adres en de protocolkolom. `h2` en `h3` verwijzen naar HTTP-versies, niet naar de fysieke aansluiting. Eén pagina kan veel verzoeken naar meerdere servers veroorzaken. De server kan meerdere verzoeken over één bestaande verbinding afhandelen.
