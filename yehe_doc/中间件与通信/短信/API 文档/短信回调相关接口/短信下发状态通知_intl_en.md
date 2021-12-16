## API Description

### Feature description
This API is used for Tencent Cloud SMS to notify the business of the message sending status by calling back the service URL after an SMS message is sent to a user.

### Sample URL
```
POST http://example.com/sms/callback
```

## Request Parameters
The following table lists the request parameters.

| Parameter | Required | Type | Description |
|-------------------|------|--------|---------------------------------------------------------|
| user_receive_time | Yes | string | The time when the user actually receives the message |
| nationcode | Yes | string | Country/Region code |
| mobile | Yes | string | Mobile number |
| report_status | Yes | string | Whether the SMS message is actually received. Valid values: SUCCESS (success), FAIL (failure) |
| errmsg | Yes | string | Error message of receipt status code. For more information, see [Error Codes for SMS Sending and Receipt Status](https://intl.cloud.tencent.com/document/api/382/43546)  |
| description       | Yes   | string | Description of SMS receipt status.                                    |
| sid               | Yes   | string | Sending ID (corresponding to the `SerialNo` returned by the sending API)                                          |

>?A callback request may return the results of multiple SMS requests.

Sample request:

```json
[
    {
        "user_receive_time": "2015-10-17 08:03:04",
        "nationcode": "86",
        "mobile": "13xxxxxxxxx",
        "report_status": "SUCCESS",
        "errmsg": "DELIVRD",
        "description": "The SMS message is successfully delivered",
        "sid": "xxxxxxx"
    }
]
```

## Response Parameters
The following table lists the response parameters.

| Parameter | Required | Type | Description |
|--------|------|--------|------------------------------------------|
| result | Yes | number | Error code. 0: success; other values: failure |
| errmsg | Yes | string | When `result` is 0, it displays "OK", and when `result` is not 0, it displays a specific error message. |

Sample response:

```json
{
    "result": 0,
    "errmsg": "OK"
}
```

