---
uid: PIAdapterForStructuredDataFilesDataSourceConfiguration
---

# PI Adapter for Structured Data Files data source configuration

To use the adapter, you must configure the data source to receive data.

**Note:** This document uses cURL commands to demonstrate data selection configuration, but other options are available. For more information, see [Configuration tools](xref:ConfigurationTools1-3).

## Configure Structured Data Files data source

Complete the following steps to configure a Structured Data Files data source. Use the `POST` method in conjunction with the `api/v1/configuration/<ComponentId>/DataSource` REST endpoint to initialize the configuration.

1. Using a text editor, create an empty text file.

1. Copy and paste an example configuration for a structured data files data source into the file.

    For sample JSON, see [Structured Data Files data source examples](#structured-data-files-data-source-examples).

1. Update the example JSON parameters for your environment.

    For a table of all available parameters, see [Structured Data Files data source parameters](#structured-data-files-data-source-parameters).

1. Save the file as `ConfigureDataSource.json`.

1. Open a command line session. Change directory to the location of `ConfigureDataSource.json`.

1. Enter the following cURL command (which uses the `POST` method) to initialize the data source configuration.

    ```bash
    curl -d "@ConfigureDataSource.json" -H "Content-Type: application/json" -X POST "http://localhost:5590/api/v1/configuration/StructuredDataFiles1/DataSource"
    ```

    **Notes:**
  
    * If you installed the adapter to listen on a non-default port, update `5590` to the port number in use.
    * If you use a component ID other than `StructuredDataFiles1`, update the endpoint with your chosen component ID.
    * For a list of other REST operations you can perform, like updating or deleting a data source configuration, see [REST URLs](#rest-urls).
    <br/>
    <br/>

1. Configure data selection.

    For more information, see [PI Adapter for Structured Data Files data selection configuration](xref:PIAdapterForStructuredDataFilesDataSelectionConfiguration).

    **Note:** You can decide to have a default data selection file generated automatically or you can create the data selection file yourself.

## Structured Data Files data source schema

The full schema definition for the Structured Data Files data source configuration is in the `StructuredDataFiles_DataSource_schema.json` file located in one of the following folders:

Windows: `%ProgramFiles%\OSIsoft\Adapters\StructuredDataFiles\Schemas`

Linux: `/opt/OSIsoft/Adapters/StructuredDataFiles/Schemas`

## Structured Data Files data source parameters

The following parameters are available for configuring a Structured Data Files data source:

| Parameter                     | Required | Type      | Description |
|-------------------------------|----------|-----------|-------------|
| **FriendlyName** | Optional | `string` | The label to use for the data source. |
| **InputDirectory** | Required | `string` | Location of the source files to process.<br><br>Example: `C:\\InputDirectory` |
| **OutputDirectory** | Required | `string` | Location for the files to be moved to after being processed.<br><br>Example: `C:\\OutputDirectory` |
| **FileNameFilter** | Optional | `string` | File name filter for files in the InputDirectory. Use `*` as the wildcard character.<br><br>Example: `*.csv` |
| **HasHeader** | Optional | `bool` | Indicates if a header line is present in the file.<br><br>Default value: `false` |
| **Culture** | Optional | `string` | Locale setting for the input files.<br><br>Example: `en-US`<br>Default value: local culture |
| **TimeZone** | Optional | `string` | Time zone of timestamps in the input files. If specified, the value must be a valid entry from the IANA time zone database.<br><br>Example: `America/Los_Angeles`<br>Default value: `Etc/UTC` |
| **Format** | Optional | `string` | Input file format.<br><br>Allowed values: `Csv`, `Json`, `Xml`<br><br>Default value: `Csv` |
| **Compression** | Optional | `string` | Input file compression format.<br><br>Allowed value: `None`, `Zip`, `Tar`, `GZip`, `TarGZip`<br>Default value: `None` |
| **Encoding** | Optional | `string` | Character encoding used in the input files. <br><br>Allowed value: `UTF8`, `ASCII`, `Unicode`<br>Default value: `UTF8` |
| **FieldSeparator** | Optional | `string` | Character used to delineate fields in the input files. Only applies to CSV files.<br><br>Default value: `,` |
| **LineSeparator** | Optional | `string` | Character(s) used to separate lines in the input files. Only applies to CSV files.<br><br>Default value: `\n` |
| **StreamIdPrefix** | Optional | `string` | The stream ID prefix applied to all data items collected from the data source. <br><br>Default value: `{ComponentId}` |
| **DefaultStreamIdPattern** | Optional | `string` | Specifies the default stream ID pattern to use.<br><br>Possible parameters: `{FriendlyName}`, `{ValueField}`<br>Default pattern: `{FriendlyName}.{ValueField}` |

## Structured Data Files data source examples

The following are examples of valid Structured Data Files data source configurations:

### Structured Data Files data source configuration #1

```json
{
  "InputDirectory": "C:\\InputDirectory",
  "OutputDirectory": "C:\\OutputDirectory"
}
```

### Structured Data Files data source configuration #2

```json
{
  "FriendlyName": "Weather",
  "InputDirectory": "C:\\InputDirectory",
  "FileNameFilter": "*.csv",
  "OutputDirectory": "C:\\OutputDirectory",
  "HasHeader": true,
  "Culture": "fr-FR",
  "TimeZone": "Europe/Paris",
  "Compression": "Zip",
  "FieldSeparator": "|"
}
```

## REST URLs

| Relative URL | HTTP verb | Action |
| ------------ | --------- | ------ |
| api/v1/configuration/\<ComponentId\>/DataSource  | `GET` | Retrieves the Structured Data Files data source configuration |
| api/v1/configuration/\<ComponentId\>/DataSource  | `POST` | Creates the Structured Data Files data source configuration |
| api/v1/configuration/\<ComponentId\>/DataSource  | `PUT` | Configures or updates the Structured Data Files data source configuration |
| api/v1/configuration/\<ComponentId\>/DataSource | `DELETE` | Deletes the Structured Data Files data source configuration |

**Note:** Replace `<ComponentId>` with the ID of your Structured Data Files component, for example `StructuredDataFiles1`.
