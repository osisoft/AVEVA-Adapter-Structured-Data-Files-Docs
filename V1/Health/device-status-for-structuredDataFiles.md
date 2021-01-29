---
uid: DeviceStatusForStructuredDataFiles
---

# Device status

The device status indicates the health of the component and whether it is currently communicating properly with the data source. This time-series data is stored within a PI point or OCS stream, depending on the endpoint type.

The StructuredDataFiles adapter sends a status value of `Good` when all configured StructuredDataFiles devices respond within the specified timeout. When a StructuredDataFiles device fails to process file to more than one **AllowedConsecutiveFailedRequests**,  it is considered disconnected and a `DeviceInError` status is sent. For more information, see [PI Adapter for StructuredDataFiles data source configuration](xref:PIAdapterforStructuredDataFilesDataSourceConfiguration). For any individual device that transitions from connected to disconnected and vice versa, an appropriate status is sent. If there are one or more disconnected devices, `DeviceInError` is sent; if all devices are connected, `Good` is sent.

| Property                          | Type                                 | description                    |
|-----------------------------------|--------------------------------------|--------------------------------|
| **Time**                          | `string`                               | Timestamp of the event        |
| **DeviceStatus**                  | `string`                               | The value of the `DeviceStatus` |

The possible statuses:

| Status                            | Meaning                               |
|-----------------------------------|---------------------------------------|
| `Good`                          | Connected to a DataSource, able to process files successfully. |
| `ConnectedNoData`               | Connected to a DataSource, but error processing files. |
| `No Status`                     | Connected to a Datasource, but no files to process. |
| `Starting`                      | The component is currently in the process of starting up and is not yet connected to the data source. |
| `DeviceInError`                 | The component encountered an error either while connecting to the data source. |
| `Shutdown`                      | The component is either in the process of shutting down or has finished. |
| `Removed`                       | The adapter component has been removed and will no longer collect data. |
| `NotConfigured`                 | The adapter component has been created but is not yet configured. |
