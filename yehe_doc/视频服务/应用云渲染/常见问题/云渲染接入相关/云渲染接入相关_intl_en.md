### What preparations should I make before integration?
Please see [Integration Preparations](https://intl.cloud.tencent.com/document/product/1158/49607).

### Does the `Region` parameter in CAR TencentCloud APIs indicate the concurrency pack region?
No. `Region` is a common parameter of CAR TencentCloud APIs and doesn't need to be specified, as CAR will select the optimal access region based on `UserIP`.

### Does CAR support user queuing?
The queue page of CAR needs to be developed by you. For more information, see [Queue Feature](https://intl.cloud.tencent.com/document/product/1158/49615#.E6.8E.92.E9.98.9F.E5.8A.9F.E8.83.BD).

### What do `UserId` and `RequestId` mean respectively?
`UserId` is the custom unique user identifier passed in to CAR, such as `user123456`. After CAR receives the requested TencentCloud API, it will return a `RequestId`, such as `01fdc815-c4e7-4642-819e-a011856dfd5a1`, to the business.

### How do I view `RequestId`?
1. Get `RequestId` of `CreateSession` on the **Network** tab in Chrome DevTools.
2. The returned values of the TencentCloud API include `RequestId`. We recommend you record it on the business backend.

### Can I get the public IP of the CAR resources to implement access allowlists or other features?
No. The public IP provided by CAR is not fixed, so you need to open UDP port 8000 to all source IPs. If there are no special security problems, we recommend you open all UDP ports.
