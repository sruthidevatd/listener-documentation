## Curl Example
Replace <Stream Secret Key> with the stream Secret key for your stream.
Replace stg-example.com with your domain.
Replace <Stream-id> with the streamer id.

```bash
curl -i -N  -H "Connection: Upgrade" -H "Authorization: token <Stream Secret Key>" \
-H "Upgrade: websocket" -H "Host: listener-streamer-services-stg-example.com" \ 
-H "Origin: listener-streamer-services-stg-example.com" \
https://listener-streamer-services-stg-example.com/v1/streamer/<Stream-id>
```
