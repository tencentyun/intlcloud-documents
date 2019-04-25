# Rest API Overview (V3)

## Differences Between V3 and V2

- V3 is fully based on HTTPS and no longer provides HTTP access.
- V3 supports POST access and no longer provides GET access.

- V3 uses  HTTP Basic Authentication for access authorization. API requests can be done using common HTTP tools such as curl and Postman.

- In V3, APIs are categorized according to business functions, including Push API, Tag API, Device API, and Tool API. The same URL is used for all APIs in one category to improve API usability.

- V3 has improvements in functionality. A tool API for arrival statistics query is added, which is currently under beta test.

For V2, see the documentation at https://xg.qq.com/docs/server_api/v2/rest.html.

_** Note: It is recommended to use the V3 APIs, and V2 APIs may be discontinued in the future.**_



  

## API Overview

TPNS provides REST-compliant HTTP APIs for developers to remotely call the services provided by it.

The APIs are mainly divided into four categories:

| API type | Description | Status |
| ---------- | --------------- | ---- |
| <a href="./push_api_v3.md">Push API</a>  | It includes various APIs used to push messages     | Normal   |
| <a href="./tag_api_v3.md">Tag API</a>    | It includes various APIs used to add, delete, and query tags | Normal   |
| Device API | It includes various APIs used to query and delete account | Implementing |
| Tool API | It includes various APIs used to locate problems and query other data | Implementing |



## Request Method
- HTTPS is supported
- POST is supported




## Authentication Method

- Basic authentication is used, i.e., adding a field (key-value pair) to the HTTP Header:

  ```
  Authorization: Basic base64_auth_string
  ```

- The generation algorithm for base64_auth_string is: `base64(APPID:SECRETKEY)`

  That is to add a colon after `APPID` followed by `SECRETKEY` to form a string and then perform `base64` encoding on the string.

- `APPID` and `SECRETKEY` can be obtained in **My apps** > **App configuration** at the [TPNS website](http://xg.qq.com/).

  

## Protocol Description

**Request URL**: `https://openapi.xg.qq.com/v3/<class_path>/<method>`

| Field name | Usage | Note |
| ----------------- | ------- | ------------- |
| openapi.xg.qq.com | API domain name | None |
| v3 | Version number | None |
| class_path | Category of the API provided | Different APIs have different path names |
| method | Feature API name | Different feature APIs have different names |



## API Limitations

- For <a href="./push_api_v3.md">Push API</a>, the APIs for full push and tag push have limitations on call frequency. The default value is 30 times per ACCESS_ID per hour.
- The size of the pushed message body cannot exceed 4 KB, and this limitation applies to the `message` field in Push API.

## Reference
- <a href="../../noun_explanation.md">Glossary</a>
- [Standard HTTP Error Codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes#4xx_Client_Error)
