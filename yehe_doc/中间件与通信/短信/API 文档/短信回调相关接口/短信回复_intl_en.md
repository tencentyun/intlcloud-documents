## API Description

### Feature description
This API is used for Tencent Cloud SMS to notify the business of the SMS reply by calling back the service URL after a user receives an SMS message and replies to it.

### Sample URL
```
POST http://example.com/sms/callback
```

## Request Parameters
The following table lists the request parameters.

| Parameter | Required | Type | Description |
|------------|------|--------|----------------------------------------------|
| extend | No | string | Extended code of the channel, which is disabled by default (an null value must be entered) |
| mobile | Yes | string | Mobile number |
| nationcode | Yes | string | Country/Region code |
| sign       | Yes   | string | SMS signature                                     |
| text       | Yes   | string | User reply                               |
| time | Yes | number | Unix timestamp in seconds           |

Sample request:

```json
{
    "extend": "Extended code",
    "mobile": "13xxxxxxxxx",
    "nationcode": "86",
    "sign": "SMS signature",
    "text": "User reply",
    "time": 1457336869
}
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

