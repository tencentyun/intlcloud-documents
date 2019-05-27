In the [How It Works](https://cloud.tencent.com/document/product/583/32553) document, it is mentioned that three types of SCF functions are required to sustain the interaction with API Gateway:
- Registration function: This function is triggered when a WebSocket connection is requested and established between the client and API Gateway, notifying SCF of the secConnectionID of the WebSocket connection. The secConnectionID is usually recorded in the persistent store in this function for reverse push of subsequent data.
- Cleanup function: This function is triggered when the client initiates a WebSocket disconnection request, notifying SCF to prepare to disconnect the secConnectionID. The secConnectionID is usually cleaned from the persistent store in this function.
- Transfer function: This function is triggered when the client sends data through the WebSocket connection, notifying SCF of the secConnectionID of the connection and the data sent. Business data is usually processed in this function. For example, it determines whether to push data to other secConnectionIDs in the persistent storage.

>! When you need to actively push data to a secConnectionID or disconnect a secConnectionID, the reverse push address of API Gateway has to be used.

This document uses Python2.7 as an example to illustrate how to write the main_handler for various functions and how to create and use API Gateway.

## Creating a Function

### Registration function

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf).
2. In the navigation pane on the left, select **[Functions](https://console.cloud.tencent.com/scf/list)** to enter the function management page.
3. Click **Create**, select "Blank function", and define a function name to create a function. For example, you can create a blank function named Register.
4. In the created Register blank function, select the "Function code" tab and copy the following code into the online editing box. You can keep the function code below as the default configuration.
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
>! In this function, you can add other business logics as needed. For example, you can save secConnectionID to TencentDB or create and associate a chat room.

### Transfer function

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf).
2. In the navigation pane on the left, select **[Functions](https://console.cloud.tencent.com/scf/list)** to enter the function management page.
3. Click **Create**, select "Blank function", and define a function name to create a function. For example, you can create a blank function named Transmission.
4. In the created Transmission blank function, select the "Function code" tab and copy the following code into the online editing box. You can keep the function code below as the default configuration.
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
> - In this function, you can add other business logics as needed. For example, you can forward the data obtained this time to another secConnectionID stored in TencentDB.
> - In the API details in API Gateway, you can get the reverse push address. For details, see [Configuring API Gateway](#ConfigureAPIGateway).

### Cleanup function

1. Log in to the [SCF console](https://console.cloud.tencent.com/scf).
2. In the navigation pane on the left, select **[Functions](https://console.cloud.tencent.com/scf/list)** to enter the function management page.
3. Click **Create**, select "Blank function", and define a function name to create a function. For example, you can create a blank function named Delete.
4. In the created Delete blank function, select the "Function code" tab and copy the following code into the online editing box. You can keep the function code below as the default configuration.
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
> - In this function, you can add other business logics as needed. For example, you can remove the disconnected secConnectionID this time from TencentDB or force the client of a secConnectionID to go offline.
> - In the API details in API Gateway, you can get the reverse push address. For details, see [Configuring API Gateway](#ConfigureAPIGateway).

<span id="ConfigureAPIGateway"></span>
## Configuring API Gateway

### Create an API

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=8).
2. Select the same region as SCF and click **Create** to create a service.
3. Click **API configuration** to enter the "API management" page.
4. Click **Create** to enter the "Create an API" page.
5. In "Frontend configuration", set the "Frontend type" to "WEBSOCKET", and enter the "Path" and "Authentication type" based on your actual needs. See the figure below:
![](https://main.qcloudimg.com/raw/255e351bf7926e1a984e2735877bbb80.png)
6. Click **Next**.
7. In "Backend configuration", set the "Backend type" to "cloud function", and set parameters such as "Transfer function", "Registration function" and "Cleanup function" based on your actual needs. See the figure below:
>! 
> - Backend timeout: After the client establishes a WebSocket connection, if there is no message sent, the connect will be closed by API Gateway after the timeout elapses.
> - Integration response (not recommended): If Integration response is selected, the return value of SCF needs to be returned in the agreed upon JSON data structure.

 ![](https://main.qcloudimg.com/raw/ed7baa101cbd407f6d046b51a9ebb57b.png)

8. Complete the subsequent steps as prompted.

### Release a service

1. Switch to the **Service information** tab and click **Release**. See the figure below:
![](https://main.qcloudimg.com/raw/25cac411f73a735e481d31f965666e6d.png)
2. In the **Release a service** window that pops up, select "Release environment" and click **Submit**.
3. Click **OK**.
4. Switch to the **API management** tab, and click the API ID/name to view the API details and the reverse push address of WebSocket. See the figure below:
![](https://main.qcloudimg.com/raw/8a5f79013046f66eba25aa10fc7f7986.png)
>! The push address will be used when the server actively sends a message to the client or disconnects from the client.


### Get the WebSocket connection address

Switch to the **Environment management** tab to view the API service address. See the figure below:
![](https://main.qcloudimg.com/raw/48b5e37072da95df2238ec3cd2eec504.png)
Based on the service address, it can be inferred that the API address of WebSocket is: "ws://service-0sua8j6z-1256608914.ap-beijing.apigateway.myqcloud.com/release/websocket"
>! The API address of WebSocket needs to have the path "/websocket" of the API in it.
