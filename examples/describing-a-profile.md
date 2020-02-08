# Describing a profile

In ESDL you can describe a profile for timeseries. Any energy related information that changes over time could be described. Examples of profiles would be a profile for hourly energy consumption data or a profile for the cost development of a particular heatpump for the coming 30 years.

A possibility is to use a DateTimeProfile for this kind of data. A dateTimeProfile contains elements for every timestamp. As an alternative this kind of data can be stored in an InfluxDB database and referred to from an ESDL object of type InfluxDBProfile. Other timeseries databases can be supported in future.

```xml
<esdl:DateTimeProfile xmi:version='2.0'
xmlns:xmi='http://www.omg.org/XMI'
xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'
xmlns:esdl='http://www.tno.nl/esdl/1808'
xsi:schemaLocation='http://www.tno.nl/esdl/1808 ../esdl/model/esdl.ecore'
 id="NEDU_E1A_2019" name="NEDU E1A 2019" profileType="PERCENTAGE" xsi:type="esdl:DateTimeProfile">
    <esdl:element from="2019-01-01T00:00:00" to="2019-01-01T00:15:00" value="3.561000e-05"/>
    <esdl:element from="2019-01-01T00:15:00" to="2019-01-01T00:30:00" value="3.532000e-05"/>
    <esdl:element from="2019-01-01T00:30:00" to="2019-01-01T00:45:00" value="3.504000e-05"/>
    <esdl:element from="2019-01-01T00:45:00" to="2019-01-01T01:00:00" value="3.454000e-05"/>
    <esdl:element from="2019-01-01T01:00:00" to="2019-01-01T01:15:00" value="3.367000e-05"/>
    <esdl:element from="2019-01-01T01:15:00" to="2019-01-01T01:30:00" value="3.275000e-05"/>
    <esdl:element from="2019-01-01T01:30:00" to="2019-01-01T01:45:00" value="3.170000e-05"/>
    <esdl:element from="2019-01-01T01:45:00" to="2019-01-01T02:00:00" value="3.061000e-05"/>
    <esdl:element from="2019-01-01T02:00:00" to="2019-01-01T02:15:00" value="2.934000e-05"/>
```

