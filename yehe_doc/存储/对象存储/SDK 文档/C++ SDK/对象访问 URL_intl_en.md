## Overview

This document provides sample code for getting an object access URL.

## Getting an Object Access URL

#### Method prototype

```cpp
std::string GetObjectUrl(const std::string& bucket, const std::string& object, bool https = true, const std::string& region);
```

#### Sample request

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID (APPID is required), which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket. Replace it with your bucket name.
std::string object_name = "exampleobject";
//Get the HTTPS URL of the object. The region is the one configured in config.json.
cos.GetObjectUrl(bucket_name, object_name);
//Get the HTTP URL of the object. The region is the one configured in config.json.
cos.GetObjectUrl(bucket_name, object_name, false);
//Get the HTTPS URL of the object. The region is ap-shanghai.
std::string object_url = cos.GetObjectUrl(bucket_name, object_name, true, "ap-shanghai");  
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------- | ------ | -------- |
| bucket | Bucket name      | String | Yes       |
| object | Object name        | String | Yes       |
| https  | Whether to use HTTPS | Bool   | No       |
| region | Region        | String | No       |

#### Response description

An object access URL is returned upon success.
