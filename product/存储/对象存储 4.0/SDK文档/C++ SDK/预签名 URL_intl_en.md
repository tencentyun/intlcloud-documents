## Overview
The SDK for C++ provides APIs to generate signatures and get pre-signed request URLs. For more information, see the directions and examples in this document.


## Generating a Signature

### Feature Description

This API is used to calculate and generate a signature.

### Method Prototype 1

```
static std::string Sign(const std::string& secret_id,
                        const std::string& secret_key,
                        const std::string& http_method,
                        const std::string& in_uri,
                        const std::map<std::string, std::string>& headers,
                        const std::map<std::string, std::string>& params);
```

#### Parameter Descriptions 

| Parameter Name | Description | Type |
| ----------- | ----------------------------------------------------- | ------------------------ |
| secret_id | Developer-owned project ID for authentication purpose | String |
| secret_key | Developer-owned project key | String |
| http_method | HTTP method such as POST, GET, HEAD, and PUT, which is case-insensitive when passed in | String |
| in_uri | HTTP URI | String |
| headers | Key-value pairs of the HTTP headers | map&lt;string,string&gt; |
| Params | Key-value pairs of the HTTP parameters | map&lt;string,string&gt; |

#### Return Result Descriptions

The signature string is returned, which can be used within the specified validity period (set by CosSysConfig and 60 seconds by default). If an empty string is returned, the signature calculation failed.

### Method Prototype 2

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

#### Parameter Descriptions 

| Parameter Name | Description | Type |
| --------------- | ---------------------------------------------------- | ------------------------- |
| secret_id | Developer-owned project ID for authentication purpose | String |
| secret_key | Developer-owned project key | String |
| http_method | HTTP method such as POST, GET, HEAD, and PUT, which is case-insensitive when passed in | String |
| in_uri | HTTP URI | String |
| headers | Key-value pairs of the HTTP headers | map &lt;string,string&gt; |
| Params | Key-value pairs of the HTTP parameters | map &lt;string,string&gt; |
| start_time_in_s | Start time of the signature's validity period | uint64_t |
| end_time_in_s | End time of the signature's validity period | uint64_t |

#### Return Result Descriptions

The signature string is returned, which can be used within the specified validity period (set by CosSysConfig and 60 seconds by default). If an empty string is returned, the signature calculation failed.


## Getting a Pre-signed Request URL 

```go
std::string GeneratePresignedUrl(const GeneratePresignedUrlReq& req)
```

### Parameter Descriptions

| Parameter | Description |
| ---- | ------------------------------------------- |
| req | GeneratePresignedUrlReq, which is the request for the GeneratePresignedUrl operation |

The HTTP_METHOD enumeration is defined as follows:
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

## Example of Pre-signing a Request
A pre-signed request can be initiated by setting a permanent or temporary key according to the CosConfig class. For more information on the configuration file, see [Getting Started](https://intl.cloud.tencent.com/document/product/436/12301).

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";

// Add the bucket name, object key, and HTTP request method.
qcloud_cos::GeneratePresignedUrlReq req(bucket_name, object_name, qcloud_cos::HTTP_GET);
std::string presigned_url = cos.GeneratePresignedUrl(req); 

```
