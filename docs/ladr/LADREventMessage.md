# LADR Event Message

## XML schema and samples

- Go to [LADR Event Message Schema definition](https://github.com/hlepori/test_ladr/tree/main/schemas/ladrEventMessage) on Github

- Go to [Examples of LADR Messages](https://github.com/hlepori/test_ladr/tree/main/samples) on Github

## UML description

```mermaid
classDiagram
%% -------------------
class LadrMessage
<<LADR_Application>> LadrMessage
LadrMessage : + originator [0..1] PersonOrOrganization
LadrMessage : + recipient [0..1] PersonOrOrganization
LadrMessage : + uniqueMessageIdentifier [1] UniversallyUniqueIdentifier
LadrMessage : + timestamp [1] Time
LadrMessage : + receiptTime [1] Time
%% -------------------
class LadrMessageType
<<LADR_Application>> LadrMessageType
LadrMessageType : LADR_EVENT_MESSAGE
LadrMessageType <-- LadrMessage : +type [1]
%% -------------------
class EventInformation
<<LADR_Application>> EventInformation
EventInformation : + adtActivationMethod [0..1] CharacterString
EventInformation : + contributorCode [0..1] PersonOrOrganization
EventInformation : + dataSource [0..1] CharacterString
LadrMessage --> EventInformation : +eventInformation [0..1]
%% -------------------
class Flight
<<FIXM_Core>> Flight
LadrMessage --> Flight : +flight [1]
%% -------------------
class Aircraft
<<FIXM_Core>> Aircraft
Aircraft : +registration [1] AircraftRegistration
Aircraft : +aircraftAddress [1] AircraftAddress
Flight --> Aircraft : +aircraft [1]
%% -------------------
class FlightCapabilities
<<FIXM_Core>> FlightCapabilities
Aircraft --> FlightCapabilities : +capabilities [1]
%% -------------------
class CommunicationCapabilities
<<FIXM_Core>> CommunicationCapabilities
CommunicationCapabilities : +selectiveCallingCode [0..1] SelectiveCallingCode
CommunicationCapabilities : +otherCommunicationCapabilities [0..1] CharacterString
FlightCapabilities --> CommunicationCapabilities : +communication [1]
%% -------------------
class SurvivalCapabilities
<<FIXM_Core>> SurvivalCapabilities
FlightCapabilities --> SurvivalCapabilities : +survival [1]
%% -------------------
class SurvivalCapabilitiesExtension
<<FIXM_Core>> SurvivalCapabilitiesExtension
SurvivalCapabilities --> SurvivalCapabilitiesExtension : +extension [1]
%% -------------------
class LadrSurvivalCapabilitiesExtension
<<LADR_extension>> LadrSurvivalCapabilitiesExtension
SurvivalCapabilitiesExtension <| -- LadrSurvivalCapabilitiesExtension
%% -------------------
class EmergencyLocatorTransmitter
<<LADR_extension>> EmergencyLocatorTransmitter
EmergencyLocatorTransmitter : hexId [1] CharacterString
LadrSurvivalCapabilitiesExtension --> EmergencyLocatorTransmitter : +carriedElt [1]
%% -------------------
class AircraftOperator
<<FIXM_Core>> AircraftOperator
AircraftOperator : + designatorICAO [1] AircraftOperatorDesignator
Flight --> AircraftOperator : +operator[1]
%% -------------------
class FlightEmergency
<<FIXM_Core>> FlightEmergency
Flight --> FlightEmergency : +emergency [1]
%% -------------------
class LastContact
<<FIXM_Core>> LastContact
FlightEmergency --> LastContact : +lastContact [1]
%% -------------------
class LastPositionReport
<<FIXM_Core>> LastPositionReport
LastPositionReport : + timeAtPosition [1] SignificantPointChoice
LastContact --> LastPositionReport : +lastContact [1]
%% -------------------
class SignificantPointChoice
<<FIXM_Core>> SignificantPointChoice
SignificantPointChoice : + position [1] GeographicalPosition
LastPositionReport --> SignificantPointChoice : +position [1]
%% -------------------
class LastPositionReportExtension
<<FIXM_Core>> LastPositionReportExtension
LastPositionReport --> LastPositionReportExtension : +extension [1]
%% -------------------
class LadrLastPositionReportExtension
<<LADR_extension>> LadrLastPositionReportExtension
LadrLastPositionReportExtension : + groundSpeed [1] GroundSpeed
LadrLastPositionReportExtension : + heading [1] Bearing
LadrLastPositionReportExtension : + horizontalAccuracy [0..1] Distance
LastPositionReportExtension <|-- LadrLastPositionReportExtension
%% -------------------
class LadrAltitude
<<LADR_extension>> LadrAltitude
LadrAltitude : + altitude [1] Altitude
LadrLastPositionReportExtension --> LadrAltitude : +altitude [1]
%% -------------------
class LadrAltitudeSourceType
<<LADR_extension>> LadrAltitudeSourceType
LadrAltitudeSourceType : BARO
LadrAltitudeSourceType : GNSS
LadrAltitude --> LadrAltitudeSourceType : +altitudeSource [1]
%% -------------------
class FlightIdentification
<<FIXM_Core>> FlightIdentification
FlightIdentification : + aircraftIdentification [1] AircraftIdentification
Flight --> FlightIdentification : +flightIdentification [1]
%% -------------------
```

## Message description with business rules

| Property | Rules |
| :---     | :------  |
| LadrMessage.**originator** | `PRESENCE`<br>OPTIONAL<br><br>`DATATYPE`<br>PersonOrOrganization<br><br>`PROCESSING`<br>[*NM*] On input NM will process the property as follows...  <br><br> |
| LadrMessage.**recipient** | `PRESENCE`<br>OPTIONAL<br><br>`DATATYPE`<br>PersonOrOrganization<br><br> |
| LadrMessage.**timestamp** | `PRESENCE`<br>MANDATORY<br><br>`DATATYPE`<br>Time<br><br>`ENCODING RULE`<br>pattern = `-?([1-9][0-9]{3,}\|0[0-9]{3})-(0[1-9]\|1[0-2])-(0[1-9]\|[12][0-9]\|3[01])T(([01][0-9]\|2[0-3]):[0-5][0-9]:[0-5][0-9](\.[0-9]+)?\|(24:00:00(\.0+)?))Z`<br><br>`ENCODING RULE`<br>UTC time only<br><br>`FIXM Guidance`<br>[date-time-specification](https://docs.fixm.aero/#/general-guidance/date-time-specification)<br><br>|
| LadrMessage.**type** | `PRESENCE`<br>OPTIONAL<br><br>`DATATYPE`<br>PersonOrOrganization<br><br>`ENCODING RULE`<br>value=LADR_EVENT_MESSAGE<br><br> |
|...|...|