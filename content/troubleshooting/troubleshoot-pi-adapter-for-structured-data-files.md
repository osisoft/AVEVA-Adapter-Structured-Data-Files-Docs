---
uid: TroubleshootPiAdapterForStructuredDataFiles
---

# Troubleshoot PI Adapter for Structured Data Files

PI Adapter for Structured Data Files provides troubleshooting features that enable you to verify adapter configuration, confirm connectivity, and view message logs. If you are unable to resolve issues with the adapter or need additional guidance, contact OSIsoft Technical Support through the [OSIsoft Customer Portal](https://my.osisoft.com/).

## Check configurations

Incorrect configurations can interrupt data flow and cause errors in values and ranges. Perform the following steps confirm correct configuration for your adapter.

1. Navigate to [data source configuration](xref:PIAdapterForSDFDataSourceConfiguration) and verify that the value entered for each parameter is correct.

    * **InputDirectory:** The input directory containing structured data files is valid.
    * **OutputDirectory:** The output directory for processed structured data files is valid.
    * **FileNameFilter**: The pattern value matches files intended for processing. If the value is intended, the adapter will not process the correct files.
    * **HasHeader**: If processing CSV files that include a header line, verify that this parameter is set to `true`.
    * **Culture**: Verify that the intended culture is set.
    * **TimeZone**: Verify that the intended timezone is set.
    * **Format**: Verify that the value matches the file type for processing.
    * **Compression**: If processing files that are compressed, verify that the value is set to correct format.
    * **Encoding**: Verify that the value is set to the correct encoding.
    * **FieldSeparator**: If processing CSV files, verify that the correct delineation character is set.
    * **LineSeparator**: If processing CSV files, verify that the correct character for separating lines is set.<br><br>

2. Navigate to [data selection configuration](xref:PIAdapterForSDFDataSelectionConfiguration) and verify that the value entered for each parameter is correct.

    * **ValueField**: The JSONPath, XPath, or CSV expression is valid. With an invalid expression, the adapter cannot extract a data value.
    * **TimeField**: The JSONPath, XPath, or CSV expression is valid. With an invalid expression, the adapter cannot extract a timestamp.
    * **DataType**: The correct data type is referenced. An incorrect data type causes data conversion to fail.
    * **TimeFormat**: The correct time format is referenced. A time format that does not match the value from **TimeField** means that the adapter cannot convert the timestamp.<br/><br/>

3. Navigate to [egress endpoints configuration](xref:EgressEndpointsConfiguration) and verify each configured endpoint's **Endpoint** property and credentials are correct.

    * For a PI server or EDS endpoint, verify **UserName** and **Password**.
    * For an OCS endpoint, verify **ClientId** and **ClientSecret**.

## Check connectivity

Perform the following steps to verify active connections to the data source and egress endpoints.

1. Start PI Web API and verify that the PI point values are  updating or start OCS and verify that the stream values are updating.

2. If configured, use a health endpoint to determine the status of the adapter.

    For more information, see [Health and diagnostics](xref:HealthAndDiagnostics).

## Check logs

Perform the following steps to view the adapter and endpoint logs to isolate issues for resolution.

1. Navigate to the logs directory:

    Windows: `%ProgramData%\OSIsoft\Adapters\StructuredDataFiles\Logs`
    Linux: `/usr/share/OSIsoft/Adapters/StructuredDataFiles/Logs`

2. Optional: Change the log level of the adapter to receive more information and context.

    For more information, see [Logging configuration](xref:LoggingConfiguration).
