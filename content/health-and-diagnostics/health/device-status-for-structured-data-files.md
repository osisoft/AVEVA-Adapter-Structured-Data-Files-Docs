---
uid: DeviceStatusForStructuredDataFiles
---

# Device status

The device status indicates the health of this component and if it is currently communicating properly with the data source. This time-series data is stored within a PI point or OCS stream, depending on the endpoint type. During healthy steady-state operation, a value of `Good` is expected.

| Property                          | Type                                 | description                    |
|-----------------------------------|--------------------------------------|--------------------------------|
| **Time**                          | `string`                               | Timestamp of the event        |
| **DeviceStatus**                  | `string`                               | The value of the `DeviceStatus` |

The possible statuses:

| Status                            | Meaning                               |
|-----------------------------------|---------------------------------------|
| `Good`                          | The component is connected to the data source and is successfully processing files. |
| `ConnectedNoData`               | The component is connected to the data source, but a data file contained no data for selected items. |
| `AttemptingFailover`            | The component is attempting to fail over.|
| `Starting`                      | The component is currently in the process of starting up and is not yet connected to the data source. |
| `DeviceInError`                 | The component encountered an error while processing files, either a file can not be opened or moved successfully. |
| `Shutdown`                      | The component is in the process of shutting down or has finished. |
| `Removed`                       | The component has been removed and will no longer collect data. |
| `NotConfigured`                 | The component has been created but is not yet configured. |
