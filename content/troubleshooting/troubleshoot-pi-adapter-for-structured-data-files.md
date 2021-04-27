---
uid: TroubleshootPiAdapterForStructuredDataFiles
---

# Troubleshoot PI Adapter for Structured Data Files

If the adapter is not working as expected, you can troubleshoot by viewing message logs and verifying adapter configuration and connectivity. If you are unable to resolve issues with the adapter or need additional guidance, contact OSIsoft Technical Support through the [OSIsoft Customer Portal](https://my.osisoft.com/).

## Check configurations

Incorrect configurations can interrupt data flow and cause errors in values and ranges. Perform the following steps confirm correct configuration for your adapter.

1. Navigate to [data source configuration](xref:PIAdapterForSDFDataSourceConfiguration) and verify that the value entered for each parameter is correct.

    <!-- Mark Bishop 4/22: Requesting SME assistance on:

    1. Which parameters to check when troubleshooting. We should omit any parameters on this last won't "break" data collection.
    2. For parameters that will "break" data collection, list how the misconfigured value affects data collection. Examples from Modbus:

        * DeviceId - The referenced device exists in the data source configuration.

            A non-existent or incorrect DeviceId causes the adapter to not find the data source device.

        * UnitId - The correct UnitId number is referenced.

            An incorrect UnitId number can cause the adapter to request data from a different or non-existent device.

    -->

    * **FriendlyName:**

        <!-- SWAG: Omit parameter -->

    * **InputDirectory:**

        <!-- SWAG: The input directory containing structured data files is valid. -->

    * **OutputDirectory:**

        <!-- SWAG: The output directory for processed structured data files is valid. -->

    * **FileNameFilter**:

        <!-- SWAG: The pattern value matches files intended for processing. If the value is intended, the adapter will not process the correct files. -->

    * **HasHeader**:

        <!-- SWAG: If processing CSV files that include a header line, verify that this parameter is set to `true`. -->

    * **Culture**:

        <!-- SWAG: Verify that the intended culture is set. -->

    * **TimeZone**:

        <!-- SWAG: Verify that the intended timezone is set. -->

    * **Format**:

        <!-- SWAG:  Verify that the value matches the file type for processing. -->

    * **Compression**:

        <!-- SWAG: If processing files that are compressed, verify that the value is set to correct format. -->

    * **Encoding**:

        <!-- SWAG: Verify that the value is set to the correct encoding. -->

    * **FieldSeparator**:

        <!-- SWAG: If processing CSV files, verify that the correct delineation character is set. -->

    * **LineSeparator**:

        <!-- SWAG: If processing CSV files, verify that the correct character for separating lines is set. -->

    * **StreamIdPrefix:**

        <!-- SWAG: Omit parameter -->

    * **DefaultStreamIdPattern:**

        <!-- SWAG: Omit parameter -->


2. Navigate to [data selection configuration](xref:PIAdapterForSDFDataSelectionConfiguration) and verify that the value entered for each parameter is correct.

    <!-- Mark Bishop 4/22: Requesting SME assistance on:

    1. Which parameters to check when troubleshooting. We should omit any parameters on this last won't "break" data collection. 
    2. For parameters that will "break" data collection, list how the misconfigured value affects data collection. Examples from Modbus:

        * DeviceId - The referenced device exists in the data source configuration.

            A non-existent or incorrect DeviceId causes the adapter to not find the data source device.

        * UnitId - The correct UnitId number is referenced.

            An incorrect UnitId number can cause the adapter to request data from a different or non-existent device.

    -->

    * **Name:**

        <!-- SWAG: omit parameter -->

    * **DataFilterId:**

        <!-- SWAG: omit parameter -->

    * **Selected:**

        <!-- SWAG: omit parameter -->

    * **StreamId:**

        <!-- SWAG: omit parameter -->

    * **ValueField**:

        <!-- SWAG: The JSONPath, XPath, or CSV expression is valid. With an invalid expression, the adapter cannot extract a data value. -->

    * **TimeField**:

        <!-- SWAG: The JSONPath, XPath, or CSV expression is valid. With an invalid expression, the adapter cannot extract a timestamp. -->

    * **DataType**:

        <!-- SWAG: The correct data type is referenced. An incorrect data type causes data conversion to fail. -->

    * **TimeFormat**:

        <!-- SWAG: The correct time format is referenced. A time format that does not match the value from **TimeField** means that the adapter cannot convert the timestamp.<br/><br/> -->


3. Navigate to [egress endpoints configuration](xref:EgressEndpointsConfiguration) and verify each configured endpoint's **Endpoint** property and credentials are correct.

    * For a PI server or EDS endpoint, verify **UserName** and **Password**.
    * For an OCS endpoint, verify **ClientId** and **ClientSecret**.

## Check connectivity

Perform the following steps to verify active connections to the data source and egress endpoints.

1. Start PI Web API and verify that the PI point values are updating or verify within OCS that the stream values are updating.

2. If configured, use a health endpoint to determine the status of the adapter.

    For more information, see [Health and diagnostics](xref:HealthAndDiagnostics).

## Check logs

Perform the following steps to view the adapter and endpoint logs to isolate issues for resolution.

1. Navigate to the logs directory:

    Windows: `%ProgramData%\OSIsoft\Adapters\StructuredDataFiles\Logs`
    Linux: `/usr/share/OSIsoft/Adapters/StructuredDataFiles/Logs`

2. Optional: Change the log level of the adapter to receive more information and context.

    For more information, see [Logging configuration](xref:LoggingConfiguration).
