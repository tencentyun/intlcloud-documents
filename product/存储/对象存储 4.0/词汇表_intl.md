Before getting started with COS, you need to understand the following basic concepts and terms.
### Bucket
A bucket is used to store objects in COS. Multiple objects can be stored in one bucket. A bucket name consists of a user-defined string and a system-generated numeric string, which are connected with a dash. This name structure can ensure the uniqueness of a bucket name. For more information, see [Bucket Overview](/document/product/436/13312).
### Object
An object is the basic unit stored in COS. For more information, see [Object Overview](/document/product/436/13324).
### Region
Region is where the COS' IDC is located. You can select the region for storing data by taking such factors as cost and request origin into consideration. It is recommended to select the nearest region based on your business scenario to maximize object upload and download speed. For more information, see [Region and Access Domain Name](/document/product/436/6224).
A region is specified when a bucket is created, and cannot be modified once being specified. All objects in the bucket are stored in the IDC in the region. You cannot set regions for objects.
### APPID
APPID is one of the Tencent Cloud account IDs, and is used to associate with cloud resources. After applying for a Tencent Cloud account successfully, you will be assigned an APPID automatically. APPID can be found in **Account Info** on the [Tencent Cloud Console](https://console.cloud.tencent.com/developer).
### API key
API key is the security credential used for authentication when a user accesses a Tencent Cloud API. An API key consists of SecretId and SecretKey. Multiple cloud API keys can be created under one user account. A user who does not have a cloud API key needs to create one by going to [Cloud API Key Console](https://console.cloud.tencent.com/capi), otherwise he or she will be unable to call the cloud APIs.
### SecretId 
SecretId is part of a cloud API key, and is used to identify the API caller.
### SecretKey
SecretKey is part of a cloud API key, and is used for signature string encryption and server-side signature string verification.
### Default access domain name
The default access domain name consists of bucket name, COS region ID and object name. The default access domain name uniquely points to an object in COS. After a user uploads an object, Tencent Cloud automatically creates a default access domain name for the object. For more information, see [Domain Name Management](/document/product/436/13396).
### CDN accelerating access domain name
A CDN accelerating access domain name consists of bucket name, CDN acceleration ID and object name. This domain name uniquely points to an object in COS. After a user uploads an object and enables CDN acceleration, Tencent Cloud automatically creates a CDN accelerating access domain name for the object, which speeds up the access through cache nodes deployed across the country. For more information, see [Configure CDN Acceleration](https://cloud.tencent.com/document/product/436/18424).

