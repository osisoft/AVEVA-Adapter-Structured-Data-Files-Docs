---
uid: PIAdapterForStructuredDataFilesDataSelectionConfiguration
---

# PI Adapter for Structured Data Files data selection configuration

In addition to the data source configuration, you need to provide a data selection configuration to specify the data you want the adapter to collect from the data sources.

**Note:** This document uses cURL commands to demonstrate data selection configuration, but other options are available. For more information, see [Configuration tools](xref:ConfigurationTools1-3).

## Configure Structured Data Files data selection

Complete the following steps to configure Structured Data Files data selection. Use the `POST` method in conjunction with the `api/v1/configuration/<ComponentId>/DataSelection` REST endpoint to initialize the configuration.

1. Using a text editor, create an empty text file.

1. Copy and paste an example configuration for data selection into the file.

    For sample JSON, see [Structured Data Files data selection examples](#structured-data-files-data-selection-examples).

1. Update the example JSON parameters for your environment.

    For a table of all available parameters, see [Structured Data Files data selection parameters](#structured-data-files-data-selection-parameters).

1. Save the file as `ConfigureDataSelection.json`.

1. Open a command line session. Change directory to the location of `ConfigureDataSelection.json`.

1. Enter the following cURL command (which uses the `POST` method) to initialize the data selection configuration.

      ```bash
      curl -d "@ConfigureDataSelection.json" -H "Content-Type: application/json" -X POST "http://localhost:5590/api/v1/configuration/StructuredDataFiles1/DataSelection"
      ```

    **Notes:**
  
    * If you installed the adapter to listen on a non-default port, update `5590` to the port number in use.
    * If you use a component ID other than `StructuredDataFiles1`, update the endpoint with your chosen component ID.
    * For a list of other REST operations you can perform, like updating or deleting a data selection configuration, see [REST URLs](#rest-urls).

## Structured Data Files data selection schema

The full schema definition for the Structured Data Files data selection configuration is in the `StructuredDataFiles_DataSelection_schema.json` file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\StructuredDataFiles\Schemas`

Linux: `/opt/OSIsoft/Adapters/StructuredDataFiles/Schemas`

## Structured Data Files data selection parameters

| Parameter        | Required | Type      | Description |
|------------------|----------|-----------|-------------|
| **Name** | Optional | `string` | The optional friendly name of the data item collected from the data source. If not configured, the default value is null and results in the **StreamId** value being used also as a **Name**. |
| **DataFilterId** | Optional | `string` | The identifier of a data filter defined in the [Data filters configuration](xref:DataFiltersConfiguration). <br>By default, no filter is applied. |
| **Selected** | Optional | `boolean` | If `true`, data for this item is collected and sent to one or more configured OMF endpoint.<br><br>Allowed value: `true` or `false`<br>Default value:`true` |
| **StreamId** | Optional | `string` | The custom identifier used to create the streams. If not specified, the adapter generates a default value based on the **DefaultStreamIdPattern** in the [PI Adapter for Structured Data Files data source configuration](xref:PIAdapterForStructuredDataFilesDataSourceConfiguration).<br>A properly configured custom stream ID follows these rules: <br> Is not case-sensitive.<br>Can contain spaces.<br>Cannot start with two underscores `__` .<br>Can contain a maximum of 100 characters.<br>Cannot use the following characters:<br>\/  \:  \? \#  \[  \]  \@  \!  \$  \&  \'  \(  \)  \\  \*  \+  \,  \;  \=  \%  \<  \>  \`|
| **ValueField** | Required | `string` | Name of the value field. XPath and JsonPath are supported.<br> Example: \"FanSpeed\".<br> Allowed Values: Any name to represent the value.|
| **TimeField** | Required | `string` | Name of the time field. XPath and JsonPath are supported.  If no timestamp is provided in the file, the following reserved values can be used to specify the timestamp:<br> - **FileCreationTime** - UTC time the file was created. <br> -  **FileModifiedTime** - UTC time the file was modified.<br> - **AdapterGeneratedTime** - UTC time the file is processed by the adapter. <br> Example: \"FanSpeedTimeStamp\"|
| **DataType** | Required | `string` | Data type of the values specified in the **ValueField** parameter.<br> Example: "Int32" <br> Allowed values: SByte, Byte, Int16, UInt16, Int32, UInt32, Int64, UInt64, Single, Double, Decimal, Boolean, DateTime, String |
| **TimeFormat**| Optional | `string` | Time format of the timestamp specified in the **TimeField** parameter.<br> Default value: null.<br> Example: \"mm\/dd\/yy\".|

## Structured Data Files data selection examples

The following are examples of valid Structured Data Files data selection configurations:

### Structured Data Files data selection configuration example with custom TimeFormat

```json
[
  {
    "Selected": true,
    "Name": "Name",
    "StreamId": "StreamId",
    "ValueField": "FanSpeed",
    "TimeField": "FileCreationTime",
    "TimeFormat": "mm/dd/yy",
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
    "TimeField": "PressureTimeStamp",
    "DataType": "Int16"
  }
]
```

### Structured Data Files data selection configuration example using XPath in the ValueField

```json
[
  {
    "Selected": true,
    "Name": "Name",
    "StreamId": "StreamId",
    "ValueField": "/bookstore/book/title",
    "TimeField": "bookStoreTimeStamp",
    "DataType": "String"
  }
]
```
## REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/configuration/\<ComponentId\>/DataSelection  | `GET` | Retrieves the Structured Data Files data selection configuration |
| api/v1/configuration/\<ComponentId\>/DataSelection  | `PUT` | Configures or updates the Structured Data Files data selection configuration |
| api/v1/configuration/\<ComponentId\>/DataSelection | `DELETE` | Deletes the Structured Data Files data selection configuration |
| api/v1/configuration/\<ComponentId\>/DataSelection | `PATCH` | Allows partial updating of configured data selection items. <br>**Note:** The request must be an array containing one or more data selection items. Each data selection item in the array must include its **StreamId**. |
| api/v1/configuration/\<ComponentId\>/DataSelection/\<StreamId\> | `PUT` | Updates or creates a new data selection with the specified **StreamId**.|
| api/v1/configuration/\<ComponentId\>/DataSelection/\<StreamId\> | `DELETE` | Deletes a specific data selection item of the Structured Data Files data selection configuration. |

**Note:** Replace `<ComponentId>` with the ID of your Structured Data Files component, for example `StructuredDataFiles1`.
