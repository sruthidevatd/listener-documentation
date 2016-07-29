Teradata Listener Ingest API allows data to be sent to a Teradata Listener instance. This is the only way to stream data into Listener.

Ingest is a service that receives data and passes it off to Kafka for handling. Ingest is only in charge of accepting the data and ensuring it lands in Kafka for sorting and streaming to a target.

## Base URL

The Ingest API has its own hostname, which varies across Listener installations. It is customized during the installation of Listener, and set by the administrator. Typically, it follows this format:

    https://listener-ingest-services.YOURCOMPANY.DOMAIN/v1/

Ask your administrator for the proper domain for your installation.

## Versioning

The API is versioned and it is recommended that you use `/v1/` in the path to denote the specific version to use. If you do not use the version path, then it will default to the most recent version of the API.

When breaking changes are made to the API, they are released as a new version. Using a specific version should prevent errors in your applications from changes to the API.

## Authorization
To publish data, a source must be registered with the Teradata Listener. This can be accomplished through the Listener REST API or through the application interface. Once a source is registered, a key is generated and then used in an **Authorization** header for all requests sending data to the Ingest API.

The **Authorization** header currently supports only type **_token_** and is followed by the registered source's API key. For example, if the registered source's API key is `87c3c7bb-045f-4f9d-a3a6-ba7c036ef70a`, the header would appear as follows:

```http
Authorization: token 87c3c7bb-045f-4f9d-a3a6-ba7c036ef70a
```

## Message Size Limits
Listener **accepts up to 1 MB of data for a single message**. It is possible to send multiple messages where the total size of each individual message exceeding 1 MB. However, the Ingest API is used in priority over HTTP; therefore, if the connection is dropped, the entire request will fail regardless of the size of the data. In addition, performance of streaming data through Listener will decrease with large messages; therefore, we recommend sending messages in the smallest size possible

If you attempt to send more than 1 MB in a single data packet, the packet will be rejected. If you do not use the Sync header to ensure the packet is ingested properly, you will still get a successful API response. Because ingest is asynchronous by default, you can trust that the API response means that only the data was received, not properly ingested. There are logs that indicate if the pipeline was unable to accept the packet due to size limits.

Listener is a real time streaming system and as such it does not support batch loading files; it requires data be sent through the Ingest API.

## Media Types

This API uses the [JSON](http://www.json.org) Media-Type to transport data in all responses. It also supports JSON for all requests.

Data sent to Ingest can be in any data format. When sending a single message, Ingest does not attempt to parse or transform the data. When sending multiple messages at once, you can request it be split into multiple messages using a custom delimiter or by sending a JSON array that will be parsed and split into individual messages.

## Confirmation of Receipt

By default, any data sent to Ingest is handled asynchronously. Every data packet is given a UUID when it is handed off to the router; however, to ensure speed of the Ingest API, UUIDs are not sent back. There is additional latency required to capture the UUID and return it during the response.

If the client requires a response with UUIDs to track messages through Listener and into its storage target, you must send a **Sync** header with value **1** with the request. This will lengthen the time the request to Ingest runs due to wait time for UUID confirmations.

```
Sync: 1
```

If the **Sync** header is not sent or is not set to **1**, no response body will be sent back to the client.
