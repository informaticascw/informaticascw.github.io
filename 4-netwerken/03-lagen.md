(netwerken-h03)=
# Lagen en inkapseling

## Inleiding

In hoofdstuk 1 zag je dat bits als signalen worden verstuurd en in hoofdstuk 2 dat een {term}`frame` een apparaat op het lokale netwerk bereikt. Voor een website is meer nodig: het bericht moet bij de juiste computer komen, soms via meerdere netwerken, en daar bij het juiste programma. Die taken zijn verdeeld over lagen. Elke laag gebruikt de diensten van de laag eronder.

**Laag:** alle vijf. **Vraag:** welke taak hoort bij welke laag, en hoe verpakt elke laag de gegevens van de laag erboven?

In dit hoofdstuk krijg je het overzicht. De protocollen van de lagen werk je in de volgende hoofdstukken uit; hun details hoef je nu nog niet te kennen.

## Vijf lagen, vijf vragen

We gebruiken een {term}`lagenmodel` met vijf lagen. Een laag is geen aparte kast: één computer voert taken uit meerdere lagen uit.

| Laag | Welke vraag lost de laag op? | Wat gebruikt de laag daarvoor? |
| --- | --- | --- |
| {term}`Toepassingslaag <toepassingslaag>` | Wat vraagt of levert het programma? | Een bericht van het programma, bijvoorbeeld een verzoek om een webpagina |
| {term}`Transportlaag <transportlaag>` | Voor welk programma zijn de gegevens bedoeld, en hoe betrouwbaar moeten ze aankomen? | {term}`Poortnummers <poortnummer>`; {term}`TCP` regelt ook volgorde en herhaling |
| {term}`Netwerklaag <netwerklaag>` | Naar welke computer moet het bericht, ook via andere netwerken? | Bron- en bestemmings-IP-adres |
| {term}`Datalinklaag <datalinklaag>` | Naar welk apparaat op deze lokale verbinding? | Bron- en bestemmings-MAC-adres bij {term}`Ethernet` |
| {term}`Fysieke laag <fysieke laag>` | Hoe gaan de {term}`bits <bit>` over het {term}`medium`? | Signalen op koper, glasvezel of radio |

Een protocol is een verzameling concrete afspraken. {term}`IP` is bijvoorbeeld het protocol van de netwerklaag, {term}`HTTP` een protocol van de toepassingslaag en TCP en {term}`UDP` zijn protocollen van de transportlaag. Dezelfde taak kan door verschillende protocollen worden uitgevoerd: een browser stuurt hetzelfde HTTP-verzoek via een kabel of via wifi. Alleen de onderste laag verandert.

## Inkapseling: elke laag voegt informatie toe

Een ontvanger moet kunnen herkennen wat hij krijgt en voor wie het bedoeld is. Daarom voegt de zender bij elke laag besturingsinformatie toe, meestal als {term}`header` vóór de gegevens. Dat heet {term}`inkapseling`.

We volgen één klein HTTP-bericht dat via TCP, IPv4 en Ethernet wordt verstuurd:

1. De toepassing maakt het bericht: een verzoek om `/rooster.html`.
2. TCP voegt een TCP-header toe met onder andere poortnummers en volgnummers. Dit geheel heet een {term}`TCP-segment`.
3. IP behandelt dat segment als inhoud en voegt een IP-header toe. Dit geheel heet een {term}`IP-pakket`.
4. Ethernet behandelt het IP-pakket als inhoud en voegt een header ervoor en een {term}`trailer` erachter toe. De trailer bevat de foutcontrole ({term}`FCS`). Dit geheel is het frame.
5. De fysieke laag zet de bits van het frame om in signalen. Zij voegt geen header toe.

```{figure} images/inkapseling.svg
:alt: Een Ethernetframe bevat een IP-pakket; dat bevat een TCP-segment met de toepassingsgegevens. De Ethernetheader en trailer staan buiten het IP-pakket.

Het segment zit in het pakket en het pakket in het frame. Elke header hoort bij zijn eigen laag.
```

De inhoud die een laag vervoert heet de {term}`payload`. Voor Ethernet is dat hier het hele IP-pakket, niet alleen de tekst van de webpagina. Eén bericht van een programma kan over meerdere TCP-segmenten worden verdeeld; de figuur toont bewust één klein bericht.

## Ontkapseling: de ontvanger pakt uit

De ontvanger werkt in omgekeerde richting. De netwerkinterface haalt de bits uit de signalen. De datalinklaag controleert het frame, verwerkt de Ethernetheader en geeft de inhoud door aan de netwerklaag. IP verwerkt de IP-header en geeft de inhoud door aan TCP. TCP verwerkt de TCP-header, voegt ontvangen {term}`bytes <byte>` in de goede volgorde samen en levert ze af bij het programma. Dit heet {term}`ontkapseling`. Elke laag gebruikt alleen zijn eigen header.

::: {exercise} Zonder Filius: wat zit waarin?
:label: nw03-o1

1. Orden van buiten naar binnen: toepassingsgegevens, Ethernetframe, TCP-segment, IP-pakket.
2. Staan een bestemmings-MAC-adres en een bestemmings-IP-adres in dezelfde header?
3. Een IP-pakket is 100 bytes. Ethernetheader en -trailer samen zijn in dit voorbeeld 18 bytes. Hoe groot is het frame? Is het IP-pakket zelf nu 118 bytes?
:::

::: {solution} nw03-o1
:class: dropdown

1. Ethernetframe → IP-pakket → TCP-segment → toepassingsgegevens.
2. Nee. Het MAC-adres staat in de Ethernetheader en het IP-adres in de IP-header. De Ethernetheader zit buiten het IP-pakket.
3. Het frame is 118 bytes. Het IP-pakket blijft 100 bytes: de 18 bytes zijn de buitenste verpakking.
:::

## Wat doet een router?

Een {term}`router` ontvangt een frame, haalt het IP-pakket eruit en kijkt naar het IP-adres van de bestemming. Daarmee kiest hij de volgende verbinding en verpakt hij het pakket in een nieuw frame. Op Ethernet krijgt dat frame de MAC-adressen voor de volgende stap. De router hoeft de inhoud van de webpagina niet te begrijpen.

Zonder {term}`NAT` blijven de IP-adressen van afzender en bestemming onderweg gelijk. Het IP-pakket verandert wel een klein beetje: de {term}`TTL`, een teller die bij elke router met 1 afneemt, wordt aangepast.

Een {term}`switch` kiest op basis van MAC-adressen, een router op basis van IP-adressen. Dat zijn twee verschillende beslissingen, ook als beide in één apparaat zitten.

## Klassikaal: een bericht inpakken en uitpakken

Maak groepen van negen: vier zenderrollen, vier ontvangerrollen en één routerrol. Aan beide kanten zijn de rollen toepassing, transport, netwerk en datalink. De docent geeft elke rol alleen de velden die die rol invult. De toepassingsrol kent de tekst, de netwerkrol het IP-adres van de bestemming en de datalinkrol het MAC-adres van de eerste ontvanger.

1. Bouw het bericht met gevouwen kaarten: transportinformatie om de toepassingsgegevens, IP-informatie om het segment en een frame om het pakket.
2. Geef het bericht door aan de ontvangers. Elke ontvangerrol haalt alleen zijn eigen verpakking weg. Alleen de toepassingsrol leest de tekst.
3. Laat nu de routerrol tussen zender en ontvanger staan. De router haalt het frame weg en verpakt het IP-pakket in een nieuw frame met andere MAC-adressen, zonder de toepassingsgegevens te openen.
4. Leg het oude en het nieuwe frame naast elkaar. Wat is veranderd en wat is gelijk gebleven?

De fysieke overdracht en de foutcontrole worden niet nagespeeld.

::: {exercise} Filius: twee lagen terugvinden
:label: nw03-o2

1. Open de gegevensuitwisseling bij een ping tussen twee computers uit je netwerk. Zoek, voor zover jouw versie dat toont, Ethernet- en IP-velden in hetzelfde bericht. Noteer één MAC-adres en één IP-adres en leg uit waarvoor elk adres dient.
2. Het venster toont de velden niet in elkaar genest. Betekent dat dat een frame geen IP-pakket bevat?
3. Waarom mag je bij deze ping geen TCP-segment tekenen?
:::

::: {solution} nw03-o2
:class: dropdown

1. Het MAC-adres dient voor aflevering op het lokale netwerk, het IP-adres voor de bron of bestemming van het pakket. De waarden komen uit je eigen netwerk.
2. Nee. Het venster is een weergave; de figuur laat zien hoe de verpakking in elkaar zit.
3. Ping gebruikt {term}`ICMP`, geen TCP. De figuur toont één HTTP/TCP-voorbeeld, niet de inhoud van elk IP-pakket.
:::
