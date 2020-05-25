
The version feature is mainly used to fix the function configuration and code and avoid the impact of development, debugging, and testing on the business. After [publishing a function version](https://intl.cloud.tencent.com/document/product/583/15371), you can use the version by invoking the function on the specified version.
> The `$LATEST` version is used for code development and testing.

### Version trigger

Currently, all published versions of functions can be independently bound to triggers. For the same function, different versions are independent of one another, and each trigger can independently trigger the function.
> There is a limit to the number of triggers under one user account. For more information, please see [Quota Limits](https://intl.cloud.tencent.com/document/product/583/11637). To increase the maximum number of triggers (i.e., quota limit), you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for application.

### TencentCloud API-Triggered Versions

When the `InvokeFunction` API of TencentCloud API is used to trigger a function invocation, the specific version to be triggered can be specified with the optional parameter `Qualifier`. Without this parameter, the `$DEFAULT` alias will be triggered by default.

