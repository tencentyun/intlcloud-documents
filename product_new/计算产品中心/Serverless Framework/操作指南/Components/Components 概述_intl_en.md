Serverless Components is a scenario-based solution that supports orchestration and organization of multiple Tencent Cloud resources for different use cases such as Express framework integration and website deployment. It can greatly simplify the configuration and management of Tencent Cloud resources while interconnecting Tencent Cloud products such as gateways, COS, and CAM, so that you can focus more on your business development.


## Differences Between Components and Framework CLI


| Item | Feature | Configuration | Supported Languages |
|---------|---------|---------|---------|
| Serverless Components | A workflow framework that covers testing and deployment | Mainly involves configurations of SCF and its triggers | All SCF-compatible programming languages except Java, such as Node.js, Python, PHP, and Go |
| Serverless Framework | A scenario-oriented framework that supports deploying and orchestrating various Tencent Cloud resources such as COS, API Gateway, CAM, and databases | Customizable resource-specific configuration | Node.js |

## Benefits and Features

- **Ease of use**
Serverless Components is built around your scenarios (e.g., websites, blogs, payment systems, and image services). It abstracts underlying infrastructure configuration and enables you to implement your business scenarios with simple configurations.
- **Reusability**
A serverless component can be easily created and deployed through a very simple `serverless.yml` file. Plus, its JavaScript library `serverless.js` supports extension and reuse with simple syntax.
- **Fast deployment**
The deployment of most serverless components is about 20 times faster than traditional configuration tools. They allow rapid deployment and remote verification which help effectively reduce the workload of local emulation and debugging.

## Best Practices
 
- **[Quick Deployment of an Express Framework](https://intl.cloud.tencent.com/document/product/1040/33161)**
With the Express component, you can deploy your existing projects on cloud with just a few modifications. In just a few seconds, you can deploy a pay-as-you-go Express.js application on Tencent Cloud Serverless Architecture.
- **[Quick Deployment of a Static Website](https://intl.cloud.tencent.com/document/product/1040/33162)**
The static website component now supports the latest web frameworks and technologies such as React and Vue.js, allowing you to deploy a static website in COS in a matter of seconds.
- **[Quick Deployment of a Full-stack Application (vue.js + express.js)](https://intl.cloud.tencent.com/document/product/1040/33160)**
Combines Express components and Website components to build a serverless application with complete frontend and backend.

## Basic Components

You can either choose from the best practices composed of basic components or orchestrate and deploy the basic components as needed by your use case.

- [SCF component](https://intl.cloud.tencent.com/document/product/1040/33164)
- [API Gateway component](https://intl.cloud.tencent.com/document/product/1040/33165)
- [COS component](https://intl.cloud.tencent.com/document/product/1040/33166)
- [CAM - role component](https://intl.cloud.tencent.com/document/product/1040/33167)
- [CAM - policy component](https://intl.cloud.tencent.com/document/product/1040/33168)


