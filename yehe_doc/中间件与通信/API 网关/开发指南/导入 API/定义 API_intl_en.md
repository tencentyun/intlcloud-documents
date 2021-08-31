Standard RESTful APIs can be defined using the OpenAPI Specification. Generally, OpenAPI documents have 3 required objects:
- openapi: version number of the OpenAPI Specification.
- info: API metadata.
- paths: API request path and operation.

This document describes the mappings between the OpenAPI Specification and the API Gateway by object.

## openapi
The API Gateway supports OpenAPI Specification 3.0.0.

## info
The following table describes the mappings between OpenAPI and the info object of the API Gateway.

| OpenAPI Object     | Data Type | OpenAPI Object Description   | API Gateway Object |
|------------------|----------|--------------------|--------------|
| info.title       | String   | Name of the service to which an API belongs | Not used       |
| info.description | String   | Description of the service to which an API belongs | Not used       |
| info.version     | String   | Version number             | Not used       |

## paths
The following table describes the mappings between OpenAPI and the paths object of the API Gateway.

| OpenAPI Object          | Data Type | OpenAPI Object Description | API Gateway Object     |
|-----------------------|----------|------------------|------------------|
| paths.path            | Object   | API request path     | API frontend request path |
| operation.operationId | String   | API name         | API name         |
| operation.description | String   | API description         | Not used           |
| operation.parameters  | Object   | API request parameter     | API request parameter     |
| operation.responses   | String   | API response         | Not used           |

>?
>- For the object definition in OpenAPI Specification 3.0.0, see [OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.0.md).
>- For the process of importing APIs, see [Importing APIs](https://intl.cloud.tencent.com/document/product/628/37875).
>- For complete examples of importing APIs, see [Examples of Importing APIs](https://intl.cloud.tencent.com/document/product/628/37873).
