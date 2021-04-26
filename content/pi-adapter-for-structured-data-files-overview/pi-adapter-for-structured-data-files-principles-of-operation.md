---
uid: PIAdapterforSDFPrinciplesOfOperation
---

# PI Adapter for Structured Data Files principles of operation

The adapter's operations focus on data collection and stream creation.

## Adapter configuration

For the adapter to start data collection, you need to configure the adapter by defining the following:

- **Data source**: Provide the data source input directory from which the adapter should collect data. You must also provide an output directory, which is where the adapter copies processed files.
- **Data selection**: Select items for which the adapter should gather data from the files.

For more information, see [PI Adapter for Structured Data Files data source configuration](xref:PIAdapterForSDFDataSourceConfiguration) and [PI Adapter for Structured Data Files data selection configuration](xref:PIAdapterForSDFDataSelectionConfiguration).

## Data collection

When the adapter starts, it begins scanning for files in the input directory that match the configured file name filter. These files are processed in the order of their creation time starting with the oldest. After a file has been processed, it will be moved to the output directory. If the input directory is empty when scanned by the adapter, the adapter will wait five seconds before rescanning.

**Notes:**

* You must assign the following permissions to the adapter service account to successfully process structured data files:

    | Directory        | Read     | Write    |
    |------------------|:--------:|:--------:|
    | input directory  | &#x2714; | &#x2714; |
    | output directory |          | &#x2714; |

* If the adapter is not able to open a file from the input directory or move a file to the output directory after processing it, new files will not be processed until the problem is resolved. Do not open a file once it has been placed in the input directory as this could prevent the adapter from opening or moving it.

### Supported file types

The adapter supports files that are in CSV, JSON, or XML format. The raw data files can be uncompressed or compressed as a zip, gzip, tar, or tar.gzip files. The files can have UTF-8, ASCII, or Unicode encoding.

**Note:** Compression is only supported at the individual file level. The adapter does not support compressed archives that contain multiple files.

### Supported data types

The following table lists value data types that the adapter supports for data collection and types of streams that will be created.

| Value data type | Stream data type |
|-----------------|------------------|
| SByte     | `Int16`  |
| Byte     | `Int16`  |
| Int16     | `Int16`  |
| UInt16     | `UInt16`  |
| Int32     | `Int32`  |
| UInt32     | `UInt32`  |
| Int64     | `Int64`  |
| UInt64     | `UInt64`  |
| Single     | `Single`  |
| Double     | `Double`  |
| Decimal     | `Single`  |
| DateTime     | `DateTime`  |
| String     | `String`  |

## Stream creation

The adapter creates a stream with two properties for a selected item. The properties are described in the following table:

| Property name | Data type | Description |
|---------------|-----------|-------------|
| `Timestamp`     | DateTime  | Timestamp of the given item update. |
| `Value`         | Specified on the type of incoming value | Value of the item update. |

**Note:** If streams are deleted from an endpoint while the adapter is running, the ingress component must be restarted to recreate the streams. See [Start and stop ingress component](xref:StartAndStopIngressComponent).

Certain metadata are sent with each stream created.
The following metadata are common for every adapter type:

- **ComponentId**: Specifies the data source, for example, _StructuredDataFiles1_
- **ComponentType**: Specifies the type of adapter, for example, _StructuredDataFiles_

Metadata specific to PI Adapter for Structured Data Files:

- **InputDirectory**: Location of the source files to process.

The metadata level is set in [General configuration](xref:GeneralConfiguration). For PI Adapter for Structured Data Files, the following metadata is sent for the individual level:

- `None`: No metadata
- `Low`: AdapterType (_ComponentType_) and DataSource (_ComponentId_)
- `Medium`: AdapterType (_ComponentType_) and DataSource (_ComponentId_)
- `High`: AdapterType (_ComponentType_), DataSource (_ComponentId_), InputDirectory

Each stream created for a given item has a unique identifier (stream ID). If you specify a custom stream ID for the item in data selection configuration, the adapter uses that stream ID to create the stream. Otherwise, the adapter constructs the stream ID with the following format constructed from the data source's `FriendlyName` and the item's `ValueField`:

```code
<Adapter Component ID>.<FriendlyName>.<ValueField>
```

**Note:** The naming convention is affected by `StreamIdPrefix` and `DefaultStreamIdPattern` settings in data source configuration. For more information, see [PI Adapter for Structured Data Files data source configuration](xref:PIAdapterForSDFDataSourceConfiguration).
