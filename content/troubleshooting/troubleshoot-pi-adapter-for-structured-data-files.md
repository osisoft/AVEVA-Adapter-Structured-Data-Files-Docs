---
uid: TroubleshootPiAdapterForStructuredDataFiles
---

# Troubleshoot PI Adapter for Structured Data Files

If the adapter is not working as expected, you can troubleshoot by viewing message logs and verifying adapter configuration and connectivity. If you are unable to resolve issues with the adapter or need additional guidance, contact AVEVA PI Support through the [AVEVA Customer Portal](https://my.osisoft.com/).

## Check configurations

Incorrect configurations can interrupt data flow and cause errors in values and ranges. Perform the following steps confirm correct configuration for your adapter.

1. Navigate to [data source configuration](xref:PIAdapterForSDFDataSourceConfiguration) and validate each parameter value.

2. Navigate to [data selection configuration](xref:PIAdapterForSDFDataSelectionConfiguration) and validate each parameter value.

3. Navigate to [egress endpoints configuration](xref:EgressEndpointsConfiguration) and verify each configured endpoint's **Endpoint** property and credentials are correct.

    * For a PI server endpoint, verify **UserName** and **Password**.
    * For an ADH endpoint, verify **ClientId** and **ClientSecret**.

## Check connectivity

Perform the following steps to verify active connections to the data source and egress endpoints.

1. Based on your egress endpoints, verify that data values are updating.

    * For PI Server, send a request to the PI Web API to verify that PI point values are updating. Use Postman or a Web browser to send the request. For more information, see [PI Web API Reference](https://techsupport.osisoft.com/Documentation/PI-Web-API/help/controllers/point.html).

        Alternatively, use any PI Client software to read point values from the PI Data Archive directly.

    * For ADH, view the ADH portal to verify that data streams are updating. For more information, see [Getting started with trend data](https://ocs-docs.osisoft.com/Content_Portal/Quickstarts/Getting-Started-Trend.html).

        Alternatively, you can use Postman to send an API request to verify data streams. For more information, see [API calls for reading data](https://ocs-docs.osisoft.com/Content_Portal/Documentation/SequentialDataStore/Reading_Data_API.html).

2. If configured, use a health endpoint to determine the status of the adapter.

    For more information, see [Health and diagnostics](xref:HealthAndDiagnostics).

## Check logs

Perform the following steps to view the adapter and endpoint logs to isolate issues for resolution.

1. Navigate to the logs directory:

    Windows: `%ProgramData%\OSIsoft\Adapters\StructuredDataFiles\Logs`
    Linux: `/usr/share/OSIsoft/Adapters/StructuredDataFiles/Logs`

2. Optional: Change the log level of the adapter to receive more information and context.

    For more information, see [Logging configuration](xref:LoggingConfiguration).
