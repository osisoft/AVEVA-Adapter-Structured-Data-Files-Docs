---
uid: PIAdapterforSDFPrinciplesOfOperation
---

# PI Adapter for Structured Data Files principles of operation

The Structured Data Files adapter's operations focus on data collection and streams creation.

## Adapter configuration

For the Structured Data Files adapter to start data collection, you need to configure the adapter by defining the following:

- Data source: Provide the data source from which the adapter should collect data.
- Data selection: Select Structured Data Files items to which the adapter should request data or subscribe for data.
- Logging: Set up the logging attributes to manage the adapter logging behavior.

For more information, see [PI Adapter for Structured Data Files data source configuration](xref:PIAdapterforSDFDataSourceConfiguration), [PI Adapter for Structured Data Files data selection configuration](xref:PIAdapterforSDFtDataSelectionConfiguration), and [Logging configuration](xref:LoggingConfiguration).

## Data collection

The Structured Data Files adapter collects time-series data from selected objects... The adapter supports...

### Object types and data types

The following table lists object types that the Structured Data Files adapter supports for data collection and types of streams that will be created.

| Structured Data Files object type | Stream data type |
|------------------|------------------|
| TBD     | `TBD`  |
| TBD     | `TBD`  |

## Stream creation

The Structured Data Files adapter creates a stream with two properties for a selected Structured Data Files item. The properties are described in the following table:

| Property name | Data type | Description |
|---------------|-----------|-------------|
| `Timestamp`     | DateTime  | Timestamp of the given Structured Data Files item value update. |
| `Value`         | Specified on the type of incoming Structured Data Files value | Value of the Structured Data Files item update. |

**Note:** If streams are deleted from an endpoint while the adapter is running, the adapter process must be restarted in order for the streams to be recreated.

Certain metadata are sent with each stream created.
The following metadata are common for every adapter type:

- **ComponentId**: Specifies the data source, for example, _SDF1_
- **ComponentType**: Specifies the type of adapter, for example, _SDF1_

Metadata specific to the Structured Data Files adapter:

- **Device**: The Device ID of the Structured Data Files device
- **SourceId**: SourceId is constructed using the following pattern: {DeviceId}.{ObjectType}{ObjectId}.{PropertyIdentifier}
- **LocalName**: The Structured Data Files ObjectName as provided by the Structured Data Files object

The metadata level is set in [General configuration](xref:GeneralConfiguration). For the Structured Data Files adapter, the following metadata is sent for the individual level:

- `None`: No metadata
- `Low`: AdapterType (_ComponentType_) and DataSource (_ComponentId_)
- `Medium`: AdapterType (_ComponentType_) and DataSource (_ComponentId_)
- `High`: AdapterType (ComponentType), DataSource (ComponentId), Device, SourceId and LocalName

Each stream created for a given Structured Data Files item has a unique identifier (stream ID). If you specify a custom stream ID for the Structured Data Files item in data selection configuration, the adapter uses that stream ID to create the stream. Otherwise, the adapter constructs the stream ID with the following format constructed from the Structured Data Files item node ID:

```code
<Adapter Component ID>.<Device ID>.<Object Type><Object ID>.<Property Identifier>
```

**Note:** The naming convention is affected by `StreamIdPrefix` and `DefaultStreamIdPattern` settings in data source configuration. For more information, see [PI Adapter for Structured Data Files data source configuration](xref:PIAdapterforSDFDataSourceConfiguration).
