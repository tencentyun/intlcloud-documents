## Overview
The C++ SDK provides APIs to generate signatures and obtain pre-signed URLs. For detailed directions, see the description and examples below.
For details about how to use a pre-signed URL for uploads, see [Upload via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14114). For details about how to use a pre-signed URL for downloads, see [Download via Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/14116).

>?
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
>



## Generating a Signature

### Description

Calculate and generate a signature.

### Method prototype 1

```
static std::string Sign(const std::string& secret_id,
                        const std::string& secret_key,
                        const std::string& http_method,
                        const std::string& in_uri,
                        const std::map<std::string, std::string>& headers,
                        const std::map<std::string, std::string>& params);
```

#### Parameter description 

| Parameter | Description | Type |
| ----------- | ----------------------------------------------------- | ------------------------ |
| secret_id   | ID to verify the developer’s identity for the project  | String                   |
| secret_key      | Key owned by the developer to verify identity for the project  |String                   |
| http_method | HTTP method, such as POST, GET, HEAD, and PUT; case-insensitive | String |
| in_uri      | HTTP uri                                              | String                   |
| headers     | HTTP header key-value pair                  | map&lt;string,string&gt; |
| params      | HTTP params key-value pair                 | map&lt;string,string&gt; |

#### Response description

A signature string is returned, which can be used during the specified validity period (It is set using `CosSysConfig`. Default value: 60 sec). If an empty string is returned, the signature fails to be calculated.

### Method prototype 2

```
static std::string Sign(const std::string& secret_id,
                        const std::string& secret_key,
                        const std::string& http_method,
                        const std::string& in_uri,
                        const std::map<std::string, std::string>& headers,
                        const std::map<std::string, std::string>& params,
                        uint64_t start_time_in_s,
                        uint64_t end_time_in_s);
```

#### Parameter description 

| Parameter | Description | Type |
| --------------- | ---------------------------------------------------- | ------------------------- |
| secret_id       |  ID to verify the developer’s identity for the project  | String                    |
| secret_key      | Key owned by the developer to verify identity for the project  | String                    |
| http_method     | HTTP method, such as POST, GET, HEAD, and PUT; case-insensitive | String    |
| in_uri          | HTTP uri                                             | String                    |
| headers         | HTTP header key-value pair                    | map &lt;string,string&gt;  |
| params          | HTTP params key-value pair                    | map &lt;string,string&gt; |
| start_time_in_s | Start time of the signature                | uint64_t                  |
| end_time_in_s   | End time of the signature                | uint64_t                  |

#### Response description

A signature string is returned, which can be used during the specified validity period (It is set using `CosSysConfig`. Default value: 60 sec). If an empty string is returned, the signature fails to be calculated.


## Getting a Pre-signed Request URL 

```go
std::string GeneratePresignedUrl(const GeneratePresignedUrlReq& req)
```

### Parameter description

| Parameter | Description |
| ---- | ------------------------------------------- |
| req  | `GeneratePresignedUrlReq`, request of the `GeneratePresignedUrl` operation  |

The enumerated values of `HTTP_METHOD` are defined as follows:

```
typedef enum {
	HTTP_HEAD,
    HTTP_GET,
    HTTP_PUT,
    HTTP_POST,
    HTTP_DELETE,
    HTTP_OPTIONS
} HTTP_METHOD;
```

## Pre-signed Request Samples
You can initiate a pre-signed request by setting a permanent or temporary key using the `CosConfig` class. For the detailed configuration file, please see [Getting Started](https://intl.cloud.tencent.com/document/product/436/12301).

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";

// Add the bucket name, object key, and HTTP request method.
// Note: users do not need to encode object_name.
qcloud_cos::GeneratePresignedUrlReq req(bucket_name, object_name, qcloud_cos::HTTP_GET);
std::string presigned_url = cos.GeneratePresignedUrl(req); 

```
