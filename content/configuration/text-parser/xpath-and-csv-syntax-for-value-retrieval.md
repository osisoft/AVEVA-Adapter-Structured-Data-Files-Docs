---
uid: XPathAndCSVSyntaxForValueRetrievalSDF
---

# XPath and CSV syntax for value retrieval

For information on which semantics are used for retrieving values from XML and CSV files, see the following documentation:

- XML - [XML Path Language (XPath)](https://www.w3.org/TR/1999/REC-xpath-19991116/)
- CSV - Column Index (1 based) or Header value (if header defined)

The following syntaxes are used to extract values from XML or CSV documents.

### XML - Simple XPath example

```xml
<values>
  <value>
    <time>2020-08-10T12:10:46.0928791Z</time>
    <value>1.234567890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:47.0928791Z</time>
    <value>12.34567890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:48.0928791Z</time>
    <value>123.4567890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:49.0928791Z</time>
    <value>1234.567890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:50.0928791Z</time>
    <value>12345.67890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:51.0928791Z</time>
    <value>123456.7890</value>
  </value>
  <value>
    <time>2020-08-10T12:10:52.0928791Z</time>
    <value>12345678.90</value>
  </value>
  <value>
    <time>2020-08-10T12:10:53.0928791Z</time>
    <value>123456789.0</value>
  </value>
</values>
```

The following data selection item configuration with XPath reads a series of values:

```json
[
    {
        "valueField": "./values/value/value",
        "indexField": "./values/value/time",
        "dataType": "float64",
        "selected": true
    }
]
```

### XML - Complex XPath example

```xml
<sample>
  <success>true</success>
  <result>
    <id>964879</id>
    <name>Home</name>
    <latitude>null</latitude>
    <longitude>null</longitude>
    <child>
      <data>
        <items>
          <item>
            <id>1603836</id>
            <name>Thermostat1</name>
            <feature>
              <name>thermostat</name>
              <temperature>70</temperature>
              <scale>f</scale>
              <heat_min>55</heat_min>
              <heat_max>90</heat_max>
              <cool_min>60</cool_min>
              <cool_max>99</cool_max>
              <datetime>2021-09-06T17:00:00Z</datetime>
            </feature>
          </item>
          <item>
            <id>1603836</id>
            <name>Thermostat1</name>
            <feature>
              <name>thermostat</name>
              <temperature>71</temperature>
              <scale>f</scale>
              <heat_min>56</heat_min>
              <heat_max>91</heat_max>
              <cool_min>59</cool_min>
              <cool_max>99</cool_max>
              <datetime>2021-09-06T17:01:00Z</datetime>
            </feature>
          </item>
          <item>
            <id>1603836</id>
            <name>Thermostat1</name>
            <feature>
              <name>thermostat</name>
              <temperature>69</temperature>
              <scale>f</scale>
              <heat_min>54</heat_min>
              <heat_max>92</heat_max>
              <cool_min>58</cool_min>
              <cool_max>99</cool_max>
              <datetime>2021-09-06T17:02:00Z</datetime>
            </feature>
          </item>
        </items>
      </data>
    </child>
  </result>
</sample>
```

The following data selection item configuration with XPath reads all the `heat_min` values from the XML above:

```json
[
    {
        "valueField": "./sample/result/child/data/items/item/feature/heat_min",
        "indexField": "./sample/result/child/data/items/item/feature/datetime",
        "dataType": "float64",
        "selected": true
    }
]
```

The following data selection item configuration with XPath uses a predicate to read all the `heat_min` values with a value greater than or equal to 55 from the XML above:

```json
[
    {
        "valueField": "./sample/result/child/data/items/item/feature[heat_min>=55]/heat_min",
        "indexField": "./sample/result/child/data/items/item/feature[heat_min>=55]/datetime",
        "dataType": "float64",
        "selected": true
    }
]
```

### CSV - Simple CSV column index example

```csv
2020-08-10T12:10:46.0928791Z,1.234567890
2020-08-10T12:10:47.0928791Z,12.34567890
2020-08-10T12:10:48.0928791Z,123.4567890
2020-08-10T12:10:49.0928791Z,1234.567890
2020-08-10T12:10:50.0928791Z,12345.67890
2020-08-10T12:10:51.0928791Z,123456.7890
2020-08-10T12:10:52.0928791Z,12345678.90
2020-08-10T12:10:53.0928791Z,123456789.0
```

The following data selection item configuration using the CSV column index requires the data source configuration be configured with `HasHeader=false`. The column indexes are 1 based and configured as strings.

```json
[
    {
        "valueField": "2",
        "indexField": "1",
        "dataType": "float64",
        "selected": true
    }
]
```

### CSV - Simple CSV column header example

```csv
Date,Value
2020-08-10T12:10:46.0928791Z,1.234567890
2020-08-10T12:10:47.0928791Z,12.34567890
2020-08-10T12:10:48.0928791Z,123.4567890
2020-08-10T12:10:49.0928791Z,1234.567890
2020-08-10T12:10:50.0928791Z,12345.67890
2020-08-10T12:10:51.0928791Z,123456.7890
2020-08-10T12:10:52.0928791Z,12345678.90
2020-08-10T12:10:53.0928791Z,123456789.0
```

The following data selection item configuration using the CSV column header requires the data source configuration be configured with `HasHeader=true`.

```json
[
    {
        "valueField": "Value",
        "indexField": "Date",
        "dataType": "float64",
        "selected": true
    }
]
```
