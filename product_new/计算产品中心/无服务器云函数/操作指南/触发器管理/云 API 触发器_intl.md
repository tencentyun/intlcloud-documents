## Overview
You can write SCF functions to handle your own business logic and trigger the functions through the management APIs exposed by the SCF. The management APIs are collectively referred to as TencentCloud API in Tencent Cloud. By using the Invoke API of SCF, you can trigger and call functions as needed.
The detailed TencentCloud API calling method can be found in the [function execution API document](https://cloud.tencent.com/document/product/583/17243). TencentCloud API triggers have the following characteristics:
- **Call method**: The sync or async trigger can be defined according to the InvocationType parameter.
- **Custom event**: The event or data content that triggers the function can be defined according to the ClientContext parameter, and the content has to be encoded in JSON format.

## TencentCloud API Call
To trigger a function through TencentCloud API, you need to:
1. [Authenticate the API](https://cloud.tencent.com/document/product/583/17239);
2. [Enter the common parameters](https://cloud.tencent.com/document/product/583/17238);
3. Parse the [returned result](https://cloud.tencent.com/document/product/583/17240).

In addition, if you do not want to construct or parse the request content on your own, you can directly use the TencentCloud API SDK to trigger functions. The TencentCloud API SDK provides implementations for Python, PHP, JAVA, GO, .NET, and Node.js languages. The detailed usage of each language-specific SDK can be found in [Tencent Cloud SDK Center](https://cloud.tencent.com/document/sdk).
