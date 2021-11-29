### Data source configuration with required parameters

```json
{
  "inputDirectory": "C:\\InputDirectory",
  "outputDirectory": "C:\\OutputDirectory"
}

```

### Data source configuration with optional parameters (Windows)

```json
{
  "friendlyName": "Weather",
  "inputDirectory": "C:\\InputDirectory",
  "fileNameFilter": "*.csv",
  "outputDirectory": "C:\\OutputDirectory",
  "hasHeader": true,
  "culture": "fr-FR",
  "timeZone": "Europe/Paris",
  "compression": "Zip",
  "fieldSeparator": "|",
  "purgeDelay": "5.04:03:02.0000000"
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
