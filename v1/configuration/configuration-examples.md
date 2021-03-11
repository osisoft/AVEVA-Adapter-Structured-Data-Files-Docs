---
uid: PIAdapterForStructuredDataFilesConfigurationExamples
---

# PI Adapter for Structured Data Files configuration examples

The following JSON samples provide examples for all configurations available for PI Adapter for Structured Data Files.

## System components configuration with two Structured Data Files adapter instances

```json
[
  {
    "ComponentId": "StructuredDataFiles1",
    "ComponentType": "StructuredDataFiles"
  },
  {
    "ComponentId": "StructuredDataFiles2",
    "ComponentType": "StructuredDataFiles"
  },
  {
    "ComponentId": "OmfEgress",
    "ComponentType": "OmfEgress"
  }
]
```

## Adapter configuration

```json
{
  "StructuredDataFiles1": {
    "Logging": {
      "logLevel": "Information",
      "logFileSizeLimitBytes": 34636833,
      "logFileCountLimit": 31
    },
    "DataSource": {
      "FriendlyName": "Weather",
      "InputDirectory": "C:\\InputDirectory",
      "FileNameFilter": "*.csv",
      "OutputDirectory": "C:\\OutputDirectory",
      "HasHeader": true,
      "Culture": "fr-FR",
      "TimeZone": "Europe/Paris",
      "Compression": "Zip",
      "FieldSeparator": "|"
    },
    "DataSelection": [
      {
        "Selected": true,
        "Name": "Name",
        "StreamId": "StreamId",
        "ValueField": "FanSpeed",
        "TimeField": "FileCreationTime",
        "TimeFormat": "mm/dd/yy",
        "DataType": "Int32"
      }
    ]
  },
  "System": {
    "Logging": {
      "logLevel": "Information",
      "logFileSizeLimitBytes": 34636833,
      "logFileCountLimit": 31
    },
    "HealthEndpoints": [],
    "Diagnostics": {
      "enableDiagnostics": true
    },
    "Components": [
      {
        "componentId": "Egress",
        "componentType": "OmfEgress"
      },
      {
        "componentId": "StructuredDataFiles1",
        "componentType": "StructuredDataFiles"
      }
    ],
    "Buffering": {
      "BufferLocation": "C:/ProgramData/OSIsoft/Adapters/StructuredDataFiles/Buffers",
      "MaxBufferSizeMB": -1,
      "EnableBuffering": true
    }
  },
  "OmfEgress": {
    "Logging": {
      "logLevel": "Information",
      "logFileSizeLimitBytes": 34636833,
      "logFileCountLimit": 31
    },
    "DataEndpoints": [
      {
        "id": "WebAPI EndPoint",
        "endpoint": "https://PIWEBAPIServer/piwebapi/omf",
        "userName": "USERNAME",
        "password": "PASSWORD"
      },
      {
        "id": "OCS Endpoint",
        "endpoint": "https://OCSEndpoint/omf",
        "clientId": "CLIENTID",
        "clientSecret": "CLIENTSECRET"
      },
      {
        "Id": "EDS",
        "Endpoint": "http://localhost:/api/v1/tenants/default/namespaces/default/omf",
        "UserName": "eds",
        "Password": "eds"
      }
    ]
  }
}
```

## Data source configuration

The following are representations of data source configurations for the Structured Data Files adapter.

### Data source configuration with required parameters

```json
{
  "InputDirectory": "C:\\InputDirectory",
  "OutputDirectory": "C:\\OutputDirectory"
}

```

### Data source configuration with optional parameters

```json
{
  "FriendlyName": "Weather",
  "InputDirectory": "C:\\InputDirectory",
  "FileNameFilter": "*.csv",
  "OutputDirectory": "C:\\OutputDirectory",
  "HasHeader": true,
  "Culture": "fr-FR",
  "TimeZone": "Europe/Paris",
  "Compression": "Zip",
  "FieldSeparator": "|"
}
```

## Data selection configuration

The following are representations of data selection configurations for the Structured Data Files adapter.

### Data selection configuration with custom TimeFormat

```json
[
  {
    "Selected": true,
    "Name": "Name",
    "StreamId": "StreamId",
    "ValueField": "FanSpeed",
    "TimeField": "FileCreationTime",
    "TimeFormat": "mm/dd/yy",
    "DataType": "Int32"
  }
]
```

### Data selection configuration with unselected item

```json
[
  {
    "Selected": false,
    "Name": "Name",
    "StreamId": "StreamId",
    "ValueField": "Pressure",
    "TimeField": "PressureTimeStamp",
    "DataType": "Int16"
  }
]
```

### Data selection configuration with XPath ValueField

```json
[
  {
    "Selected": true,
    "Name": "Name",
    "StreamId": "StreamId",
    "ValueField": "/bookstore/book/title",
    "TimeField": "bookStoreTimeStamp",
    "DataType": "String"
  }
]

```
