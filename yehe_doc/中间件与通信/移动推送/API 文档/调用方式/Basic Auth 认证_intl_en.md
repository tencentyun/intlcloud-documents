This document describes the Basic Auth authentication methods of Tencent Push Notification Service.

For Basic Auth authentication with `AccessId` and `SecretKey`, the key is easy to be compromised and the security is not high. You are recommended to use [signature authentication](https://www.tencentcloud.com/document/product/1024/34213).



## Obtaining a Key
1. Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns), and select **Configuration Management** > **Basic Configuration** in the left sidebar.
2. Get `Access ID` and `SECRET KEY` from the Application Information column.


## Generating a Signature
1. **Generate a Request String** 
This step generates a request string.
The generation algorithm is: `base64(Access ID:SECRETKEY)`, which adds a colon after `Access ID` followed by `SECRETKEY` to form a string and then perform `base64` encoding on the string.
Sample:
```
base64(150000****:cf43dac624820*****c1fe5fc993)
```

2. **Perform Basic Auth verification and authentication**
 Basic authentication is used, i.e., adding a field (key-value pair) to the HTTP Header:
  ```
  Authorization: Basic base64_auth_string
  ```
Sample:
```
Authorization:Basic base64(150000****:cf43dac624820*****c1fe5fc993)
```
