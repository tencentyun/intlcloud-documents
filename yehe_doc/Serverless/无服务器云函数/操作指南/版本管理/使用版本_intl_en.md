
The version feature is mainly used to fix the function configuration and code and avoid the impact of development, debugging, and testing on the business. After [publishing a function version](https://intl.cloud.tencent.com/document/product/583/15371), you can use the version by invoking the function on the specified version.
> The `$LATEST` version is used for code development and testing.

### Version trigger

Currently, all published versions of functions can be independently bound to triggers. For the same function, different versions are independent of one another, and each trigger can independently trigger the function.
For the number of triggers, the following restrictions apply:
- Up to two triggers can be configured on the function trigger page.
For example, if you have created a `demo1` function on the function trigger page and bound two COS triggers to version 1 of the function, then you cannot add COS triggers for other versions of the function. Only new timer or CMQ topic triggers can be added.
- Function triggers configured in other products or services are not subject to this restriction.
For example, any number of API Gateway triggers can be configured to trigger the same function.

> To increase the maximum number for triggers (i.e. quota limit), you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

### TencentCloud API-Triggered Versions

When the `InvokeFunction` API of TencentCloud API is used to trigger a function invocation, the specific version to be triggered can be specified with the optional parameter `Qualifier`. Without this parameter, the `$LATEST` version will be triggered by default.

