(netwerken-h10)=
# DHCP: automatisch instellen

## Inleiding

Tot nu toe stelde je IP-adressen, maskers en gateways met de hand in. Dat is onwerkbaar als er elke dag nieuwe apparaten bij komen, zoals telefoons en laptops. Met {term}`DHCP` krijgt een apparaat die instellingen automatisch van een server.

**Laag:** {term}`toepassingslaag`. **Vraag:** hoe krijgt een apparaat zonder instellingen toch een IP-adres, masker, gateway en DNS-server?

## DHCP: wie stelt al die adressen in?

Een {term}`client` die op een netwerk wordt aangesloten, kent nog geen netwerkgegevens. Hij zoekt een {term}`server` met vier berichten:

1. **Discover:** de client roept naar iedereen dat hij een configuratie zoekt.
2. **Offer:** een DHCP-server biedt een adres en andere instellingen aan.
3. **Request:** de client vraagt dat aanbod aan.
4. **Acknowledge:** de server bevestigt.

Behalve het {term}`IP-adres` kan de configuratie onder andere het {term}`masker <subnetmasker>`, de {term}`gateway` en DNS-serveradressen bevatten. Het adres wordt voor beperkte tijd uitgeleend: de {term}`lease`. Een DHCP-server is geen DNS-server, ook al kan één computer beide diensten uitvoeren.

De eerste berichten zijn broadcasts, want de client heeft nog geen adres en kent de server niet. {term}`Routers <router>` sturen broadcasts niet vanzelf door naar andere netwerken. In grotere netwerken kan een speciaal ingestelde DHCP-relay dat oplossen; dat stel je hier niet in.

::: {exercise} Zonder Filius: DHCP volgen
:label: nw10-o1

1. Waarom kan een nieuwe client zijn DHCP-vraag niet rechtstreeks aan één server richten?
2. Welke vier instellingen kan een client via DHCP krijgen?
3. Waarom bewijst een geslaagde DHCP-configuratie niet dat DNS en de webserver werken?
:::

::: {solution} nw10-o1
:class: dropdown

1. Hij heeft nog geen IP-adres en kent het adres van de server niet. Daarom begint hij met een broadcast.
2. IP-adres, subnetmasker, gateway en DNS-serveradres.
3. DHCP stelt alleen de netwerkinstellingen in. DNS en de webserver zijn aparte diensten.
:::

::: {exercise} Filius: automatische instellingen
:label: nw10-o2

1. Werk in een kopie van `08-website.fls`. Installeer op de DNS-server ook de DHCP-server, als jouw Filius-versie die heeft.
2. Kies voor het server-LAN een pool van `192.168.20.100` tot en met `192.168.20.120`, masker `255.255.255.0`, gateway `192.168.20.1` en DNS `192.168.20.53`. Houd vaste serveradressen buiten de pool.
3. Voeg één nieuwe client toe op dezelfde {term}`switch` en stel die in op automatische adresconfiguratie. Start de DHCP-server en vraag de configuratie aan.
4. Controleer de ontvangen instellingen en bezoek de oefenwebsite op naam. Wat heeft DHCP ingesteld en welke dienst levert nog steeds de pagina?
5. Bewaar als `10-dhcp.fls`.
:::

::: {solution} nw10-o2
:class: dropdown

De client krijgt een vrij adres uit de pool en de ingestelde extra gegevens. DHCP levert de netwerkconfiguratie, DNS de naamkoppeling en de webserver de pagina. Menunamen en opties kunnen per Filius-versie verschillen.
:::
