## Overview
You can write SCF functions to handle your own business logic and trigger the functions through the management APIs exposed by SCF. The management APIs are collectively referred to as TencentCloud API in Tencent Cloud. By using the `Invoke` API of SCF, you can trigger and invoke functions as needed.
The detailed TencentCloud API call method can be found in [Invoke](https://intl.cloud.tencent.com/document/product/583/17243). TencentCloud API triggers have the following characteristics:
- **Invocation method**: the sync or async triggering method can be defined according to the `InvocationType` parameter.
- **Custom event**: the event or data content that triggers the function can be defined according to the `ClientContext` parameter, and the content has to be encoded in JSON format.

## TencentCloud API Call
To trigger a function through TencentCloud API, you need to:
1. [Authenticate the API](https://intl.cloud.tencent.com/document/product/583/17239);
2. [Enter the common parameters](https://intl.cloud.tencent.com/document/product/583/17238);
3. Parse the [returned result](https://intl.cloud.tencent.com/document/product/583/17240).

In addition, if you do not want to construct or parse the request content on your own, you can directly use the TencentCloud API SDK for Python, PHP, Java, Go, .NET, or Node.js to trigger functions. For more information on how to use the SDK, please see [SDK](https://intl.cloud.tencent.com/document/product/494).

