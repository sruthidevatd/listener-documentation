Latency is the measurement of time it takes for a message to flow through a segment of the Listener application. Due to the asynchronous nature of Listener, you cannot track a single message through the entire application with certainty; however, you can use it to determine the latency for data flowing in general for all of Listener or a specific source or target.

* [Latency object](#latency-object)
* [Router latency](#listener-latency)
* [Source latency](#source-latency)
* [Target latency](#target-latency)

## Latency object

A latency object contains a lot of aggregated values for you to consume.

Property             | Type      | Description
--------             |-----      | -----------
router_latency_stats | object    | Object containing router latency stats.
time                 | timestamp | Timestamp of the aggregated data point.
total_latency_stats  | boolean   | Object containing combined router and writer latency stats.
writer_latency_stats | boolean   | Object containing writer latency stats.

All properties are __Read-Only__.

## Router latency

Latency for all data from the time it is received by Kafka until the time it takes for the router to sort it into the correct stream. Latency values are returned in microsecond values; therefore, if you want to get the value in seconds, you must multiply by 1,000,000.

> Tip: Due to the aggregation, this is useful for obtaining a sense of how well Listener is handling the routing of data into individual streams.

#### Definition

```http
GET https://listener-app-services.teradata.com/v1/sources/latency?interval,timeframe HTTP/1.1
```

Parameter   | Required | Type   | Sample   | Purpose
---------   | -------- | ----   | -------- | -------
`interval`  | Optional | string | `1m` | Time interval for each data point.
`timeframe` | Optional | string | `7d` | Time frame to query into the past.

Both parameters use a simple date string to denote a time range. It uses an integer and character combination to denote the range. `s` = seconds, `m` = minutes, `h` = hours, `d` = days, `w` = weeks, `M` = months.

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X PUT \
  -i \
  https://listener-app-services.teradata.com/v1/sources/latency
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
[
  {
    "doc_count": 375,
    "router_latency_stats": {
      "avg": 2982.816,
      "count": 375,
      "max": 13953,
      "min": 418,
      "std_deviation": 6946.194437878245,
      "std_deviation_bounds": {
        "lower": -10909.57287575649,
        "upper": 16875.204875756488
      },
      "sum": 1118556,
      "sum_of_squares": 21430053172,
      "variance": 48249617.168810666
    },
    "time": "2015-12-11T21:13:00Z",
    "total_latency_stats": {
      "avg": null,
      "count": 0,
      "max": null,
      "min": null,
      "std_deviation": null,
      "std_deviation_bounds": {
        "lower": null,
        "upper": null
      },
      "sum": null,
      "sum_of_squares": null,
      "variance": null
    },
    "writer_latency_stats": {
      "avg": null,
      "count": 0,
      "max": null,
      "min": null,
      "std_deviation": null,
      "std_deviation_bounds": {
        "lower": null,
        "upper": null
      },
      "sum": null,
      "sum_of_squares": null,
      "variance": null
    }
  }
]
```

#### Response Codes

Code | Meaning
---- | -------
201  | Metrics were loaded successfully.
401  | The Authorization header was missing, or could not be found.







## Source latency

Latency for all data from the time it is received by Kafka until the time it takes for the router to sort it into the specified stream. Latency values are returned in microsecond values; therefore, if you want to get the value in seconds, you must multiply by 1,000,000.

#### Definition

```http
GET https://listener-app-services.teradata.com/v1/sources/{source_id}/latency?interval,timeframe HTTP/1.1
```

Parameter   | Required | Type   | Sample   | Purpose
---------   | -------- | ----   | -------- | -------
`source_id` | Required | string | `758fbda4-accc-4f90-8f09-cc0a164c8c28` | Time interval for each data point.
`interval`  | Optional | string | `1m` | Time interval for each data point.
`timeframe` | Optional | string | `7d` | Time frame to query into the past.

Both parameters use a simple date string to denote a time range. It uses an integer and character combination to denote the range. `s` = seconds, `m` = minutes, `h` = hours, `d` = days, `w` = weeks, `M` = months.

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X PUT \
  -i \
  https://listener-app-services.teradata.com/v1/sources/758fbda4-accc-4f90-8f09-cc0a164c8c28/latency
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
[
  {
    "doc_count": 375,
    "router_latency_stats": {
      "avg": 2982.816,
      "count": 375,
      "max": 13953,
      "min": 418,
      "std_deviation": 6946.194437878245,
      "std_deviation_bounds": {
        "lower": -10909.57287575649,
        "upper": 16875.204875756488
      },
      "sum": 1118556,
      "sum_of_squares": 21430053172,
      "variance": 48249617.168810666
    },
    "time": "2015-12-11T21:13:00Z",
    "total_latency_stats": {
      "avg": null,
      "count": 0,
      "max": null,
      "min": null,
      "std_deviation": null,
      "std_deviation_bounds": {
        "lower": null,
        "upper": null
      },
      "sum": null,
      "sum_of_squares": null,
      "variance": null
    },
    "writer_latency_stats": {
      "avg": null,
      "count": 0,
      "max": null,
      "min": null,
      "std_deviation": null,
      "std_deviation_bounds": {
        "lower": null,
        "upper": null
      },
      "sum": null,
      "sum_of_squares": null,
      "variance": null
    }
  }
]
```

#### Response Codes

Code | Meaning
---- | -------
201  | Metrics were loaded successfully.
401  | The Authorization header was missing, or could not be found.
404  | 404_STATUS







## Target latency

Latency for all data flowing from the time a piece of data is ingested into Listener until the time it is written to a target. Latency values are returned in millisecond values; therefore, if you want to get the value in seconds you must multiply by 1,000.

#### Definition

```http
GET https://listener-app-services.teradata.com/v1/targets/{target_id}/latency?interval,timeframe HTTP/1.1
```

Parameter   | Required | Type   | Sample   | Purpose
---------   | -------- | ----   | -------- | -------
`target_id` | Required | string | `758fbda4-accc-4f90-8f09-cc0a164c8c28` | Time interval for each data point.
`interval`  | Optional | string | `1m` | Time interval for each data point.
`timeframe` | Optional | string | `7d` | Time frame to query into the past.

Both parameters use a simple date string to denote a time range. It uses an integer and character combination to denote the range. `s` = seconds, `m` = minutes, `h` = hours, `d` = days, `w` = weeks, `M` = months.

#### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer TOKEN" \
  -X PUT \
  -i \
  https://listener-app-services.teradata.com/v1/targets/758fbda4-accc-4f90-8f09-cc0a164c8c28/latency
```

#### Example Response

```http
HTTP/1.1 200 OK
Content-Type: application/json
```
```json
[
  {
    "doc_count": 375,
    "latency": {
      "avg": 2982.816,
      "count": 375,
      "max": 13953,
      "min": -7418,
      "std_deviation": 6946.194437878245,
      "std_deviation_bounds": {
        "lower": -10909.57287575649,
        "upper": 16875.204875756488
      },
      "sum": 1118556,
      "sum_of_squares": 21430053172,
      "variance": 48249617.168810666
    },
    "time": "2015-12-11T21:13:00Z"
  }
]
```

#### Response Codes

Code | Meaning
---- | -------
201  | Metrics were loaded successfully.
401  | The Authorization header was missing, or could not be found.
404  | 404_STATUS
