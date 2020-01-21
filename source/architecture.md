# Architecture of S-ENDA

  S-ENDA architecture is described using the C4 model (https://c4model.com/)

## Context diagram

```plantuml
@startuml S-ENDA context diagram
!includeurl https://raw.githubusercontent.com/RicardoNiepel/C4-PlantUML/release/1-0/C4_Container.puml

LAYOUT_LEFT_RIGHT

Person(researcher, "Researcher")
Person(developer, "Developer")
Person(scientistproducer, "Scientist data producer")

System(senda, "S-ENDA")

SystemDb_Ext(externaldata, "External data sources")

System_Boundary(portals, "Portals") {
    System_Ext(searchengine, "Search Engine")
    System_Ext(geonorge, "GeoNorge")
    System_Ext(datacite, "DataCite")
}


Rel(researcher, portals, "Searches", "Web UI")
Rel(researcher, portals, "Searches", "Terminal")

Rel(developer, senda, "Registeres service", "API/Web UI")
Rel(senda, portals, "Pushes metadata", "API")
Rel(senda, geonorge, "Pushes metadata", "manually")

Rel(scientistproducer, senda, "Registeres dataset", "API/Web UI")

Rel(senda, scientistproducer, "Gets feedback", "?")
Rel(senda, developer, "Gets feedback", "?")

Rel(senda, externaldata, "Indexes external data", "OAI-PMH")

@enduml
```
