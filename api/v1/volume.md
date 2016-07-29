Volume is the measurement of the size and amount of data flowing through Listener. Due to the asynchronous nature of Listener, you cannot track a single packet through the entire flow with certainty; however, you can use it to determine the volume for data flowing in general for all of Listener or a specific source.

* [Volume Object](#volume-object)
* [Listener Volume](#listener-volume)
* [Source Volume](#source-volume)

## Volume Object

A volume object contains a lot of aggregated values to consume.

Property             | Type      | Description
---------            | -----     | -----------
avg_bytes.value      | number    | Average number of bytes during window.
time                 | timestamp | Timestamp of the aggregated data point.
total_bytes.value    | number    | Total number of bytes flowing during window.
total_docs.value     | number    | Total number of records flowing during window.

All properties are __Read-Only__.

## Listener Volume

Volume for all data flowing into Ingest during a given time frame.

#### Definition

```http
GET https://listener-app-services.teradata.com/v1/sources/volume?interval,timeframe HTTP/1.1
```

Parameter   | Required | Type   | Sample   | Purpose
---------   | -------- | ----   | -------- | -------
`interval`  | Optional | string | `1m` | Time interval for each data point.
`timeframe` | Optional | string | `7d` | Time frame to query into the past.

Both parameters use a simple date string to denote a time range. They use an integer and character combination to denote the range. `s` = seconds, `m` = minutes, `h` = hours, `d` = days, `w` = weeks, `M` = months.

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -i \
  https://listener-app-services.teradata.com/v1/sources/volume
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
[
  {
    "avg_bytes": {
      "value": 99025
    },
    "time": "2015-05-04T17:11:00Z",
    "total_bytes": {
      "value": 321534487
    },
    "total_docs": {
      "value": 3247
    }
  }
]
```

#### Response Codes

Code | Meaning
---- | -------
200  | Metrics were loaded successfully.
401_STATUS







## Source Volume

Volume for all data flowing into Ingest for a single source during a given time frame.

#### Definition

```http
GET https://listener-app-services.teradata.com/v1/sources/{source_id}/volume?interval,timeframe HTTP/1.1
```

Parameter   | Required | Type   | Sample   | Purpose
---------   | -------- | ----   | -------- | -------
`source_id` | Required | string | `758fbda4-accc-4f90-8f09-cc0a164c8c28` | Time interval for each data point.
`interval`  | Optional | string | `1m` | Time interval for each data point.
`timeframe` | Optional | string | `7d` | Time frame to query into the past.

Both parameters use a simple date string to denote a time range. They use an integer and character combination to denote the range. `s` = seconds, `m` = minutes, `h` = hours, `d` = days, `w` = weeks, `M` = months.

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X PUT \
  -i \
  https://listener-app-services.teradata.com/v1/sources/758fbda4-accc-4f90-8f09-cc0a164c8c28/volume
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
[
  {
    "avg_bytes": {
      "value": 99025
    },
    "time": "2015-05-04T17:11:00Z",
    "total_bytes": {
      "value": 321534487
    },
    "total_docs": {
      "value": 3247
    }
  }
]
```

#### Response Codes

Code | Meaning
---- | -------
200  | Metrics were loaded successfully.
401_STATUS
404  | 404_STATUS
