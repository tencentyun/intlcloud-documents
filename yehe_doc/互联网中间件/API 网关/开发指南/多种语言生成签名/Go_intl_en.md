## Operation Scenarios

This document describes how to authenticate and manage your APIs through key pair authentication in Go.

## Directions
1. In the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as "key pair authentication" (for more information, please see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service where the API resides to the release environment (for more information, please see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).
3. Create a key pair on the key management page in the console.
4. Create a usage plan on the usage plan page in the console and bind it to the created key pair (for more information, please see [Sample Usage Plan](https://intl.cloud.tencent.com/document/product/628/11816)).
5. Bind the usage plan to the API or the service where the API resides.
6. Generate signing information in Go by referring to the [Sample Code](#example).

## Notes
- The eventually delivered HTTP request contains at least two headers: `Date` or `X-Date` and `Authorization`. More optional headers can be added in the request. If `Date` is used, the server will not check the time; if `X-Date` is used, the server will check the time.
- The value of `Date` header is the construction time of the HTTP request in GMT format, such as Fri, 09 Oct 2015 00:00:00 GMT.
- The value of `X-Date` header is the construction time of the HTTP request in GMT format, such as Mon, 19 Mar 2018 12:08:40 GMT. It cannot deviate from the current time for more than 15 minutes.
- If it is a microservice API, you need to add two fields in the header: `X-NameSpace-Code` and `X-MicroService-Name`. They are not needed for general APIs and are included in the demo by default.

<span id="example"></span>
## Sample Code
```
package main

import (
	"time"
	"fmt"
	"crypto/hmac"
	"crypto/sha1"
	"io"
	"io/ioutil"
	"encoding/base64"
	"net/http"
)


func calcAuthorization(source string, secretId string, secretKey string) (sign string, dateTime string, err error) {
	timeLocation, _ := time.LoadLocation("Etc/GMT")
	dateTime = time.Now().In(timeLocation).Format("Mon, 02 Jan 2006 15:04:05 GMT")
	sign = fmt.Sprintf("x-date: %s\nsource: %s", dateTime, source)
	fmt.Println(sign)

	//hmac-sha1
	h := hmac.New(sha1.New, []byte(secretKey))
	io.WriteString(h, sign)
	sign = fmt.Sprintf("%x", h.Sum(nil))
	sign = string(h.Sum(nil))
	fmt.Println("sign:", fmt.Sprintf("%s", h.Sum(nil)))

	//base64
	sign = base64.StdEncoding.EncodeToString([]byte(sign))
	fmt.Println("sign:", sign)

	auth := fmt.Sprintf("hmac id=\"%s\", algorithm=\"hmac-sha1\", headers=\"x-date source\", signature=\"%s\"", 
		secretId, sign)
	fmt.Println("auth:", auth)
		
	return auth, dateTime, nil
}

func main () {
	SecretId := "your SecretId" // `SecretId` in key pair
	SecretKey := "your SecretKey" // `SecretKey` in key pair
	source := "xxxxxx" // Arbitrary signature watermark value

	sign, dateTime, err := calcAuthorization(source, SecretId, SecretKey)
	if err != nil {
		fmt.Println(err)
		return
	}

	defaultDomain := "service-xxxxxxxx-1234567890.ap-guangzhou.apigateway.myqcloud.com" // Service domain name of API

	reqUrl := "https://service-xxxxxxxx-1234567890.ap-guangzhou.apigateway.myqcloud.com/release/yousa" // API access path
	client := &http.Client{
		Timeout: 7 * time.Second,//set timeout
	}

	req, err := http.NewRequest("GET", reqUrl, nil) //set body
	if err != nil {
		fmt.Println(err)		
		return 
	}

	req.Header.Set("Accept", "*/*")
	req.Header.Set("Accept-Charset", "utf-8;")
	req.Header.Set("Host", defaultDomain)
	req.Header.Set("Source", source)
	req.Header.Set("X-Date", dateTime)
	req.Header.Set("Authorization", sign)
	
	// If it is a microservice API, you need to add two fields in the header: 'X-NameSpace-Code' and 'X-MicroService-Name'. They are not needed for general APIs.
	req.Header.Set("x-NameSpace-Code", "testmic")
	req.Header.Set("x-MicroService-Name", "provider-demo")

	resp, err := client.Do(req)
	if err != nil {
		fmt.Println(err)		
		return 
	}
	defer resp.Body.Close()

	fmt.Println("status code:", resp.StatusCode)
	
	//get resp header
	var headerMsg string
	for key, _ := range resp.Header {
		headerMsg += fmt.Sprintf("\n%s:%s", key, resp.Header.Get(key))
	}
	fmt.Println(headerMsg)

	body, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		fmt.Println(err)		
		return 
	}

	fmt.Println(string(body))
	
}
```
