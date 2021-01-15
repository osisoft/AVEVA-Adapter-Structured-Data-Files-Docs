---
uid: PIAdapterForStructuredDataFilesDataSelectionConfiguration
---

# PI Adapter for Structured Data Files data selection configuration

In addition to the data source configuration, you need to provide a data selection configuration to specify the data you want the adapter to collect from the data sources.

## Configure Structured Data Files data selection

**Note:** You cannot modify Structured Data Files data selection configurations manually. You must use the REST endpoints to add or edit the configuration.

Complete the following steps to configure the Structured Data Files data selection:

1. Use any text editor to create a file that contains a Structured Data Files data selection in the JSON format.
    - For content structure, see [Structured Data Files data selection examples](#structured-data-files-data-selection-examples).
    - For a table of all available parameters, see [Structured Data Files data selection parameters](#structured-data-files-data-selection-parameters).
2. Save the file. For example, `ConfigureDataSelection.json`.
3. Use any of the [Configuration tools](xref:ConfigurationTools1-3) capable of making HTTP requests to run either a POST or PUT command to their appropriate endpoint:

    **Note:** The following examples use SDF1 as the adapter component name. For more information on how to add a component, see [System components configuration](xref:SystemComponentsConfiguration1-3).
  
    `5590` is the default port number. If you selected a different port number, replace it with that value.

    - **POST** endpoint: `http://localhost:5590/api/v1/configuration/<componentId>/DataSelection/`

      Example using `curl`:

      ```bash
      curl -d "@ConfigureDataSelection.json" -H "Content-Type: application/json" -X POST "http://localhost:5590/api/v1/configuration/SDF1/DataSelection/"
      ```

      **Note:** Run this command from the same directory where the file is located.

    - **PUT** endpoint: `http://localhost:5590/api/v1/configuration/<componentId>/DataSelection/<StreamId>`

      Example using `curl`:

        ```bash
        curl -d "@ConfigureDataSelection.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/SDF1/DataSelection/MyFileSource.Temperature"
        ```

        **Note:** Run this command from the same directory where the file is located.

## Structured Data Files data selection schema

The full schema definition for the Structured Data Files data selection configuration is in the `StructuredDataFiles_DataSelection_schema.json` file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\StructuredDataFiles\Schemas`

Linux: `/opt/OSIsoft/Adapters/StructuredDataFiles/Schemas`

## Structured Data Files data selection parameters

| Parameter        | Required | Type      | Description |
|------------------|----------|-----------|-------------|
| **Name** | Optional | `string` | The optional friendly name of the data item collected from the data source. If not configured, the default value is null and results in the ****StreamId**** value being used also as a ****Name****. |
| **DataFilterId** | Optional | `string` | The identifier of a data filter defined in the [Data filters configuration](xref:DataFiltersConfiguration). <br>By default, no filter is applied. |
| **Selected** | Optional | `boolean` | If true, data for this item is collected and sent to one or more configured OMF endpoint.<br><br>Allowed value: `true` or `false`<br>Default value:`true` |
| **StreamId** | Optional | `string` | The custom identifier used to create the streams. If not specified, the Structured Data Files adapter generates a default value based on the `DefaultStreamIdPattern` in the [PI Adapter for Structured Data Files data source configuration](xref:PIAdapterForStructuredDataFilesDataSourceConfiguration).<br>A properly configured custom stream ID follows these rules: <br> Is not case-sensitive.<br>Can contain spaces.<br>Cannot start with two underscores ("__").<br>Can contain a maximum of 100 characters.<br>Cannot use the following characters:<br>\/  \:  \? \#  \[  \]  \@  \!  \$  \&  \'  \(  \)  \\  \*  \+  \,  \;  \=  \%  \<  \>  \`|
| **ValueField** | Required | `string` | Name of the value field. XPath and JsonPath are supported <br> Example: \"FanSpeed\".<br> Allowed Values: Any name to represent the value.|
| **TimeField** | Required | `string` | Name of the time field. XPath and JsonPath are supported.  If no timestamp is provided in the file, the following values can be used to specify the timestamp:<br> - FileCreationTime - UTC time the file was created. <br> -  FileModifiedTime - UTC time the file was modified.<br> - AdapterGeneratedTime - UTC time the file is processed by the adapter. <br> Example: \"FanSpeedTimeStamp\"|
| **DataType** | Required | `string` | Data type of the values specified in the ValueField property.<br> Example: "Int32" <br> Allowed values: SByte, Byte, Int16, UInt16, Int32, UInt32, Int64, UInt64, Single, Double, Decimal, Boolean, DateTime, String |
| **TimeFormat**| Optional | `string` | Time format of the timestamp specified in the TimeField property.<br> Default: null.<br> Example: "mm\/dd\/yy".|

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
| api/v1/configuration/_ComponentId_/DataSelection  | GET | Retrieves the Structured Data Files data selection configuration |
| api/v1/configuration/_ComponentId_/DataSelection  | PUT | Configures or updates the Structured Data Files data selection configuration |
| api/v1/configuration/_ComponentId_/DataSelection | DELETE | Deletes the Structured Data Files data selection configuration |
| api/v1/configuration/_ComponentId_/DataSelection | PATCH | Allows partial updating of configured data selection items. <br>**Note:** The request must be an array containing one or more data selection items. Each data selection item in the array must include its *StreamId*. |
| api/v1/configuration/_ComponentId_/DataSelection/_StreamId_ | PUT | Updates or creates a new data selection with the specified *StreamId*|
| api/v1/configuration/_ComponentId_/DataSelection/_StreamId_ | DELETE | Deletes a specific data selection item of the Structured Data Files data selection configuration |

**Note:** Replace _ComponentId_ with the Id of your Structured Data Files component, for example SDF1.
