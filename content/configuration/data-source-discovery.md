---
uid: PIAdapterForSDFDataSourceDiscovery
---

# Data source discovery

A discovery against the data source of a Structured Data Files adapter allows you to specify the optional **query** parameter. The query discovers the contents of the data source and narrows down the scope of the discovery. You can add the discovered items to the data selection.

## Structured Data Files query string

The string of the **query** parameter must contain string items in the following form: <br><!-- Query string --><br><br>

| String item      | Required | Description |
|------------------|----------|-------------|
<!-- Insert string items here -->

### Query rules

The following rules apply for specifying the query string:

- The query is made up of key=value pairs.
- Pairs are separated with a semicolon (`;`).
- Keys and values are separated with an equals (`=`).
<!-- Add more query rules here if necessary -->

**Note:** The data source might contain tens of thousands of metrics. Ensure that the query will only return data for the selection items you are interested in.

## Discovery query example

The query parameter must be specified in the following form:
<!-- Query string -->

### Structured Data Files data source discovery initiation

```json
{
  "id" : "40",
  "query" : " "
}
```

### Structured Data Files data source discovery results

```json
[
  {
    "id": "40",
    "query": " ",
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
    "TimeField": "PressureTimeStamp",
    "DataType": "Int16"
  }
]
```