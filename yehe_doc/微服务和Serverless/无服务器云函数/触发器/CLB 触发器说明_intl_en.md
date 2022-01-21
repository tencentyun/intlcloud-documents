You can implement backend web services by writing SCF functions and providing services through CLB, which will pass the request content as parameters to the function and return the result from the function back to the requester as the response.

Characteristics of CLB triggers:
- **Push model**
After a CLB trigger receives a request from CLB, if CLB is configured to connect with a function on the backend, the function will be triggered for execution, and CLB will send the information of the request as `event` input parameters to the triggered function, including the specific method how the request is received as well as the `path`, `header`, and `query` of the request.
- **Sync invocation**
A CLB trigger invokes functions synchronously. For more information on invocation types, please see [Invocation Types](https://intl.cloud.tencent.com/document/product/583/9694).

>?
- The CLB trigger feature is currently in beta test. You can click [here](https://intl.cloud.tencent.com/apply/p/z4oxc9h8ult) for trial application.
- CLB accounts are divided into standard accounts and traditional accounts. Traditional accounts cannot be bound to SCF. We recommend you upgrade them to standard accounts. 
>

## CLB Trigger Configuration

CLB triggers can be configured in either the **[SCF](https://console.cloud.tencent.com/scf/index)** or **[CLB](https://console.cloud.tencent.com/clb/index)** console.
<dx-tabs>
::: SCF console
In the **SCF console**, you can [add CLB triggers in trigger method](https://intl.cloud.tencent.com/document/product/583/31441), select existing CLB instances, create routing rules, and configure URL request paths.
:::
::: CLB console
When configuring routing rules in the **CLB console**, you can choose **Cloud Function** as the backend and select functions in the same region as the CLB instance. In the CLB console, you can also configure and manage advanced CLB capabilities, such as WAF protection, SNI multi-domain certificate, and ENI.
:::
</dx-tabs>



## CLB Trigger Binding Limits

- One CLB path rule can be bound to only one function, but one function can be bound to multiple CLB rules as the backend. Rules with the same path, listener, and host are regarded as the same rule and cannot be bound repeatedly.
- Currently, CLB triggers can only be bound to functions in the same region; for example, a function created in the Guangzhou region can only be bound to and triggered by CLB rules created in the Guangzhou region.


## Request and Response
Request method refers to the method to process request sent from CLB to SCF, and response method refers to the method to process the returned value sent from SCF to CLB. Both request and response methods are automatically processed by the CLB trigger. When it triggers the function, data structures must be returned in the request method.
>! `X-Vip`, `X-Vport`, `X-Uri`, `X-Method`, and `X-Real-Port` fields must be customized in the CLB console before they can be transferred. For custom configurations, see [Layer-7 Custom Configuration](https://intl.cloud.tencent.com/document/product/214/32427).


#### Event message structure of integration request for CLB trigger[](id:datastructures)
When a CLB trigger receives a request, event data will be sent to the bound function in JSON format as shown below.

>! In the CLB trigger scenario, all requests and responses need to be transferred in JSON. For images, files, and other data, as directly passing in JSON content will cause invisible characters to be lost, Base64 encoding is required as detailed below:
> - If the `Content-type` is `text/*`, `application/json`, `application/javascript`, or `application/xml`, CLB will not transcode the body content.
> - For all other types, CLB will Base64-encode them first and then forward them.


```
{  
  "headers": { 
    "Content-type": "application/json",  
    "Host": "test.clb-scf.com",  
    "User-Agent": "Chrome",  

    "X-Stgw-Time": "1591692977.774",  
    "X-Client-Proto": "http",  
    "X-Forwarded-Proto": "http",  
    "X-Client-Proto-Ver": "HTTP/1.1",  
    "X-Real-IP": "9.43.175.219",
    "X-Forwarded-For": "9.43.175.xx"  
 
    "X-Vip": "121.23.21.xx",  
    "X-Vport": "xx",  
    "X-Uri": "/scf_location",  
    "X-Method": "POST"    
    "X-Real-Port": "44347",  
  },  
  "payload": {  
    "key1": "123",  
    "key2": "abc"  
  },
}  
```

The data structures are as detailed below:

| Structure | Description |
| ---------- | --- |
| X-Stgw-Time | Request start timestamp |
| X-Forwarded-Proto | `scheme` structure of the request |
| X-Client-Proto-Ver | Protocol type |
| X-Real-IP | Client IP address |   
| X-Forward-For | Passed proxy IP address |
| X-Real-Port | Records the `Path` parameters configured in API Gateway and their actual values (optional custom configuration of CLB) |
| X-Vip | CLB VIP address (optional custom configuration of CLB) |
| X-Vport | CLB Vport (optional custom configuration of CLB) |
| X-Url | CLB request path (optional custom configuration of CLB) |
| X-Method | CLB request method (optional custom configuration of CLB) |

>! 
> - The content may be increased significantly during CLB iteration. At present, it is guaranteed that the content of the data structure will only be increased but not reduced, so that the existing structure will not be compromised.
> - Parameters in real requests may appear in multiple locations and can be selected based on your business needs.

### Integration response
Integration response means that CLB parses the returned content of the function and constructs an HTTP response based on the parsed content. With the aid of integration response, you can control the status code, headers, and body content of the response by using code and implement response to content in custom formats, such as XML, HTML, JSON, and even JS. When using integration response, data structures need to be returned in the [returned data structures of integration response for CLB trigger](#clbStructure) before they can be successfully parsed; otherwise, the error message `{"errno":403,"error":"Analyse scf response failed."}` will appear.


#### Returned data structures of integration response for CLB trigger[](id:clbStructure)
If integration response is set for CLB, data needs to be returned in the following structures:

```
{
    "isBase64Encoded": false,
    "statusCode": 200,
    "headers": {"Content-Type":"text/html"},
    "body": "<html><body><h1>Heading</h1><p>Paragraph.</p></body></html>"
}
```
The data structures are as detailed below:

| Structure | Description |
| ---------- | --- |
| isBase64Encoded | This indicates whether the content in the `body` is Base64-encoded binary. It should be `true` or `false` in JSON format. |
| statusCode | HTTP return code, which should be an integer value. |
| headers | HTTP return header, which should contain multiple `key-value` or `key:[value,value]` objects. Both key and value should be strings. |
| body | HTTP return body. |

If you need to return multiple headers with the same key, you can use a string array to describe different values; for example:
```
{
    "isBase64Encoded": false,
    "statusCode": 200,
    "headers": {"Content-Type":"text/html","Key":["value1","value2","value3"]},
    "body": "<html><body><h1>Heading</h1><p>Paragraph.</p></body></html>"
}
```

