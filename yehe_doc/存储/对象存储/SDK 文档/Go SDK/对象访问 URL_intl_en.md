## Overview

This document provides code samples to obtain an object URL.

## Obtaining Object URLs

#### Description

The SDK allows you to obtain object access URLs for anonymous download or distribution.

>! The COS Go SDK version should not be earlier than v0.7.26.

#### Method prototype

```
func (s *ObjectService) GetObjectURL(key string) *url.URL
```

#### Sample request


[//]: # (.cssg-snippet-get-object-url-alias)
```go
name := "exampleobject"
ourl := c.Object.GetObjectURL(name)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |

#### Response description

An object access URL is returned upon success.
