# Uitbreidingen
In dit hoofdstuk staan suggesties voor uitbreidingen die je kunt maken. Natuurlijk kun je ook zelf uitbreidingen verzinnen.

## Ideeen voor uitbreidingen
- 1 pagina per product toevoegen (nieuw entrypoint :id, nieuwe static webpagina, aangepast javascript, linkje op oude webpagina)
- 1 bestelpagina (nieuwe static webpagina)
- meer tabellen en producten
- wie dit kocht kocht ook dat / dit product past bij deze producten 
- sorteren
- meerdere plaatjes per product
- verschillende eigenschappen per soort (1:1)
- varianten, zoals maten
- prijs range filter 
- ...

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