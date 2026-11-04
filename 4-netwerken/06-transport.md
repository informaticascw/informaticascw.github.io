(netwerken-h07)=
# Poorten, TCP en UDP

## Inleiding

Een {term}`IP-adres` brengt gegevens bij een computer. Daarop draaien tegelijk een browser, een chatprogramma en een spel. Bovendien kunnen onderweg gegevens verloren gaan, dubbel aankomen of in een andere volgorde binnenkomen. De transportlaag lost beide problemen op.

**Laag:** {term}`transportlaag`. **Vraag:** hoe komen gegevens bij het juiste programma terecht, en hoe zorg je dat ze volledig en in de goede volgorde aankomen?

Je leert eerst hoe poorten programma’s en verbindingen onderscheiden. Daarna bekijk je wat {term}`TCP` extra biedt en wat {term}`UDP` juist niet zelf regelt.

## Klassikaal: een boodschap met ontbrekende delen

Werk met drie teams: zender, netwerk en ontvanger. De ontvanger heeft twee postvakken, genummerd 80 en 5000. De zender krijgt een tekst in zes genummerde delen, allemaal voor hetzelfde postvak. Het netwerkteam houdt één deel achter, verwisselt twee delen en levert één deel dubbel af. De ontvanger kan niet zien wat het netwerk achterhoudt.

1. Probeer eerst zonder terugmeldingen de tekst samen te stellen.
2. Spreek daarna af dat de ontvanger meldt welk deel hij als volgende mist. De zender bewaart kopieën en stuurt zo nodig opnieuw.
3. Kan de ontvanger nu de juiste tekst precies één keer in het juiste postvak leggen?

TCP nummert in werkelijkheid {term}`bytes <byte>` in plaats van tekstdelen. De oefening laat wel volgorde, ontbrekende gegevens, bevestigingen en het juiste ontvangende programma zien.

## Poorten: een adres voor het programma

Een transportbericht bevat een bron- en een bestemmingspoort ({term}`poortnummer`). Een poortnummer is geen fysieke aansluiting: het helpt het besturingssysteem de gegevens bij het juiste programma of de juiste verbinding af te leveren.

Een webserver luistert bij gewoon {term}`HTTP` meestal op TCP-poort 80 en bij {term}`HTTPS` meestal op TCP-poort 443. Een {term}`client` kiest doorgaans een tijdelijke bronpoort. Een TCP-verbinding wordt herkend aan beide IP-adressen en beide poortnummers. TCP en UDP hebben elk hun eigen poortnummers.

### Voorbeeld

Client `192.168.10.10:51000` maakt verbinding met {term}`server` `192.168.20.10:80`. Een tweede verbinding kan bronpoort `51001` gebruiken. Antwoorden gaan van serverpoort 80 terug naar de bijbehorende clientpoort.

::: {exercise} Zonder Filius: naar welk programma?
:label: nw07-o1

1. Geef de bron- en bestemmingspoort van het antwoord van de server op de verbinding met clientpoort 51000.
2. Twee clients gebruiken allebei bronpoort 51000 naar dezelfde serverpoort. Waarom raken hun verbindingen niet door elkaar?
3. Waarom is een TCP-poort iets anders dan poort 3 op een {term}`switch`?
:::

::: {solution} nw07-o1
:class: dropdown

1. Bronpoort 80, bestemmingspoort 51000.
2. De IP-adressen van de clients verschillen. Een verbinding wordt herkend aan beide IP-adressen en beide poorten samen.
3. Een switchpoort is een fysieke aansluiting. Een TCP-poort is een getal in de transportinformatie waarmee software verbindingen en programma’s onderscheidt.
:::

## Wat voegt TCP toe?

{term}`IP` garandeert niet dat elk {term}`pakket <IP-pakket>` aankomt of dat pakketten in volgorde aankomen. TCP biedt de toepassing een betrouwbare, geordende {term}`bytestroom`. TCP verdeelt de gegevens in {term}`segmenten <TCP-segment>`, houdt volgnummers bij, verwerkt bevestigingen en verstuurt ontbrekende gegevens opnieuw. Dubbele gegevens geeft TCP niet dubbel aan het programma.

### Voorbeeld: een ontbrekend stuk

De ontvanger heeft bytes 1–4 en 9–12, maar 5–8 ontbreken. Hij kan 1–12 nog niet in volgorde aan het programma geven. Aan de volgnummers en bevestigingen merkt de zender dat er iets ontbreekt en stuurt dat opnieuw, bijvoorbeeld na een wachttijd. Daarna levert TCP alle bytes in de goede volgorde af. Een dubbel ontvangen stuk geeft TCP niet nogmaals af.

De nummers zijn hier vereenvoudigd; je hoeft de echte {term}`TCP-header <header>` niet te kennen. Het gaat om het verschil: IP bezorgt losse pakketten en TCP maakt daar voor het programma een geordende stroom van.

Voordat gegevens stromen, bouwen client en server een verbinding op met een {term}`handshake`: de berichten SYN, SYN-ACK en ACK. TCP past ook de hoeveelheid gegevens die tegelijk onderweg is aan op de ontvanger en het netwerk. Die regelalgoritmen behandelen we niet.

Betrouwbaar betekent niet dat een verbinding altijd slaagt. Valt een kabel blijvend uit, dan kan ook TCP niets bezorgen en krijgt het programma uiteindelijk een foutmelding. TCP versleutelt gegevens niet.

## Wanneer UDP?

UDP verstuurt afzonderlijke {term}`datagrammen <datagram>` met poortnummers. UDP bouwt zelf geen verbinding op, bevestigt de ontvangst niet en herstelt de volgorde niet. Een programma kan die taken zelf toevoegen. Bij live geluid is een stukje dat te laat opnieuw wordt verstuurd minder bruikbaar dan een stukje dat wordt overgeslagen.

| Eigenschap | TCP | UDP |
| --- | --- | --- |
| Verbinding vooraf | Ja | Niet door UDP zelf |
| Betrouwbare, geordende stroom | Door TCP verzorgd | Niet door UDP verzorgd |
| Grenzen tussen berichten van het programma behouden | Nee (bytestroom) | Ja (datagrammen) |
| Versleuteling | Nee | Nee |

HTTP/3 gebruikt QUIC boven UDP; QUIC zorgt zelf voor betrouwbaarheid en beveiliging. ‘Websites gebruiken altijd TCP’ is dus te stellig. In onze Filius-voorbeelden gebruikt HTTP wel TCP.

::: {exercise} Zonder Filius: kies en onderbouw
:label: nw07-o2

1. Waarom is het belangrijk dat bij een download geen bytes ontbreken?
2. Waarom is wachten op een oud geluidsfragment vervelend bij een live gesprek?
3. Iemand zegt: ‘UDP kan nooit betrouwbare communicatie opleveren.’ Verbeter die uitspraak.
:::

::: {solution} nw07-o2
:class: dropdown

1. Ontbrekende bytes kunnen het bestand onbruikbaar maken. De download moet alle bytes in de goede volgorde afleveren.
2. Wachten vergroot de {term}`vertraging`, terwijl het gesprek al verder is.
3. UDP zelf biedt dat niet, maar een protocol of programma boven UDP kan betrouwbaarheid toevoegen.
:::

::: {exercise} Filius: TCP herkennen
:label: nw07-o3

1. Gebruik C als webserver in je bestaande netwerk: installeer en start de webserver. Installeer op A een webbrowser.
2. Open de gegevensuitwisseling en bezoek vanaf A `http://192.168.20.10`.
3. Zoek de opbouw van de TCP-verbinding en noteer de gebruikte poorten. Welke kant begon?
4. Vergelijk met een ping naar hetzelfde adres. Zie je daar ook een TCP-opbouw?
5. Bewaar als `07-transport.fls`.
:::

::: {solution} nw07-o3
:class: dropdown

De browser is de client en begint de verbinding. De webserver gebruikt normaal TCP-poort 80 en de client een tijdelijke bronpoort. Bij een nieuwe verbinding zijn de opbouwberichten zichtbaar. Ping gebruikt {term}`ICMP` en heeft geen handshake. Een bestaande verbinding kan hergebruikt worden: start de simulatie opnieuw als je juist de eerste verbinding wilt zien.
:::

## Eigen apparaat: meerdere verbindingen

Open in de ontwikkeltools van je browser het tabblad Netwerk en laad een pagina. Zoek, als beschikbaar, het externe adres en de kolom met het protocol. `h2` en `h3` zijn versies van HTTP. Eén pagina kan veel verzoeken aan meerdere servers veroorzaken, en een server kan meerdere verzoeken over één bestaande verbinding afhandelen.
