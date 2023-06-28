---
uid: ConfigurationExamples
---

# Configuration examples

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

The following example is a complete configuration for the PI Adapter for Structured Data Files.

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
        "IndexField": "FileCreationTime",
        "IndexFormat": "mm/dd/yy",
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
      "EnablePersistentBuffering": true
    },
    "General": {
      "enableDiagnostics": true,
      "metadataLevel": "Medium"
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
        "id": "ADH Endpoint",
        "endpoint": "https://ADHEndpoint/omf",
        "clientId": "CLIENTID",
        "clientSecret": "CLIENTSECRET"
      }
    ]
  },
  "DataFilters": [
    {
      "id": "DuplicateData",
      "absoluteDeadband": 0,
      "percentChange": null,
      "expirationPeriod": "1:00:00"
    }
  ]
}
```

## Data source configuration

The following are representations of data source configurations for the Structured Data Files adapter.


[!include[Data source configurations](../_includes/data-source-configuration.md)]
