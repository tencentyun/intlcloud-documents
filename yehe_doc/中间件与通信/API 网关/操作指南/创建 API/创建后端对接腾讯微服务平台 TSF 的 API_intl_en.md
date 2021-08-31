## Overview

This document describes how to create an API connecting to the TSF in the backend through the API Gateway console.


## Prerequisites
You have [created a service](https://intl.cloud.tencent.com/document/product/628/11787).


## Directions
### Step 1. Create a microservice API

1. Log in to the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1).
2. In the service list, click the name of the target service to view it.
3. In the service details, click the **Manage API** tab and choose to create a **General API** or **Microservice API** based on the backend business type. If your business is implemented in TSF, select **Microservice API**.
4. Click **Create** for subsequent configuration.

### Step 2. Perform frontend configuration

1. Enter the API name.
2. Enter the URL path.
   You can write a valid URL path as needed. If you need to configure a dynamic parameter in the path, use `{}` to enclose the parameter name. For example, the `/user/{userid}` path declares the `userid` parameter in the path, which must be defined as a path-type input parameter. A query parameter does not need to be defined in the URL path.
3. Select the request method.
   The request method is HTTP method. You can choose from GET, POST, PUT, DELETE, HEAD, and ANY.
4. Select the authentication type: no authentication or key pair.
5. Select whether to support CORS.
6. Enter the parameter configuration.
   ![](https://main.qcloudimg.com/raw/3ae7a13c209b91c240b8e468732b5702.png)
   **Input parameters** include parameters from the header, query, and path locations, where a path parameter corresponds to a dynamic parameter defined in the URL path.
   For any parameter, the parameter name, parameter type, and parameter data type must be specified. Whether a parameter is required and its default value, sample data, and description can be specified optionally. Using these configuration items, API Gateway helps you with the documentation and preliminary verification of input parameters.
   Two required parameters `X-NameSpace-Code` and `X-MicroService-Name` need to be passed in for the call. They control which microservice the API Gateway request will be sent to and can be placed in header, path, or query. If the parameters are placed in path, just like for general APIs, you need to configure the path parameter in the path, such as `/{X-NameSpace-Code}/{X-MicroService-Name}`. If the variable `X-NameSpace-Code` is `crgt` and `X-MicroService-Name` is `coupon-activity`, then the access URL will be `https://access domain name/crgt/coupon-activity/`. Except these 2 fixed parameters, other parameters can be configured in the same way as the general APIs are.

	- In the namespace of [Tencent Service Framework](https://console.cloud.tencent.com/tsf/namespace), the `X-NameSpace-Code` path parameter is the code value of the namespace selected for the backend configuration.

	- In the service management of [Tencent Service Framework](https://console.cloud.tencent.com/tsf/service), the `X-MicroService-Name` path parameter is the microservice name of the cluster selected for the backend configuration.

7. Click **Next** and configure the backend.

### Step 3. Configure TSF in the backend

1. Select the cluster and namespace of the microservices to be interconnected with.
2. Select the microservices. The API publisher can integrate multiple microservices in 1 API.
   Please make sure that the added microservices, including those deployed on CVMs and containers, can be accessed by API Gateway (over the public network and NodePort).
   ![](https://main.qcloudimg.com/raw/d9197a8a06ac8156f09e4dfb6aa1fe12.png)

	> ?Currently, API Gateway only supports forwarding requests to service instances of the same deployment type (virtual machine or container) in TSF. If there are microservice instances deployed on both virtual machines and containers under a service, API Gateway cannot be used as the request entry.

3. Configure the backend path.
   This refers to the specific backend service request path. If you need to configure a dynamic parameter in the path, use `{}` to enclose the parameter name. In the parameter mapping configuration, this parameter name will be configured as the input parameter from the frontend configuration. The path here can be different from the frontend path. The backend path is the actual service request path.
4. Set the backend timeout period.
   This refers to the timeout period of the backend service call initiated by API Gateway (up to 30 seconds). During a call, if there is no response within the timeout period, API Gateway will terminate the call and return the corresponding error message.
5. Select the load balancing method.
6. Set the session persistence.
7. Set the parameters.

	- Backend parameters: `X-NameSpace-Code` and `X-MicroService-Name` are fixed parameters and cannot be mapped. Other configured parameters can be mapped.
  If your `Body` parameter only has a form format, you can directly map the frontend and backend parameters when configuring them. If it is in JSON format, the JSON parameter will be directly passed through by API Gateway.
	- Mapped parameters: parameter mapping is used to map the input parameters from the frontend to the parameters of the actual backend service. By default, parameter mapping will map an input parameter by using the same name and parameter location. In addition, you can change the parameter mapping method as needed. For example, you can map the input parameter from path to the query parameter in the backend service.
	- Constant parameters: You can add custom constant parameters as needed. They remain the same in each API call. In addition, you can use system parameters to pass certain required system information to the backend service.

8. Click **Next** and configure the response result.

### Step 4. Configure the response

API response configuration: includes the configuration of API response data and API error codes.
API response data configuration: indicates the type of returned data, including the data samples of successful and failed calls.
API error code definition: indicates the additional error code, error message, and description.

> ?Currently, API Gateway directly passes through the response result to the requester without processing it. When SDK documentation is generated, the entered sample responses will also be displayed in the documentation, which will help users better understand the meanings of APIs.

## Instructions

To allow access to the backend microservice through API Gateway, you need to open the security group of the virtual machine where the microservice resides to the internet. You can set the source, protocol port, and access policy of the security group access.
When setting the access source, you need to at least open the IP ranges 9.0.0.0/8 and 100.64.0.0/10 where API Gateway resides. You can also open other sources as needed.

- For an application deployed on a virtual machine, the corresponding service port of the virtual machine must be opened. For an application deployed on a container, the service port of the virtual machine where the container resides, instead of NodePort, needs to be opened.
- For container applications, IP drifting occurs often. Therefore, we recommend that you open service ports that run on containers and need to be exposed externally on all machines in the cluster.
