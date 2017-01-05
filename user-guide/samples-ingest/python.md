You can use Python to make an HTTP request to the Ingest API. The following example uses the requests package to create a POST request that sends a single JSON message to the source and prints the response object.

```
import urllib2

req = urllib2.Request("https://listener-ingest-services-demo.ln.uda.io/message", data='''{"testing": "123"}''', headers={"Authorization": "token 7836e0e6-2937-4ff9-9463-eff988e02de2"})
f = urllib2.urlopen(req) ```