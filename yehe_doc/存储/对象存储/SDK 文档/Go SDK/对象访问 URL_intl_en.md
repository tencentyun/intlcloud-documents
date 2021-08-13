## Overview

This document provides code samples related to obtaining an object URL.

## Obtaining Object URLs

#### Feature description

The SDK allows you to obtain object access URLs for anonymous download or distribution.

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
| Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes |

#### Response description

An object access URL is returned upon success.
