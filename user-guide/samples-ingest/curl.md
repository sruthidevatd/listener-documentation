You can use cURL from the terminal to make an HTTP request to the Ingest API. The following example will POST a single JSON message to the source and display the response headers.

```
curl \
  -H "Content-Type: application/json" \
  -H "Authorization: token 7836e0e6-2937-4ff9-9463-eff988e02de2" \
  -X POST -d '{"testing":"123"}' \
  -i \
  https://listener-ingest-services-demo.ln.uda.io/message ```
