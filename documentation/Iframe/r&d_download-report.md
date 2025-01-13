## Prerequisites

- get the Access Token:

## Flow of Exporting a report as pdf/image/csv

1. exportToFileInGroup

endpoint: `https://api.powerbi.com/v1.0/myorg/groups/{groupId}/reports/{reportId}/ExportTo`

method: `POST`

Authorization: Bearer {accessToken}

parameters: groupId, reportId

body:

```json
{ "format": "PDF" }
```

Could also enter csv, image, or pbix as format

returns: starts the export job of the report and returns the exportId as id

2. GetExportToFileStatusInGroup

endpoint: <https://api.powerbi.com/v1.0/myorg/groups/{groupId}/reports/{reportId}/exports/{exportId}>

method: GET

Authorization: Bearer {accessToken}

returns: report status, resourceLocation (can download the report on status: "Succeeded" from the resourceLocation. link valid till 1 day)

3. GetFileOfExportToFileInGroup

endpoint: <https://api.powerbi.com/v1.0/myorg/groups/{groupId}/reports/{reportId}/exports/{exportId}/file>

method: GET

Authorization: Bearer {accessToken}

returns: the exported file

```

```

### Notes

1. in user-owns-data scenarios the reports have the inbuilt export report as pdf/image/csv options
2. in app-owns-data scenarios (which we use in our scale RCM app), the Paginated reports have the export option built in the report
3. in app-owns-data scenario for normal reports (or non-paginated reports) we need to create that functionality ourselves to download report by calling the PowerBi API.
4. we can also export the reports using power-automate flows. which will export and store the reports in sharepoint.

### hurdles

1. calling the exportToFileInGroup api gives error: FeatureNotAvailableError
   wip: r&d to find and fix the issue...
