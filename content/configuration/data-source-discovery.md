---
uid: PIAdapterForSDFDataSourceDiscovery
---

# Data source discovery

A discovery against the data source of a Structured Data Files adapter allows you to specify the optional **query** parameter. The query discovers the contents of the data source and narrows down the scope of the discovery. You can add the discovered items to the data selection.

## Structured Data Files query string

The string of the **query** parameter may contain none, any, or all string items in the following form: <br>`INCLUDEDATATYPE=<DATA_TYPE_1>,<DATA_TYPE_2>;EXCLUDEDATATYPE=<DATA_TYPE_1>,<DATA_TYPE_2>;INCLUDEFIELD=<FIELD_1>,<FIELD_2>;EXCLUDEFIELD=<FIELD_1>,<FIELD_2>;`<br><br>

| String item      | Required | Description |
|------------------|----------|-------------|
| `INCLUDEDATATYPE`  | Optional | Supported data types to include during discovery. Discovery looks for the specified data types in the files found in the discovery directory in the data source configuration. |
| `EXCLUDEDATATYPE`  | Optional | Supported data types to exclude during discovery. Discovery ignores the specified data types in the files found in the discovery directory in the data source configuration. |
| `INCLUDEFIELD`  | Optional | Name of the fields to include during discovery. Discovery looks for the specified fields in the files found in the discovery directory in the data source configuration. |
| `EXCLUDEFIELD`  | Optional | Name of the fields to exclude during discovery. Discovery ignores the specified fields in the files found in the discovery directory in the data source configuration. |

### Query rules

The following rules apply for specifying the query string:

- The query is made up of key=value pairs.
- Pairs are separated with a semicolon (`;`).
- Keys and values are separated with an equals (`=`).
- Multiple values per key are supported. These values are separated with a comma (`,`).
- Special characters are replaced by the text parser. For more information, see [Text parser](xref:TextParser#special-characters-support)

**Note:** The data source might contain tens of thousands of metrics. Ensure that the query will only return data for the selection items you are interested in.

## Discovery query example

The query parameter must be specified in the following form:
`INCLUDEDATATYPE=<DATA_TYPE_1>,<DATA_TYPE_2>;EXCLUDEDATATYPE=<DATA_TYPE_1>,<DATA_TYPE_2>;INCLUDEFIELD=<FIELD_1>,<FIELD_2>;EXCLUDEFIELD=<FIELD_1>,<FIELD_2>;`

### Structured Data Files data source discovery initiation

```json
{
  "id" : "40",
  "query" : "INCLUDEDATATYPE=int16,float32;EXCLUDEFIELD=Volume"
}
```

### Structured Data Files data source discovery results

```json
[
  {
    "id": "40",
    "query": "INCLUDEDATATYPE=int16,float32;EXCLUDEFIELD=Volume",
    "startTime": "2020-12-14T14:19:01.4383791-08:00",
    "endTime": "2020-12-14T14:19:31.8549164-08:00",
    "progress": 30,
    "itemsFound": 700,
    "newItems": 200,
    "resultUri": "http://127.0.0.1:5590/api/v1/Configuration/SDFComponentId/Discoveries/40/result",
    "autoSelect": false,
    "status": "Complete",
    "errors": null
  }
]
```

### Structured Data Files discovered selection items

```json
[
  {
    "Selected": false,
    "Name": "Name",
    "StreamId": "StreamId",
    "ValueField": "Pressure",
    "IndexField": "PressureTimeStamp",
    "IndexFormat": null,
    "DataType": "int16"
  }
]
```
