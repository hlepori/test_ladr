# LADR Event Upload Message

```mermaid
    sequenceDiagram
    autonumber
    actor Contributor
    participant LADR
    actor User
    rect rgb(255, 255, 0)
    Contributor->>LADR: LADR Event Upload Message
    end
    LADR->>Contributor: LADR Event Upload Validation Message
    LADR->> User: LADR Event Notification Message
    LADR->>User: LADR Event Message 
    User->>LADR: Event Notification Acknowledgment Message       
    User->>LADR: Event Validation Message
```

## XML schema and samples



## UML description

```mermaid
classDiagram
class LadrMessage	
<<LADR_Application>> LadrMessage	
LadrMessage : + timestamp [1] Time	
class LadrMessageType	
<<LADR_Application>> LadrMessageType	
LadrMessageType : LADR_EVENT_UPLOAD_MESSAGE	
LadrMessageType <-- LadrMessage : +type [1]	
class Flight	
<<FIXM_Core>> Flight	
class AircraftOperator	
<<FIXM_Core>> AircraftOperator	
AircraftOperator : + designatorIcao [1] AircraftOperatorDesignator	
Flight --> AircraftOperator : +operator [1]	
class Aircraft	
<<FIXM_Core>> Aircraft	
Aircraft : + aircraftAddress [0..1] AircraftAddress	
class FlightCapabilities	
<<FIXM_Core>> FlightCapabilities	
class CommunicationCapabilities	
<<FIXM_Core>> CommunicationCapabilities	
CommunicationCapabilities : + otherCommunicationCapabilities [0..1] CharacterString	
CommunicationCapabilities : + selectiveCallingCode [0..1] SelectiveCallingCode	
FlightCapabilities --> CommunicationCapabilities : +communication [0..1]	
class SurvivalCapabilities	
<<FIXM_Core>> SurvivalCapabilities	
class SurvivalCapabilitiesExtension	
<<FIXM_Core>> SurvivalCapabilitiesExtension	
class LadrSurvivalCapabilitiesExtension	
<<LADR_Application>> LadrSurvivalCapabilitiesExtension	
LadrSurvivalCapabilitiesExtension : + carriedEltHexId [0..*] CharacterString	
SurvivalCapabilitiesExtension<|-- LadrSurvivalCapabilitiesExtension	
SurvivalCapabilities --> SurvivalCapabilitiesExtension : +extension [0..*]	
FlightCapabilities --> SurvivalCapabilities : +survival [0..1]	
Aircraft --> FlightCapabilities : +capabilities [0..1]	
Aircraft : + registration [0..1] AircraftRegistrationList	
Flight --> Aircraft : +aircraft [0..1]	
class FlightEmergency	
<<FIXM_Core>> FlightEmergency	
class LastContact	
<<FIXM_Core>> LastContact	
class LastPositionReport	
<<FIXM_Core>> LastPositionReport	
class SignificantPointChoice	
<<FIXM_Core>> SignificantPointChoice	
class GeographicalPosition	
<<FIXM_Core>> GeographicalPosition	
GeographicalPosition : + pos [1] LatLongPos	
SignificantPointChoice --> GeographicalPosition : +position [1]	
LastPositionReport --> SignificantPointChoice : +position [1]	
class LastPositionReportExtension	
<<FIXM_Core>> LastPositionReportExtension	
class LadrLastPositionReportExtension	
<<LADR_Application>> LadrLastPositionReportExtension	
LadrLastPositionReportExtension : + altitude [1] Altitude	
class Bearing	
<<FIXM_Core>> Bearing	
class ZeroBearingType	
<<FIXM_Core>> ZeroBearingType	
ZeroBearingType : TRUE_NORTH	
ZeroBearingType : MAGNETIC_NORTH	
Bearing --> ZeroBearingType : +zeroBearingType [1]	
LadrLastPositionReportExtension --> Bearing : +heading [0..1]	
class LadrAltitudeSource	
<<LADR_Application>> LadrAltitudeSource	
LadrAltitudeSource : BARO	
LadrAltitudeSource : GNSS	
LadrLastPositionReportExtension --> LadrAltitudeSource : +altitudeSource [1]	
LadrLastPositionReportExtension : + groundSpeed [1] GroundSpeed	
class Distance	
<<FIXM_Core>> Distance	
LadrLastPositionReportExtension --> Distance : +horizontalAccuracy [0..1]	
LastPositionReportExtension<|-- LadrLastPositionReportExtension	
LastPositionReport --> LastPositionReportExtension : +extension [1..*]	
LastContact --> LastPositionReport : +position [1]	
FlightEmergency --> LastContact : +lastContact [1]	
Flight --> FlightEmergency : +emergency [1]	
class FlightIdentification	
<<FIXM_Core>> FlightIdentification	
FlightIdentification : + aircraftIdentification [0..1] AircraftIdentification	
Flight --> FlightIdentification : +flightIdentification [0..1]	
LadrMessage --> Flight : +flight [1]	
class LadrEvent	
<<LADR_Application>> LadrEvent	
class PersonOrOrganization	
<<FIXM_Core>> PersonOrOrganization	
PersonOrOrganization : + identifier [1] CharacterString	
LadrEvent --> PersonOrOrganization : +contributorCode [1]	
LadrEvent : + dataSource [1] CharacterString	
LadrEvent : + adtActivationMethod [0..1] CharacterString	
LadrMessage --> LadrEvent : +ladrEvent [1]	
```

## Message description with business rules

| Property | Rules |
| :---     | :------  |
| LadrMessage.**originator** | `PRESENCE`<br>OPTIONAL<br><br>`DATATYPE`<br>PersonOrOrganization<br><br>`PROCESSING`<br>[*NM*] On input NM will process the property as follows...  <br><br> |
| LadrMessage.**recipient** | `PRESENCE`<br>OPTIONAL<br><br>`DATATYPE`<br>PersonOrOrganization<br><br> |
| LadrMessage.**timestamp** | `PRESENCE`<br>MANDATORY<br><br>`DATATYPE`<br>Time<br><br>`ENCODING RULE`<br>pattern = `-?([1-9][0-9]{3,}\|0[0-9]{3})-(0[1-9]\|1[0-2])-(0[1-9]\|[12][0-9]\|3[01])T(([01][0-9]\|2[0-3]):[0-5][0-9]:[0-5][0-9](\.[0-9]+)?\|(24:00:00(\.0+)?))Z`<br><br>`ENCODING RULE`<br>UTC time only<br><br>`FIXM Guidance`<br>[date-time-specification](https://docs.fixm.aero/#/general-guidance/date-time-specification)<br><br>|
| LadrMessage.**type** | `PRESENCE`<br>MANDATORY<br><br>`DATATYPE`<br>PersonOrOrganization<br><br>`ENCODING RULE`<br>value=LADR_EVENT_MESSAGE<br><br> |
|...|...|