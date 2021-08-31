## Microservice Development

If your system is developed under a microservice architecture, then:
* There will be a lot of microservice modules.
* Each module has its own APIs.
* Each module has its own service address or [CLB](https://intl.cloud.tencent.com/product/clb).
* Certain API calls are contextual.
* In certain cases, multiple APIs need to be called to get the final data.
* The call specifications, naming conventions, and parameter designs of APIs may vary.
* The APIs of each module require verification and authentication.
* The API requests to certain modules may increase due to business surges.

In this case, it will become increasingly troublesome to manage and use APIs as microservice modules increase. API Gateway can be leveraged to address those issues by helping:
* manage APIs in a unified manner, so that users can query and call APIs in the same place.
* automatically generate the documentation and SDK and complete test calls, making it easy for users or developers to quickly get started with APIs.
* set a request traffic limit, so that backend modules will not fail due to pressure surges.
* unify the specifications, naming conventions, and parameter call methods of APIs.
* implement unified API authentication.


## Serverless Development

After you write a cloud function in Serverless Cloud Function [(SCF)](https://intl.cloud.tencent.com/product/scf), if you want to provide an API service for it so that apps, frontend webpages, or clients can access it, an access method will be required.

In this case, you can use API Gateway to configure an API for integration with the backend cloud function. Then, each request to the API will trigger the execution of the cloud function to implement the corresponding business feature. For serverless development, you only need to pay for actual requests and executions.


## API Exposure of Traditional Applications

- With API Gateway, traditional applications do not need to expose their existing APIs directly to the internet, thus avoiding server vulnerabilities and security issues.
- Traffic control in API Gateway can help prevent excessive sudden requests from being passed to your application, ensuring high stability of your business.
- When used in combination with Tencent Cloud CAM, API Gateway can grant different users or clients different permissions for the purpose of access control.
