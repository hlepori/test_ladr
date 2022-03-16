# LADR Event Upload Validation Message

```mermaid
    sequenceDiagram
    autonumber
    actor Contributor
    participant LADR
    actor User
    Contributor->>LADR: LADR Event Upload Message
    rect rgb(255, 255, 0)
    LADR->>Contributor: LADR Event Upload Validation Message
    end
    LADR->> User: LADR Event Notification Message
    LADR->>User: LADR Event Message 
    User->>LADR: Event Notification Acknowledgment Message       
    User->>LADR: Event Validation Message
```

## XML schema and samples

- Go to [Schema definition](https://github.com/hlepori/test_ladr/tree/main/schemas/ladrEventUploadValidationMessage) on Github

- Go to [XML examples](https://github.com/hlepori/test_ladr/tree/main/samples) on Github

## UML description

```mermaid
classDiagram
class LadrMessage	
<<LADR_Application>> LadrMessage	
LadrMessage : + timestamp [1] Time	
class LadrMessageType	
<<LADR_Application>> LadrMessageType	
LadrMessageType : LADR_EVENT_UPLOAD_VALIDATION_MESSAGE	
LadrMessageType <-- LadrMessage : +type [1]	
LadrMessage : + receiptTime [1] Time	
class LadrEvent	
<<LADR_Application>> LadrEvent	
class PersonOrOrganization	
<<FIXM_Core>> PersonOrOrganization	
PersonOrOrganization : + identifier [1] CharacterString	
LadrEvent --> PersonOrOrganization : +contributorCode [1]	
LadrEvent : + identifier [1] UniversallyUniqueIdentifier	
LadrMessage --> LadrEvent : +ladrEvent [1]	
class LadrMessageValidationStatus	
<<LADR_Application>> LadrMessageValidationStatus	
LadrMessageValidationStatus : NOT_VALID	
LadrMessageValidationStatus : VALID	
LadrMessage --> LadrMessageValidationStatus : +messageValidationStatus [1]	
LadrMessage : + uploadMessageValidatedTime [0..1] Time	
LadrMessage : + messageLoggedAsUnvalidTime [0..1] Time	
LadrMessage : + referencedMessageIdentifier [1] UniversallyUniqueIdentifier	
```

## Message description with business rules

| Property | Rules |
| :---     | :------  |
| LadrMessage.**originator** | `PRESENCE`<br>OPTIONAL<br><br>`DATATYPE`<br>PersonOrOrganization<br><br>`PROCESSING`<br>[*NM*] On input NM will process the property as follows...  <br><br> |
| LadrMessage.**recipient** | `PRESENCE`<br>OPTIONAL<br><br>`DATATYPE`<br>PersonOrOrganization<br><br> |
| LadrMessage.**timestamp** | `PRESENCE`<br>MANDATORY<br><br>`DATATYPE`<br>Time<br><br>`ENCODING RULE`<br>pattern = `-?([1-9][0-9]{3,}\|0[0-9]{3})-(0[1-9]\|1[0-2])-(0[1-9]\|[12][0-9]\|3[01])T(([01][0-9]\|2[0-3]):[0-5][0-9]:[0-5][0-9](\.[0-9]+)?\|(24:00:00(\.0+)?))Z`<br><br>`ENCODING RULE`<br>UTC time only<br><br>`FIXM Guidance`<br>[date-time-specification](https://docs.fixm.aero/#/general-guidance/date-time-specification)<br><br>|
| LadrMessage.**type** | `PRESENCE`<br>MANDATORY<br><br>`DATATYPE`<br>PersonOrOrganization<br><br>`ENCODING RULE`<br>value=LADR_EVENT_MESSAGE<br><br> |
|...|...|