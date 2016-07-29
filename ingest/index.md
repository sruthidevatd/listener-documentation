Teradata Listener Ingest API allows data to be sent to a Teradata Listener instance. This is the only way to stream data into Listener.

Ingest is a service that receives data and passes it off to Kafka for handling. Ingest is only in charge of accepting the data and ensuring it lands in Kafka for sorting and streaming to a target.

## Versions

* [Ingest REST API V1](v1/index.md)
  * [Sending a single message](v1/message.md)
  * [Sending multiple messages](v1/messages.md)
