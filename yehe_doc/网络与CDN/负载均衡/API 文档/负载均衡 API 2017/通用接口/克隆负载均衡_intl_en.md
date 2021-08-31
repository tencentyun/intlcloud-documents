## API Description
This API is used to clone all configurations of a CLB instance, including its attribute, security group, listener and real server bound.
Domain name for API calls: `lb.api.qcloud.com`
>!
- If there are many CLB configurations, the API tends to time out. Please wait patiently.
- The API does not support concurrent calls.
- Currently, a classic CLB instance cannot be cloned.
- All the cloned CLB instances are pay-as-you-go. The cloned ones will be automatically deleted once the clone fails.
- All the cloned CLB instances are named after “cloneFrom-lb-xxx” (a clone from the `lb-xxx` CLB instance).

## Request Parameters
The list below contains only the API request parameters. Common parameters should be added when you call the API. For more information, see [Common Request Parameters](https://intl.cloud.tencent.com/document/product/214/11594). The `Action` field for this API is `CloneLB`.

| Parameter | Required | Type  | Description                                           |
|---------|---------|---------|---------|
| loadBalancerId | Yes | String | CLB instance ID. |
| cloneType | Yes | String | Clone type.<li>all: both the listener and the RS binding relationship will be cloned.</li><li>onlyListener: only the listener will be cloned, but the RS binding relationship will not. </li> |
|zone | No |String | Availability zone in which the CLB instance is cloned. It is the same as that specified in [purchase parameters](https://intl.cloud.tencent.com/document/product/214/1254). |

## Response Parameters
| Parameter | Type | Description |
|---------|---------|---------|
| cloneLBId | String | ID of new CLB instances from the clone.|

## Example
Request
```
https://lb.api.qcloud.com/v2/index.php?Action=CloneLB
&<Common request parameters>
&loadBalancerId=lb-xxx
&cloneType=all
```
Response
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "cloneLBId": "lb-sss"
}
```


