
Compose a cloud function to implement logic and provide API service via API gateway. API Gateway passes the request to the function in the form of parameter and forwards the response from function to the requester. For more information, please see__BLANK __

API Gateway triggers have the following characteristics:

- **Push model** : After API Gateway receives an API request, if the API is configured to connect with a function on the backend of the gateway, the function will be triggered for execution, and API Gateway will encapsulate information about the API request into input parameters of the request, including the specific service and API rule that receive the request, actual path and method of the request, and request parameters such as `path` , `header` And `query` , and send them to the triggered function in the form of event input parameters. 
   For more information about call types, see [Call Types](https://cloud.tencent.com/document/product/583/9694#.E8.B0.83.E7.94.A8.E7.B1.BB.E5.9E.8B) .

## API Gateway Trigger Configuration

API Gateway triggers can be configured in the **[SCF console](https://console.cloud.tencent.com/scf/index)** And the **[API Gateway console](https://console.cloud.tencent.com/apigateway/index)** .

- In **SCF console** , you can add API Gateway triggers, select existing or create new API services, and define the request methods (currently, six methods are supported, i.e., **"ANY", "GET", "HEAD", "POST", "PUT", and "DELETE"** ), environments (test, pre-release, and release environments), and authentication methods (API Gateway key pair).
- When configuring API rules in the **API Gateway console** , you can choose Cloud Function as the backend, and select functions in the same region as the API services.

When you configure the connection with SCF in API Gateway, you also need to configure the timeout. The request timeout in API Gateway and the execution timeout in SCF take effect respectively. The timeout rules are as follows:

* API Gateway timeout > SCF timeout: The SCF timeout takes effect first, the API request response is `200 http code` , but the return content is the error message of SCF timeout.
* API Gateway timeout < SCF timeout: The API Gateway timeout takes effect first, the API request response is `5xx http code` , which indicates that the request timed out.

## Limitation on API Gateway Trigger Binding

In API Gateway, one API rule can be bound to only one function, but one function can be bound to multiple API rules as the backend. At the same time, currently, API gateway triggers only support binding of Intra-region cloud functions. For example, cloud functions created in Guangzhou can only be bound and triggered by rules in API services created in Guangzhou. If you want to use an API Gateway configuration in a specific region to trigger a cloud function, you can create a function in the same region.

## Request and Response

Request method is the method to process request sent from API Gateway to SCF. And response method is the method to process the returned value sent from SCF to API Gateway.

### Integration Request and Passthrough Request

Integration request means that API Gateway converts the content of the HTTP request into request data structures which are passed to the function for handling as event input parameters of the function.

Passthrough request means that API Gateway passes the body content of the HTTP request to the function as event input parameters of the function. The passthrough request feature is still in the planning stage.

> Currently, when an API Gateway trigger triggers a function, integration request is always used.

<a id="datastructures"></a>

#### Event message structures of integration request for API Gateway trigger

When an API Gateway trigger receives a request, it sends the event data to the bound function in JSON format as shown below.

```
{
  "requestContext": {
    "serviceId": "service-f94sy04v",
    "path": "/test/{path}",
    "httpMethod": "POST",
    "requestId": "c6af9ac6-7b61-11e6-9a41-93e8deadbeef",
    "identity": {
      "secretId": "abdcdxxxxxxxsdfs"
    },
    "sourceIp": "10.0.2.14",
    "stage": "release"
  },
  "headers": {
    "Accept-Language": "en-US,en,cn",
    "Accept": "text/html,application/xml,application/json",
    "Host": "service-3ei3tii4-251000691.ap-guangzhou.apigateway.myqloud.com",
    "User-Agent": "User Agent String"
  },
  "body": "{\"test\":\"body\"}",
  "pathParameters": {
    "path": "value"
  },
  "queryStringParameters": {
    "foo": "bar"
  },
  "headerParameters":{
    "Refer": "10.0.2.14"
  },
  "stageVariables": {
    "stage": "release"
  },
  "path": "/test/value",
  "queryString": {
    "foo" : "bar",
    "bob" : "alice"
  },
  "httpMethod": "POST"
}
```

The data structures are detailed as below:

|Parameter Name|DESCRIPTION|
|-|-|
|Where: <li>`serviceId` , `path` , and `httpMethod` Are service ID, API path, and method of API Gateway; <li>`stage` Indicates the environment of the request source API; <li>`requestId` Identifies the unique ID of the current request; <li>`identity` Identifies the user's authentication method and information; <li>`sourceIp` Identifies the request source IP|Path|Full path information of the actual request|
|HttpMethod|HTTP method of the actual request|
|QueryString|Full query content of the actual request|
|Body|Record the content after the actual request is converted to a String string.|
|Headers|Full header content of the actual request|
|PathParameters|Path parameters configured in API Gateway and the actual values|
|QueryStringParameters|Query parameters configured in API Gateway and the actual values|
|HeaderParameters|Header parameters configured in API Gateway and the actual values|


> - During the iteration of the API gateway, more content may be added within the requestContext. Parameters in the data structure will be increased only rather than being deleted to avoid data corruption.
> - Parameters in the actual request may appear in multiple locations and can be selected based on your business needs.

### Integration Response and Passthrough Response

Integration response means that API Gateway parses the return content of the function and constructs an HTTP response based on the parsed content. By using the integrated response, the status code, headers, and body content of the response can be controlled independently by the code, and the content response in a custom format, such as response to XML, HTML, JSON, or even JS content, can be implemented. When using the integrated response, you need to follow the [Integrated response return data structure of API Gateway trigger](#apiStructure) Can be successfully parsed by the API gateway, otherwise it will appear `{"errno":403,"error":"Invalid scf response format. please check your scf response format."}` Error Info.

Passthrough response means that API Gateway directly passes the return content of the function to the API requester. Generally, the data format of this type of responses is fixed to JSON format, the status code is defined according to the status of function execution, and status code 200 is returned if the function is successfully executed. With passthrough response, you can obtain the JSON format and parse the structures at the call location to obtain the content in the structures.

> - If the API gateway trigger is currently configured through the API gateway console, the way to handle the response is pass through response by default. To enable the integrated response, please select the backend configuration location in the API configuration. **Enable integrated response** And return the content in the code according to the data structure described below
> - If the API Gateway trigger is configured through the SCF console, the integration response feature is enabled by default. Please pay attention to the format of return data.

<span id="apiStructure"></span>

#### Return data structures of integration response for API Gateway trigger

If integration response is set for API Gateway, data structures similar to the content below need to be returned.

```
{
    "isBase64Encoded": False,
    "statusCode": 200,
    "headers": {"Content-Type":"text/html"},
    "body": "<html><body><h1>Heading</h1><p>Paragraph.</p></body></html>"
}
```

The data structures are detailed as below:

|Parameter Name|DESCRIPTION|
|-|-|
|IsBase64Encoded|This indicates whether the content in the body is Base64-encoded binary. It should be `true` Or `false` In JSON format|
|StatusCode|HTTP return code. It should be an integer value|
|Headers|HTTP return header. It should contain multiple key-value objects.|
|Body|HTTP retun body|

<style>.params{margin-bottom:0px !important;}</style>



