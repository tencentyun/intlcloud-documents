## Feature Description

This callback allows you to view the profile update operations by users in real time on the app backend.

## Notes

- To enable this callback, you must configure a callback URL and toggle on the corresponding protocol. For more information on the configuration method, see [Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- During this callback, the IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the `SDKAppID` contained in the request URL is the `SDKAppID` of the app.
- For more security considerations, see the **Security Considerations** section in [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354).

## Callback Triggering Scenarios

- App users modify their profiles through the client.
- App admins modify user profiles through RESTful APIs.

## Callback Triggering Timing

This callback is triggered after the user profile is successfully modified.

## API Description
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
| CallbackCommand | Fixed value: `Profile.CallbackPortraitSet`.                  |
| contenttype     | Fixed value: json                                            |
| ClientIP        | Client IP, such as 127.0.0.1                                 |
| OptPlatform     | Client platform. For valid values, see the description of `OptPlatform` in the **Callback Protocol** section of [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354). |

### Sample request

```
{
  "CallbackCommand": "Profile.CallbackPortraitSet",
  "Operator_Account": "id1",
  "From_Account": "id1",
  "EventTime": 1656921052497,
  "ProfileItem": [
    {
      "Tag": "Tag_Profile_IM_Nick",
      "Value": "nick1"
    },
    {
      "Tag": "Tag_Profile_IM_Gender",
      "Value": "Gender_Type_Male"
    },
    {
      "Tag": "Tag_Profile_IM_AllowType",
      "Value": "AllowType_Type_NeedConfirm"
    },
    {
      "Tag": "Tag_Profile_Custom_Data",
      "Value": "your custom data"
    }
  ]
}
```

### Request fields

| Field            | Type          | Description                                                  |
| ---------------- | ------------- | ------------------------------------------------------------ |
| CallbackCommand  | String        | Callback command                                             |
| Operator_Account | String        | `UserID` of the user who triggers the update operation       |
| From_Account     | String        | `UserID` of the user who updates the profile                 |
| EventTime        | Integer       | Timestamp in milliseconds                                    |
| ProfileItem      | Array         | List of successfully updated user profile items              |
| Tag              | String        | Field name of the successfully updated profile. For more information, see [Profile Management](https://intl.cloud.tencent.com/document/product/1047/33520). |
| Value            | uint32/string | Value of the successfully updated profile field. For more information, see [Profile Management](https://intl.cloud.tencent.com/document/product/1047/33520). |

### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "ErrorInfo": ""
}
```

### Response fields

| Field        | Type    | Required | Description                                                  |
| ------------ | ------- | -------- | ------------------------------------------------------------ |
| ActionStatus | String  | Yes      | Request result. OK: succeeded; FAIL: failed.                 |
| ErrorCode    | Integer | Yes      | Error code. 0: the app backend processing succeeded; 1: the app backend processing failed. |
| ErrorInfo    | String  | Yes      | Error information                                            |

## References

- [Third-Party Callback Overview](https://intl.cloud.tencent.com/document/product/1047/34354)
