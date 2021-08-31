## Overview
This document describes how to create a microservice API in the API Gateway Console and configure the frontend and backend in detail.

## Directions
### Creating microservice API
1. Log in to the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=1).
2. In the service list, click the name of the target service to view it.
3. In the service details, click the **Manage API** tab and choose to create a **general API** or **microservice API** based on the backend business type. If your business is implemented in TSF, please select **Microservice API**.
4. Click **Create** for subsequent configuration.

### Frontend configuration
1. Enter the API name and select the cluster name and namespace of the microservice to which the frontend is connected.

2. Select the microservice. You can connect multiple microservices to one API.
Please make sure that the added services can be accessed by API Gateway, including microservices deployed by on CVM and TKE (for public network access and NodePort access).
>?Currently, API Gateway only supports forwarding requests to service instances of the same deployment type (virtual machine or container) in TSF. If there are microservice instances deployed on both virtual machines and containers under a service, API Gateway cannot be used as the request entry.
3. Enter the URL path (`Path`).
You can write a valid URL path as needed. If you need to configure a dynamic parameter in the path, please use `{}` to enclose the parameter name. For example, the `/user/{userid}` path declares the `userid` parameter in the path, which must be defined as a path-type input parameter. A query parameter does not need to be defined in the URL path.
4. Select the request method.
The request method is HTTP, and you can choose from GET, POST, PUT, DELETE, HEAD, and ANY.
5. Select the authentication type: no authentication or key pair.
6. Select whether to support CORS.
7. Enter the parameter configuration.

**Input parameters** include parameters from the header, query, and path, where a path parameter corresponds to a dynamic parameter defined in the URL path.
For any parameter, the parameter name, parameter type, and parameter data type must be specified, and whether it is required, its default value, sample data, and description can be specified optionally. With these configuration items, API Gateway helps you with documentation and preliminary verification of input parameters.
Two required parameters `X-NameSpace-Code` and `X-MicroService-Name` need to be passed in for the call. They control to which microservice the API Gateway request will be sent and can be placed in `Header`, `Path`, or `Query`. If in `Path`, just like for general APIs, you need to configure the path parameter in the path, such as `/{X-NameSpace-Code}/{X-MicroService-Name}`. If the variable `X-NameSpace-Code` is `crgt` and `X-MicroService-Name` is `coupon-activity`, then the access URL will be `https://access domain name/crgt/coupon-activity/`. Except these two fixed parameters, other parameters can be configured in the same way as for general APIs.
 - The `X-NameSpace-Code` path parameter is the code value configured in the [Tencent Service Framework](https://console.cloud.tencent.com/tsf/namespace) namespace of the namespace selected in the configuration.
 - The `X-MicroService-Name` path parameter is the microservice name configured in the [Tencent Service Framework](https://console.cloud.tencent.com/tsf/service) service management of the cluster selected in the configuration.

8. Click **Next** and configure the backend.

### Backend configuration
1. Configure the backend path.
This refers to the specific backend service request path. If you need to configure dynamic parameters in the path, please use the `{}` symbols to enclose the parameter name. This parameter name will be configured as the input parameter from the frontend configuration in the configuration mapped by the parameter. The path here can be different from the frontend for path mapping, which is the request path for real service.
2. Set the backend timeout period.
This refers to the timeout period of the backend service call initiated by API Gateway (up to 30 seconds). During a call, if there is no response after the timeout period elapses, API Gateway will terminate the call and return the corresponding error message.
3. Select the load balancing method.
4. Set session persistence.
5. Set the parameters.
 - Backend parameters: `X-NameSpace-Code` and `X-MicroService-Name` are fixed parameters and cannot be mapped. Other parameters configured by you can be mapped.
 If your `Body` parameter only has a form format, you can directly map the frontend and backend parameters when configuring them. If it is in JSON format, the JSON parameter will be directly passed through by API Gateway.
 - Mapped parameters: parameter mapping is used to map the input parameters from the frontend to the parameters of the actual backend service. By default, parameter mapping will map the input parameter by using the same name and parameter position. At the same time, you can change the parameter mapping method as needed. For example, you can map the input parameter from `Path` to the `Query` parameter in the backend service.
 - Constant parameters: you can add custom constant parameters as needed. They remain the same in each API call. In addition, you can use system parameters to pass certain required system information to the backend service.
6. Click **Next** and configure the response result.


### Response result

API response configuration includes the configuration of API response data and that of API error codes. Response result configuration is only used for document generation.
API response data configuration indicates the type of returned data, including data samples of successful and failed calls.
API error code definition indicates additional error code, error message, and description.



### Use instructions
To allow access to the backend microservice through API Gateway, you need to open the security group of the virtual machine where the service resides to the internet. You can set the source, protocol port, and access policy of the security group access.
When setting the access source, you need to at least open the IP ranges 9.0.0.0/8 and 100.64.0.0/10 where API Gateway resides. You can also open other sources as needed.
- For an application deployed on a virtual machine, the corresponding service port of the virtual machine must be opened. For an application deployed on a container, the service port of the virtual machine where the container resides instead of `NodePort` needs to be opened.
- For container applications, IP drifting often occurs; therefore, we recommend you open service ports that run on containers and need to be exposed externally on all machines in the cluster.

