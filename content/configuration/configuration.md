---
uid: StructuredDataFilesConfiguration
---
# Configuration

Before you can begin using the adapter, you must configure the data source and data selection using the adapter's REST API. <!-- I would really like to see the configurations listed in order here, so that I have a road map of what I need to do. You could then indicate which ones are optional and get rid of the some are required and others are optional sentences. -->

The examples in the configuration topics use cURL, a commonly available tool on both Windows and Linux. You can configure the adapter with any programming language or tool that supports making REST calls or with the EdgeCmd utility. For more information, see the [EdgeCmd utility documentation](https://docs.osisoft.com/bundle/edgecmd/page/index.html).

To validate successful configurations, you can perform data retrieval (`GET` commands) with a browser, if available, on your device.

For more information on PI Adapter configuration tools, see [Configuration tools](xref:ConfigurationTools).

## Quick Start

This Quick Start guides you through setup of each configuration file available for the PI Adapter for Structured Data Files. As you complete each step, perform each **Required** configuration to establish a data flow from a data source to one or more endpoints. Some configurations are optional.

**Important:** If you want to complete the optional configurations in each step below, complete those tasks _before_ the required tasks.

1. Configure system components.

    | Configuration | Description | Required | Optional |
    |--|--|:-:|:-:|
    | [system components](xref:SystemComponentsConfiguration) | Defines each component instance on the system host. | &#x2714; |  |
    <br>

1. Configure egress endpoints.

    | Configuration | Description | Required | Optional |
    |--|--|:-:|:-:|
    | [network proxy](xref:ConfigureANetworkProxy) | If there is a proxy between the adapter and your egress endpoints, define it using this configuration. |  | &#x2714; |
    | [egress endpoints](xref:EgressEndpointsConfiguration) | Defines the final locations that the adapter sends OMF data. | &#x2714; |  |
    <br>

1. **Optional:** Configure health endpoints.

    | Configuration | Description | Required | Optional |
    |--|--|:-:|:-:|
    | [general](xref:GeneralConfiguration) | Defines whether diagnostic information is included in health data. Requires a health endpoint. |  | &#x2714; |
    | [health endpoint](xref:HealthEndpointConfiguration) | Defines endpoint where PI adapters produce and store health data. |  | &#x2714; |
    <br>

1. **Optional:** Complete buffering and logging configurations. 

    | Configuration | Description | Required | Optional |
    |--|--|:-:|:-:|
    | [buffering](xref:BufferingConfiguration) | Defines whether data buffering is enabled, the volume of data buffered, and the location of buffered files. |  | &#x2714; |
    | [logging](xref:LoggingConfiguration) | Defines custom logging options. |  | &#x2714; |
    <br>

1. Complete data source configurations. The adapter starts collecting data immediately after you complete the **data source** configuration.

    **Important:** Complete all other adapter configuration steps before data source configuration. This practice ensures a complete history of data collection.

    | Configuration | Description | Required | Optional |
    |--|--|:-:|:-:|
    | [data filter](xref:DataFiltersConfiguration) | A reusable file that defines what data within the data source files are received.<br/><br/>Can be used in conjunction with **data selection** configurations. |  | &#x2714; |
    | [data selection](xref:PIAdapterForSDFDataSelectionConfiguration) | Defines what data within the data source files are received. | &#x2714; |  |
    | [data source](xref:PIAdapterForSDFDataSourceConfiguration) | Defines the source that the adapter receives data files from. | &#x2714; |  |
