## API Description

**Request method**: POST.

```plaintext
Service URL/v3/device/set_custom_attribute
```

API service URLs correspond to service access points one by one. Please select the [service URL](https://intl.cloud.tencent.com/document/product/1024/38517) corresponding to the service access point of your application.

**Feature**: this API is used to manage personalized attributes at the token level, including creation, deletion, update, and query operations.

## Parameter Description

### Request parameters

| Parameter | Required | Type | Description |
| -------- | -------- | ------- | ------------------------------------------------------------ |
| cmd      | Yes       | Integer | Operation type: <li>1: adding an attribute.<li>2: updating an attribute.<li>3: deleting an attribute.<li>4: deleting all attributes.<li>5: querying attributes. |
| token    | Yes       | String  | Unique ID assigned to each device by TPNS.<li> [Suggestions on getting TPNS token (Android)](https://intl.cloud.tencent.com/document/product/1024/30713#suggestions-on-getting-tpns-token)<li> [Suggestions on getting TPNS token (iOS)](https://intl.cloud.tencent.com/document/product/1024/30726#suggestions-on-getting-tpns-token) |
| attributeInfo   | Yes (when `cmd` is `1`, `2`, or `3`)   | Map | Attribute details. See the description of the `attributeMap` parameter below. |
| attributeMap | Yes (when `cmd` is `1`, `2`, or `3`) | Map | Attribute details: <li> `key` indicates the attribute name and can contain up to 50 bytes. <br>**Note:** you should have created an attribute in the [TPNS console](https://console.cloud.tencent.com/tpns) > **Toolbox** > **User Attribute Management**; otherwise, this parameter will be filtered out, and `invalidAttribute` will be returned. <li> `value` indicates the attribute value and can contain up to 50 bytes.</li> |

<span id="attributeInfo"></span>

### Response parameters

| Parameter | Returned | Type | Description  |
| ---------------- | ---------- | ------- | ------------------------------------------------------------ |
| retCode          | Yes         | Integer | Error code. For more information, please see [Server-Side Error Codes](https://intl.cloud.tencent.com/document/product/1024/33763). |
| errMsg           | Yes         | String  | Error message when an error occurs in the request.                                       |
| attributeInfo    | Yes (when `cmd` is `5`)    | Map     | Attribute details.                                                   |
| invalidAttribute | Yes (when the attribute is invalid) | Array   | Details of the invalid attribute.                                               |

## Samples

### Adding an attribute

#### Sample request
Add three attributes to a token.
```
{
    "cmd": 1,
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

#### Sample response

```
{
    "retCode": 0,
    "errMsg": "success",
    "invalidAttribute": [
        "high"   // The corresponding key value does not exist in the console
    ]
}
```
### Updating an attribute

#### Sample request
Update the value of the `name` attribute to `workman`.
```
{
    "cmd": 2,    
    "token": "04cac74a714f61bf089987a986363d88****",
    "attributeInfo": {
         "attributeMap": {
            "name": "workman"   
        }
    }
}



```
#### Sample response

```
{
    "retCode": 0,
    "errMsg": "success"
}
```

### Deleting an attribute

#### Sample request

Delete the `workman` value of the `name` attribute.
```
{
    "cmd": 3,    
    "token": "04cac74a714f61bf089987a986363d88****",
    "attributeInfo": {
         "attributeMap": {
            "name": "workman"  
        }
    }
}



```

#### Sample response

```
{
    "retCode": 0,
    "errMsg": "success"
}
```
### Deleting all attributes

#### Sample request

Delete all attributes of a token.
```
{
    "cmd": 4,    
    "token": "04cac74a714f61bf089987a986363d88****"  

}
```

#### Sample response

```
{
    "retCode": 0,
    "errMsg": "success"
}
```

### Querying attributes
#### Sample request
Query the attribute details of a token.
```
{
    "cmd": 5,    
    "token": "04cac74a714f61bf089987a986363d88****"

}
```

#### Sample response

```
{
    "retCode": 0,
    "errMsg": "success",
    "attributeInfo": {
        "attributeMap": {
            "nickname": "workman"
        }
    }
}
```

