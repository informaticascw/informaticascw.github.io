(physcomp-h5)=
# Toestandsdiagrammen

## Inleiding: game

% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4855353

In deze module leer je te werken met toestandsdiagrammen. Als introductie daarop kun je met de gehele klas de volgende opdracht doen.

```{exercise} Toestanden in games
:label: opdracht3game
Bekijk gezamenlijk het volgende fragment uit een game waarin de hoofdrolspeler een bewaker moet proberen uit te schakelen. Kijk goed naar de bewaker en beschrijf in welke toestanden de bewaker kan zijn. Beschrijf ook hoe de bewaker in elk van die toestanden terecht komt. Met andere woorden: wat moet er gebeuren voordat de bewaker in een bepaalde toestand terecht komt.
```

```{iframe} https://www.youtube.com/embed/it9t0whAyPg
:width:100%
Automaat bewaker
```

% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4913221
Wellicht heb je de volgende toestanden gevonden, ook al noem je ze waarschijnlijk anders

1. Waakzaam, rondkijkend
2. Alert, klar voor actie, rondkijkend
3. Gealarmeerd, achter vijand aan lopend
4. Verdwaasd, rondlopend
5. Dood

Op basis van deze toestanden kun je een toestandsdiagram maken, waarin duidelijk wordt hoe de bewaker van de ene toestand in de andere komt. De getallen geven de toestanden aan zoals hierboven staat beschreven.

```{figure} 5-game-toestanden.png
```

Je kunt in het toestandsdiagram bijvoorbeeld zien dat als de bewaker in toestand 1 is en hij ziet een vijand, dan wordt de toestand van de bewaker 2.

In de bovenstaande uitwerking zie je totaal 5 toestanden en 6 toestandsovergangen. Misschien zijn er wel meer hoor, alleen in dit korte fragment kun je ze niet allemaal zien.

Het losse pijltje naar toestand 1 betekent dat dit de begintoestand is, oftewel de initiële toestand.

```{exercise} Verbreding: Unplugged Nooddienstregeling bij de spoorwegen
:label: opdracht3unplugged
Je kunt ook als inleiding ook de unplugged activiteit doen die je via de onderstaande link vindt.

[Nooddienstregeling bij de spoorwegen](http://www.informaticaunplugged.nl/de-werkvormen/nooddienstregeling-bij-de-spoorwegen/)
```

## Toestanden en toestandsovergangen
%bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4875018

Hieronder zie je een voorbeeld van een onderdeel van een frisdrankautomaat. Dit onderdeel houdt bij hoeveel geld de gebruiker van de automaat heeft ingeworpen. Voor het gemak gaan we uit van slechts twee munten: 50 cent en 1 euro. En alle frisdranken in de automaat kosten 2 euro.

```{figure} 5-frisdrank-toestanden.png
```

De bollen zijn _toestanden_. Dit toestandsdiagram kent dus vijf toestanden. De frisdrankautomaat begint in de starttoestand, dat is in dit geval de toestand ‘Start: 0 euro’. Bij elke toestand zie je enkele _overgangen_. Bijvoorbeeld de overgang van de _starttoestand_ ‘0 euro’ naar ‘0,5 euro’. Die toestandsovergang vindt plaats als de gebruiker begint met het inwerpen van een muntstuk van 50 eurocent.  
Je ziet dat een toestandsovergang ook naar dezelfde toestand kan gaan. Kijk maar bij de toestand ‘2 euro’. Na de toestandsovergang ‘Inworp 50 cent’ is de toestand nog steeds ‘2 euro’. 

```{figure} 5-frisdrank-toestanden-kleur.png
```

```{exercise} Frisdrankautomaat bedienen
:label: opdracht3frisbedienen

Je kunt zelf even met de frisdrankautomaat oefenen. Klik op de link hieronder om te activeren. Via de blauw en oranje knop kun je zogenaamd 50 cent of 1 euro inwerpen en dan zie je in welke toestand de automaat terecht komt.

[Bedien de frisdrankautomaat door hier te klikken.](https://maken.wikiwijs.nl/userfiles/2fe8467d59075d55fdbd2ce3f016c23bdeeeed34.html)

Op hoeveel manieren kun je twee euro inwerpen?
```

```{solution} opdracht3frisbedienen
:class: dropdown
Dat kan op de volgende vier manieren:
- 50ct + 50ct + 50ct + 50ct
- 50ct + 1 euro + 50ct
- 50ct + 50ct + 1 euro
- 1 euro + 50ct + 50ct

De meeste automaten geven teveel ingeworpen muntjes direct bij het inwerpen terug. Daarom tellen we die mogelijkheden niet mee in dit antwoord.
```

Een toestandsovergang wordt meestal uitgevoerd op basis van informatie uit één van de sensoren. Als iemand één euro in de frisdrankautomaat doet, wordt dat door één of meerdere sensoren gedetecteerd. Hoe dat precies werkt is hierbij niet belangrijk. Uit de toestandsdiagram kun je opmaken naar welke toestand de automaat moet gaan als iemand die euromunt inwerpt.

```{exercise} Frisdrankautomaat vragen
:label: opdracht3fris
Vul in. In welke toestand komt de automaat als iemand de volgende munten ingooit: 50 cent en nog eens 50 cent? Dat is toestand
`______`
. In welke toestand komt de automaat als iemand de volgende munten ingoot: 50 cent, 1 euro, 1 euro? Dat is toestand
`______`
.  Het is (wel of niet?)
`______`
mogelijkheid dat de automaat van de toestand ‘2 euro’ nog in een andere toestand komt.
```

```{solution} opdracht3fris
:class: dropdown
- `1`
- `2`
- `niet`
```

## Acties in een toestandsdiagram
%bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4875030

Het vorige toestandsdiagram is nog niet volledig, de gebruiker moet immers wel een frisdrank kunnen selecteren. In het volgende toestandsdiagram voegen we een overgang ‘selectie’ toe aan alle toestanden. ‘Selectie’ betekent dat de gebruiker een frisdrank kiest.

```{figure} 5-frisdrank-toestanden-actie.png
```

Aan een toestandsovergang kan een actie worden gekoppeld. Bij de frisdrankautomaat wordt de actie: ‘geef frisdrank’ uitgevoerd als de gebruiker een frisdrank selecteert en de toestand is: ‘2 euro’. Acties zijn altijd gekoppeld aan toestandsovergangen en niet aan toestanden. Een toestandsovergang mag één of meer acties hebben, maar dat hoeft niet. Voor het uitvoeren van acties worden vaak actuatoren gebruikt, zoals een lampje, display of motor.

In deze module gebruiken we steeds een dubbele punt om het onderscheid te maken tussen toestandsovergang en actie.

```
<toestandsovergang> : <actie>
```

```{exercise} Werking frisdrankautomaat
:label: opdracht3werkfris
Beschrijf de werking van deze frisdrankautomaat in 2 of 3 zinnen.
```

```{solution} opdracht3werkfris
:class: dropdown
**Uitleg**

De automaat houdt bij hoeveel geld (50 cent en 1 euro-muntstukken) er is ingeworpen. Pas als het totaal gelijk is of meer dan 2 euro kan de gebruiker een frisdrank selecteren. De automaat geeft geen geld terug (niet een erg klantvriendelijke automaat dus).
```

## Tabel met toestandsovergangen
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4875031

Voor het overzicht laten we de toestandsovergangen die naar dezelfde toestand verwijzen ook wel eens weg, zoals hieronder.

```{figure} 5-frisdrank-toestanden-tabel.png
```

Het is echter wel verstandig om goed na te denken over wat er in alle gevallen gebeurt. Bijvoorbeeld, wat gebeurt er in toestand ‘1 euro’ als de gebruiker een frisdrank selecteert? Door over alle mogelijkheden na te denken voorkom je fouten die je later veel tijd kosten om te herstellen. Je kunt dat ook in een tabel weergeven door alle toestanden te combineren met alle mogelijke toestandsovergangen. Daarbij geef je voor alle mogelijkheden aan wat de nieuwe toestand wordt.

```{table} 
| Toestand ↓ / Toestandsovergang → | Inworp 50 cent | Inworp 1 euro | Selectie |
| --- | --- | --- | --- | 
| Start: | 0 euro | 0,5 euro | 1 euro | 0 euro |
| 0,5 euro | 1 euro | |  |
| 1 euro |  |  |  |
| 1,5 euro |  |  |  | 	 
| 2 euro |  |  |  |
```	 

In de bovenstaande tabel zie je alle toestanden in de linker kolom. Je ziet ook alle mogelijke gebeurtenissen in de bovenste rij. Voor iedere combinatie moet de tabel beschrijven wat de nieuwe toestand wordt. Dit kan dus ook dezelfde toestand blijven. De tabel hierboven is nog niet volledig ingevuld.

```{exercise} Tabel toestandsdiagram
:label: opdracht3tabel
Maak de tabel hierboven af.
```

````{solution} opdracht3tabel
:class: dropdown
**Uitleg**

```{table}
| Toestand ↓ / Toestandsovergang → | Inworp 50 cent | Inworp 1 euro | Selectie |
| --- | --- | --- | --- | 
| Start: | 0 euro | 0,5 euro | 1 euro | 0 euro |
| 0,5 euro | 1 euro | 1,5 euro | 0,5 euro |
| 1 euro | 2 euro | 2 euro | 1 euro |
| 1,5 euro | 2 euro | 2 euro | 1,5 euro | 	 
| 2 euro | 2 euro | 2 euro | 0 euro: geef frisdrank |
```	
````

(physcomp-5-gebeurtenis)=
## Verbreding: Toestandsovergang bij gebeurtenis of status

In het voorbeeld van de frisdankautomaat is er een toestandsovergang als er wat gebeurt. De gebeurtenis is het inwerpen van een muntje. De gebeurtenis duurt kort, het is een moment waarop je het muntje inwerpt. Je kunt je voorstellen dat het inwerpen het moment is waarop het muntje tegen een drukknopje komt. Het moment dat het muntje tegen de drukknop komt, verandert de drukknop van niet-ingedrukt naar wel-ingedrukt. Een gebeurtenis is dus een verandering van een waarde. De waarde is in dit geval niet-ingedrukt of wel-ingedrukt.

Je kunt een toestandsdiagram ook anders maken. Een toestandsovergang vindt dan niet plaats bij een verandering van een waarde, maar als een sensor (bijvoorbeeld een drukknop) een bepaalde waarde heeft. Je hebt dan twee keer zoveel toestanden nodig. Elke keer als er de schakelaar wordt ingedrukt door een muntje ga je naar een volgende toestand waarin gewacht wordt tot het muntje verder valt. Voor een mens duurt dat wachten zo kort dat je het niet eens merkt, maar voor de computer in de frisdrankautomaat duurt dat wachten best lang. Als het muntje verder is gevallen, dan staat de schakelaar weer in de niet-ingedrukt stand. Je gaat dan naar de toestand met het nieuwe bedrag.

Je kunt dus kiezen voor twee soorten toestandsovergangen:
1. als er een verandering van een waarde is (een gebeurtenis)
2. als er een bepaalde waarde wordt gezien (status)

Bij het voorbeeld van de frisdrankautomaat in dit hoofdstuk hebben we gewerkt met manier 1 (gebeurtenissen), omdat we dan minder toestanden hoefden te gebruiken. In het volgende hoofdstuk [](#physcomp-h6) zul je beide manieren tegen komen.

In het hoofdstuk [](#physcomp-h7) gebruiken we vooral manier 2 (status), omdat toestandsdiagrammen die gemaakt zijn op manier 2 gemakkelijker om te zetten zijn in code.

## Regels voor een toestandsdiagram
% bron: https://maken.wikiwijs.nl/135422/Cyclus_1#!page-4875036

Een toestandsdiagram is gebonden aan strenge regels:

- Een toestandsdiagram bestaat uit toestanden (bollen) en toestandsovergangen (pijlen)
- Alle toestanden worden weergegeven als bollen. In de bol staat een korte beschrijving van de toestand.
- Er is altijd precies één starttoestand, die herken je aan de pijl die niet verbonden is aan een andere toestand.
- Alle toestandsovergangen worden weergegeven als een pijl, die één kant op wijst. Bij de pijl staat een korte beschrijving van de toestandsovergang.
- Een toestand kan nooit twee of meer keer dezelfde toestandsovergang hebben.
- Een toestandsovergang mag dezelfde toestand als begin en eind hebben.
- Bij een toestandsovergang mogen één of meerdere acties staan. In deze module gebruiken we steeds een dubbele punt om het onderscheid te maken tussen toestandsovergang en actie.

```{seealso} Toestandsdiagrammen tekenen
Je kunt toestandsdiagrammen prima op papier tekenen. Dat gaat vaak het snelst, maar pas op dat het wel leesbaar blijft. Een handige tool om toestandsdiagrammen mee te maken vind je via de volgende site.

[Finite State Machine Designer](http://madebyevan.com/fsm/)
```