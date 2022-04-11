# Topics to be discussed

## Message identifier

### Requirement

### To be discussed

---

## Contributor Code    

### Requirement (from ICAO Doc 10150)

|Field|Format|LADR functionality|Example|
|:-|:-|:-|:-|
|Contributor Code|NNN|Establish contributor domain for data validation.| 001 |

The pattern NNN is currently enforced in the LADR schemas as follows.

```xml
<xs:simpleType name="ContributorCodeType">
  <xs:restriction base="xs:string">
    <xs:pattern value="([0-9]){3}"/>
  </xs:restriction>
</xs:simpleType>
```

### To be discussed

In some prototype's samples, Contributor Code is sometimes set to "USMCC". This value does not match the format specified by Doc 10150 / does not validate.

```xml
<!-- Raw text 352362 1 27925787A2BFDFF 2022-01-19 13:00:05 -->
<LadrMessage>
  <contributor>
    <identifier>USMCC</identifier>      
```

What would be the right pattern for this field? Should this code be normalized?

> Note: In principle, EUROCONTROL will foresee a process to connect contributors to the LADR.


### Resolution

> TODO

---

## Data source

### Requirement (from ICAO Doc 10150)

|Field|Format|LADR functionality|Example|
|:-|:-|:-|:-|
|Data source|TTTTTT|Enable identification of the source of data (manufacturerm type of ADT)| GCP-01 |

The pattern TTTTTT is currently enforced in the LADR schemas as follows.

```xml
<xs:simpleType name="DataSourceType">
  <xs:restriction base="xs:string">
	  <xs:pattern value="([A-Z]|[0-9]){6}"/>
  </xs:restriction>
</xs:simpleType>
```

### To be discussed

In some prototype's samples, data source is sometimes set to "SPMCC", i.e. 5 characters. This value does not match the format specified by Doc 10150 / does not validate.

```xml
<ladr:LadrMessage>
  <ladr:flight>
    <fx:emergency>
      <ladr:dataSource>SPMCC</ladr:dataSource>
```

What would be the right pattern for this field?

### Resolution

> TODO

---

## ADT activation method

### Requirement (from ICAO Doc 10150)

|Field|Format|LADR functionality|Example|
|:-|:-|:-|:-|
|ADT activation method|TTTTTT|Defined code which indicated if the activation was manual or automatic, and what parameter exceedance triggered the automatic activation, if applicable. Also incorporates cancellation message to provide information when the ADT system no longer transmits due to the activating condition no longer being fulfilled.|431832|

The pattern TTTTTT is currently enforced in the LADR schemas as follows.

```xml
<xs:simpleType name="AdtActivationMethodType">
	<xs:restriction base="xs:string">
		<xs:pattern value="([A-Z]|[0-9]){6}"/>
	</xs:restriction>
</xs:simpleType>
```
### To be discussed

Looking at the examples provided by Doc 10150, should the format rather be NNNNNN (i.e. six numeric characters) ?

|ADT Activator|
|:-|
|431401|
|431832|
|431100|
|531604|
|401300|

In some prototype's samples, 
- Data source is sometimes set to "MANUAL". This value matches the pattern, but is this truly a value that is expected/allowed?

```xml
<ladr:LadrMessage>
  <ladr:flight>
    <fx:emergency>
      <ladr:dataSource>SPMCC</ladr:dataSource>
       <ladr:ADTActivationMethod>MANUAL</ladr:ADTActivationMethod>
```

- Data source is sometimes set to "AUTOMATIC-A". This value does not match the pattern / does not validate.

```xml
<ladr:LadrMessage>
  <ladr:flight>
    <fx:emergency>
      <ladr:dataSource>SPMCC</ladr:dataSource>
       <ladr:ADTActivationMethod>AUTOMATIC-A</ladr:ADTActivationMethod>
```

What would be the right pattern for this field: TTTTTT, NNNNNN, a mix... ? Any need for predefined values?

### Resolution

> TODO

---

## Time at position

---

## Message temporality

