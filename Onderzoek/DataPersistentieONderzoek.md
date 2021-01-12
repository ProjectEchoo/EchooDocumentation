# Data persistentie onderzoek document

## Inhoudsopgave

  - [Inhoudsopgave](#inhoudsopgave)
  - [Aanleiding](#aanleiding)
  - [Deelvragen](#deelvragen)
  - [Resultaten](#resultaten)
    - [1. Welke database structuren zijn er?](#1.-Welke-database-structuren-zijn-er?)
    - [2. Op welke manieren zijn databases te schalen?](#2.-Op-welke-manieren-zijn-databases-te-schalen?)
  - [conclusie](#conclusie)
<br/>

## Aanleiding
Ik heb binnen mijn project gekozen om met twee verschillende database structuren te werken, Mysql en Cassandra. In dit onderzoeksdocument kijk ik nog eens goed naar de verschillend database structuren die er beschikbaar zijn en of deze aansluiten bij mijn project. 

Ook leg ik in dit onderzoek een groote focus op de schaalbaarheid van een database structuur omdat mijn project vaak om moet kunnen gaan maat grote hoeveelheden data.

Mijn project bevat momenteel de volgende databases

- Account service: MYSQL database
- Group service: MYSQL database
- UserRelation service: MYSQL database
- Posts service: Cassandra database
- Comment service: Cassandra database
- Chat service: Cassandra database

De aanleiding van het onderzoek is dat ik wil vaststellen of mijn huidige structuur de juiste is. Ook wil ik meer te weten komen over hoe een databasestructuur kan meeschalen met grote hoeveelheden data.


## Deelvragen
Ik heb dit onderzoek verdeelt in de volgende deelvragen:

1. Welke database structuren zijn er?
2. Op welke manieren zijn databases te schalen?

## Resultaten

### 1. Welke database structuren zijn er?

Databases kunnen we onderverdelen in twee categoriën: Relationele databases en niet-relationele databases

#### Relationele databases (SQL)

Relationele databases zijn het meest bekend en worden nog steeds het meest gebruikt. De grondlegger van het relationeel model was Ted Codd. Hij publiceerde in 1970 een baanbrekend artikel, waarbij hij begrippen uit de relationele algebra toepaste op het probleem van het opslaan van grote hoeveelheden gegevens. Dit was het begin van een ontwikkeling in de databasewereld die binnen enkele jaren zorgde voor de definitie van het relationeel databasemodel.


Relationele databases zijn gebaseerd op het relationele model, een intuïtieve, eenvoudige manier om gegevens in tabellen weer te geven. In een relationele database is elke rij in de tabel een record met een uniek ID dat de sleutel wordt genoemd. De kolommen van de tabel bevatten attributen van de gegevens en elk record heeft meestal een waarde voor elk attribuut, waardoor het gemakkelijk is om de relaties tussen gegevenspunten vast te stellen. Alle relationele databases bieden de standaard create/read/update/delete (CRUD) functionaliteit wat aangeroepen kan worden met Structured Query Language (SQL) statements.

### Wat zijn de voordelen van een relationele database:
- data integriteit<br>
Een belangrijk voordeel van in gebruik van een relationele database is 'referentiële integriteit'. Referentiële integriteit verwijst naar de nauwkeurigheid en consistentie van gegevens.<br><br>
Referentiële integriteit behoudt de gegevensintegriteit door middel van "constraints". Constraints zijn de regels die de nauwkeurigheid van de gegevens afdwingen door te voorkomen dat een gerelateerd record wordt verwijderd zonder eerst het primaire record in de hoofdtabel te verwijderen. Als een relatie tussen primaire en externe sleutel correct is toegevoegd, wordt de transactie geblokkeerd als er geprobeert word om een primair record te verwijderen zonder eerst gerelateerde records uit andere tabellen te verwijderen. Dit voorkomt zogenoemde 'orphaned records' waarmee records worden bedoeld die een externe sleutel bevatten waarvan geen primare sleutel bestaat.<br><br>De drie regels die referentiële integriteit afdwingen zijn:
  1. Een externe sleutel moet een overeenkomstige primaire sleutel hebben.

  2. Wanneer een record in een primaire tabel wordt verwijderd, moeten alle gerelateerde records die verwijzen naar de primaire sleutel ook worden verwijderd.

  3. Als de primaire sleutel voor een record verandert, moeten alle overeenkomstige records in andere tabellen die de primaire sleutel als externe sleutel gebruiken, ook worden gewijzigd.

- Database vergrendelen en gelijktijdigheid<br>
  Er kunnen conflicten ontstaan ​​in een database wanneer meerdere gebruikers of applicaties dezelfde gegevens tegelijkertijd proberen te wijzigen. Vergrendelingstechnieken en gelijktijdigheidstechnieken verminderen de kans op conflicten terwijl de integriteit van de gegevens behouden blijft.<br><br>
  Vergrendelen voorkomt dat andere gebruikers en applicaties toegang krijgen tot gegevens terwijl deze worden bijgewerkt. In sommige databases is vergrendeling van toepassing op de hele tabel, wat een negatieve invloed heeft op de prestaties van de toepassing. Andere databases, zoals Oracle relationele databases, passen vergrendelingen toe op recordniveau, waardoor de andere records in de tabel beschikbaar blijven, wat bijdraagt ​​aan betere applicatieprestaties.<br><br>Concurrency beheert de activiteit wanneer meerdere gebruikers of applicaties tegelijkertijd zoekopdrachten in dezelfde database oproepen. Deze mogelijkheid biedt de juiste toegang tot gebruikers en applicaties volgens het beleid dat is gedefinieerd voor gegevensbeheer.


#### Nadelen van relationele databases:

- Ze werken niet goed, of totaal niet, met ongestructureerde / semi-gestructureerde data dankzij de database-schema's en gedwongen types.
- De tabellen worden niet per se een-op-een gemapped naar objecten of classes die dezelfde data representeren
- Om het migreren van de ene database naar de andere te laten slagen, moeten de database-schema's en types identiek zijn in de doel database.
- Kunnen niet horizontaal geschaald worden, alleen verticaal (wat duur is)

#### Niet-relationele databases (NoSQL)

Relationele databases zijn gestructureerd. In deze databases moet duidelijk gedefinieerd worden welk type data er in welke kolom moet komen te staan. Dit is bij een NoSQL database niet zo. Deze databases maken het mogelijk om ongestructureerde en semigestructureerd data op te slaan en te manipuleren. 

Er zijn een aantal types NoSQL databases:

##### Key-Value stores

Relationele databases zijn gestructureerd. In deze databases moet duidelijk gedefinieerd worden welk type data er in welke kolom moet komen te staan. Dit is bij een NoSQL database niet zo. Deze databases maken het mogelijk om ongestructureerde en semigestructureerd data op te slaan en te manipuleren. 

Aanbieders: Redis en Amazon DynamoDB

##### Wide Column Stores

Database-schema-agnostische systemen dat gebruikers data op laat slaan in `column families` of tabellen, een soort multi-dimensionale key-value store.

Schaalbaarheid het voornaamste doel van dit type. Hierdoor is het mogelijk om petabytes aan data te onderhouden en te verdelen over duizenden servers. Technisch gezien hebben ze geen database-schema, maar ze bieden een SQL-achtige taal aan, genaamd CQL, om data manipulatie makkelijker te maken. 

Aanbieders: Cassandra, Scylla en HBase

##### Document Stores

Document stores zijn database-schema-vrije systemen die data opslaan in de vorm van JSON documenten. Deze manier van opslaan doet denken aan de key-value en wide column stores, maar bij document stores is de naam van het document de key, en alles wat er in het document zit de value. 
Document stores hebben geen uniforme structuur en kunnen veel verschillende value types bevatten, die meerdere lagen diep kunnen gaan. Hierdoor zijn document stores erg geschikt om semigestructureerd data op te slaan, verspreidt over meerdere systemen. 


Aanbieders: MongoDB en Couchbase

##### Graph Databases

Bij graph databases wordt data gerepresenteerd als een netwerk van gerelateerde nodes of objecten. Dit om op deze manier data visualisaties en analystics mogelijk te maken.  Een node of een object bevat `free-form` data wat verbonden is met relaties en gegroepeerd aan de hand van labels. Graph-Oriented database management systemen zijn ontworpen met de nadruk op het illustreren van de verbindingen tussen data punten.

Dit type is daarom erg geschikt om relaties tussen data punten te analysteren. Hiermee kan bijvoorbeeld fraude worden voorkomen of Facebook’s vrienden graph. 

Aanbieders: Neo4J en Datastax Enterprise Graph

##### Search Engines

Search engines slaan data op met database-schema-vrije JSON documenten. Deze lijken op document stores, maar hebben een grotere nadruk op het toegankelijk maken van gestructureerde en semigestructureerde data via text-based searches.

Aanbieders: Elasticsearch, Splunk en Solr

## Voordelen:

- Bieden een grote flexibiliteit dankzij de database-schema-vrije manier van data opslag
- NoSQL schalen makkelijk horizontaal bij en hebben een hogere fouttolerantie. Ze blijven dus goed werken wanneer er een storing in een component is
- Data kan makkelijk over meerdere nodes worden gedistribueerd. Om beschikbaarheid en partitie tolerantie te verbeteren kan er voor `eventual consistency` gekozen worden

Nadelen:

- NoSQL databases zijn op minder grote schaal toegepast en minder volwassen dan de SQL varianten.
- Er is geen standaard voor alle NoSQL types.

### 2. Op welke manieren zijn databases te schalen?

Wanneer enorm veel gebruikers tegelijkertijd berichten/reacties plaatsen of chatberichten versturen, moet deze verstuurde data correct worden opgeslagen. Dit zonder dat de gebruikers hierbij moeten wachten op acties van anderen. Het moet dus niet zo zijn dat een gebruiken geen reactie kan plaatsen omdat de database bezig is met het verwerken van een chatbericht. Hoe kan dit probleem worden tegengegaan? 

Er zijn een aantal ontwikkel patronen die hierbij kunnen helpen.

#### 1. Query optimization & Connection Pool

De eerste oplossing is om veelvoorkomende niet-dynamische data in de cache op te slaan. Echter, naast deze application-layer cache kun je niks aan de latency problemen doen die dynamische data opvragen. Het is dan mogelijk om overtollige kolommen (die vaak in where of join on queries voorkomen) toe te voegen aan tabellen die vaak aangesproken worden om de-normalisatie te creëren. Dit zorgt ervoor dat minder join queries nodig zijn, grote queries opgebroken kunnen worden in meerdere kleinere queries en dat de resultaten van deze queries in de application layer worden opgeteld. 
Het tweaken van database connecties is een andere optimalisatie. Dankzij een connection pool kunnen er database connecties gecached worden. Elke netwerkconnectie is kostbaar en met een connection pool kun je deze connecties optimaliseren. Door connection pool libraries is het ook mogelijk om deze cache over meerdere threads te delen, maar dit kan niet over instanties.   


Op basis van 20-50 requests per minuut zullen deze optimalisaties tussen de 20% en 50% van de latency problemen verhelpen.

#### 2. Vertical Scaling

Verticaal schalen is het vergroten van de capaciteiten van de machine waarop de applicatie draait. Dit wordt gedaan door het RAM geheugen en opslag geheugen te vergroten en een betere CPU te installeren.

Verticaal schalen gebeurt door een nieuwe betere machine als `slave` in te stellen van de bestaande machine `de master`. Een `master slave` configuratie wordt toegepast en de data replicatie begint. Wanneer het repliceren van de data voltooid is, dient de nieuwe machine naar master gepromoot te worden en kan de oudere machine offline.

Dit is niet de beste manier om te schalen, aangezien het ontzettend duur is en je zal snel tegen de limieten aanlopen daar je niet onbeperkt veel RAM of betere CPU's kan installeren

#### 3. Command Query Responsibility Segregation (CQRS)

CQRS is een goede manier om de latency te verbeteren omdat in het algemeen een write transactie zwaarder is dan een read transactie. Slave machines, die dezelfde data bevatten als de master dankzij de master-slave replicatie, kunnen worden bijgeplaatst. Alle write transacties (de C uit CQRS) worden naar de master gestuurd en alle read transacties (de Q uit CQRS) naar de slaves.  


#### 4. Partitioning

Als een bepaalde tabel veel meer verkeer krijgt dan andere tabellen is het mogelijk om deze tabel te scheiden van de rest. Als deze tabel geen of weinig referentie(s) heeft naar andere tabellen is dit geen probleem. Dit is partitionering. Verschillende databases kunnen andere data hosten op basis van andere functionaliteit wanneer de resultaten in de application-layer samengevoegd kunnen worden. Hierdoor kan worden gefocust op het schalen van de functionaliteit met hoge read/write requests. Dit kost wel meer code aanpassingen omdat de application-layer moet zorgen dat de data wordt samengevoegd. 

#### 5. Horizontaal schalen

Waar je bij verticaal schalen de capaciteit van de machine vergroot, plaats je bij horizontaal schalen juist machines bij. Elke machine bevat hetzelfde database-schema en dezelfde set aan tabellen. Elke machine houdt een deel van de data bij.


## Conclusie

Er zijn dus twee types databases: Relationele en NOSQL. Elk type heeft zijn eigen voordelen, maar de belangrijkste verschillen zijn dat een relationele database slecht verticaal schaalt, maar dat dankzij de ACID regels de data erg betrouwbaar is. Een niet-relationele database schaalt dan horizontaal weer erg goed, maar heeft een hogere fout tolerantie.

Er zijn veel manieren om de latency te verlagen / load te verdelen voor de database. Vooral het partitioneren, horizontaal schalen en het partitioneren van data centers zijn het effectiefst.

Ik vond het vooral erg interessant om de verschillende manieren van data schaalbaarheid te onderzoek.Momenteel pas ik al partitionering toe. Elke service heeft zijn eigen database met relevante informatie. Maar zelf was ik nog niet bekend met een aantal van de andere technieken vooral CQRS vond ik interressant en ben ik ook van plan om toe te passen in een komend project.
