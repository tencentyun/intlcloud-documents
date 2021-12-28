## Overview

This document provides an overview of the API and sample code for getting an object access URL.

## Getting an Object Access URL

#### Description

The API is used to get object access URLs for anonymous download or distribution.

>! The COS Go SDK version should not be earlier than v0.7.26.

#### Method prototype

```
func (s *ObjectService) GetObjectURL(key string) *url.URL
```

#### Sample request


[//]: # (.cssg-snippet-get-object-url-alias)
```go
key := "exampleobject"
ourl := c.Object.GetObjectURL(key)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |

#### Response description

An object access URL is returned upon success.
