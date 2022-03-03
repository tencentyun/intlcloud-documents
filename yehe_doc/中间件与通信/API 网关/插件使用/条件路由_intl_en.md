
## Overview

The conditional routing plugin can forward different client requests to different backend addresses based on the request and system parameter values. It is widely used in scenarios such as grayscale release, blue-green deployment, and tenant routing.

## Directions

### Step 1. Create a plugin

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway)
2. On the left sidebar, click **Plugin** to enter the plugin list page.
3. Click **Create** in the top-left corner of the page and select **Conditional Routing** as the plugin type to create a conditional routing plugin.
   You can create up to 10 routing policies in a conditional routing plugin and need to enter the following content in each policy:

| Parameter | Required | Description |
| -------- | -------- | ------------------------------------------------------------ |
| Policy name     | Yes     | Current policy name, which can contain up to 50 characters and must be unique in the same plugin. |
| Weight         | Yes     | Priority for policy match. You can enter a positive integer between 0 and 100. If it is not set, it will be 0 by default.</br>The greater the weight, the higher the match priority. For policies with the same weight, the later the creation time, the higher the priority. |
| Trigger condition | Yes     | Conditional expression that judges whether the client request meets the condition. For more information, see the relevant description below. |
| Backend type | Yes     | Public network URL/IP, VPC resources, SCF, Mock, and TSF are supported.  |
| Backend configuration | Yes     | Backend to which the client request will be forwarded if the request meets the condition. Enter the backend configuration in YAML format. |

![](https://main.qcloudimg.com/raw/e961c1531b24f9da006e3b9981ffb507.png)

### Step 2. Bind an API and make the plugin effective

1. Select the just created plugin in the list and click **Bind API** in the **Operation** column.
2. In the **Bind API** pop-up window, select the service, environment, and the API to which the plugin needs to be bound.
   ![](https://main.qcloudimg.com/raw/d7fd3c3539d6f623f45ebfdf0674d97e.png)
3. Click **OK** to bind the plugin to the API. At this time, the configuration of the plugin has taken effect for the API.

## Conditional Expression Writing Guide

### Parameter description

A conditional expression supports the following two types of parameters:

- **Request parameter in a certain location**: currently, only `Header`, `Path`, and `Query` parameters are supported.
   - If the `a` parameter in the `Header` location is configured in the frontend configuration, you can use `header.a` to represent this parameter in the plugin.
   - The `Path` parameter has no parameter name and is therefore represented by a path; for example, `path='/test'` indicates that the condition is met if the request path is `/test`.
   - The value definition of the `Path` parameter must start with `/`, such as `'/test'`.
   
- You can **use `sysparam` to reference system parameters of the current request** without defining them in the API; however, if you define a parameter with the same name in the API, the value in the API will be overwritten by the value of the custom parameter. We recommend you enter the parameter value in lower camel case and make it case-insensitive. The following system parameters can be used in the routing plugin:
   - sysparam.clientIp: client IP.
   - sysparam.httpScheme: request protocol, which is HTTP or HTTPS.
   - sysparam.clientUa: `UserAgent` field uploaded by the client.

>?The parameter location is case-insensitive, while the parameter name is case-sensitive; for example, in the above `header.a` parameter, the parameter location `header` is case-insensitive, while the parameter name `a` is case-sensitive.

A conditional expression supports the following constant types:


| Constant Type | Description | Example |
|---------|---------|---------|
| STRING | String | Double and single quotation marks are supported, such as "Hello" and 'hello' |
| INTEGER | Integer | 1001, -1 |
| NUMBER | Floating point | 0.1, 100.0 | 
| BOOLEAN | Boolean | true, false |

### Writing rules

- You can use `and` and `or` to concatenate different expressions.
- You can use parentheses `()` to specify the priority for condition match.
- As a built-in function, `Random()` can generate a floating point parameter where the value is in `NUMBER` data type and ranges from 0 to 1 for random judgment.
- If a nonexistent parameter such as `param.unknown = 1` is used in the expression, `false` will be returned.
- You can use the regular expression function `regex()` to match the parameter value, for example, `regex(query.name,"colou?r")`. You need to enclose the string in the regular expression with single or double quotation marks.
- You can use the `exists()` function to specify whether a parameter exists, for example, `exists(header.Accept)`.
- Both `==` and `=` can be used to judge the "equal to" relationship.

### Sample conditional expressions

- The result is true with a probability of 5%:
  **Random() < 0.05**
- `UserName` in the custom `Header` parameter is `Admin`, and the source IP is 47.47.74.77:
  **header.UserName = 'Admin' and sysparam.clientIp = '47.47.74.77'**
- The user ID (a parameter in `Header`) of the current request is `1001`, `1098`, or `2011`, and the request uses the HTTPS protocol:
  **sysparam.httpScheme = 'https' and (header.id = 1001 or header.id = 1098 or header.id = 2011)**

## Backend Configuration Writing Guide

You can enter the configuration of the backend connected to public network URL/IP, VPC resources, SCF, Mock, and TSF:

- The backend configuration must be in the YAML format.
- The fields in the backend configuration are in one to one correspondence to the fields in the [CreateApi](https://intl.cloud.tencent.com/document/product/628/36661) API.
- The conditional routing plugin creation page lists the demo configuration code for each type of backend. You can configure the backend simply by modifying the parameter values.

### Backend connection to public network URL/IP

```yml
ServiceConfig:
  Method: GET
  Path: /test
  Url: 'http://test.com'
ServiceType: HTTP
```

### Backend connection to VPC resources

```yml
ServiceConfig:
  Method: GET
  Path: /test
  Url: 'http://test.com'
  UniqVpcId: vpc-xxxxx
  Product: clb
ServiceType: HTTP
```

### Backend connection to SCF

```yml
ServiceScfFunctionName: scftest
ServiceScfFunctionNamespace: mynamespace
ServiceScfFunctionQualifier: $DEFAULT
ServiceScfFunctionType: EVENT
ServiceScfIsIntegratedResponse: false
ServiceType: SCF
```

### Backend connection to Mock

```yml
ServiceMockReturnMessage: hello mock from strategy
ServiceType: MOCK
```

### Backend connection to TSF

```yml
X-MicroService-Name: consumer-demo
X-NameSpace-Code: mytsf
MicroServices:
  - ClusterId: cls-xxxxxx
    MicroServiceName: tsf-demo
    NamespaceId: namespace-xxxxxx
ServiceConfig:
  Method: ANY
  Path: /xxxx
  Url: ''
ServiceTsfHealthCheckConf:
  IsHealthCheck: true
ServiceTsfLoadBalanceConf:
  IsLoadBalance: true
  Method: RoundRobinRule
  SessionStickRequired: false
ServiceType: TSF
```

## pluginData

```json
[
    {
        "strategy_name":"route-to-http", // Policy name, which can contain up to 50 letters, digits, and special symbols (%~_\-.{}?&=) and must be unique in the same plugin
        "strategy_weight":2, // Priority for policy match. You can enter a positive integer between 0 and 100. If it is not set, it will be 0 by default
        "condition":"query.age<30 and query.need_verify=false or query.level>3", // Conditional expression
        "backend_type":"HTTP", // Type of the backend for routing and forwarding. Valid values: MOCK, HTTP, SCF, VPC, UPSTREAM, TSF
        "backend_config":{  // Backend configuration
            "ServiceConfig":{
                "Method":"GET",
                "Path":"/v1/bpi/currentprice.json",
                "Url":"https://api.coindesk.com"
            },
            "ServiceType":"HTTP"
        }
    }
]
```


## Notes

If a request cannot match a routing policy configured in the conditional routing plugin bound to an API, it will be forwarded to the default API backend.
