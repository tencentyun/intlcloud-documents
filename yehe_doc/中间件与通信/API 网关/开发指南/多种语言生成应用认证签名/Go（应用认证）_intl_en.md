## Overview

This document describes how to manage access to your APIs through application authentication in Go.

## Directions

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as **App Authentication**. To learn more about the authentication types, please find the documentation for different types of backends in [Creating API - Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service where the API resides to an environment. See [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809).
3. Create an application on the [Application](https://console.cloud.tencent.com/apigateway/app) page in the console.
4. Select the created application in the application list, click **Bind API**, select the service and API, and click **Submit** to bind the application to the API.
5. Generate signing information in Go by referring to the [Sample Code](#Sample-Code).

## Environment Dependencies

API Gateway provides code samples for JSON request mode and form request mode. Please select an appropriate mode according to your business needs.

## Notes

- For more information on operations such as application lifecycle management, authorizing an app to access the API, and binding an app with an API, please see [Application Management](https://intl.cloud.tencent.com/document/product/628/40306).
- For the application signature generation process, please see [Application Authentication](https://intl.cloud.tencent.com/document/product/628/40304).

## Sample Code[](id:Sample-Code)
### Sample code for JSON request method
<dx-codeblock>
:::  golang
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
	"strings"
	"time"
)

func main() {
	/* Environment name (for the release environment, you don't need to add environment information to the request path):
	   Release: /release or ""
	   Test: /test
	   Prerelease: /prepub
	*/
	const environment = ""
	const Url = "http://service-xxxxxxxx-1234567890.hk.apigw.tencentcs.com/app"
	// Application's `ApiAppKey`
	const ApiAppKey = "Your ApiAppKey"
	// Application's `ApiAppSecret`
	const ApiAppSecret = "Your ApiAppSecret"

	const GmtFormat = "Mon, 02 Jan 2006 15:04:05 GMT"
	const HTTPMethod = "POST"
	const Accept = "application/json"
	const ContentType = "application/json"

	// Parse `Host` and `Path` according to `Url`
	u, err := url.Parse(Url)
	if err != nil {
		log.Fatal(err)
	}
	Host := u.Hostname()
	Path := u.Path
	if environment != "" {
		Path = strings.TrimPrefix(Path, environment)
	}

	// Get the current UTC time
	xDate := time.Now().UTC().Format(GmtFormat)

	bodyStr := `{"arg1":"a","arg2":"b"}`

	h := md5.New()
	h.Write([]byte(bodyStr))
	md5Str := hex.EncodeToString(h.Sum(nil))
	ContentMD5 := base64.StdEncoding.EncodeToString([]byte(md5Str))

	// Construct the signature
	signingStr := fmt.Sprintf("x-date: %s\n%s\n%s\n%s\n%s\n%s", xDate, HTTPMethod, Accept, ContentType,
		ContentMD5, Path)
	mac := hmac.New(sha1.New, []byte(ApiAppSecret))

	_, err = mac.Write([]byte(signingStr))
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

### Sample code for form request method
<dx-codeblock>
:::  golang
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
	/* Environment name (for the release environment, you don't need to add environment information to the request path):
		Release: /release or ""
		Test: /test
		Prerelease: /prepub
	*/
	const environment	= ""
	const Url			= "http://service-xxxxxxxx-1234567890.hk.apigw.tencentcs.com/app"
	// Application's `ApiAppKey`
	const ApiAppKey 	= "Your ApiAppKey"
	// Application's `ApiAppSecret`
	const ApiAppSecret 	= "Your ApiAppSecret"


const GmtFormat 	= "Mon, 02 Jan 2006 15:04:05 GMT"
const HTTPMethod 	= "POST"
const Accept 		= "application/json"
const ContentType 	= "application/x-www-form-urlencoded"
const ContentMD5 	= ""

// Parse `Host` and `Path` according to `Url`
u, err := url.Parse(Url)
if err != nil {
	log.Fatal(err)
}
Host				:= u.Hostname()
Path				:= u.Path
if environment != "" {
	Path = strings.TrimPrefix(Path, environment)
}

// Get the current UTC time
xDate				:= time.Now().UTC().Format(GmtFormat)

// Request body
body			 	:= map[string]string{
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
	"Host": Host,
	"Accept": Accept,
	"Content-Type": ContentType,
	"x-date": xDate,
	"Authorization": sign,
}
bodyValues := url.Values{}
for k, v := range body {
	bodyValues.Add(k, v)
}


// Send the request
req, err := http.NewRequest(HTTPMethod, Url, strings.NewReader(bodyValues.Encode()))
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
