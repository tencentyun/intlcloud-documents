## Feature Description

Through this callback, the app backend can view the user deletion from blocklist in real time.

## Precautions

- To enable this callback, you must configure the callback URL and toggle on the corresponding protocol. For details on the configuration method, see [Third-Party Callback Configuration](https://intl.cloud.tencent.com/document/product/1047/34520).
- Callback direction: The IM backend initiates an HTTP POST request to the app backend.
- After receiving the callback request, the app backend must check whether the SDKAppID contained in the request URL is consistent with its own SDKAppID.
- For other security-related issues, see [Third-Party Callback Overview: Security Considerations](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.AE.89.E5.85.A8.E8.80.83.E8.99.91).

## Callback Triggering Scenarios

- An app user uses a client to initiate a request to remove users from blocklist.
- The app backend initiates a request to remove users from blocklist through the RESTful API.

## Callback Triggering Time

The callback is triggered after the IM backend receives a request to remove users from blocklist and successfully remove the users.

## API Description

### Request URL example

In the following example, the callback URL configured in the app is `https://www.example.com`.
**Example:**

```
https://www.example.com?SdkAppid=$SDKAppID&CallbackCommand=$CallbackCommand&contenttype=json&ClientIP=$ClientIP&OptPlatform=$OptPlatform
```

### Request parameters

| Parameter       | Description                                                  |
| --------------- | ------------------------------------------------------------ |
| https           | The request protocol is HTTPS, and the request method is POST. |
| www.example.com | The callback URL.                                            |
| SdkAppid        | The SDKAppID assigned by the IM console when an application is created. |
| CallbackCommand | The value is fixed to Sns.CallbackBlackListDelete.           |
| contenttype     | The value is fixed to JSON.                                  |
| ClientIP        | The client IP address, whose format is similar to: 127.0.0.1. |
| OptPlatform     | The client platform. For details on the possible values, see the OptPlatform parameter in [Third-Party Callback Overview: Callback Protocols](https://intl.cloud.tencent.com/document/product/1047/34354#.E5.9B.9E.E8.B0.83.E5.8D.8F.E8.AE.AE). |

### Request packet example

```
{
    "CallbackCommand": "Sns.CallbackBlackListDelete",
    "PairList": [
        {
            "From_Account": "id",
            "To_Account": "id1"
        },
        {
            "From_Account": "id",
            "To_Account": "id2"
        },
        {
            "From_Account": "id",
            "To_Account": "id3"
        }
    ]
}
```

### Request packet fields

| Field           | Type   | Description                                                  |
| --------------- | ------ | ------------------------------------------------------------ |
| CallbackCommand | String | The callback command.                                        |
| PairList        | Array  | The account pair for which the deletion from blocklist is successful. |
| From_Account    | String | From_Account deletes To_Account from its blocklist.          |
| To_Account      | String | To_Account is deleted from the blocklist of From_Account.    |

### Response packet example

```
{
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "ErrorInfo": ""
}
```

### Response packet fields

| Field        | Type    | Attribute | Description                                                  |
| ------------ | ------- | --------- | ------------------------------------------------------------ |
| ActionStatus | String  | Required  | The request processing result. OK: succeeded. FAIL: failed.  |
| ErrorCode    | Integer | Required  | The error code. 0 indicates that app backend processing was successful, and 1 indicates that app backend processing failed. |
| ErrorInfo    | String  | Required  | Error information.                                           |

## References

- [Third-party callback overview](https://intl.cloud.tencent.com/document/product/1047/34354)
- RESTful APIs: [Adding users to the blocklist](https://intl.cloud.tencent.com/document/product/1047/34911)
