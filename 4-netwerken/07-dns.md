(netwerken-h07)=
# DNS: adressen opzoeken

## Inleiding

Je typt een websiteadres in de browser, bijvoorbeeld `http://nieuws.school.test/rooster.html`. Zo’n adres heet een {term}`URL`. Het bevat een protocol (`http`), de naam van een computer (de hostnaam `nieuws.school.test`) en een pad (`/rooster.html`). Het netwerk kan niets met een naam: het heeft een {term}`IP-adres` nodig. Het {term}`DNS` zoekt dat IP-adres bij de hostnaam.

**Laag:** {term}`toepassingslaag`. **Vraag:** hoe vindt een computer het IP-adres dat bij een naam hoort?

## Klassikaal: een naam omzetten in een adres

Maak twee rollen: clients en een DNS-balie. De DNS-balie heeft alleen een lijst met namen en bijbehorende adressen. Alle clients krijgen een URL, zoals `http://nieuws.school.test/sport.html`.

1. Laat de clients eerst de hele URL aan de DNS-balie voorleggen. De balie kent alleen namen en kan niets met het pad.
2. Spreek af dat clients alleen de hostnaam vragen. De balie antwoordt met een adres.
3. Verander op de lijst alleen het adres dat bij een naam hoort. De URL van de clients blijft gelijk, maar ze komen nu bij een ander adres uit.

Bespreek wat de DNS-balie wel en niet weet.

## DNS: namen en adressen koppelen

Het Domain Name System koppelt namen aan gegevens, waaronder IP-adressen. Een {term}`A-record` koppelt een naam aan een IPv4-adres; voor IPv6 is er het AAAA-record.

Je computer vraagt dit meestal aan een {term}`resolver <DNS-resolver>`. Die heeft het antwoord misschien al in een {term}`cache`. Zo niet, dan zoekt hij het op, eventueel via verwijzingen naar andere DNS-servers. DNS is wereldwijd verdeeld: geen enkele server kent alle namen. Rootservers en servers voor topleveldomeinen verwijzen door; gezaghebbende servers beheren de gegevens van hun eigen domeinen.

Een eenvoudige DNS-vraag gaat vaak via UDP-poort 53; DNS kan ook {term}`TCP` gebruiken.

DNS levert geen webpagina en vertaalt niet de hele URL. Bij `http://nieuws.school.test/sport.html` zoekt DNS alleen de hostnaam `nieuws.school.test` op. Het pad `/sport.html` gaat pas later naar de webserver. Namen met `.test` zijn bedoeld voor oefenomgevingen en bestaan niet op het publieke internet.

### Voorbeeld

DNS antwoordt dat `nieuws.school.test` bij `192.168.20.10` hoort. Je computer kan nu verkeer naar dat adres sturen. Bij een volgende vraag kan het antwoord uit een cache komen, dus niet elke vraag start een nieuwe zoekactie over de hele wereld.

::: {exercise} Zonder Filius: wie weet het?
:label: nw07-o1

1. Welke DNS-vraag hoort bij `http://nieuws.school.test/rooster.html`?
2. Waarom hoeven links niet te veranderen als een website naar een nieuw IP-adres verhuist?
3. Een computer vraagt kort na elkaar twee keer naar dezelfde naam. Waarom kan het tweede antwoord sneller komen?
:::

::: {solution} nw07-o1
:class: dropdown

1. Vraag naar het adres van `nieuws.school.test`, niet naar `/rooster.html`.
2. Alleen de DNS-koppeling verandert; de naam blijft hetzelfde. Oude antwoorden kunnen nog tijdelijk in een cache staan.
3. Het eerste antwoord is bewaard in een cache, dus de resolver hoeft het niet opnieuw op te zoeken.
:::

::: {exercise} Filius: een DNS-server instellen
:label: nw07-o2

1. Open `06-transport.fls`. Computer C heeft adres `192.168.20.10`.
2. Voeg aan het netwerk van C een DNS-server toe met adres `192.168.20.53`, masker `255.255.255.0` en {term}`gateway` `192.168.20.1`.
3. Installeer en start de DNS-server. Maak een adresrecord voor `nieuws.school.test` naar `192.168.20.10`.
4. Stel op A het DNS-serveradres `192.168.20.53` in. Laat de gateway goed staan.
5. Ping vanaf A eerst `192.168.20.10` en daarna `nieuws.school.test`.
6. Zoek in de gegevensuitwisseling de DNS-vraag, het DNS-antwoord en de daaropvolgende ping. Welke computer geeft het DNS-antwoord?
7. Bewaar als `07-dns.fls`.
:::

::: {solution} nw07-o2
:class: dropdown

Beide pings werken. Bij de ping op naam gaat eerst een DNS-vraag naar `192.168.20.53`, die het adres `192.168.20.10` teruggeeft. Daarna gaat de ping naar `192.168.20.10`. De DNS-server levert alleen het adres en doet zelf niets met de ping. Dit voorbeeld heeft één lokale DNS-server en bootst de wereldwijde DNS-structuur niet na.
:::
