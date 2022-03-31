## Overview

This document describes how to manage access to your APIs through application authentication in Go.

## Directions

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as **App authentication**. To learn more about the authentication types, please find the documentation for different types of backends in [Creating API - Overview](https://intl.cloud.tencent.com/document/product/628/11795).
2. Release the service where the API resides to an environment. See [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809).
3. Create an application on the [Application](https://console.cloud.tencent.com/apigateway/app) page in the console.
4. Select the created application in the application list, click **Bind API**, select the service and API, and click **Submit** to bind the application to the API.
5. Generate signing information in Go by referring to the [Sample Code](#Sample-Code).

## Environmental Dependencies

API Gateway provides sample codes with the request body in JSON format and form-data format. Please select as needed.

## Notes

- For more information on operations such as application lifecycle management, authorizing an app to access the API, and binding an app to an API, please see [Application Management](https://intl.cloud.tencent.com/document/product/628/40306).
- For the application signature generation process, please see [Application Authentication](https://intl.cloud.tencent.com/document/product/628/40304).

## Sample Code[](id:Sample-Code)

### Sample code with the request body in JSON format
<dx-codeblock>
:::  go
package main

import (
    "crypto/hmac"
    "crypto/md5"
    "crypto/sha1"
    "encoding/base64"
    "encoding/hex"
    "fmt"
    "io/ioutil"
    "log"
    "net/http"
	"net/url"
	"sort"
    "strings"
    "time"
)

func main() {
    // Application's `ApiAppKey`
    const ApiAppKey = "Your ApiAppKey"
    // Application's `ApiAppSecret`
	const ApiAppSecret = "Your ApiAppSecret"
	
    const Url = "http://service-xxx-xxx.gz.apigw.tencentcs.com/"

    const GmtFormat = "Mon, 02 Jan 2006 15:04:05 GMT"
    const HTTPMethod = "GET"
    const Accept = "application/json"
    const ContentType = "application/json"

    // Parse `Host` and `Path` according to `Url`
    u, err := url.Parse(Url)
    if err != nil {
        log.Fatal(err)
    }
    Host:= u.Hostname()
	Path:= u.Path
	Query := u.RawQuery
	
	// Environment information is not included in the signature path
	if strings.HasPrefix(Path, "/release") {
		Path = strings.TrimPrefix(Path, "/release")
	}else if strings.HasPrefix(Path, "/test") {
		Path = strings.TrimPrefix(Path, "/test")
	}else if strings.HasPrefix(Path, "/prepub") {
		Path = strings.TrimPrefix(Path, "/prepub")
	}
	
	if Path == "" {
		Path = "/"
	}

	// Splice query parameters. The query parameters need to be sorted in lexicographical order.
	if len(Query) > 0 {
		args, _ := url.ParseQuery(Query)

		var keys []string
		for k := range args {
			keys = append(keys, k)
		}
		sort.Strings(keys)

		sortQuery := ""
		for _, k := range keys {
			if args[k][0] != "" {
				sortQuery = sortQuery + "&" + k + "=" + args[k][0]
			} else {
				sortQuery = sortQuery + "&" + k 
			}
		}
		sortQuery = strings.TrimPrefix(sortQuery, "&")
		
    	Path = Path + "?" + sortQuery
	}

    // Get the current UTC time
    xDate := time.Now().UTC().Format(GmtFormat)
	ContentMD5 := ""
	bodyStr := `{"arg1":"a","arg2":"b"}`
	if HTTPMethod == "POST" {
		h := md5.New()
		h.Write([]byte(bodyStr))
		md5Str := hex.EncodeToString(h.Sum(nil))
		ContentMD5 = base64.StdEncoding.EncodeToString([]byte(md5Str))
	}

    // Construct the signature
    signingStr := fmt.Sprintf("x-date: %s\n%s\n%s\n%s\n%s\n%s", xDate, HTTPMethod, Accept, ContentType,
        ContentMD5, Path)
    mac := hmac.New(sha1.New, []byte(ApiAppSecret))

    _, err= mac.Write([]byte(signingStr))
    if err != nil {
        log.Fatal(err)
    }
    signature := base64.StdEncoding.EncodeToString(mac.Sum(nil))
    sign := fmt.Sprintf("hmac id=\"%s\", algorithm=\"hmac-sha1\", headers=\"x-date\", signature=\"%s\"",
        ApiAppKey, signature)

    // Construct the request
    headers := map[string]string{
        "Host":          Host,
        "Accept":        Accept,
        "Content-Type":  ContentType,
        "x-date":        xDate,
        "Authorization": sign,
    }

    // Send the request
    req, err := http.NewRequest(HTTPMethod, Url, strings.NewReader(bodyStr))
    if err != nil {
        log.Fatal(err)
    }

    for k, v := range headers {
        req.Header.Add(k, v)
    }

    res, err := http.DefaultClient.Do(req)
    if err != nil {
        log.Fatal(err)
    }
    defer res.Body.Close()

    resBody, _ := ioutil.ReadAll(res.Body)

    fmt.Println(string(resBody))
}
:::
</dx-codeblock>


### Sample code with the request body in form-data format
<dx-codeblock>
:::  go
package main

import (
    "crypto/hmac"
    "crypto/sha1"
    "encoding/base64"
    "fmt"
    "io/ioutil"
    "log"
    "net/http"
    "net/url"
    "sort"
    "strings"
    "time"
)

func main() {
    // Application's `ApiAppKey`
    const ApiAppKey = "Your ApiAppKey"
    // Application's `ApiAppSecret`
	const ApiAppSecret = "Your ApiAppSecret"
	
    const Url = "http://service-xxx-xxx.gz.apigw.tencentcs.com/"

    const GmtFormat = "Mon, 02 Jan 2006 15:04:05 GMT"
    const HTTPMethod = "POST"
    const Accept = "application/json"
    const ContentType = "application/x-www-form-urlencoded"

    // Parse `Host` and `Path` according to `Url`
    u, err := url.Parse(Url)
    if err != nil {
        log.Fatal(err)
    }
    Host := u.Hostname()
	Path := u.Path
    Query := u.RawQuery
	
	// Environment information is not included in the signature path
	if strings.HasPrefix(Path, "/release") {
		Path = strings.TrimPrefix(Path, "/release")
	}else if strings.HasPrefix(Path, "/test") {
		Path = strings.TrimPrefix(Path, "/test")
	}else if strings.HasPrefix(Path, "/prepub") {
		Path = strings.TrimPrefix(Path, "/prepub")
	}
	
	if Path == "" {
		Path = "/"
	}

	// Splice query parameters. The query parameters need to be sorted in lexicographical order. In this demo, it is assumed the parameters are already sorted.
	if len(Query) > 0 {
    	Path = Path + "?" + Query
	}

    // Get the current UTC time
    xDate := time.Now().UTC().Format(GmtFormat)
    ContentMD5 := ""
    
    // Request body form data
	body := map[string]string{
        "arg1": "a",
        "arg2": "b",
    }
    var bodyKeys []string
    for k := range body {
        bodyKeys = append(bodyKeys, k)
    }
    
    var bodyBuilder strings.Builder
    sort.Strings(bodyKeys)
    for _, k := range bodyKeys {
        bodyBuilder.WriteString(fmt.Sprintf("%s=%s&", k, body[k]))
    }
    bodyStr := bodyBuilder.String()
    // Remove the last `&`
    bodyStr = bodyStr[:len(bodyStr) - 1]

    // Construct the signature
    signingStr := fmt.Sprintf("x-date: %s\n%s\n%s\n%s\n%s\n%s?%s", xDate, HTTPMethod, Accept, ContentType,
        ContentMD5, Path, bodyStr)
    mac := hmac.New(sha1.New, []byte(ApiAppSecret))

    _, err	= mac.Write([]byte(signingStr))
    if err != nil {
        log.Fatal(err)
    }
    signature := base64.StdEncoding.EncodeToString(mac.Sum(nil))
    sign := fmt.Sprintf("hmac id=\"%s\", algorithm=\"hmac-sha1\", headers=\"x-date\", signature=\"%s\"",
        ApiAppKey, signature)

    // Construct the request
    headers := map[string]string{
        "Host":          Host,
        "Accept":        Accept,
        "Content-Type":  ContentType,
        "x-date":        xDate,
        "Authorization": sign,
    }

    // Send the request
    req, err := http.NewRequest(HTTPMethod, Url, strings.NewReader(bodyStr))
    if err != nil {
        log.Fatal(err)
    }

    for k, v := range headers {
        req.Header.Add(k, v)
    }

    res, err := http.DefaultClient.Do(req)
    if err != nil {
        log.Fatal(err)
    }
    defer res.Body.Close()

    resBody, _ := ioutil.ReadAll(res.Body)

    fmt.Println(string(resBody))
}
:::
</dx-codeblock>



### Sample code according to the hmac_sm3 algorithm

For more information, see [Sample Project](https://bruceppeng-1300555551.cos.ap-nanjing.myqcloud.com/%E5%9B%BD%E5%AF%86hmac_sm3%E7%AE%97%E6%B3%95.zip).
<dx-codeblock>
:::  go
package main

import (
    "crypto/md5"
    "encoding/base64"
    "encoding/hex"
    "fmt"
    "io/ioutil"
    "log"
    "net/http"
	"net/url"
	"sort"
    "strings"
    "time"
    "unsafe"
)

/*
#cgo CFLAGS: -I./
#cgo LDFLAGS: -L./ -lTencentSM
#include "sm.h" // Quotation mark is used because it is not a standard "C" header file
*/
import "C"


func mySM3_HMAC(data []byte, dataLen int, key []byte, keyLen int, mac []byte, macLen int) int {
    if data == nil || key == nil || mac == nil || len(mac) != macLen {
		panic("invalid parameter")
	}
	return int(C.SM3_HMAC((*C.uchar)(unsafe.Pointer(&data[0])), (C.size_t)(dataLen),
		(*C.uchar)(unsafe.Pointer(&key[0])), (C.size_t)(keyLen), (*C.uchar)(unsafe.Pointer(&mac[0]))))
}

func main() {
    // Application's `ApiAppKey`
    const ApiAppKey = "Your ApiAppKey"
    // Application's `ApiAppSecret`
	const ApiAppSecret = "Your ApiAppSecret"
	
    const Url = "http://service-xxx-xxx.gz.apigw.tencentcs.com/a?c=1&b=3"

    const GmtFormat = "Mon, 02 Jan 2006 15:04:05 GMT"
    const HTTPMethod = "GET"
    const Accept = "application/json"
    const ContentType = "application/json"

    // Parse `Host` and `Path` according to `Url`
    u, err := url.Parse(Url)
    if err != nil {
        log.Fatal(err)
    }
    Host:= u.Hostname()
	Path:= u.Path
	Query := u.RawQuery
	
	// Environment information is not included in the signature path
	if strings.HasPrefix(Path, "/release") {
		Path = strings.TrimPrefix(Path, "/release")
	}else if strings.HasPrefix(Path, "/test") {
		Path = strings.TrimPrefix(Path, "/test")
	}else if strings.HasPrefix(Path, "/prepub") {
		Path = strings.TrimPrefix(Path, "/prepub")
	}
	
	if Path == "" {
		Path = "/"
	}

	// Splice query parameters. The query parameters need to be sorted in lexicographical order.
	if len(Query) > 0 {
		args, _ := url.ParseQuery(Query)

		var keys []string
		for k := range args {
			keys = append(keys, k)
		}
		sort.Strings(keys)

		sortQuery := ""
		for _, k := range keys {
			if args[k][0] != "" {
				sortQuery = sortQuery + "&" + k + "=" + args[k][0]
			} else {
				sortQuery = sortQuery + "&" + k 
			}
		}
		sortQuery = strings.TrimPrefix(sortQuery, "&")
		
    	Path = Path + "?" + sortQuery
	}

    // Get the current UTC time
    xDate := time.Now().UTC().Format(GmtFormat)
	ContentMD5 := ""
	bodyStr := `{"arg1":"a","arg2":"b"}`
	if HTTPMethod == "POST" {
		h := md5.New()
		h.Write([]byte(bodyStr))
		md5Str := hex.EncodeToString(h.Sum(nil))
		ContentMD5 = base64.StdEncoding.EncodeToString([]byte(md5Str))
	}

    // Construct the signature
    signingStr := fmt.Sprintf("x-date: %s\n%s\n%s\n%s\n%s\n%s", xDate, HTTPMethod, Accept, ContentType,
        ContentMD5, Path)

    data := []byte(signingStr)
    key := []byte(ApiAppSecret)
    var out [32]byte

    mySM3_HMAC(data[:], len(data), key[:], len(key), out[:], len(out))
    signature := base64.StdEncoding.EncodeToString(out[:])
    
    sign := fmt.Sprintf("hmac id=\"%s\", algorithm=\"hmac-sm3\", headers=\"x-date\", signature=\"%s\"",
        ApiAppKey, signature)

    // Construct the request
    headers := map[string]string{
        "Host":          Host,
        "Accept":        Accept,
        "Content-Type":  ContentType,
        "x-date":        xDate,
        "Authorization": sign,
    }

    // Send the request
    req, err := http.NewRequest(HTTPMethod, Url, strings.NewReader(bodyStr))
    if err != nil {
        log.Fatal(err)
    }

    for k, v := range headers {
        req.Header.Add(k, v)
    }

    res, err := http.DefaultClient.Do(req)
    if err != nil {
        log.Fatal(err)
    }
    defer res.Body.Close()

    resBody, _ := ioutil.ReadAll(res.Body)

    fmt.Println(string(resBody))
}
:::
</dx-codeblock>


