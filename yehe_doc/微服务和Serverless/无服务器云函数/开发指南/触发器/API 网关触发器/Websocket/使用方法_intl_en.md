In the [How It Works](https://intl.cloud.tencent.com/document/product/583/31437) document, it is mentioned that three types of SCF functions are required to sustain the interaction with API Gateway:
- Registration function: this function is triggered when a WebSocket connection is requested and established between the client and API Gateway, notifying SCF of the `secConnectionID` of the WebSocket connection. The `secConnectionID` is usually recorded in the persistent storage in this function for reverse push of subsequent data.
- Cleanup function: this function is triggered when the client initiates a WebSocket disconnection request, notifying SCF to prepare to disconnect the `secConnectionID`. The `secConnectionID` is usually cleaned from the persistent storage in this function.
- Transfer function: this function is triggered when the client sends data through the WebSocket connection, notifying SCF of the `secConnectionID` of the connection and the data sent. Business data is usually processed in this function. For example, it determines whether to push data to other `secConnectionID` values in the persistent storage.

>! When you need to actively push data to a `secConnectionID` or disconnect a `secConnectionID`, the reverse push address of API Gateway has to be used.

This document uses Python 2.7 as an example to describe how to write the `main_handler` for various functions.

## Sample Function Code

### Registration function
```
# -*- coding: utf8 -*-
import json
import requests
def main_handler(event, context):
    print('Start Register function')
    print("event is %s"%event)
    retmsg = {}
    global connectionID
    if 'requestContext' not in event.keys():
        return {"errNo":101, "errMsg":"not found request context"}
    if 'websocket' not in event.keys():
        return {"errNo":102, "errMsg":"not found websocket"}
    connectionID = event['websocket']['secConnectionID']
    retmsg['errNo'] = 0
    retmsg['errMsg'] = "ok" 
    retmsg['websocket'] = {
            "action":"connecting",
            "secConnectionID":connectionID
        }
    if "secWebSocketProtocol" in event['websocket'].keys():
        retmsg['websocket']['secWebSocketProtocol'] = event['websocket']['secWebSocketProtocol']
    if "secWebSocketExtensions" in event['websocket'].keys():
        ext = event['websocket']['secWebSocketExtensions']
        retext = []
        exts = ext.split(";")
        print(exts)
        for e in exts:
            e = e.strip(" ")
            if e == "permessage-deflate":
                #retext.append(e)
                pass
            if e == "client_max_window_bits":
                #retext.append(e+"=15")
                pass
        retmsg['websocket']['secWebSocketExtensions'] = ";".join(retext)
    print("connecting \n connection id:%s"%event['websocket']['secConnectionID'])
    print(retmsg)
    return retmsg
```
>! In this function, you can add other business logic as needed. For example, you can save `secConnectionID` to TencentDB or create and associate a chat room.

### Transfer function
```
# -*- coding: utf8 -*-
import json
import requests
g_connectionID = 'xxxx'  # Forward the message to a specific WebSocket connection
sendbackHost = "http://set-7og8wn64.cb-beijing.apigateway.tencentyun.com/api-xxxx" # API Gateway's reverse push address, which can be obtained after the API is created in the next step
# Actively push the message to the client
def send(connectionID,data):
    retmsg = {}
    retmsg['websocket'] = {}
    retmsg['websocket']['action'] = "data send"
    retmsg['websocket']['secConnectionID'] = connectionID
    retmsg['websocket']['dataType'] = 'text'
    retmsg['websocket']['data'] = json.dumps(data)
    print("send msg is %s"%retmsg)
    r = requests.post(sendbackHost, json=retmsg)   
def main_handler(event, context):
    print('Start Transmission function')
    print("event is %s"%event)
    if 'websocket' not in event.keys():
        return {"errNo":102, "errMsg":"not found web socket"}
    for k in event['websocket'].keys():
        print(k+":"+event['websocket'][k])
    # Send the content to a specific client
    #connectionID = event['websocket']['secConnectionID']
    data = event['websocket']['data']
    send(g_connectionID,data)
    return event
```
>! 
> - In this function, you can add other business logic as needed. For example, you can forward the data obtained in this request to another `secConnectionID` stored in TencentDB.
> - In the API details in API Gateway, you can get the reverse push address.

### Cleanup function
```
import json
import requests
g_connectionID = 'xxxx'  # Forward the message to a specific WebSocket connection
sendbackHost = "http://set-7og8wn64.cb-beijing.apigateway.tencentyun.com/api-xxxx" # API Gateway's reverse push address, which can be obtained after the API is created in the next step
# Actively send disconnection information
def close(connectionID):
    retmsg = {}
    retmsg['websocket'] = {}
    retmsg['websocket']['action'] = "closing"
    retmsg['websocket']['secConnectionID'] = connectionID
    r = requests.post(sendbackHost, json=retmsg)
    return retmsg
def main_handler(event, context):
    print('Start Delete function')
    print("event is %s"%event)
    if 'websocket' not in event.keys():
        return {"errNo":102, "errMsg":"not found web socket"}
    for k in event['websocket'].keys():
        print(k+":"+event['websocket'][k])        
    #close(g_connectionID)
    return event
```
>! 
> - In this function, you can add other business logic as needed. For example, you can remove the `secConnectionID` disconnected in this request from TencentDB or force the client of a `secConnectionID` to go offline.



