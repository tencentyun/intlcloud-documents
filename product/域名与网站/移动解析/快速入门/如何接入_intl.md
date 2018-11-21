>Note:
>When you are using the free edition or the enterprise edition without using the SDK, **the LocalDNS resolution method has to be retained as an alternative** during the accessing process. For details, see [here](/doc/product/379/bestpractices).

### 1. Activating the Service
You need to activate the HttpDNS service in the console first.
Currently, activation is only allowed for accounts verified as organizations.

>Note: Individual developers can use the free API for accessing. For details, see [API documentation](https://cloud.tencent.com/document/product/379/3524).
Organization users can also test the service with the free API first.

### 2. Using HttpDNS API to Resolve a Domain Name
Once the service is activated, the authorization ID and key will be sent to you via email.

Only after obtaining the authorization ID and key can you request resolution in the format of `http://119.29.29.29/d?dn=[encrypted domain name string]&id=[authorization ID]&ttl=1`.

For detailed encryption method, see [Encryption Guidelines](https://cloud.tencent.com/document/product/379/3530).

### 3. Transforming the Client
>Change the resolution method of the client to HttpDNS resolution. Please note that **the LocalDNS resolution method has to be retained as an alternative** during the accessing process. For details, see [here](/doc/product/379/bestpractices).

### 4. Applying for SDK Use (Optional)
Enterprise edition users can apply for access through SDK. Tencent Cloud provides Tencent's proprietary **Zhiying Analysis SDK** which supports customization and direct embedding in apps for calling and has been widely used in various game clients of Tencent with sophisticated and stable functionality.

For details, see the following documents:
[SDK for iOS >>](https://cloud.tencent.com/document/product/379/6469)
[SDK for Android >>](https://cloud.tencent.com/document/product/379/6470)
