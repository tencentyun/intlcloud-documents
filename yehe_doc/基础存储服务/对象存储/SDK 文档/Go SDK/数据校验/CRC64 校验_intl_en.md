## Overview

Errors may occur when data is transferred between the client and the server. COS can not only verify data integrity through [MD5 and custom attributes](https://intl.cloud.tencent.com/document/product/436/32467), but also the CRC64 check code.

COS will calculate the CRC64 value of the newly uploaded object and store the result as object attributes. It will carry x-cos-hash-crc64ecma in the returned response header, which indicates the CRC64 value of the uploaded object calculated according to [ECMA-182 standard](https://www.ecma-international.org/publications/standards/Ecma-182.htm). If an object already has a CRC64 value stored before this feature is activated, COS will not calculate its CRC64 value, nor will it be returned when the object is obtained.

## Description

APIs that currently support CRC64 include:

- APIs for simple upload
	- [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) and [POST Object](https://intl.cloud.tencent.com/document/product/436/14690): you can get the CRC64 check value for your file from the response headers.
- Multipart upload APIs
	- [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750): you can compare and verify the CRC64 value returned by COS against the value calculated locally.
	- [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742): returns a CRC64 value for the entire object only if each part has a CRC64 attribute. Otherwise, no value is returned.
- The [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) operation returns a corresponding CRC64 value.
- When you call the [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881), the CRC64 value is returned only if the source object has one.
- The [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) and [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) operations return the CRC64 value provided the object has one. You can compare and verify the CRC64 value returned by COS against that calculated locally.

## SDK Description

SDK APIs get CRC64 values from response headers. When files are uploaded, the SDK verifies the CRC64 values by default.

>! The COS Go SDK version should not be earlier than v0.7.23.

#### Sample request
```go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/cos-go-sdk-v5"
    "net/http"
    "net/url"
    "strings"
)

func main() {
    // Replace examplebucket-1250000000 and COS_REGION with the actual information
    u, _ := url.Parse("https://examplebucket-1250000000.cos.COS_REGION.myqcloud.com")
    b := &cos.BaseURL{BucketURL: u}
    client := cos.NewClient(b, &http.Client{
        Transport: &cos.AuthorizationTransport{
            SecretID:  "SECRETID",  // Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
            SecretKey: "SECRETKEY", // Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
        },
    })
    // Disable CRC64 verification. CRC64 verification is enabled by default. You are strongly advised not to disable CRC64 verification.
    // client.Conf.EnableCRC = false

    name := "exampleobject"
    // Upload the object with a string
    f := strings.NewReader("test")
    // The SDK automatically verifies the CRC64 value
    resp, err := client.Object.Put(context.Background(), name, f, nil)
    if err != nil {
        // ERROR
    }
    // Get the CRC64 value from the response header
    fmt.Printf("CRC64: %v\n", resp.Header.Get("x-cos-hash-crc64ecma"))
}
```

#### Response description

| Parameter | Description | Type |
| --------------- | ------------ | ------ |
| Response        | HTTP response     | Struct |
| Response.Header | HTTP response header | Struct |
| Response.Body   | HTTP response data | Struct |

