(netwerken-les01)=
# Bits versturen

## Inleiding

Je verstuurt een foto. De verbinding vervoert die foto niet als één herkenbaar plaatje, maar als signalen waaruit de ontvanger {term}`bits <bit>` moet afleiden. Daarvoor moeten zender en ontvanger dezelfde {term}`afspraken <afspraak>` gebruiken.

**Laag:** {term}`fysieke laag`. **Hoofdvraag:** hoe krijgt de ontvanger dezelfde reeks bits als de zender?

Je onderzoekt eerst hoe je een 0, een 1 en de grenzen ertussen herkenbaar maakt. Daarna vergelijk je overdrachtscapaciteit en {term}`vertraging`.

## Klassikaal: een bericht zonder woorden

Werk in teams van vier: een zender, ontvanger, tijdwaarnemer en controleur. De docent geeft alleen de zender een geheime reeks van acht bits. Tussen zender en ontvanger zit enkele meters afstand. Andere teams doen tegelijk mee.

In de eerste ronde mag de zender alleen een zaklamp of een omhooggehouden kaart gebruiken. Geen praten, schrijven of wijzen naar de bits. Spreek nog geen code af. De ontvanger schrijft op wat hij denkt te ontvangen.

Vergelijk de uitkomst. Spreek daarna een code, een startteken en een vast tempo af. Probeer een nieuwe reeks. Laat de ontvanger het bericht terugmelden, zodat de zender kan controleren of het klopt. Verhoog ten slotte het tempo totdat fouten optreden.

Bespreek welke afspraken het verschil maakten. De uitleg hieronder beschrijft deze ook zonder de oefening.

## Een bit is nog geen signaal

Een bit is een waarde: 0 of 1. Om die over te dragen heb je een fysiek verschijnsel nodig. Via koper kun je elektrische signalen gebruiken, via glasvezel licht en via {term}`wifi` radiogolven. Een zender zet bits om in signalen; de ontvanger leidt daar de bits weer uit af.

‘Licht aan is 1 en uit is 0’ lijkt voldoende. Maar is een lange periode licht één 1 of zijn het tien enen? Ontvangers hebben ook afspraken nodig over timing. Echte netwerkverbindingen gebruiken uitgebreidere coderingen dan dit eenvoudige voorbeeld.

Bij een {term}`protocol` spreken apparaten af hoe ze communiceren. De functie van de fysieke laag is het overdragen van bits. De concrete afspraken over signalen en timing vullen die {term}`functie` in.

### Voorbeeld

Je spreekt af: iedere seconde één bit, beginnen na twee korte flitsen. Vier seconden licht kan nu vier enen betekenen. Zonder de tijdafspraak blijft dat onduidelijk.

::: {exercise} Zonder Filius: ontbrekende afspraak
:label: nw01-o1

1. Een zender verstuurt `1001`. Waarom is alleen ‘aan is 1’ onvoldoende?
2. Noem twee afspraken die zender en ontvanger naast de bitbetekenis nodig hebben.
3. Waarom helpt harder of feller zenden niet altijd als berichten verkeerd worden begrepen?
:::

::: {solution} nw01-o1
:class: dropdown

1. Zonder timing weet de ontvanger niet waar de afzonderlijke bits beginnen en eindigen; ook het begin van het bericht moet herkenbaar zijn.
2. Bijvoorbeeld een startteken en een vaste bitduur.
3. Sterkte lost een ontbrekende code of tijdafspraak niet op; storing of te hoog tempo kan ook een rol spelen.
:::

## Snelheid en vertraging

De overdrachtssnelheid drukken we uit in {term}`bits per seconde`, bijvoorbeeld 100 Mbit/s. In deze module gebruiken we ‘{term}`bandbreedte`’ voor de beschikbare overdrachtscapaciteit. Eén {term}`byte` bestaat uit acht bits; MB en Mbit betekenen dus niet hetzelfde.

Vertraging is de tijd die overdracht en verwerking kosten. Een snelle verbinding kan toch een merkbare wachttijd hebben. Ook de route, afstand, wachtrijen en {term}`servers <server>` spelen mee. De langzaamste verbinding onderweg kan de doorvoer beperken.

### Voorbeeld

Een bestand van 20 MB bevat 160 Mbit, gerekend met decimale eenheden. Bij 40 Mbit/s duurt alleen het overbrengen theoretisch 4 seconden. Opstarttijd, protocolinformatie en ander verkeer zijn daarin niet meegerekend.

::: {exercise} Zonder Filius: sneller of eerder?
:label: nw01-o2

1. Bereken de minimale overdrachtstijd van 12 MB bij 24 Mbit/s.
2. Verbinding X heeft 1000 Mbit/s en 80 ms vertraging; Y heeft 100 Mbit/s en 10 ms. Welke is gunstiger voor heel korte interactieve berichten? Welke voor een groot bestand? Licht je aannames toe.
:::

::: {solution} nw01-o2
:class: dropdown

1. 12 × 8 / 24 = 4 seconden.
2. Voor korte berichten kan Y prettiger zijn door de lagere vertraging. Voor grote bestanden kan X meer doorvoer bieden. Dit geldt als de andere onderdelen van het pad en de server geen grotere beperking vormen.
:::

## In het echt en in Filius

Bekijk op je apparaat of je wifi of {term}`Ethernet` gebruikt. Bekijk een netwerkkabel en, als die beschikbaar is, een glasvezelaansluiting. Een kabel kan meerdere aders bevatten; één bit hoeft niet letterlijk één puls op één draad te zijn.

::: {exercise} Filius: je eerste verbinding
:label: nw01-o3

1. Maak in de ontwerpmodus twee computers en verbind ze met een kabel. Geef ze de namen A en B. Bewaar als `01-verbinding.fls`.
2. Klik een computer aan en zoek de instellingen voor {term}`IP-adres` en {term}`subnetmasker`. Je hoeft die nu nog niet te begrijpen of aan te passen.
3. Wijs aan welk onderdeel in je tekening de fysieke verbinding voorstelt.
4. Leg uit waarom de tekening nog niet bewijst dat A een webpagina van B kan ophalen.
:::

::: {solution} nw01-o3
:class: dropdown

De kabel stelt de fysieke verbinding voor. Een kabel alleen maakt nog geen werkende webdienst: ook adressering, protocolafspraken en de benodigde software moeten kloppen. Filius toont een model, geen echte elektrische of optische signalen.
:::
