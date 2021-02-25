---
uid: StructuredDataFilesConfiguration
---
# Configuration

PI Adapter for Structured Data Files collects data from XML, JSON, and CSV files stored on the edge; converts that data to the OSIsoft Message Format; and then sends the data to one or more  endpoint.

Before the adapter can begin this process, you must set several adapter configuration files by calling its REST API. Some configurations are required. Others are optional.

The examples in the configuration topics use cURL, a commonly available tool on both Windows and Linux. You can configure the adapter with any programming language or tool that supports making REST calls or with the EdgeCmd utility. For more information, see the [EdgeCmd utility documentation](https://osisoft.github.io/Edgecmd-Docs/V1.2/edgecmd-utility.html).

To validate successful configurations, you can perform data retrieval (`GET` commands) with a browser, if available, on your device.

For more information on PI Adapter configuration tools, see [Configuration tools](xref:ConfigurationTools1-3).

## Quick Start

The following table lists all configurations available for the PI Adapter for Structured Data Files along with their purpose. Complete each **Required** configuration to establish a data flow from a Structured Data Files data source to one or more endpoint. Complete them in sequential order. Some configurations are optional.

| Configuration | Description | Required | Optional |
|--|--|:-:|:-:|
| [system components][1] | Defines each component instance on the system host. | &#x2714; |  |
| [data source][2] | Defines the source that the adapter receives data files from. | &#x2714; |  |
| [data selection][3] | Defines what data within the data source files are received. | &#x2714; |  |
| [data filter][4] | A reusable file that defines what data within the data source files are received.<br/><br/>Can be used in conjunction with Structured Data File data selection configurations. |  | &#x2714; |
| [egress endpoints][5] | Defines the final locations that the adapter sends OMF data. | &#x2714; |  |
| [network proxy][6] | If that is a proxy between the adapter and your egress endpoints, define it using this configuration. |  | &#x2714; |
| [health endpoint][7] | Defines endpoint where PI adapters produce and store health data. |  | &#x2714; |
| [general][8] | Defines whether diagnostic information is included in health data.<br/><br/>**Prerequisite:** complete [health endpoint][7]. |  | &#x2714; |
| [buffering][9] | Defines whether data buffering is enabled, the volume of data buffered, and the location of buffered files. |  | &#x2714; |
| [logging][10] | Defines custom logging options. |  | &#x2714; |

[1]: xref:SystemComponentsConfiguration1-3
[2]: xref:PIAdapterForStructuredDataFilesDataSourceConfiguration
[3]: xref:PIAdapterForStructuredDataFilesDataSelectionConfiguration
[4]: xref:DataFiltersConfiguration1-3
[5]: xref:EgressEndpointsConfiguration1-3
[6]: xref:ConfigureANetworkProxy1-3
[7]: xref:HealthEndpointConfiguration1-3
[8]: xref:GeneralConfiguration1-3
[9]: xref:BufferingConfiguration1-3
[10]: xref:LoggingConfiguration1-3
