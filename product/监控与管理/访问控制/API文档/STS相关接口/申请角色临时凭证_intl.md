## API Description
This API (AssumeRole) is used to request temporary credentials for a role.
Request domain name:

```
sts.api.qcloud.com
```

## Input Parameters
The following request parameter list only provides the API request parameters. Other parameters can be found in [Common Request Parameters](https://intl.cloud.tencent.com/document/api/213/6976).

| Parameter Name | Required | Type | Description |
| ------------ | ------------ | ------------ | ------------ |
| roleArn | Yes | String | Description of a role's resources. For example: qcs::cam::uin/12345678:role/4611686018427397919, qcs::cam::uin/12345678:roleName/testRoleName. |
| roleSessionName | Yes | String | User-defined name of a temporary session |
| durationSeconds | No | Int | The validity period of the temporary credentials (in seconds). Default is 1,800 seconds. The maximum value is 7,200 seconds. |

## Output Parameters

| Parameter Name | Type |Description |
| ------------ | ------------ | ------------ |
| credentials | [credentials](#dataStructure) | The object contains a triad of token, tmpSecretId and tmpSecretKey. |

<span id="dataStructure"></span>
## Credential Data Structures

| Parameter Name | Type |Description |
|---------|---------|---------|
| token | String | Token value |
| tmpSecretId | String | Temporary security certificate ID |
| tmpSecretKey | String | Temporary security certificate ID |

## Example
#### Input

```
https://sts.api.qcloud.com/v2/index.php?Action=AssumeRole&roleArn=qcs%3a%3acam%3a%3auin%2f12345678%3arole%2f4611686018427397919
&roleSessionName=abc&durationSeconds=1800&<Common request parameters>
```

#### Output

```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "credentials": {
            "sessionToken": "5e776c4216ff4d31a7c74fe194a978a3ff2a42864",
            "tmpSecretId": "AKIDcAZnqgar9ByWq6m7ucIn8LNEuY2MkPCl",
            "tmpSecretKey": "VpxrX0IMCpHXWL0Wr3KQNCqJix1uhMqD"
        },
        "expiredTime": 1506433269,
        "expiration": "2017-09-26T13:41:09Z"
    }
}
```

