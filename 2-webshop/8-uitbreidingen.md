(webshop-uitbreidingen)=
# Uitbreidingen


```{pull-quote}

```

```{figure} scherm6.png
Schermafdruk van een voorbeeld van een webshop aan het einde van dit hoofdstuk.
```

In dit hoofdstuk staan suggesties voor uitbreidingen die je kunt maken. Natuurlijk kun je ook zelf uitbreidingen verzinnen.

## Opdracht: Uitbreidingen maken

Je kunt je webshop uniek maken door er uitbreidingen aan toe te voegen. Je kunt daarvoor ideeën uit de lijst hieronder gebruiken, maar het is natuurlijk het leukst als je creatief bent en zelf iets verzint. 

```{attention} Ideeen voor uitbreidingen
Ter inspiratie staan hier een aantal ideeën voor uitbreidingen. Uitbreidingen met één of twee sterren zijn eenvoudiger dan uitbreidingen met drie of vier sterren.

Soort producten (1:n) ⭐️
: Voeg een soort of andere eigenschap toe aan je artikelen, bijvoorbeeld het soort kledingstuk.
: Gebruik kennis uit hoofdstuk 4

Wie dit kocht, kocht ook dat (n:m) ⭐️
: Voeg toe welke artikelen veel met elkaar gekocht worden.
: Gebruik kennis uit hoofdstuk 5

Meerdere plaatjes per product ⭐️ of ⭐️⭐️ 
: Toon meerdere plaatjes per artikel.
: Een verschillend aantal plaatjes voor elk artikel moet mogelijk zijn.
: Als je een diashow voor de plaatjes toevoegt, dan is het een tweede ster.
: Gebruik kennis uit hoofdstuk 2 en eventueel 7

Sorteren van producten ⭐️⭐️
: Gebruik kennis uit hoofdstuk 6 en 7

Prijs range filter ⭐️ of ⭐️⭐️
: Maak een filter waarmee je op een minimale en maximale prijd kunt filteren.
: Als je de laagste en hoogste prijs van de gefilterde artikelen gebruikt voor de in te stellen range, dan is het een tweede ster.
: Gebruik kennis uit hoofdstuk 6 en 7

Merken pagina's ⭐️⭐️
: Maak een pagina waarop je informatie over een merk kunt vinden.
: Voeg een tabel met informatie over merken toe aan je database.
: Maak een nieuw API entrypoint `/api/brand/id`, waarbij het id het nummer van het brand is
: Gebruik kennis uit hoofdstuk 7 en 8

Favorieten ⭐️⭐️⭐️ of ⭐️⭐️⭐️⭐️
: Maak een winkelmandje waarin bezoekers hun artikelen kunnen bewaren
: Bewaar de winkelmand in de lokale opslag van de browser
: Zoek zelf kennis op over hoe dit werkt

Inloggen ⭐️⭐️⭐️ of ⭐️⭐️⭐️⭐️
: Laat beheerders inloggen via een webpagina informatie in de database aan passen, bijvoorbeeld aktieprijzen of actuele voorraad
: Het wachtwoord moet door de API worden gecontrolleerd
: Het wachtwoord moet versleuteld worden verzonden, dus je mag het niet als parameter in de URL stoppen.
: Zoek zelf kennis op over hoe je dit kunt maken
```

:::{note}Opdracht a)
### Maak een uitbreiding
Kies een uitbreiding uit de ideeën hierboven of verzin zelf een uitbreiding. Maak de uitbreiding en geef in de beschrijving van de commit(s) aan om welke uitbreiding het gaat. In het bestand `uitbreidingen.md` hou je een lijst bij van uitbreidingen die je gemaakt hebt.

Als je een uitbreiding klaar hebt, dan kies je een nieuwe uitbreiding. Zo herhaal je deze opdracht totdat je webshop helemaal naar jullie zin is.
:::

```{hint} Tips
:class: dropdown
- Begin met enkele kleine uitbreiding van één of twee sterren, probeer daarna pas de grotere uitbreidingen van drie of vier sterren.
- Maak afspraken met elkaar wie welke uitbreiding maakt, probeer te zorgen dat je niet tegelijk in hetzelfde stuk code hoeft te werken.
```

## Uitleg voor uitbreidingen
:::{note} Uitleg
### Structuur van endpoints

Een goede structuur van je endpoints zorgt ervoor dat je API bruikbaar blijft als iemand een nieuwe frontend maakt. Er zijn geen regels die een goed structuur garanderen. Er zijn wel richtlijnen die helpen bij het maken van een goede structuur. Hier zijn enkele veelgebruikte richtlijnen.

Gebruik hiërarchie
: Geef aan dat iets *onderdeel* is van iets anders:
: ✅ /gebruikers/42/boeken → alle boeken van gebruiker 42  
: ✅ /klassen/5v/leerlingen → alle leerlingen in klas 5v

Gebruik queryparameters 
: Bijvoorbeeld voor filters, sorteren of paginering
: ✅ /boeken?jaar=2024  
: ✅ /gebruikers?rol=docent&sort=naam  

Gebruik zelfstandige naamwoorden in meervoud, geen werkwoorden
: ✅ /gebruikers
: ❌ /gebruiker
: ❌ /getGebruiker

Gebruik koppelstreepjes tussen woorden, geen hoofdletters
: ✅ /middelbare-scholen
: ❌ /middelbare_scholen
: ❌ /Middelbare-Scholen

Houd het consistent
: Gebruik een duidelijke en eenduidige structuur door je hele API. Als je bijvoorbeeld `/producten` gebruikt, noem het dan niet ergens anders `/artikelen`.
:::