Currently, HTTP-triggered functions only support **API Gateway triggers**. You can bind API Gateway triggers in the [SCF console](https://console.cloud.tencent.com/scf) or bind backend functions in the [API Gateway console](https://console.cloud.tencent.com/apigateway).

### Trigger Type Description
For HTTP-triggered functions, triggers support two creation methods: **default creation** and **custom creation**. You can choose an appropriate method according to the actual situation:

|| Default Creation (Basic API Gateway) | Custom Creation (Standard API Gateway) |
|------|--------|--------|
| Default domain name | Supported | Supported |
| Binding to custom domain name | Manual binding | Management in API Gateway console |
| Request method configuration | Supported | Supported |
| Release environment configuration | Supported | Supported |
| Authentication method configuration | Supported | Supported |
| Visibility in API Gateway console | Invisible | Visible |
| Advanced API Gateway capabilities (such as plugin and dedicated instance) | Not supported | Supported |
| Billing method | Gateway calls are not billed. | It is billed by standard API Gateway billable items. |
| Type conversion | The gateway can be upgraded to a standard API Gateway instance. After upgrade, you can use all gateway capabilities and billed by standard API Gateway billable items. | The gateway edition cannot be changed. A standard API Gateway instance cannot be rolled back to a basic API Gateway instance in default creation. |



### Trigger Overview
Characteristics of HTTP API Gateway triggers:
- **Passthrough HTTP request**
After API Gateway receives an HTTP request, if the API Gateway backend is connected with an SCF function, the function will be triggered. At this time, API Gateway will directly pass through the HTTP request, without performing `event` type format conversion. HTTP request information includes the specific service that receives the request, API rule, actual request path, method, and `path`, `header`, and `query` of the request.
- **Sync invocation**
API Gateway invokes the function synchronously, and it will wait for the function to return before the timeout period configured in it elapses. For more information on invocation types, see [Invocation Types](https://intl.cloud.tencent.com/document/product/583/9694).

### Trigger Configuration
Basic gateways can only be bound in the default creation method in the SCF console.

API Gateway triggers can be configured in the **[SCF console](https://console.cloud.tencent.com/scf/index)** or the **[API Gateway console](https://console.cloud.tencent.com/apigateway/index)**. For more information on trigger configuration, see [Overview](https://intl.cloud.tencent.com/document/product/583/12513).


### Trigger Binding Limits

In API Gateway, one API rule can be bound to only one function, but one function can be bound to multiple API rules as the backend. You can create an API with different paths in the [API Gateway console](https://console.cloud.tencent.com/apigateway/index) and point the backend to the same function. APIs with the same path, same request method, and different release environments are regarded as the same API and cannot be bound repeatedly.


### Request and Response
Request method is the method to process request sent from API Gateway to SCF, and response method is the method to process the returned value sent from SCF to API Gateway. For HTTP-triggered functions, API Gateway will add the information required for function triggering in the `header` and directly pass through the original request to trigger the backend function.

>!The following parameters don't support custom configuration:
- `connection` field
- Custom fields starting with `X-SCF-`

