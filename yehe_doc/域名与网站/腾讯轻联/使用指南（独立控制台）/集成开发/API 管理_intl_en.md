
## Overview
With many new APIs launched every day, and more and more enterprises starting to open up their web APIs, API use cases are increasing. Nowadays, the number of daily API calls is surging, and how to manage these APIs securely and efficiently has become a challenge to enterprises.

iPaaS offers the API publishing feature, which allows you to quickly package published apps to generate APIs for users to manage and call, and provides API management capabilities to control access permissions and traffic scheduling for APIs.

## Directions
### API Management Page

Log in to the [iPaaS console](https://ipaas.tencentcloud.com/login) and click **Integration development** > **APIs** on the left sidebar.

On the **APIs** page, you can create or view API services, view API catalogs, manage API subscription credentials, and manage the approvals.
![](https://qcloudimg.tencent-cloud.cn/raw/a1b9c723d79940bd0b733b07f4262aeb.png)
There are three API service status: configuring, running, and stopped. You can hover to see service domain name to view the publishing environment and domain name of the API service.
The operations supported by the API service include: view, create new API, lauch, remove, delete, view description files, and view release history.

### Creating an Service

The API management feature supports OpenAPI Specification v3.0.0. For the object definitions of OpenAPI Specification v3.0.0, see [OpenAPI Specification](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.0.md). You can click **Create** to enter the API creation page.

There are two ways to create an API service: including manually creating and importing service.

<dx-tabs>
::: Creating an API service by importing a description file
1. On the [APIs] page, click **Import API service**. On the **Basic settings** page, configure the following information and click **Next**.
	- Upload description file: Upload a YAML or JSON file up to 100 KB in size.
	- File format: Select **YAML** or **JSON**. 
![](https://qcloudimg.tencent-cloud.cn/raw/da6d1ec5b7f13dcab948ff267b8ecab3.png)

2. On the **Policy info** page, configure the following information and click **Done** to create the API service.
 - Access control by IP: You can enable this as needed. After it is enabled, you can enter multiple IPs to restrict access based on the allowlist/blocklist.
 - Request rate limit: The maximum number of allowed access requests per unit of time from the configuration time. Value range: 1–1000.
![](https://qcloudimg.tencent-cloud.cn/raw/4707295ce1aabcc031562c5ca7f97fb7.png)
:::
::: Creating an API service manually
1. On the [APIs] page, click **Create**. On the **Basic settings** page, configure the following information and click **Next**.
 - Service name: Enter an API name.
 - Protocol: Select **HTTP**, **HTTPS**, or **HTTP&HTTPS**.
 - Group: You can configure groups if you want to group API services and quickly filter them by group.
 - Description (optional): Enter a simple description of the API service.
![](https://qcloudimg.tencent-cloud.cn/raw/d4aba705d333c1af1d464fddc4c47fd5.png)

2. On the **Policy info** page, configure the following information and click **Done** to create the API service.
 - Access control by IP: You can enable this as needed. After it is enabled, you can enter multiple IPs to restrict access based on the allowlist/blocklist.
 - Request rate limit: The maximum number of allowed access requests per unit of time from the configuration time. Value range: 1–1000.
![](https://qcloudimg.tencent-cloud.cn/raw/4707295ce1aabcc031562c5ca7f97fb7.png)
:::
</dx-tabs>


### Creating an API

After we have created an API service, we can start editing its specific API. Including API request path, request method, authentication policy, request parameters, policy settings, backend service type and other operations.
There are 3 steps to create a new API (The appendix uses postman as an example to introduce how to call the API from the user side).

#### Step 1: Basic configuration
![](https://qcloudimg.tencent-cloud.cn/raw/e72ece717d327eb6094b6e161498ae26.png)
API name and description support customization. For grouping, you can choose the default grouping or create a new grouping.
- Request method: GET, POST, PATCH, PUT, DELETE, HEAD.
- Authentication strategy: NoAuth, BasicAuth, OAuth2.0, HMAC.
- Backbounce service type: integration stream, third-party service, database, Mock. The request parameters of integration flow, third-party service, and Mock can be added by yourself, up to 30.
![](https://qcloudimg.tencent-cloud.cn/raw/bdf8c20d5b0e803c8fc6c97d850f3fe7.png)

#### Step 2: Backend configuration
![](https://qcloudimg.tencent-cloud.cn/raw/13de663e8b98fcf03e3e5d00d95d3890.png)
- Backend resource path: Take the integration flow backend service as an example, here you need to select the integration flow triggered by webhook.
- Backend timeout period: It can be preset by default or customized.
- Request method: choose according to user needs. Support: GET, POST, PATCH, PUT, DELETE, HEAD.
- Parameter definition: Support configuration of front-end and back-end parameter mapping.

#### Step 3: Response configuration
Support configuration response example and error code configuration.
![](https://qcloudimg.tencent-cloud.cn/raw/0c507c57e4f001ad05940b60fc3b989f.png)
When all the above configurations are completed, click **Finish**, and the API list will be returned, and the created API information will be displayed here.

### API list
The created API will be displayed in the API list, and you can create, view and edit APIs on this page. You can publish APIs, set and view API description files and call credentials, and view API subscription details.
![](https://qcloudimg.tencent-cloud.cn/raw/ec26d3b455494ae7b1cbf70298743d27.png)
​
The left side is the API list, and the default tab page on the right side is the detailed configuration information of the API: API access path, request method, parameters, backend service type, etc. can be viewed here.
​
1. Click the **Debug** tab page to enter the API debugging page. On the API debugging page, you can configure the request Header and Body content of this API Endpoint, and click **Send Request**.
![](https://qcloudimg.tencent-cloud.cn/raw/40d0a4cbb55acc92a5f88e9e4518c573.png)
2. The test results are then available. We will return the Response status code and result returned by the backend service to the user for further debugging.
3. Click **Publish** in the upper right corner to publish this API to the corresponding environment.
![](https://qcloudimg.tencent-cloud.cn/raw/f0733f950f62484bb53122014a4b90a4.png)
4. After release, the API status after release is **Running**.
5. **Copy** in the upper right corner can overwrite the current version to the version in the configuration. After replication, the API service can be published again. An API service can be published to multiple environments.
6. You can view its logs and monitoring on the API details page. For detailed information on logs and monitoring, see [Operation and Maintenance Center-Monitoring Management](https://cloud.tencent.com/document/product/1270/80363) and [Operation and Maintenance Center-Running Log](https://cloud.tencent .com/document/product/1270/80364).
7. After the API service is released, the service can be stopped.

### Description file
The description file is a description for the current API service. The YAML/JSON format file is displayed on the left, and the Swagger visualization content is displayed on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/8307e6e4997e374f0f5cc1245d303d29.png)

### Call Credentials
When creating an API service, if the selected authentication strategy is NoAuth, this option can be ignored. Conversely, if the API service requires authentication, you need to configure the calling credentials on this page. With any calling credentials under the current service, you can call any API under the service.
![](https://qcloudimg.tencent-cloud.cn/raw/875578d6850e39fb7ee41c618c3fd0c3.png)
The above picture is the certificate list page, the created certificate will be displayed here, select **New Credential** to create a new certificate. Customize the credential information and save it.

### Subscription Details
The listed API service can be subscribed and invoked by all sub-UINs under the business owner's UIN. This menu allows you to view the status of the current API service being subscribed.
![](https://qcloudimg.tencent-cloud.cn/raw/207e14152837258de23bbd355a9d2ce2.png)
Here you can see a list of all users who have subscribed to the API, and at the same time, you can remove a user's subscription.

### operation
#### Delete API service
Click **Delete** to delete the current API service. After deletion, all configurations under the API service will be cleared and cannot be restored. The running service cannot be deleted directly, it needs to be stopped first and then deleted.
![](https://qcloudimg.tencent-cloud.cn/raw/cf39fb82eb9cee0c28b33ada2c134deb.png)

#### API Launch and Remove
- Launch: The running API service can be shared with other employees of the enterprise through the **shelf** function. Submit the listing application at the **API Service** > **Operation** > **More** > **Launch** path. The submitted API service will be reviewed by the enterprise administrator. After the review is passed, it can be displayed on the API In the directory, it is supported to be subscribed by all sub-accounts under the current main account.
- Remove: After the API service is put on the shelf, if you do not want to continue to be subscribed by other employees, you can complete it by taking it off the shelf. Submit an application for removal from **API Service** > **Operation** > **More** > **Removal**. After submitting the application, you need to contact the system administrator or the project administrator of the project for review , it can be taken off the shelf after the review is passed, and the API cannot be subscribed after it is taken off the shelf. The delisted API service will be moved out of the API directory.
![](https://qcloudimg.tencent-cloud.cn/raw/c89a91ac0efababd8ec43d0045548c9a.png)

#### View release history
Published API services can change state, environment, etc. Go to **API Service** > **Operations** > **More** > **View Release History** path. This function can view the historical situation after the release of the API service (up to 10 items can be displayed).
![](https://qcloudimg.tencent-cloud.cn/raw/60d110fcbce3af83455970072ca6cb2f.png)


### API catalog
The API catalog displays listed API services. Similar to an API service market, after the service is put on the shelf, it is not limited to the project dimension, and can be viewed, subscribed to and called by all sub-accounts under the current admin account. This page provides a quick search for services by their properties. At the same time, you can apply for subscription or unsubscribe API service.
![](https://qcloudimg.tencent-cloud.cn/raw/0ee88c14ce6ceeedcb7b5a50a59b343e.png)

#### Subscribe
When applying for API service subscription, you need to select or create a new subscription certificate. Associate the credentials with the API service. After being approved by the system administrator, you can successfully subscribe.
![](https://qcloudimg.tencent-cloud.cn/raw/c0c06ccc3810dca2ca342e3e5b902df6.png)

#### Unsubscribe
After canceling the subscription, the API service cannot be called, and this operation does not need to be reviewed by the system administrator.

### Subscription Credentials
This list can display or search for all subscription certificates, and at the same time, new certificates can be created. Subscription credentials are used to subscribe to services in the API catalog. Credentials are keys to an API service. When applying to subscribe to the API service, associate the credential with the API service, fill in the credential when calling, and the service can be called successfully. At the same time, you can see the Key and Secret of various authentication types of the credential, which can be directly copied when calling.
![](https://qcloudimg.tencent-cloud.cn/raw/36554efed79855b3b4b7239bd8a89e84.png)
One credential supports association with multiple API services. All API services associated with this credential can be viewed on the **subscribed API** tab page.
![](https://qcloudimg.tencent-cloud.cn/raw/2551c27add492ef959c705f3d8002f9d.png)
When creating a new credential, you can customize the relevant attributes.


### Approvals Management
Approvals management is divided into two functions: my applications and my approvals. Matters related to approvals are handled on this function page.
- Submitted by me: Displays all review information submitted by an individual. All characters are visible.
![](https://qcloudimg.tencent-cloud.cn/raw/79ad54380e482611db953377950a5121.png)
- I Reviewed: This page shows the information that needs to be reviewed. Visible only to System Admin and Project Admin roles. Other role access page data is empty.
  - The system administrator approves all requests for project API service delisting or API service subscription.
  - The project administrator approves the request for API service release or API service subscription within the project.
  ![](https://qcloudimg.tencent-cloud.cn/raw/1fa2a55139952a724c4f5d27e330191b.png)


## API call examples
### Call the API from the user side (take postman as an example)
- NoAuth:
![](https://qcloudimg.tencent-cloud.cn/raw/c8f0989e13ad33d5180ae002220ded34.png)
- BasicAuth:
   1. Copy the calling address of the API (the API service must be successfully published first):
![](https://qcloudimg.tencent-cloud.cn/raw/a9cc133d1eaf38041879a94cd3d90d39.png)
   2. Enter the API list page, create or open the existing "Call credentials" to view the AK/SK information used for BasicAuth:
![](https://qcloudimg.tencent-cloud.cn/raw/8276c2eaf4e7493dca9a5886c14fc610.png)
   3. Open postman, and fill in the API call address obtained above and the AK/SK information used for BasicAuth respectively:
![](https://qcloudimg.tencent-cloud.cn/raw/32d532e45c22b2b98b54d66439afa71b.png)
- OAuth2.0:
   1. Copy the call address of the API (the API service needs to be successfully published first), the method is the same as above.
   2. Enter the API list page, create or open the existing "Credentials" to view the AK/SK information for OAuth2.0:
![](https://qcloudimg.tencent-cloud.cn/raw/cea66a48609ad674467ab1324cfd1c5f.png)
   3. Enter the API list page, click and copy the "View token URL" corresponding to the API.
![](https://qcloudimg.tencent-cloud.cn/raw/48bd0ad53a188d2f3204a3d60138e77b.png)
   4. Create a new request in postman to get accsee_token.
       - First, enter the "Token acquisition link" obtained in step 3 in the input field, and select the GET request method.
       - Next, select the Params tab, and enter the AK/SK information for OAuth2.0 obtained in step 2 (see the figure below for the format).
       - Finally, click the **send** button to generate the "access_token" content in the figure below and copy it.
![](https://qcloudimg.tencent-cloud.cn/raw/8f147349be87da1da052d190533284e2.png)
   5. Re-open a request interface in postman, fill in the API call address obtained in step 1, and select OAuth2.0 for Type. And fill in the accsee_token obtained in step 4 on the right, and click **send** to see the access result (if you also set request parameters when configuring the API, you must also enter it here by location).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/WbI2107_d0a87645936d9984932bb34a74cc21fe.png)

- HMAC:
  1. Copy the call address of the API (the API service needs to be successfully published first), the method is the same as above, no more drawings.
  2. Enter the API service details page, create or open the existing "Call Credentials", and you can view the AK/SK information used for HMAC:
![](https://qcloudimg.tencent-cloud.cn/raw/96cd886f9854eacba0d0777279087f4a.png)
  3. Open postman, and fill in the API call address obtained in step 1 in the input box.
  4. Switch postman to the Pre-request Script tab, and paste the following code segment (note that the HMAC Key and Secret obtained in step 2 are used to replace the hmac_key and hmac_secret variable values in the code segment).
![](https://staticintl.cloudcachetci.com/yehe/backend-news/9EpR147_66845f28a4d9e8e4aae3d689d73c85ef.png)

```
var hmac_key = "2e4d0bbad47e3b5e3a0c";
var hmac_secret = "815ba6d666d58ef1e79b";
var time = new Date().toUTCString();
console.log("time:" + time)
var signed_headers_string = "";
signing_string= pm.request.method + "\n" + pm.request.url.getPath() + "\n" + pm.request.url.getQueryString() + "\n" + hmac_key + "\n" + time + "\n" + signed_headers_string;
console.log("signing_string:\n" + signing_string);

var signatureBytes = CryptoJS.HmacSHA256(signing_string, hmac_secret);
var requestSignatureBase64String = CryptoJS.enc.Base64.stringify(signatureBytes);
console.log("requestSignatureBase64String:" + requestSignatureBase64String)

//used in Header
pm.globals.set("sign", requestSignatureBase64String); //hmac signature
pm.globals.set("hmac_key", hmac_key); //hmac key
pm.globals.set("date", time); //request time
```

5. Switch postman to the Headers tab, and enter the 4 KEY-VALUE pairs in the figure below. Finally, click the **send** button to see the return result of calling the API. 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Rz73063_15374d13a67f41e1e478c1474fbcfd11.png)