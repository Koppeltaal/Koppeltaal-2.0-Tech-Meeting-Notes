# MEMO


##  Advies technische kopgroep Koppeltaal 2.0 leveranciers betreffende koppeltaal FHIR profiel (-en)

### Aanwezig
Jan-Wijbrand Kolman, Theo Stolker, Joris Scharp en Roland Groen

## Inleiding

In de extra meeting KT 2.0 leveranciers tech meetup d.d. 23 jun. 2022 is ter agenda gekomen de discussie rond de koppeltaal profielen. Tijdens de simulaties zijn zijn een aantal bevinden gedaan, deze vormen voor ons het startpunt van de discussie. 


## Profielen in koppeltaal

We stellen vast dat er in bij het vaststellen van huidige koppeltaal er het beeld wordt  gecreëerd dat een enkel FHIR profiel het uitgangspunt is. Als leveranciers stellen we vast dat dit onmogelijk is. We zien hier drie knelpunten:



* Sommige attributen zijn voor de ene applicatie verplicht terwijl ze in andere domeinen niet  voorkomen (e-mail en volledig adres, 06-nummer).
* Sommige entiteiten komen in domeinen niet  voor en zijn voor bepaalde applicaties wel vereist (CareTeam).
* Verder is er ook zo dat er use cases zijn die (bewust) niet in KT1.x gerealiseerd zijn door de beperkingen die koppeltaal oplegt (anoniem gebruik).

In de huidige koppeltaal-implementatie zorgt dit voor dialecten. 


## Onze analyse en oplossingsrichtingen


### Profielen per domein

FHIR profielen zijn er om een reden. En de reden is deze. Een instelling zou per domein het FHIR profiel moeten vaststellen en publiceren. Hiermee kan, afhankelijk van het type domein de beschikbare en vereiste en gewenste entiteiten en velden vastleggen.

Naast het publiceren van het profiel per domein kan in het applicatie register per applicatie worden vastgelegd welke velden worden aangeleverd, ondersteund en/of vereist zijn. Domeinbeheer kan zo een domein samenstellen op basis van het profiel.

Het voordeel van deze aanpak is dat eenduidig zichtbaar is wat er in een domein beschikbaar is en of applicaties in het domein gekoppeld kunnen worden.


## Een vast profiel met launch-failures

Hoewel we voorstander zijn van het profiel per domein aanpak dragen we alsnog een oplossing aan voor het gebruik van één enkel FHIR profiel. De basis ligt in de volgende aanname:

_“Verschillende applicaties met  verschillende eisen rond velden en/of entiteiten kunnen deelnemen in een domein, zolang zij a)  de entiteiten die ze niet kunnen verwerken negeren en b) een manier hebben om, in dat geval dat dit een probleem is, het domein hiervan op de hoogte te stellen”_

Laten we dit iets uitwerken. 

Een applicatie die een e-mail adres nodig heeft kan allen Patient resources zonder e-mail adres gewoon negeren, hier is niets mis mee. Tot het moment  dat er een behandeling gestart  wordt. Dan niet meer. 

De vraag rijst dan: hoe stellen we het domein op de hoogte? De meest eenvoudig oplossing hiervoor is door het mogelijk te maken de launch te laten falen. Dit kan door de status van de activity op “failed” te zetten, en deze van een failure line te voorzien. In het voorbeeld hierboven geeft de applicatie dan aan: 

“Een patiënt zonder e-mail adres kan niet deelnemen aan deze module, voer het e-mail adres op om de patiënt van de module gebruik te  kunnen laten maken”

Als alternatief zou de applicatie gebruik kunnen maken van de HTI assumptie en de gebruiker vragen om de ontbrekende informatie.


![drawing](https://docs.google.com/drawings/d/1a6v2xGE8LvDGXpL03eVXIwzzMvE6Mxg5GwTzg8n7Zcw/export/png)
