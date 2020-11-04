## API Description

**Request method**: POST.

```plaintext
service address/v3/device/set_custom_attribute
```

The API service address corresponds to the service access point one by one; therefore, please select the service address corresponding to your application [service access point](https://intl.cloud.tencent.com/document/product/1024/38517).

**API feature**: this API is used to configured personalized attributes at the token level, including CRUD operations.

## Parameter Description

### Request parameters

| Parameter Name | Required | Type | Description |
| -------- | -------- | ------- | ------------------------------------------------------------ |
| cmd      | Yes       | Integer | Operation type: <li>1: adds attribute.<li>2: updates attribute description.<li>3: deletes attribute.<li>4: deletes all attributes.<li>5: queries attribute. |
| accessId | Yes       | Integer | Application ID, which can be obtained in the [Product Management](https://console.cloud.tencent.com/tpns) page in the console. |
| token    | Yes       | String  | Device ID of 36 bits.<li> [Suggestions on getting TPNS token (Android)](https://intl.cloud.tencent.com/document/product/1024/30713)<li> [Suggestions on getting TPNS token (iOS)](https://intl.cloud.tencent.com/document/product/1024/30726) |
| attributeInfo   | Yes if `cmd` is 1, 2, or 3   | Map | Attribute details:<li> `value` is `attributeMap` in `Map` type.<li>  `key` is attribute and attribute value. **Note:** you should have created an attribute in **[TPNS Console](https://console.cloud.tencent.com/tpns)** > **Toolbox** > **User Attribute Management**; otherwise, this parameter will be filtered out, and `invalidAttribute` will be returned.

<span id="attributeInfo"></span>

### Response parameters

| Parameter Name | Required | Type | Description |
| ---------------- | ---------- | ------- | ------------------------------------------------------------ |
| retCode          | Yes         | Integer | Error code. For more information, please see [Server-Side Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763). |
| errMsg           | Yes         | String  | Error message when an error occurs in the request.                                       |
| attributeInfo    | cmd = 5    | Map     | Attribute details.                                                   |
| invalidAttribute | When the attribute is invalid | Array   | Details of invalid attribute.                                               |

## Samples

### Sample request for adding attribute

```
{
    "cmd": 1,
    "accessId": 1500004469,
    "token": "04cac74a714f61bf089987a986363d88****",
    "attributeInfo": {
         "attributeMap": {
            "age": "100",
            "name": "Ming",
            "high": "2.66"
        }
    }
}


```

### Sample response for adding attribute

```
{
    "retCode": 0,
    "errMsg": "success",
    "invalidAttribute": [
        "high"
    ]
}
```