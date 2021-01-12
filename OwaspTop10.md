
# OWASP top 10 onderzoek
## Inleiding
Beveiliging in softwareontwikkeling is belangrijker dan ooit te voren. Je leest het vrijwel iedere week in het nieuws "Bedrijf binnen gedrongen door cybercriminelen" dit gaat vaak om kleinere bedrijven die geen groot budget aan beveiliging hebben, maar zelfs grote ondernemingen zijn niet risicovrij. Zo kwam Freepik(een van de grootste sites voor grafische content die ik zelf ook regelmatig gebruik) in augustus met het nieuws dat cybercriminelen 8.3 miljoen aan gebruiker emails en wachtwoord hashes gestolen hebben met een SQL injection attack.

Het is dus zo dat met maar een fout je applicatie misbruikt kan worden door cybercrimenelen wat vaak ernstige gevolgen heeft. De OWASP top 10 is een lijst die de top 10 meest kritieke beveiligingsrisico's voor webapplicaties bevat. In dit document bekijk ik de OWASP top 10 en beschrijf ik hoe je de beveiliging risico’s kan voorkomen.

## OWASP top 10

  - [1. Injection](#1.-injection)
  - [2. Broken Authentication](#2.-broken-Authentication)
  - [3. Sensitive Data Exposure](#3.-sensitive-data-exposure)
  - [4. XML External Entities (XXE)](#4.-XML-External-Entities-(XXE))
  - [5. Broken Access Control](#5.-Broken-Access-Control)
  - [6. Security Misconfiguration](#6.-Security-Misconfiguration)
  - [7. Cross-Site Scripting (XSS)](#7.-Cross-Site-Scripting-(XSS))
  - [8. Insecure Deserialization](#8.-Insecure-Deserialization)
  - [9. Using Components with Known Vulnerabilities](#9.-Using-Components-with-Known-Vulnerabilities)
  - [10. Insufficient Logging & Monitoring](#10.-Insufficient-Logging-&-Monitoring)
  


## 1. Injection
<b>Uitleg</b><br>
Injectie is een van de meest gebruikte cyberaanvallen op web applicaties. Zo blijkt uit een [Akamai report][1] dat in het tweede kwartaal van 2017 maar liefst 51% van alle cyber aanvallen on web applicaties gebruik maakte van injectie.

Een injectie kan plaatsvinden als onvertrouwde gebruikersdata kan worden geïnterpreteerd als onderdeel van de query. De aanvaller kan op deze manier onbedoelde commando's activeren of kan data verkrijgen zonder de benodigde autorisatie.

<b>Voorkomen</b><br>
Maak gebruik van Parameterized queries. Parameterized queries voorkomen injectie door de query op te bouwen met behulp van een context over welk onderdeel van de query gegevens zijn en welk onderdeel deel uitmaakt van de query opbouw.

## 2. Broken Authentication
<b>Uitleg</b><br/>
Broken authenticatie treed op wanner applicatiefuncties met betrekking tot authenticatie en sessiebeheer verkeerd worden geïmplementeerd.

Door dit soort fouten kan een aanvaller de verificatiemethoden die door de web applicatie gebruikt word onderscheppen of omzeilen

<b>Voorbeelden</b></br>
Voorbeelden van broken authentication zijn als een applicatie:
- Geautomatiseerde aanvallen zoals credential stuffing worden toegestaan
- Brute Force attacks worden toegestaan
- Zwakke of bekende gebruikerswachtwoorden toestaat
- Gebruikt zwakke of ineffectieve processen voor het herstellen van inloggegevens, zoals "op kennis gebaseerde antwoorden"
- Slaat wachtwoorden op als tekst, versleuteld of zwak gehasht
- Heeft geen of slechte multi-factor authenticatie
- Geeft sessie-ID's weer in de URL
- Maakt gebruikersessies sessie-ID's of authenticatietokens niet correct ongeldig na een logout

<b>Voorkomen</b><br>
Maak gebruik van externe libraries die de beveiliging voor je regelen en zorg dat deze libraries up-to-date zijn. Zorg er ook voor dat elk component wat deel uit maakt van de security grondig getest is.


## 3. Sensitive Data Exposure
<b>Uitleg</b><br/>
Sensitive data exposure neemt plaats als gevoelige data niet voldoende word beschermt door de developer waardoor deze data opgehaald kan worden door onbevoegde. 

Zo kan het zijn dat een developer bank gegevens of credentials opslaat bij een gebruikersprofiel en deze gegevens dus ook telkens onnodig en onverantwoord worden opgehaald.

<b>Voorkomen</b>
- encrypt data tijdens transport en rest
- verzend geen onnodige data zoals credentials bij een profiel request
- Gebruik de laatste encryptie algorithmes 
- Schakel caching uit op formulieren die gegevens verzamelen.


## 4. XML External Entities (XXE)
<b>Uitleg</b>
XXE aanvallen komen voor wanneer een webapplicatie gebruikt maakt van een slecht geconfigureerde XML parser. De aanvaller kan XML data die Externe entities bevatten laten uitvoeren door de parser. Deze aanval kan gebruikt worden voor het verkrijgen van vertrouwelijke gegevens, denial of service, SSRF, internal port scanning en meer

<b>Voorbeelden</b></br>
Een applicatie kan kwetsbaar zijn voor XXE aanvallen als:
- De applicatie XML uploads accepteert, en vooral van niet vertrouwde bronnen
- De applicatie een XML processor bevat die DTD niet heeft uitgeschakeld

<b>Voorkomen</b>
- Gebruik waar mogelijk minder complexe gegevensindelingen zoals JSON
- Patch of upgrade alle XML-processors en libraries die door de applicatie worden gebruikt.
- Schakel XML externe entiteit en DTD verwerking uit in alle XML-parsers in de applicatie
  
## 5. Broken Access Control
<b>Uitleg</b><br/>
Broken acces control aanvallen nemen plaats als de applicatie beperkingen op wat geauthentiseerde  gebruikers mogen doen niet goed afdwingt. Aanvallers kunnen met deze implementatie  fout misbruik maken door bijvoorbeeld toegang te krijgen tot functionaliteiten waar je als normale gebruiker niet bij hoort te kunnen. Zo kan een aanvaller bijvoorbeeld ander gebruikers beheren, vertrouwelijke gegevens bemachtigen, etc.

<b>Voorkomen</b>
- Toegang tot functionaliteit standaard weigeren.
- Gebruik toegangscontrolelijsten en op rollen gebaseerde authenticatiemechanismen.
- Gebruik externe vertrouwde libraries voor de implementatie van autorisatie.
- Test alle componenten die autorisatie bevatten.


## 6. Security Misconfiguration
<b>Uitleg</b><br/>
Security misconfiguration is de meest voorkomende beveiliging fout van web applicaties. Security mis configureren  vindt plaats wanneer er configuratie fouten worden gemaakt omtrent beveiliging van de site. Denk aan het misconfiguren van open cloud storage, http requests headers en het weergeven van gedetailleerde error messages

<b>Voorkomen</b><br/>
Schakel standaard alles uit bijvoorbeeld:
- Administratie interfaces
- gedetailleerde error messages
- standaard login
- Configureer de server om ongeautoriseerde toegang, directory listing, enz. Te voorkomen.
- Voer periodieke scans uit om security misconfiguration te detecteren.

## 7. Cross-Site Scripting (XSS)
<b>Uitleg</b><br/>
XSS komt voor wanneer een applicatie ongevalideerde gebruikersdata weergeeft op een webpagina. Met een XSS aanval kan een aanvaller javascript laten uitvoeren op slachtoffers webbrowser. Deze scripts kunnen bijvoorbeeld gebruikers sessies stelen, website onbruikbaar maken, Phising aanvallen en het omleiden naar onveilige sites.

<b>Voorkomen</b><br/>
-  Valideer alle gebruiker inputs en gebruik hier betrouwbare libraries voor.
-  HTML Escape XSS kan worden voorkomen door alle gebruikersinvoer op te sanitize voordat deze wordt verwerkt en / of teruggegeven aan de browser.
-  Gebruik javascript textContent/innerText voor het weergeven van gebruiker data.

## 8. Insecure Deserialization
<b>Uitleg</b><br/>
Insecure deserialization komt voor wanneer een applicatie user input deserialiseert zonder verificatie. Een aanvaller kan kwaadaardige code opslaan in het geserialiseerde object en als de applicatie geen verificatie uitvoert voor de deserialisatie kan de kwaadaardige code worden uitgevoerd.

<b>Voorkomen</b><br/>
- Vertrouw geen ongevalideerde of onvertrouwde input. 
- Gebruik een web applicatie firewall die kwaadaardige of ongeautoriseerde deseralisatie kan detecteren

## 9. Using Components with Known Vulnerabilities
<b>Uitleg</b><br/>
Using components with known vulnerabilities vind plaats wanneer een applicatie gebruik maakt van een component(e.g., framework, libraries) wat beveiliging fouten bevat die algemeen bekend zijn. Dit kan in erge gevallen er voor zorgen dat een server kan worden opgenomen omdat het component dezelfde rechten als de server heeft.

<b>Voorkomen</b><br/>
- Zorg ervoor dat de gebruikte componenten regelmatig geüpdatet worden
- Scan regelmatig de applicatie voor exploits

## 10. Insufficient Logging & Monitoring
<b>Uitleg</b><br/>
 onvoldoende logboekregistratie en monitoring, in combinatie met geen of onvoldoende met incidentrespons zorgt ervoor dat een aanvaller een applicatie nog verder aan te vallen, ongedetecteerd kunnen blijven, naar meer applicaties kan verspreiden en gegevens te stelen/manipuleren/vernietigen.

 De OWASP top 10 stelt dat "Uit de meeste onderzoeken naar inbreuken blijkt dat de tijd om een inbreuk te detecteren meer dan 200 dagen duurt, meestal gedetecteerd door externe partijen in plaats van interne processen of monitoring." hieruit blijkt dus dat het erg belangrijk is dat er aandacht aan word besteed.


<b>Voorkomen</b><br/>
- Zorg ervoor dat alle belangrijke applicatie event worden gelogd, denk aan logins, toegangscontrole mislukkingen, server-side input validatie, e.g.
- Zorg ervoor dat de logs op een manier gegenereerd kunnen worden die makkelijk kan worden gebruikt door gecentraliseerde oplossingen voor logboek beheer.
- Zorg voor effectieve monitoring en alarmering zodat verdachte activiteiten tijdig worden gedetecteerd en erop gereageerd.

## Conclusie
Het schrijven van dit document heeft mij erg geholpen als het gaat om een grotere bewustwording op beveiligings gebied. Op mijn vooropleiding heb ik een kleine cursus gehad over beveiliging waardoor ik al bekend was met een aantal van deze technieken(Injection, XSS, Port scanning). Ik vond het erg interessant om te lezen over de technieken waar ik nog niet bekend mee was en dan vooral XXE en insecure deserialization.

[1]:https://www.akamai.com/de/de/multimedia/documents/state-of-the-internet/q2-2017-state-of-the-internet-security-report.pdf
