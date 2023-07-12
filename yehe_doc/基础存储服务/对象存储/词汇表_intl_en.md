The following basic concepts and terms will help you get start with COS (Cloud Object Storage).
### Bucket
In COS, a bucket is for storing a object or multiple objects. A bucket name is a user-defined string connecting a system-generated numeric string with dash, thus ensuring that this bucket name is unique. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312).
### Object
An object is the basic unit stored in COS. For more information, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).
### Region
Region is where the IDC of your COS service is located. To optimize the service experience, you may select a region based on your budget and the request origin. We recommend you to choose a region closest to your customers to maximize object upload and download speed. For more information, see [Region and Access Domain Name](https://intl.cloud.tencent.com/document/product/436/6224).
You specify a region when creating a bucket. The specified region is unchangeable. All objects in the bucket are stored in the IDC in the specified region of that bucket, and specifying regions for objects is not supported.

### APPID
APPID, a Tencent Cloud account identifier, is used for associating cloud resources. You will be automatically assigned an APPID once your Tencent Cloud account is created successfully. You can find your APPID at **Account Info** on the [Tencent Cloud Console](https://console.cloud.tencent.com/developer).
### API key
API key is the security credential used for authentication when a user accesses a Tencent Cloud API. An API key consists of SecretId and SecretKey. Multiple cloud API keys can be created under one user account. A user who does not have a cloud API key needs to create one by going to [Cloud API Key Console](https://console.cloud.tencent.com/capi), otherwise he or she will be unable to call the cloud APIs.
### SecretId 
SecretId is part of a cloud API key, and is used to identify the API caller.
### SecretKey
SecretKey is part of a cloud API key, and is used for signature string encryption and server-side signature string verification.
### Default access domain name
The default access domain name consists of bucket name, COS region ID and object name. The default access domain name uniquely points to an object in COS. After a user uploads an object, Tencent Cloud automatically creates a default access domain name for the object.<!-- For more information, see [Domain Name Management]-->
### CDN accelerating access domain name
A CDN accelerating access domain name consists of bucket name, CDN acceleration ID and object name. This domain name uniquely points to an object in COS. After a user uploads an object and enables CDN acceleration, Tencent Cloud automatically creates a CDN accelerating access domain name for the object, which speeds up the access through cache nodes deployed across the country.<!-- For more information, see [Configure CDN Acceleration]-->

