## Queue Endpoint Subscription
CMQ can publish the message text of a topic and deliver it to the subscribed queue, so consumers can read it from the queue.

## HTTP Endpoint Subscription

### Delivery description
CMQ can push topic messages to the subscribed HTTP endpoint by sending POST requests. The message can be in JSON or SIMPLIFIED format.
- JSON format: the body of the pushed HTTP request contains the message body and attribute information. **The `Content-type` is `text/plain`.**
- SIMPLIFIED format: the body of the pushed HTTP request is the message body, while information such as `msgId` will be delivered to the subscriber in the HTTP request header.


If the HTTP service of the subscriber returns a standard 2xx response code (such as 200), the delivery succeeded; otherwise, the delivery failed, and the delivery retry policy has been triggered. If no response is returned after the timeout period elapses, CMQ will also consider the request as a failure and trigger the delivery retry policy. The detection timeout period is about 15 seconds.

### Header of HTTP delivery request
| Parameter Name | Description |
|---------|-------|
| x-cmq-request-id | `requestId` of the current push message |
| x-cmq-message-id | `msgId` of the current push message |
| x-cmq-message-tag | Tag of the current push message |

### Body of HTTP delivery request
The body of an HTTP request in JSON format contains the message body and attribute information.

| Parameter Name | Type | Description |
|---------|-------|-------|
| TopicOwner |String| `APPID` of the owner of the subscribed topic |
| topicName |String| Topic name |
| subscriptionName |String| Subscription name |
| msgId |String| Message ID |
| msgBody |String| Message body |
| publishTime |Int| Message published time |

The body of an HTTP request in SIMPLIFIED format is the message body published by the publisher.

### Response of HTTP delivery request
If a 2xx response code is returned, the HTTP service of the subscriber has normally processed the delivered message; if another response code is returned or no response is returned after the timeout period elapses, an error will be reported, and the delivery retry policy will be triggered.

### Sample request
In this sample, the subscribed HTTP endpoint is `http://test.com/cgi`.
JSON format:
```
POST /cgi HTTP/1.1
Host: test.com
Content-Length: 761
Content-Type: text/plain
User-Agent: Qcloud Notification Service Agent
x-cmq-request-id: 2394928734
x-cmq-message-id: 6942316962
x-cmq-message-tag: a, b

{"TopicOwner":100015036,"topicName":"MyTopic","subscriptionName":"mysubscription","msgId":"6942316962","msgBody":"test message","publishTime":11203432}
```

SIMPLIFIED format:
```
POST /cgi HTTP/1.1
Host: test.com
Content-Length: 123
Content-Type: text/plain
User-Agent: Qcloud Notification Service Agent
x-cmq-request-id: 2394928734
x-cmq-message-id: 6942316962
x-cmq-message-tag: a, b

test message
```

### Sample message subscription
The following is a message subscription demo, where all messages are delivered in the POST method; therefore, you only need to rewrite the `do_POST` method.   
This sample will print the received HTTP POST request content and deserialize `post data json` to traverse the printed request data.
```
#!/usr/bin/python
from BaseHTTPServer import HTTPServer, BaseHTTPRequestHandler
import json
class TestHTTPHandle(BaseHTTPRequestHandler):
    def do_POST(self):
		content_len = int(self.headers.getheader('content-length',0))
		post_body = self.rfile.read(content_len)
		print "receive cmq topic publisher request:"
		print self.headers
		print post_body
		post_data = json.loads(post_body)
		for k,v in post_data.iteritems():
				print "key:%s value:%s" % (k,v)
		#response http status 200 	
		self.send_response(200)
		self.end_headers()
		self.wfile.write('ok')
def start_server(port):
		http_server = HTTPServer(('0.0.0.0', int(port)),TestHTTPHandle)
		http_server.serve_forever()
if __name__ == '__main__':
		start_server(80)
```

