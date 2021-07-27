### Data source configuration with required parameters

```json
{
  "InputDirectory": "C:\\InputDirectory",
  "OutputDirectory": "C:\\OutputDirectory"
}

```

### Data source configuration with optional parameters (Windows)

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
  "FieldSeparator": "|",
  "PurgeDelay": "5.04:03:02.0000000"
}
```

### Data source configuration with optional parameters (Linux)

```json
{ 
  "friendlyName": "NA-Pumps",
  "inputDirectory": "/usr/mnt/InputDir/",
  "fileNameFilter": "*",
  "outputDirectory": "/usr/mnt/OutputDir/",
  "hasHeader": true,
  "format": "Csv",
  "compression": "None",
  "encoding": "UTF8",
  "fieldSeparator": ",",
  "lineSeparator": "\n",
  "defaultStreamIdPattern": "{FriendlyName}.{ValueField}",
  "purgeDelay": "5.04:03:02.0000000"
}
```
