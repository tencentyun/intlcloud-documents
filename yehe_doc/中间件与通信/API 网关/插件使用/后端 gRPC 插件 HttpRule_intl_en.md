## Overview

The gRPC plugin requires you to provide a `.proto` file to describe the rule for converting HTTP into gRPC. `HttpRule` is the syntax of the conversion rule.

## Prerequisites

The HTTP request body can be in JSON format only, and the request method can be RESTful only. The relationships between supported HTTP methods and CRUD operations are as listed below:

| **Supported HTTP Method** | **Corresponding CURD** |
| ------------------- | ---------------------- |
| POST                | Create                 |
| GET                 | Read                   |
| PUT                 | Update/Replace         |
| PATCH               | Update/Modify          |
| DELETE              | Delete                 |

**The following protocols are supported by the backend:**

- gRPC
- gRPCS

**The following types are supported by the backend:**

- Backend upstream (both VPC upstreams and TKE upstreams are supported)
- Private network CLB
- Public network URL backend



## How It Works

`HttpRule` defines the mapping relationship between HTTP and gRPC in two dimensions:
- **Where are parameters values in the RPC method of gRPC obtained?**
- **How is the data returned in the HTTP response in the RPC method of gRPC?**

In the RPC method definition, you can add `option (google.api.http)` as the `HttpRule` mapping syntax.
![](https://qcloudimg.tencent-cloud.cn/raw/cff6d62c07c0ed8966af5c9deab9e122.png)        
>?
>- In `HttpRule`, the HTTP method needs to be in lowercase, and an RPC method corresponds to an HTTP request.
>- There is only one method, unless you use `addtional_bindings`. For the usage methods and use cases of `addtional_bindings`, see [below](#addtional_bindings).
>
Below is a sample `.proto` file with the `HttpRule` rule:
<dx-codeblock>
:::  java
syntax = "proto3";

option go_package = "google.golang.org/grpc/examples/helloworld/helloworld";
option java_multiple_files = true;
option java_package = "io.grpc.examples.helloworld";
option java_outer_classname = "HelloWorldProto";
import "google/api/annotations.proto";

package helloworld;
// Chinese remarks are supported
// The greeting service definition.
service Greeter {
  // Sends a greeting
  rpc SayHello (HelloRequest) returns (HelloReply) {
    option (google.api.http) = {
        get: "/grpc_upstream/{name}"
        additional_bindings {
            get: "/grpc_upstream_tls/{name}"
        }
    };
  }
}

// The request message containing the user's name.
message HelloRequest {
  string name = 1;
}

// The response message containing the greetings
message HelloReply {
  string message = 1;
}
:::
</dx-codeblock>

>!You must import the relevant `HttpRule` syntax: import "google/api/annotations.proto". In addition to the `HttpRule`, all other syntaxes are the same as those of the gRPC service. Therefore, you only need to add the `HttpRule` to the original `.proto` file of the gRPC service.



### Checking the validity of `.proto` file syntax locally

**If the uploaded `.proto` file has problems, you can use the protoc tool to check the file as follows:**

1. Download [googleapis.tar.gz](https://apigw-1300555551.cos.ap-nanjing.myqcloud.com/googleapis.tar.gz).
2. Decompress `googleapis.tar.gz` to any directory such as `/tmp`.
3. Set the environment variable `GOOGLEAPIS_DIR:GOOGLEAPIS_DIR=/tmp/googleapis`.
4. Use the protoc tool to verify the validity of the `.proto` file. The file is valid if there are no errors and warnings.
<dx-codeblock>
:::  sh
protoc --include_imports --include_source_info  --proto_path=${GOOGLEAPIS_DIR} --proto_path=. --descriptor_set_out=api_descriptor.pb ex   ample.proto
:::
</dx-codeblock>




### Request parameter mapping rules

- **If the definition of the body in `HttpRule` is a specific value (not \*):**
 - **For parameters defined in the path template, get them from the path in the request URL.**
 - **For parameters defined in the body, get them from the request body.**
 - **For other parameters, get them from the query parameters in the request URL.**
- **If the body in `HttpRule` is \*:**
 - **All parameters cannot be obtained from the query parameters in the request URL.**
 - **Parameters can be obtained only from the body or URL path.**
- **If the body in `HttpRule` is undefined:**
 - **Parameters are obtained from the query parameters in the request URL by default.**
 - **If it is defined that parameters are obtained from the URL path, they will be obtained from the URL path according to the path template rule.**



### Use cases
1. Take getting parameters of a GET request as an example (parameters are obtained from the query parameters by default unless otherwise specified in the path template):
<dx-codeblock>
:::  java
service Messaging {
   rpc GetMessage(GetMessageRequest) returns (Message) {
     option (google.api.http) = {
         get:"/v1/messages/{message_id}"
     };
   }
 }
message GetMessageRequest {
   message SubMessage {
     string subfield = 1;
   }
   string message_id = 1;  // Mapped to URL path.
   int64 revision = 2;     // Mapped to URL query parameter `revision`.
   SubMessage sub = 3;     // Mapped to URL query parameter `sub.subfield`.
 }
:::
</dx-codeblock>
<ul><li><code>message_id</code> in <code>GetMessageRequest</code> is obtained from the URL path, and other parameters, such as <code>revision</code> and <code>subfield</code> in <code>sub</code>, are obtained from the query parameters of the URL.</li>
<li><code>{message_id}</code> in "/v1/messages/{message_id}" is the path template. The parameter specifying <code>message_id</code> is obtained from the URL path.</li>
<li>For the HTTP request URL <code>/v1/messages/123456?revision=2&sub.subfield=foo</code>, the corresponding gRPC request is <code>GetMessage(message_id: "123456" revision: 2 sub: SubMessage(subfield:"foo"))</code>.</li></ul>
2. PATCH request parameters are obtained from the URL path and body. Note that if the body is \*, you cannot get parameters from the query parameters of the request.
<dx-codeblock>
:::  java
 service Messaging {
   rpc UpdateMessage(Message) returns (Message) {
     option (google.api.http) = {
       patch: "/v1/messages/{message_id}"
       body: "*"
     };
   }
 }
 message Message {
   string message_id = 1;
   string text = 2;
 }
:::
</dx-codeblock>
<ul><li>The request parameter <code>message_id</code> is obtained from the URL path of the request, while other parameters such as <code>text</code> are obtained from the body. Note that if the body is \*, parameters won't be obtained from the query parameters of the request.</li>
<li>For the HTTP request <code>PATCH /v1/messages/123456 { "text": "Hi!" }</code>, the corresponding gRPC request is <code>UpdateMessage(message_id: "123456" text: "Hi!")</code>.</li></ul>
3. If the body is not \*:
<dx-codeblock>
:::  java
 service Messaging {
   rpc UpdateMessage(UpdateMessageRequest) returns (Message) {
     option (google.api.http) = {
       patch: "/v1/messages/{message_id}"
       body: "message"
     };
   }
 }
 message UpdateMessageRequest {
   string message_id = 1;  // mapped to the URL
   Message message = 2;    // mapped to the body
 }
 
 message Message {
    string text = 1; // The resource content.
 }
:::
</dx-codeblock>
For the HTTP request <code>PATCH /v1/messages/123456 { "text": "Hi!" }</code>, the corresponding gRPC request is <code>UpdateMessage(message_id: "123456" text: "Hi!")</code>.
4. Use cases of `additional_bindings`:
`additional_bindings` is used for API compatibility or exposure of two HTTP requests with the same RPC method.
<dx-codeblock>
:::  java
 service Messaging {
   rpc GetMessage(GetMessageRequest) returns (Message) {
     option (google.api.http) = {
       get: "/v1/messages/{message_id}"
       additional_bindings {
         get: "/v1/users/{user_id}/messages/{message_id}"
       }
     };
   }
 }
 message GetMessageRequest {
   string message_id = 1;
   string user_id = 2;
 }
:::
</dx-codeblock>
In this way, two HTTP requests use the same RPC method, and the request mappings are as detailed below:
<ul><li>For the HTTP request <code>GET /v1/messages/123456</code>, the corresponding gRPC request is <code>GetMessage(message_id: "123456")</code>.</li>
<li>For the HTTP request <code>GET /v1/users/me/messages/123456</code>, the corresponding gRPC request is <code>GetMessage(message_id: "123456")</code>.</li></ul>

>?For the detailed `HttpRule`, see [http.proto](https://github.com/googleapis/googleapis/blob/master/google/api/http.proto).

## Notes

Only one `.proto` file can be uploaded for a gRPC backend plugin. Therefore, you need to place all RPC methods that need to be exposed into the same `.proto` file and add `HttpRule`.

## FAQs

#### The error message "The `proto file format error` parameter format is incorrect. Modify it and perform the operation again" is reported when I save the gRPC plugin. What should I do?
The submitted `.proto` file is in an incorrect format. This may be because `HttpRule` isn't imported. In this case, you need to add `import "google/api/annotations.proto"` to the `.proto` file.


#### The error message "Api with grpc(s) backend needs GrpcGateway plugin be configured" is reported when I access a service provided by API Gateway. What should I do?  
Solution: Bind the gRPC backend plugin to this API.
![](https://qcloudimg.tencent-cloud.cn/raw/91c6ef7ac266b6286d26fad359549a5c.png)                      
Example of successful access after modification:
![](https://qcloudimg.tencent-cloud.cn/raw/6e6cb660c671dbee3f904fc8b9e3ce5d.png)


#### The error message "failed to transcode .proto file Unknown path "/something"" is reported when I access a service provided by API Gateway. What should I do?

Solution: The path defined in `option` in `HttpRule` in the `.proto` file is different from the one you accessed. Check the `.proto` file and modify the paths to the same value. 
![](https://qcloudimg.tencent-cloud.cn/raw/fc261fed06f0c56b4624ef7b8558baea.png)                       
Solution example:
![](https://qcloudimg.tencent-cloud.cn/raw/86085332cb903ed73c8f8a42af8e92b8.jpg)        
Example of successful access after modification:
![](https://qcloudimg.tencent-cloud.cn/raw/6e6cb660c671dbee3f904fc8b9e3ce5d.png)        



