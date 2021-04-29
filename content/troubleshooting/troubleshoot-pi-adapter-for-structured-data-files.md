---
uid: TroubleshootPiAdapterForStructuredDataFiles
---

# Troubleshoot PI Adapter for Structured Data Files

If the adapter is not working as expected, you can troubleshoot by viewing message logs and verifying adapter configuration and connectivity. If you are unable to resolve issues with the adapter or need additional guidance, contact OSIsoft Technical Support through the [OSIsoft Customer Portal](https://my.osisoft.com/).

## Check configurations

Incorrect configurations can interrupt data flow and cause errors in values and ranges. Perform the following steps confirm correct configuration for your adapter.

1. Navigate to [data source configuration](xref:PIAdapterForSDFDataSourceConfiguration) and validate each parameter value.

2. Navigate to [data selection configuration](xref:PIAdapterForSDFDataSelectionConfiguration) and validate each parameter value.

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
