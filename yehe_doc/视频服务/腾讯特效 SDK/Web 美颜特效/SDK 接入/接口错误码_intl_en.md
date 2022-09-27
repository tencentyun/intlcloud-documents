
## Built-in API Error Codes
The error codes returned by `webar.qcloud.com/sdk/xxx` (for example, `https://webar.qcloud.com/sdk/verify`).
The response structure is as follows:

```js
{
    "Code": xxx,
    "Message": "xxx"
}
```


### Successful requests 
 If `Code` is 0, a request is successful, and information will be returned in `Data`.

```json
{
    Code: 0,
    Data:{...}
}
```


### Authentication errors
 If `Code` is a value from 100 to 104, an authentication error occurred. The response status code is `401`.
```json
{
  "100":{
    zh: "Missing authentication parameter."
  },
  "101":{
    zh: "Signature timeout."
  },
  "102":{
    zh: "Unable to find the user."
  },
  "103":{
    zh: "Signature error."
  },
  "104":{
    zh: "Mismatch of referer or WeChatAppId."
  }
}
 

```

### Request parameter errors
If `Code` is -2, a request parameter error occurred. For details, see the value of `Message`.

```json

{
    "Code": -2,
    "Message": "LicenseKey must be a string."
}
```

### Business verification errors
If `Code` is greater than 1000, a business verification error occurred. For details, see the value of `Message`.

```json
{
    "Code": 2007,
    "Message": "The project does not exist."
}
```

### Unknown errors
If `Code` is -1, an unknown error occurred.
```json
{
    "Code": -1,
    "Message": "Unknown error."
}
```
