You can use Java to make an HTTP request to the Ingest API. The following example uses the HttpClient package to create a POST request that sends a single JSON message to the source and prints the response object.

```
StringEntity body = new StringEntity("{\"testing\": \"123\"}");
HttpPost postReq = new HttpPost("https://listener-ingest-services-demo.ln.uda.io/message");
postReq.addHeader("Authorization", "token " + 7836e0e6-2937-4ff9-9463-eff988e02de2);
postReq.setEntity(body);

HttpClient client = new DefaultHttpClient();
HttpResponse resp = client.execute(postReq); ```