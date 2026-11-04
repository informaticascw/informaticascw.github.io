(netwerken-h01)=
# Bits versturen

## Inleiding

Je verstuurt een foto. Over de verbinding gaan geen plaatjes maar signalen, zoals lichtpulsen of spanningsverschillen. De ontvanger moet daaruit dezelfde {term}`bits <bit>` afleiden als de zender verstuurde. Dat lukt alleen als beide kanten van tevoren afspreken hoe een 0, een 1 en het tempo eruitzien.

**Laag:** {term}`fysieke laag`. **Vraag:** hoe herkent de ontvanger dezelfde bitreeks als de zender verstuurde, en hoe snel kan dat?

## Klassikaal: een bitreeks overseinen

Werk in teams van vier: zender, ontvanger, tijdwaarnemer en controleur. De docent geeft alleen de zender een geheime reeks van acht bits. Zender en ontvanger staan enkele meters uit elkaar. Alle teams doen tegelijk mee.

1. **Ronde 1, zonder afspraken.** De zender gebruikt alleen een zaklamp of een omhooggehouden kaart. Praten, schrijven en wijzen zijn niet toegestaan. De ontvanger schrijft op wat hij denkt te ontvangen.
2. **Ronde 2, met afspraken.** Spreek een code, een startteken en een vast tempo af. Verstuur een nieuwe reeks. De ontvanger meldt het resultaat terug, zodat de zender kan controleren of het klopt.
3. **Ronde 3, sneller.** Verhoog het tempo tot er fouten optreden.

Bespreek welke afspraken het verschil maakten. De uitleg hieronder beschrijft die afspraken ook zonder de oefening.

## Van bit naar signaal

Een bit is een waarde: 0 of 1. Om die over te dragen is een fysiek verschijnsel nodig. Via koper gebruik je elektrische signalen, via glasvezel licht en via {term}`wifi` radiogolven. De zender zet bits om in signalen; de ontvanger leidt de bits daar weer uit af.

‘Licht aan is 1, licht uit is 0’ lijkt voldoende, maar is een lange periode licht één 1 of tien enen? De ontvanger moet dus ook weten hoe lang één bit duurt en waar een bericht begint. Echte verbindingen gebruiken uitgebreidere codes dan dit voorbeeld.

Afspraken over hoe apparaten communiceren heten een {term}`protocol`. De fysieke laag heeft één taak: bits als signalen over een {term}`medium` overbrengen. Protocollen voor die laag leggen onder andere de bitduur en de signaalvorm vast.

### Voorbeeld

Je spreekt af: één bit per seconde, beginnen na twee korte flitsen. Vier seconden licht betekent nu vier enen. Zonder de afspraak over de bitduur is dat niet te bepalen.

::: {exercise} Zonder Filius: ontbrekende afspraken
:label: nw01-o1

1. Een zender verstuurt `1001`. Waarom is alleen ‘licht aan is 1’ onvoldoende voor de ontvanger?
2. Noem twee afspraken die zender en ontvanger naast de betekenis van 0 en 1 nodig hebben.
3. De zender verkort de bitduur zonder de ontvanger te waarschuwen. Wat gaat er mis?
:::

::: {solution} nw01-o1
:class: dropdown

1. De ontvanger weet niet waar het ene bit eindigt en het volgende begint, en ook niet waar het bericht start.
2. Bijvoorbeeld een startteken en een vaste bitduur.
3. De ontvanger blijft met de oude bitduur lezen. Daardoor worden bits samengevoegd of overgeslagen en klopt de ontvangen reeks niet meer.
:::

## Snelheid en vertraging

De snelheid van een verbinding geef je aan in {term}`bits per seconde`, bijvoorbeeld 100 Mbit/s. In deze module noemen we die beschikbare overdrachtscapaciteit de {term}`bandbreedte`. Een {term}`byte` is acht bits, dus MB en Mbit zijn niet hetzelfde.

De {term}`vertraging` is de tijd tussen verzenden en aankomen. Een verbinding met veel capaciteit kan toch een merkbare vertraging hebben, bijvoorbeeld door een lange route of wachtrijen. De traagste schakel op de route bepaalt hoe snel gegevens maximaal aankomen.

### Voorbeeld

Een bestand van 20 MB is 160 Mbit (decimale eenheden). Bij 40 Mbit/s kost het overbrengen minstens 4 seconden. Opstarttijd, extra protocolinformatie en ander verkeer zijn daarbij niet meegerekend.

::: {exercise} Zonder Filius: sneller of eerder?
:label: nw01-o2

1. Bereken de minimale overdrachtstijd van 12 MB bij 24 Mbit/s.
2. Verbinding X heeft 1000 Mbit/s en 80 ms vertraging; verbinding Y heeft 100 Mbit/s en 10 ms vertraging. Welke is gunstiger voor korte interactieve berichten en welke voor een groot bestand? Geef je aanname erbij.
:::

::: {solution} nw01-o2
:class: dropdown

1. 12 × 8 / 24 = 4 seconden.
2. Voor korte berichten is Y gunstiger vanwege de lagere vertraging. Voor een groot bestand is X gunstiger vanwege de hogere capaciteit. Dat geldt als de rest van de route en de server geen grotere beperking vormen.
:::

## Fysieke verbindingen in de praktijk

Kijk op je apparaat of je verbonden bent met wifi of met {term}`Ethernet`. Bekijk een netwerkkabel en, als die er is, een glasvezelaansluiting. Een kabel bevat meestal meerdere aders; één bit hoeft dus niet letterlijk één puls op één draad te zijn.

::: {exercise} Filius: je eerste verbinding
:label: nw01-o3

1. Maak in de ontwerpmodus twee computers en verbind ze met een kabel. Geef ze de namen A en B. Bewaar als `01-verbinding.fls`.
2. Wijs aan welk onderdeel in je tekening de fysieke verbinding voorstelt.
3. Leg uit waarom deze tekening nog niet bewijst dat A een webpagina van B kan ophalen.
:::

::: {solution} nw01-o3
:class: dropdown

De kabel stelt de fysieke verbinding voor. Voor een werkende webdienst zijn ook adressering, protocolafspraken en software op beide computers nodig. Filius laat een model zien, geen echte elektrische of optische signalen.
:::
