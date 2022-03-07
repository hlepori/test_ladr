# LADR Event Message

> Go to XML schemas: 


## Overview

## UML description

```mermaid
classDiagram
class LadrMessage
LadrMessage : fb:PersonOrOrganization [1]+originator
LadrMessage : fb:PersonOrOrganization [1]+recipient
LadrMessage : fb:UniversallyUniqueIdentifier [1]+uniqueMessageIdentifier
LadrMessage : ladr:EventInformation [1]+eventInformation
```

## Template description with business rules


| Property | Rules |
| :---     | :------  |
| LadrMessage.**originator** | `PRESENCE`<br>OPTIONAL<br><br>`DATATYPE`<br>PersonOrOrganization<br><br>`PROCESSING`<br>[*NM B2B*] On input NM will process the propertu as follows...  <br><br> |
| LadrMessage.**recipient** | `PRESENCE`<br>OPTIONAL<br><br>`DATATYPE`<br>PersonOrOrganization<br><br> |
| LadrMessage.**timestamp** | `PRESENCE`<br>MANDATORY<br><br>`DATATYPE`<br>Time<br><br>`ENCODING RULE`<br>pattern = `-?([1-9][0-9]{3,}\|0[0-9]{3})-(0[1-9]\|1[0-2])-(0[1-9]\|[12][0-9]\|3[01])T(([01][0-9]\|2[0-3]):[0-5][0-9]:[0-5][0-9](\.[0-9]+)?\|(24:00:00(\.0+)?))Z`<br><br>`ENCODING RULE`<br> ISO UUID v4 only |
|...|...|