This document describes how to import APIs on different backends. The following takes the YAML format as an example.

### Mock backend
<dx-codeblock>
::: YAML
openapi: 3.0.0
info:
  title: test
  version: 1.0.1
paths:
  /:
    get:
      operationId: test
      responses:
        '200':
          description: The list of possible responsesas they are returned from executing
            this operation.
      x-apigw-api-business-type: NORMAL
      x-apigw-api-type: NORMAL
      x-apigw-backend:
        MockReturnHttpHeaders: []
        MockReturnHttpStatusCode: 200
        ServiceMockReturnMessage: success
        ServiceType: MOCK
      x-apigw-cors: false
      x-apigw-protocol: HTTP
      x-apigw-service-timeout: 15

:::
</dx-codeblock>

### Proxy backend
<dx-codeblock>
::: YAML
openapi: 3.0.0
info:
  title: testa
  version: 1.0.1
paths:
  /proxy:
    get:
      operationId: test
      responses:
        '200':
          description: The list of possible responsesas they are returned from executing
            this operation.
      x-apigw-api-business-type: NORMAL
      x-apigw-api-type: NORMAL
      x-apigw-backend:
        ServiceConfig:
          Method: GET
          Path: /
          Url: http://cloud.tencent.com
        ServiceType: HTTP
      x-apigw-cors: false
      x-apigw-protocol: HTTP
      x-apigw-service-timeout: 15

:::
</dx-codeblock>

### VPC service backend
<dx-codeblock>
::: YAML
openapi: 3.0.0
info:
  title: test
  version: 1.0.1
paths:
  /:
    get:
      operationId: test
      responses:
        '200':
          description: The list of possible responsesas they are returned from executing
            this operation.
      x-apigw-api-business-type: NORMAL
      x-apigw-api-type: NORMAL
      x-apigw-backend:
        ServiceConfig:
          Method: GET
          Path: /
          Product: clb
          UniqVpcId: vpc-xxxxxx
          Url: http://172.x.x.x:8xxx
        ServiceType: HTTP
      x-apigw-const-paramters:
      - DefaultValue: xxx
        Desc: "xxxx backend host"
        Name: Host
        Position: HEADER
      x-apigw-cors: false
      x-apigw-protocol: HTTP
      x-apigw-service-timeout: 15

:::
</dx-codeblock>

### SCF event backend
<dx-codeblock>
::: YAML
openapi: 3.0.0
info:
  title: testa
  version: 1.0.1
paths:
  /scf:
    get:
      operationId: test
      responses:
        '200':
          description: The list of possible responsesas they are returned from executing
            this operation.
      x-apigw-api-business-type: NORMAL
      x-apigw-api-type: NORMAL
      x-apigw-backend:
        IsBase64Encoded: false
        ServiceScfFunctionName: APIGWCustomRespDemo-xxxxx
        ServiceScfFunctionNamespace: default
        ServiceScfFunctionQualifier: $DEFAULT
        ServiceScfFunctionType: EVENT
        ServiceScfIsIntegratedResponse: false
        ServiceType: SCF
      x-apigw-cors: false
      x-apigw-protocol: HTTP
      x-apigw-service-timeout: 15

:::
</dx-codeblock>

### SCF HTTP-triggered function backend
<dx-codeblock>
::: YAML
openapi: 3.0.0
info:
  title: testa
  version: 1.0.1
paths:
  /scf:
    get:
      operationId: test
      responses:
        '200':
          description: The list of possible responsesas they are returned from executing
            this operation.
      x-apigw-api-business-type: NORMAL
      x-apigw-api-type: NORMAL
      x-apigw-backend:
        IsBase64Encoded: false
        ServiceScfFunctionName: flask_demo-xxxxxxxxx
        ServiceScfFunctionNamespace: default
        ServiceScfFunctionQualifier: $DEFAULT
        ServiceScfFunctionType: HTTP
        ServiceScfIsIntegratedResponse: false
        ServiceType: SCF
      x-apigw-cors: false
      x-apigw-protocol: HTTP
      x-apigw-service-timeout: 15

:::
</dx-codeblock>

### COS backend
<dx-codeblock>
::: YAML
openapi: 3.0.0
info:
  title: test
  version: 1.0.1
paths:
  /cos:
    get:
      operationId: test
      responses:
        '200':
          description: The list of possible responsesas they are returned from executing
            this operation.
      x-apigw-api-business-type: NORMAL
      x-apigw-api-type: NORMAL
      x-apigw-backend:
        ServiceConfig:
          CosConfig:
            Action: GetObject
            Authorization: true
            BucketName: xxxxxxx
            PathMatchMode: FullPath
          Path: /
        ServiceType: COS
      x-apigw-cors: false
      x-apigw-protocol: HTTP
      x-apigw-service-timeout: 15

:::
</dx-codeblock>

### TSF microservice API backend
<dx-codeblock>
::: YAML
openapi: 3.0.0
info:
  title: SCF_API_SERVICE
  version: 1.0.1
paths:
  /:
    get:
      operationId: test
      parameters:
      - description: ""
        in: header
        name: X-MicroService-Name
        required: true
        schema:
          type: string
      - description: ""
        in: header
        name: X-NameSpace-Code
        required: true
        schema:
          type: string
      responses:
        '200':
          description: The list of possible responsesas they are returned from executing
            this operation.
      x-apigw-api-business-type: NORMAL
      x-apigw-api-type: TSF
      x-apigw-backend:
        MicroServices:
        - ClusterId: cluster-xxxxxx
          MicroServiceName: provider-demo
          NamespaceId: namespace-xxxxx
        ServiceConfig:
          Path: /
        ServiceTsfHealthCheckConf:
          ErrorThresholdPercentage: 50
          IsHealthCheck: true
          RequestVolumeThreshold: 20
          SleepWindowInMilliseconds: 5000
        ServiceTsfLoadBalanceConf:
          IsLoadBalance: true
          Method: RoundRobinRule
          SessionStickRequired: false
          SessionStickTimeout: 0
        ServiceType: TSF
      x-apigw-cors: false
      x-apigw-protocol: HTTP
      x-apigw-service-timeout: 15 

:::
</dx-codeblock>

### Importing an API in JSON format 
The following takes the mock backend as an example. For other types, see the YAML format.
<dx-codeblock>
:::  JSON
{
 "openapi": "3.0.0",
 "info": {
   "description": "importMockAPI",
   "version": "1.0.0",
   "title": "Mock API"
 },
 "paths": {
   "/mock": {
     "get": {
       "description": "Import Mock API Test",
       "operationId": "importMockAPI",
       "responses": {
         "200": {
           "description": "Import Mock API Test"
         }
       }
     }
   }
 }
}

:::
</dx-codeblock>


