This document describes the methods of TPNS authentication and verification.


## Obtaining a Key
1. Log in to the [TPNS Push Console](https://console.cloud.tencent.com/tpns), and select **Configuration Management** in the left sidebar.
2. Get the application's `Access ID` and `SECRET KEY` from the Application Information column (only visible for root account).


## Generating a Signature
1. **Generate a Request String** 
This step generates a request string.
The generation algorithm is: `base64(Access ID:SECRETKEY)`, which adds a colon after `Access ID` followed by `SECRETKEY` to form a string and then perform `base64` encoding on the string.
For example:
```
base64(150000****:cf43dac624820*****c1fe5fc993)
```

2. **Perform Basic Auth verification and authentication**
 Basic authentication is used, i.e., adding a field (key-value pair) to the HTTP Header:
  ```
  Authorization: Basic base64_auth_string
  ```
For example:
```
Authorization:Basic base64(150000****:cf43dac624820*****c1fe5fc993)
```
