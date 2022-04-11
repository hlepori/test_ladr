# Topics to be discussed

---

## Message identifier

### Requirement

---

## Contributor Code    

### Requirement (from ICAO Doc 10150)

|Field|Format|LADR functionality|Example|
|:-|:-|:-|:-|
|Contributor Code|NNN|Establish contributor domain for data validation.| 001 |

### In the LADR schemas

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

## Data source

### Requirement (from ICAO Doc 10150)

|Field|Format|LADR functionality|Example|
|:-|:-|:-|:-|
|Data source|TTTTTT|Enable identification of the source of data (manufacturerm type of ADT)| GCP-01 |

### In the LADR schemas

The pattern TTTTTT is currently enforced in the LADR schemas as follows.

```xml
<xs:simpleType name="ContributorCodeType">
  <xs:restriction base="xs:string">
    <xs:pattern value="([0-9]){3}"/>
  </xs:restriction>
</xs:simpleType>
```

## ADT activation method

## Time at position

## Message temporality

