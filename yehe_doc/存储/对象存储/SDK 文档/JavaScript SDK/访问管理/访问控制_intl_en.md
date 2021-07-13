## Overview

This document provides an overview of APIs and SDK code samples related to the access control lists (ACLs) for buckets and objects.

**Bucket ACL**

| API | Operation Name | Description |
| :----------------------------------------------------------- | :------------- | :-------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting a bucket ACL | Sets an ACL for a bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying a bucket ACL | Queries the ACL of a bucket |

**Object ACL**

| API | Operation | Description |
| :----------------------------------------------------------- | :----------- | :--------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | Setting an object ACL | Sets an ACL for an object in a bucket |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | Querying an object ACL | Queries the ACL of an object |

## Bucket ACL

### Setting a bucket ACL

#### Feature description

This API (PUT Bucket acl) is used to set an ACL for a bucket.

#### Use case

Set a bucket to allow public-read:

[//]: # (.cssg-snippet-put-bucket-acl)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    ACL: 'public-read'
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user full permission for a bucket:

[//]: # (.cssg-snippet-put-bucket-acl-user)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    GrantFullControl: 'id="qcs::cam::uin/100000000001:uin/100000000001",id="qcs::cam::uin/100000000011:uin/100000000011"' // 100000000001 is uin.
}, function(err, data) {
    console.log(err || data);
});
```

Modify bucket permission with `AccessControlPolicy`:

[//]: # (.cssg-snippet-put-bucket-acl-acp)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    AccessControlPolicy: {
        "Owner": { // `Owner` is required in `AccessControlPolicy`.
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 is the UIN of the bucket owner
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 is UIN
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| ACL | Defines the access control list (ACL) attribute of the bucket. For the enumerated values, such as `private` (default) and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). | String | No |
| GrantRead        | Grants a user read access in the format: id="[OwnerUin]".<br>Use a comma (,) to separate multiple users.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite        | Grants a user write access in the format: id="[OwnerUin]".<br>Use a comma (,) to separate multiple users.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantReadAcp | Grants a user read permission for bucket ACL and policies in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp | Grants a user write permission for bucket ACL and policies in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants full permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.</br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| AccessControlPolicy | A list of all the information about the CORS configuration | Object | No |
| - Owner | Object representing the bucket owner | Object | No |
| - - ID | Complete ID of the bucket owner in the format:  `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`,<br>such as `qcs::cam::uin/100000000001:uin/100000000001’, where 100000000001 is uin | String | No |
| - Grants | List of information on the authorized user and granted permissions | ObjectArray | No |
| - - Permission | Permission granted. Valid values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL`. For the enumerated values, please see the **Action permissions** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). | String | No |
| - - Grantee | Authorized user information | Object | No |
| - - - ID | Complete ID of the grantee in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`</br>Example: `qcs::cam::uin/100000000001:uin/100000000001` where 100000000001 is the uin | String | No |
| - - - DisplayName | String representing the username, which is usually the same as the string you enter for `ID` | String | No |
| - - - URI | Preset user groups. For more information, see the `Identity (Grantee)` section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583), such as <br>`http://cam.qcloud.com/groups/global/AllUsers` or <br>`http://cam.qcloud.com/groups/global/AuthenticatedUsers` | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name       | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |

### Querying a bucket ACL

#### Feature description 

This API (GET Bucket acl) is used to query the ACL of a bucket. To call this API, you need to have permission to read the ACL of the bucket.

#### Use case

[//]: # (.cssg-snippet-get-bucket-acl)
```js
cos.getBucketAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

```json
{
    "GrantFullControl": "",
    "GrantWrite": "",
    "GrantRead": "",
    "GrantReadAcp": "id=\"qcs::cam::uin/100000000011:uin/100000000011\"",
    "GrantWriteAcp": "id=\"qcs::cam::uin/100000000011:uin/100000000011\"",
    "ACL": "private",
    "Owner": {
        "ID": "qcs::cam::uin/100000000001:uin/100000000001",
        "DisplayName": "qcs::cam::uin/100000000001:uin/100000000001"
    },
    "Grants": [{
        "Grantee": {
            "ID": "qcs::cam::uin/100000000011:uin/100000000011",
            "DisplayName": "qcs::cam::uin/100000000011:uin/100000000011"
        },
        "Permission": "READ"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter  | Description | Type |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty. | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| x-cos-acl | Defines the access control list (ACL) attribute of the bucket. For the enumerated values such as `private` and `public-read`, see the `Preset ACLs for buckets` section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` |Enum| No
| - GrantRead                                                  | ID information of the user granted read access              | String      |
| - GrantWrite                                                 | ID information of the user granted write access   | String      |
| - GrantReadAcp                                               | ID information of the user granted read access to the ACL and Policies | String      |
| - GrantWriteAcp                                               | ID information of the user granted write access to the ACL and Policies | String      |
| - GrantFullControl                                           | ID information of the user granted full access                   | String      |
| - Owner                                                      | Bucket owner information     | Object      |
| - - DisplayName                                              | Bucket owner username | String      |
| - - ID | Bucket owner ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - Grants                                                     | List of information on the authorized user and granted permissions   | ObjectArray |
| - - Permission | Specifies the permission granted to the user. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | 
| - - Grantee                                                  | Authorized user information                                               | Object      |
| - - - DisplayName                                            | Authorized user’s username                              | String      |
| - - - ID | User ID of the authorized user <br>For root accounts, the format is `qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>` <br>or `qcs::cam::anyone:anyone` representing all users. <br>For sub-accounts, the format is `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String      |
| - - - URI | Preset user groups. For more information see the `Identity (Grantee)` section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583), such as <br>`http://cam.qcloud.com/groups/global/AllUsers` or <br>`http://cam.qcloud.com/groups/global/AuthenticatedUsers` | String |


## Object ACLs

### Setting object ACL

#### Feature description 

This API (PUT Object acl) is used to set the ACL of an object in a bucket.

> !The total number of policies associated with bucket ACL, Policy, and CAM under a single root account (i.e., under the same `APPID`) cannot exceed 1,000. There is no upper limit on the number of object ACL rules. If you do not need access control for an object, do not make any configuration, and the object will inherit the permissions of its bucket.

#### Use case 

[//]: # (.cssg-snippet-put-object-acl)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',              /* Required */
    ACL: 'public-read', /*Optional*/
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user all permissions for an object:

[//]: # (.cssg-snippet-put-object-acl-user)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',              /* Required */
    GrantFullControl: 'id="100000000001"' // 100000000001 is the uin of the root account.
}, function(err, data) {
    console.log(err || data);
});
```

Grant the user permission to write the object via `AccessControlPolicy`:

[//]: # (.cssg-snippet-put-object-acl-acp)
```js
cos.putObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',              /* Required */
    AccessControlPolicy: {
        "Owner": { // `Owner` is required in `AccessControlPolicy`.
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 is the UIN of the bucket owner
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 is the UIN of the sub-account of the bucket owner
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324) | String | Yes |
| ACL | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default` <br>**Note:** If you do not need access control for the object, set `default` for this parameter or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | String | No |
| GrantRead              | Grants a user read permission for an object in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"</code>.<br><li>To authorize a root account, use <code>id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"</code>.<br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| GrantFullControl       | Grants a user full access in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<ul  style="margin: 0;"><li>To authorize a sub-account, use <code>id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"</code>.</li><li>To authorize a root account, use <code>id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"</code>.<br>Example: <code>'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'</code></li></ul> | String | No   |
| AccessControlPolicy | Sets the object's ACL attributes. | Object | No |
| - Owner | Information about the object owner | Object | No |
| - - ID | ID of the object owner in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String | No |
| - - DisplayName | Name of the object owner | String | No   |
| - Grants | A list of information about the grantee and granted permissions | ObjectArray | No |
| - - Permission | Permission granted. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | No |
| - - Grantee | Information about the grantee | Object | No |
| - - - DisplayName | Name of the grantee | String | No |
| - - - ID | ID of the authorized user in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 204, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |

### Querying object ACL

#### Feature description 

The API is used to query the ACL of an object. Only the owner of the bucket has the permission to use this API.

#### Use case 

[//]: # (.cssg-snippet-get-object-acl)
```js
cos.getObjectAcl({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Key: 'exampleobject',              /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name, formatted as `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this parameter is left empty. | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Headers returned by the request | Object |
| - ACL | Defines the ACL attribute of the object. For the enumerated values, such as `default`, `private`, and `public-read`, please see the **Preset ACL** section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `default` <br>**Note:** If you do not need access control for the object, set `default` for this parameter or leave it empty. In this way, the object will inherit the permissions of the bucket it is stored in. | String |
| - Owner | Owner of the resource | Object |
| - - ID | Object owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - - DisplayName | Object owner name | String |
| - Grants | List of information on the grantee and permissions | ObjectArray |
| - - Permission | Permission granted. Enumerated values: `READ`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String |
| - - Grantee | Grantee information | Object |
| - - - DisplayName | Name of the user | String |
| - - - ID | User ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`</br>For root accounts, <OwnerUin> and <SubUin> have the same value. | String |





