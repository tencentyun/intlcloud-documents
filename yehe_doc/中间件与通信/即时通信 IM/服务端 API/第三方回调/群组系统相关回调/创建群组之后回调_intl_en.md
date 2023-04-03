## Feature Overview

This callback allows you to view the information of the group created by the user on the application backend in real time. Specifically, it notifies the application backend of the successful group creation so that the backend can sync data.

## Notes

- To enable this callback, you must configure a callback URL and toggle on the corresponding protocol. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

- An app user creates a group successfully on the client.
- The app admin creates a group successfully through the RESTful API.

## Callback Triggering Timing

It will be triggered after a group is created successfully.

## API Calling Description

### Sample request URL

In the following sample, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | Callback URL                                                 |
| SdkAppid        | The `SDKAppID` assigned by the IM console when the app is created |
| CallbackCommand | Fixed value: `Group.CallbackAfterCreateGroup`.               |
| contenttype     | Fixed value: `JSON`.                                         |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocols** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
 {
    "CallbackCommand": "Group.CallbackAfterCreateGroup", // Callback command
    "GroupId" : "@TGS#2J4SZEAEL",
    "Operator_Account": "group_root", // Operator
    "Owner_Account": "leckie", // Group owner
    "Type": "Public", // Group type
    "Name": "MyFirstGroup", // Group name
    "MemberList": [ // Initial member list
        {
            "Member_Account": "bob"
        },
        {
            "Member_Account": "peter"
        }
    ],
    "UserDefinedDataList": [ // Custom field to be used when the user creates a group
        {
            "Key": "UserDefined1",
            "Value": "hello"
        },
        {
            "Key": "UserDefined2",
            "Value": "world"
        }
    ],
    "EventTime":"1670574414123"// Event trigger timestamp in milliseconds		
}
```

### Request fields

| Field               | Type    | Description                                                  |
| ------------------- | ------- | ------------------------------------------------------------ |
| CallbackCommand     | String  | Callback command                                             |
| groupID             | String  | The group ID.                                                |
| Operator_Account    | String  | `UserID` of the operator who initiates the group creation request |
| Owner_Account       | String  | `UserID` of the owner of the group to be created             |
| Type                | String  | Type of the group to be created (for more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529)), such as `Public`. |
| Name                | String  | Name of the group to be created                              |
| MemberList          | Array   | Initial member list of the group to be created               |
| UserDefinedDataList | Array   | Custom field for group creation, which is unavailable by default and needs to be enabled. For more information, see [Group Management](https://www.tencentcloud.com/document/product/1047/33530#.E8.87.AA.E5.AE.9A.E4.B9.89.E5.AD.97.E6.AE.B5). |
| EventTime           | Integer | Event trigger timestamp in milliseconds                      |

### Sample response

A response is sent after the app backend synchronizes the data.

```
{
    "ActionStatus": "OK",
    "ErrorInfo": "",
    "ErrorCode": 0 //The value `0` indicates that the callback result is ignored.
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. `OK`: Successful; `FAIL`: Failed             |
| ErrorCode    | Integer | Yes      | Error code. The value `0` indicates that the callback result is ignored. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References
- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful API: [Creating a Group](https://intl.cloud.tencent.com/document/product/1047/34895)
