### analyse document
# Echoo 
## Inhoudsopgave
1. [Inleiding](#Inleiding)
2. [Requirements](#Requirements)
3. [Prototype](#Prototype)
<br>

## Inleiding
<p><b>Echoo</b> is een social media platform waar gebruikers post kunnen plaatsen en bekijken. Het platform is gebaseerd op Reddit maar neemt inspiratie van verschillende andere social media platformen en combineert deze tot een uniek platform. 
De voornaamste doelen van Echoo zijn om een platform te maken waar gebruikers:

* posts kunnen creëren, bekijken en beoordelen(like/dislike)
* groepen kunnen aanmaken, betreden en verlaten
* reacties kunnen achterlaten op een post of op een andere reactie
* andere gebruikers kunnen volgen
* chats kunnen starten met een andere gebruikers  

Het uiteindelijke doel voor Echoo is om een social media platform te maken waar nieuwe content gegenereerd wort door AI. Dit valt echter voor nu buiten de scope van het project.

De frontend van de applicatie wordt gemaakt in React en zal voor gebruikers beschikbaar zijn via een webbrowser. De backend wordt ontwikkeld in Java Spring boot. Een groot focuspunt van Echoo is distrubatie en schaalbaarheid aangezien het als social media platform bestendig moet zijn tegen een groot nummer aan verschillende clients. Op basis hiervan zal ik veel van mijn technologie keuzes toelichten.</p>

<br>

## Requirements
*	FR-01 De gebruiker moet kunnen inloggen op zijn account. 
    *	K-01.1 De gebruiker moet de optie hebben om ingelogd te blijven na verlaat van de website met behulp van cookies 
    *   K-01.2 Nadat een gebruiker 5x inloggegevens foutief heeft ingevoerd zal de gebruiker 5minuten geen gebruik kunnen maken van de login functionaliteit. 
    *	B-01.1 een gebruiker kan inloggen door zijn geregistreerde e-mailadres en wachtwoord op te geven. 
*	FR-02 Er moet onderscheid zijn tussen een gebruiker account en een administratief account. 
*	FR-03 Een gebruiker moet een nieuw account kunnen aanmaken. 
    *	K-03.1 Voor het activeren van een nieuw account moet er een bevestigingsmail gestuurd worden door het systeem en bevestigd worden door de gebruiker.
    *	B-03.1 Voor een nieuw account dient er een unieke gebruikersnaam, een emailadres en  een wachtwoord opgegeven te worden
*   FR-04 Een ingelogde gebruiker moet instaat zijn zijn/haar account te beheren. 
    *   B-04.1 Alleen een administratieaccount kan een gebruikers administratiestatus wijzigen. 
    *	B-04.2 Een gebruiker moet in staat zijn om zijn opgegeven gebruikersnaam, email, beschrijving en wachtwoord te veranderen
*	FR-05 Een gebruiker kan een nieuwe groep(subreddit) aanmaken 
    *	B-05.1 voor het aanmaken van een nieuwe groep dient er een unieke groepsnaam en een beschrijving opgegeven te worden

*	FR-06 De groepseigenaar kan andere gebruikers promoveren tot een nieuwe groepsstatus
    *	K-06.1 De groepsrollen van hoogste rang naar laagste bestaan uit “owner/co-owner, administrator, elder, member”

*	FR-07 Een gebruiker kan een nieuwe post plaatsen in een gekozen groep 
    *	B-05.1 De gebruiker zelf een Echoo administrator en een groeps administrator of owner kunnen een post verwijderen.
*	FR-08 Een gebruiker kan een bericht achter laten op een post 
    *	K-07.1 Er dient zichtbaar onderscheidt gemaakt te kunnen worden tussen een bericht van de post maker en dat van een andere gebruiker.
*	FR-09 Een gebruiker kan een reactie plaatsen op een bericht van een andere gebruiker
    *	K-07.1 Er dient zichtbaar aangetoond  te kunnen worden dat het gaat om een reactie op een specifiek ander bericht

*	FR-10 Een gebruiker moet in staat zijn om een om een groep zijn post geschiedenis te kunnen sorteren
    *	K-09.1 Een groep zijn post geschiedenis moet filtreerbaar zijn op nieuwste en op populairst binnen een bepaalde tijd

*	FR-11 Een gebruiker moet instaat zijn om een privé bericht naar een ander gebruiker te kunnen sturen. 
*	FR-12 Een gebruiker moet instaat zijn om een andere gebruiker te volgen. 

*	FR-13 Een gebruiker moet instaat zijn om een andere gebruiker te blokkeren. 

*	FR-14 Een administrator is gemachtigd om andere gebruiker accounts te beheren. 
*	FR-15 Een gebruiker moet kunnen uitloggen. 
    *	B-11.1 Een gebruiker dient ingelogd te zijn. 
*	FR-15 Een gebruiker kan een nieuw wachtwoord aanmaken met behulp van een speciale link via email.
<br/> 

*	K-ALG.01 Bij onjuiste invoer moet een duidelijke foutmelding getoond worden. 
*	K-ALG.02 Bij een netwerk/server error moet er een duidelijke foutmelding getoond worden. 
*	K-ALG.03 De webapplicatie beschikt over een verzorgde en duidelijke lay-out/ui. 
*	K-ALG.04 De webapplicatie dient alle client aanvragen uiterst binnen 3 seconden te verhandelen. 

<br>

## Prototype
[Link naar designs](https://xd.adobe.com/view/b5ab4816-3960-4714-5bcd-84c1ee6ffb10-c39a/)
