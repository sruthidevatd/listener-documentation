This endpoint is designed to accept a single message and pass it through Listener. No transformation or splitting of the message occurs. Call this endpoint each time you want to send a single message.

### Definition

```http
POST https://listener-ingest-services.teradata.com/v1/message HTTP/1.1
Authorization: token SOURCE_SECRET_KEY
Content-Type: application/json
Sync: 1
```

Header        | Required | Sample Value      | Purpose
------        | -------- | ------------      | -------
Authorization | Required | Source Secret Key | Source secret key that determines to which source the data is sent.
Sync          | Optional | `1`               | Request a UUID from Ingest to ensure Kafka accepted the message. Value must be 1, or will be treated as async.


### Example Request

```bash
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: token 0f6fd50e-9515-4730-92c0-2360b5af56d3" \
  -H "Sync: 1" \
  -X POST -d '{"testing":"123"}' \
  -i \
  https://listener-ingest-services.teradata.com/v1/message
```

### Example Response

```http
HTTP/1.1 201 Created
Content-Type: application/json
```
```json
{"uuid":"15183245f6e0242ac11000000"}
```

### Response Codes

Code | Meaning
---- | -------
201  | Message was successfully received.
401_STATUS
500  | Message body could not be read or Kafka could not be reached.
