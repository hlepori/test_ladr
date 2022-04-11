# Topocis to be discussed

## Message identifier


## Contributor Code    

### Doc 10150 requirement
|Field|Format|LADR functionality|Example|
|:-|:-|:-|:-|
|Contributor Code|NNN|Establish contributor domain for data validation.| 001 |


### In the LADR schemas

The pattern NNN is currently enforced in the schemas as follows.

```xml
<xs:simpleType name="ContributorCodeType">
  <xs:restriction base="xs:string">
    <xs:pattern value="([0-9]){3}"/>
  </xs:restriction>
</xs:simpleType>
```

### Questions

- In some prototype's samples, Contributor Code is sometimes set to "USMCC". This value does not match the format specified by Doc 10150 / does not validate. 
- What would be the right pattern for this field? Should this code be normalized?

Note: In principle, EUROCONTROL will foresee a process to connect contributors to the LADR.


## Data source

## ADT activation method

## Time at position

## Message temporality

