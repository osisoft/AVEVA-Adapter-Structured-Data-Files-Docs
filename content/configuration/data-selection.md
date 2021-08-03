---
uid: PIAdapterForSDFDataSelectionConfiguration
---

# Data selection

In addition to the data source configuration, you need to provide a data selection configuration to specify the data you want the adapter to collect from the data source.

**Note:** This document uses cURL commands to demonstrate data selection configuration, but other options are available. For more information, see [Configuration tools](xref:ConfigurationTools).

## Configure Structured Data Files data selection

Complete the following steps to configure Structured Data Files data selection. Use the `PUT` method in conjunction with the `api/v1/configuration/<ComponentId>/DataSelection` REST endpoint to initialize the configuration.

1. Using a text editor, create an empty text file.

1. Copy and paste an example configuration for data selection into the file.

    For sample JSON, see [Structured Data Files data selection examples](#structured-data-files-data-selection-examples).

1. Update the example JSON parameters for your environment.

    For a table of all available parameters, see [Structured Data Files data selection parameters](#structured-data-files-data-selection-parameters).

1. Save the file as `ConfigureDataSelection.json`.

1. Open a command line session and change the working directory to the location of `ConfigureDataSelection.json`.

1. Enter the following cURL command (which uses the `PUT` method) to initialize the data selection configuration.

      ```bash
      curl -d "@ConfigureDataSelection.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/StructuredDataFiles1/DataSelection"
      ```

    **Notes:**
  
    * If you installed the adapter to listen on a non-default port, update `5590` to the port number in use.
    * If you use a component ID other than `StructuredDataFiles1`, update the endpoint with the component ID.
    * For a list of other REST operations you can perform, like updating or deleting a data selection configuration, see [REST URLs](#rest-urls).

## Structured Data Files data selection schema

The full schema definition for the Structured Data Files data selection configuration is in the `StructuredDataFiles_DataSelection_schema.json` file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\StructuredDataFiles\Schemas`

Linux: `/opt/OSIsoft/Adapters/StructuredDataFiles/Schemas`

## Structured Data Files data selection parameters

| Parameter        | Required | Type      | Description |
|------------------|----------|-----------|-------------|
| **Name** | Optional | `string` | The optional friendly name of the data item collected from the data source. If not configured, data endpoints use the **StreamId** value as the **Name**.<br><br>Default value: `null`|
| **DataFilterId** | Optional | `string` | The identifier of a data filter defined in the [Data filters configuration](xref:DataFiltersConfiguration). <br>By default, no filter is applied.<br>**Note:** If the specified **DataFilterId** does not exist, unfiltered data is sent until that **DataFilterId** is created. |
| **Selected** | Optional | `boolean` | If `true`, data for this item is collected and sent to one or more configured OMF endpoint.<br><br>Allowed value: `true` or `false`<br>Default value: `true` |
| **StreamId** | Optional | `string` | The custom identifier used to create the streams. If not specified, the adapter generates a default value based on the **DefaultStreamIdPattern** in the [PI Adapter for Structured Data Files data source configuration](xref:PIAdapterForSDFDataSourceConfiguration).<br>A properly configured custom stream ID follows these rules: <br> Is not case-sensitive.<br>Can contain spaces.<br>Cannot start with two underscores `__` .<br>Can contain a maximum of 100 characters.<br>Cannot use the following characters:<br>\/  \:  \? \#  \[  \]  \@  \!  \$  \&  \'  \(  \)  \\  \*  \+  \,  \;  \=  \%  \<  \>  \`|
| **ValueField** | Required | `string` | Name of the value field. JSONPath, XPath, and CSV are supported<sup>1</sup>. For CSV files without a header, the column index (`1` being the first column) should be specified.<br><br> Example: \"FanSpeed\".<br> Allowed Values: Any name to represent the value.|
| **IndexField** | Required | `string` | Name of the time field. JSONPath, XPath, and CSV are supported<sup>1</sup>. For CSV files without a header, the column index (`1` being the first column) should be specified. If no timestamp is provided in the file, the following reserved values can be used to specify the timestamp:<br> - **FileCreationTime** - UTC time when the file was created. <br> -  **FileModifiedTime** - UTC time when the file was modified.<br> - **AdapterGeneratedTime** - UTC time the file is processed by the adapter.<br><br>Example: \"FanSpeedTimeStamp\"|
| **DataType** | Required | `string` | Data type of the values specified in the **ValueField** parameter.<br><br>Example: "Int32" <br>Allowed values: SByte, Byte, Int16, UInt16, Int32, UInt32, Int64, UInt64, Single, Double, Decimal, Boolean, DateTime, String |
| **IndexFormat**| Optional | `string` | Time format of the timestamp specified in the **IndexField** parameter.<br><br>Default value: `null`.<br/>Example: `MM/dd/yyyy H:mm:ss zzz`.<br><br>**Note:** For more examples of time format syntax, see [Date and time processing](xref:TextParser#date-and-time-processing). |

<sup>1</sup>**Note**: For full examples of how to enter JSONPath, XPath, or CSV syntax, see the following topics:
* <xref:JSONPathSyntaxForValueRetrieval>
* <xref:XPathAndCSVSyntaxForValueRetrieval>

## Structured Data Files data selection examples

The following are examples of valid Structured Data Files data selection configurations:

### Structured Data Files data selection configuration example with custom IndexFormat

```json
[
  {
    "Selected": true,
    "Name": "Name",
    "StreamId": "StreamId",
    "ValueField": "FanSpeed",
    "IndexField": "FileCreationTime",
    "IndexFormat": "mm/dd/yy",
    "DataType": "Int32"
  }
]
```

### Structured Data Files data selection configuration example with unselected item

```json
[
  {
    "Selected": false,
    "Name": "Name",
    "StreamId": "StreamId",
    "ValueField": "Pressure",
    "IndexField": "PressureTimeStamp",
    "DataType": "Int16"
  }
]
```

## REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/configuration/\<ComponentId\>/DataSelection  | `GET` | Retrieves the data selection configuration, including all data selection items. |
| api/v1/configuration/\<ComponentId\>/DataSelection  | `PUT` | Configures or updates the data selection configuration. The adapter starts collecting data for each data selection item when the following conditions are met:<br/><br/>&bull; The data selection configuration `PUT` request is received.<br/>&bull; A data source configuration is active. |
| api/v1/configuration/\<ComponentId\>/DataSelection | `DELETE` | Deletes the active data selection configuration. The adapter stops collecting data. |
| api/v1/configuration/\<ComponentId\>/DataSelection | `PATCH` | Allows partial updates of configured data selection items.<br/><br/>**Note:** The request must be an array containing one or more data selection items. Each item in the array must include its **StreamId**. |
| api/v1/configuration/\<ComponentId\>/DataSelection/\<StreamId\> | `PUT` | Updates or creates a new data selection item by **StreamId**. For new items, the adapter starts collecting data after the request is received. |
| api/v1/configuration/\<ComponentId\>/DataSelection/\<StreamId\> | `DELETE` | Deletes a data selection item from the configuration by **StreamId**. The adapter stops collecting data for the deleted item. |

**Note:** Replace `<ComponentId>` with the ID of your Structured Data Files component, for example _StructuredDataFiles1_.
