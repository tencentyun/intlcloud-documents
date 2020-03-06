
Tencent Cloud Serverless Cloud Function (SCF) provides a serverless execution environment, enabling companies and developers to execute code without the need to purchase and manage servers. You can submit the code or compiled files and related dependencies to the SCF platform in the required format by developing functions, so that the code logic can be executed correctly on the platform.

## Development Process

The development process of functions mainly includes the following steps:
* [Writing](https://cloud.tencent.com/document/product/583/9699): Write code based on business needs.
* [Packaging](https://intl.cloud.tencent.com/document/product/583/32741): Compile and package business code and dependencies to generate the required format.
* [Deployment](https://cloud.tencent.com/document/product/583/9207): Create or update a function in the cloud using the generated package.
* [Testing](https://cloud.tencent.com/document/product/583/30397): Test the correctness of the business logic in the code.
* [Running](https://cloud.tencent.com/document/product/583/30398): Execute the actual business by configuring the trigger or using the specified trigger and triggering function.

The development process varies slightly by development method, tool, and language. For example, you can test a function locally, debug a function directly online in the web editor after deploying it, or automate the steps by completing continuous integration and deployment. Please develop the functions based on your actual scenarios.

## Programming Languages

The way the code is written varies by programming language. Currently, SCF supports the following languages:
* [Python 2.7 and Python 3.6](https://intl.cloud.tencent.com/document/product/583/11061)
* [Node.js 6.10 and Node.js 8.9](https://intl.cloud.tencent.com/document/product/583/11060)
* [PHP 5.6 and PHP 7.2](https://intl.cloud.tencent.com/document/product/583/17531)
* [Java 8](https://cloud.tencent.com/document/product/583/12214)
* [Go 1](https://cloud.tencent.com/document/product/583/18032)

When using different languages for development, please note that the deployment packages and language-related features are different. For example, the storage locations of post-compilation package, script code package, and dependent library package vary. Language-related features include handlers, event parameters, log outputs, error outputs, and environment variables.
