---
uid: PIAdapterForStructuredDataFilesDataSourceConfiguration
---

# PI Adapter for Structured Data Files data source configuration

To use the adapter, you must configure the data source to receive data.

## Configure Structured Data Files data source

**Note:** To modify a Structured Data Files data source configuration, you must use the REST endpoints to add or edit the configuration.

Complete the following steps to configure a Structured Data Files data source:

1. Use any text editor to create a file that contains a Structured Data Files data source in the JSON format.
    - For content structure, see [Structured Data Files data source examples](#structured-data-files-data-source-examples).
    - For a table of all available parameters, see [Structured Data Files data source parameters](#structured-data-files-data-source-examples).
2. Save the file. For example, `ConfigureDataSource.json`.
3. Use any of the [Configuration tools](xref:ConfigurationTools1-3) capable of making HTTP requests to run a PUT command with the contents of that file to the following endpoint: `http://localhost:5590/api/v1/configuration/<ComponentId>/DataSource/`.

      **Note:** The following example uses SDF1 as the adapter component name. For more information on how to add a component, see [System components configuration](xref:SystemComponentsConfiguration1-3).

    `5590` is the default port number. If you selected a different port number, replace it with that value.

    Example using `curl`:

    ```bash
    curl -d "@ConfigureDataSource.json" -H "Content-Type: application/json" -X PUT "http://localhost:5590/api/v1/configuration/SDF1/DataSource"
    ```

    **Note:** Run this command from the same directory where the file is located.

4. Configure data selection. For more information, see [PI Adapter for Structured Data Files data selection configuration](xref:PIAdapterForStructuredDataFilesDataSelectionConfiguration).

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
| **[InputDirectory](###Note)** | Required | `string` | Location of the source files to process.<br><br>Example: `C:\\InputDirectory` |
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
| **DefaultStreamIdPattern** | Optional | `string` | Specifies the default stream Id pattern to use.<br><br>Possible parameters: `{FriendlyName}`, `{ValueField}`<br>Default pattern: `{FriendlyName}.{ValueField}` |
### Note:
If InputDirectory is deleted while the Adapter is running, the user should restart the Adapter once the same directory is restored.  
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
| api/v1/configuration/_ComponentId_/DataSource  | GET | Retrieves the Structured Data Files data source configuration |
| api/v1/configuration/_ComponentId_/DataSource  | POST | Creates the Structured Data Files data source configuration |
| api/v1/configuration/_ComponentId_/DataSource  | PUT | Configures or updates the Structured Data Files data source configuration |
| api/v1/configuration/_ComponentId_/DataSource | DELETE | Deletes the Structured Data Files data source configuration |

**Note:** Replace _ComponentId_ with the Id of your Structured Data Files component, for example SDF1.
