Serverless Components is a scenario-based solution that supports orchestration and organization of multiple cloud resources for different use cases such as Express framework integration and website deployment. It can greatly simplify the configuration and management of cloud resources while interconnecting Tencent Cloud products such as gateways, COS, and CAM, so that you can focus more on your business development.

For more information, please see [Serverless Components on GitHub](https://github.com/serverless/components/blob/master/README.cn.md).

### Serverless Components Advantages

- **Ease of use**
Serverless Components is built around your scenarios (e.g., websites, blogs, payment systems, and image services). It abstracts underlying infrastructure configuration and enables you to implement your business scenarios with simple configurations.
- **Reusability**
A serverless component can be easily created and deployed through a very simple `serverless.yml` file. Plus, its JavaScript library `serverless.js` supports extension and reuse with simple syntax.
- **Fast deployment**
The deployment of most serverless components is about 20 times faster than traditional configuration tools. They allow rapid deployment and remote verification which help effectively reduce the workload of local emulation and debugging.

### Serverless Framework Components Best Practices

- [@serverless/tencent-scf](https://github.com/serverless-components/tencent-scf/tree/master) - SCF component
- [@serverless/tencent-express](https://github.com/serverless-components/tencent-express/tree/master) - Component used to quickly deploy Express.js-based backend services in SCF
- [@serverless/tencent-website](https://github.com/serverless-components/tencent-website/tree/master) - Component used to quickly deploy static websites in SCF


### Supported Serverless Components

Currently, Serverless Components supports a rich set of development frameworks and applications in various programming languages as detailed below:

**Basic components:**
-  [@serverless/tencent-postgresql](https://github.com/serverless-components/tencent-postgresql/tree/v2) - TencentDB for PostgreSQL serverless component
- [@serverless/tencent-apigateway](https://github.com/serverless-components/tencent-apigateway) - Tencent Cloud API Gateway component
- [@serverless/tencent-cos](https://github.com/serverless-components/tencent-cos) - Tencent Cloud COS component
- [@serverless/tencent-scf](https://github.com/serverless-components/tencent-scf/tree/v2) - Tencent Cloud SCF component
- [@serverless/tencent-cdn](https://github.com/serverless-components/tencent-cdn) - Tencent Cloud CDN component
- [@serverless/tencent-vpc](https://github.com/serverless-components/tencent-vpc/tree/v2) - Tencent Cloud VPC component



**Advanced components:**
- [@serverless/tencent-nextjs](https://github.com/serverless-components/tencent-nextjs/tree/v2) - Component used to quickly deploy Next.js-based applications in SCF
- [@serverless/tencent-nuxtjs](https://github.com/serverless-components/tencent-nuxtjs/tree/v2) - Component used to quickly deploy Nuxt.js-based applications in SCF
- [@serverless/tencent-express](https://github.com/serverless-components/tencent-express/tree/v2) - Component used to quickly deploy Express.js-based backend services in SCF
- [@serverless/tencent-egg](https://github.com/serverless-components/tencent-egg/tree/v2) - Component used to quickly deploy Egg.js-based backend services in SCF
- [@serverless/tencent-koa](https://github.com/serverless-components/tencent-koa/tree/v2) - Component used to quickly deploy Koa.js-based backend services in SCF
- [@serverless/tencent-flask](https://github.com/serverless-components/tencent-flask) - Tencent Cloud Python Flask RESTful API component
- [@serverless/tencent-django](https://github.com/serverless-tencent/tencent-django/tree/v2) - Tencent Cloud Python Django RESTful API component
- [@serverless/tencent-laravel](https://github.com/serverless-components/tencent-laravel) - Tencent Cloud PHP Laravel RESTful API component
- [@serverless/tencent-thinkphp](https://github.com/serverless-components/tencent-thinkphp) - Tencent Cloud ThinkPHP RESTful API component
- [@serverless/tencent-website](https://github.com/serverless-components/tencent-website/tree/v2) - Component used to quickly deploy static websites in SCF

**Third-party components:**
- [@authing/serverless-oidc](https://github.com/Authing/serverless-oidc) - Component used to quickly deploy Authing-based authentication
- [@twn39/tencent-fastify](https://github.com/twn39/tencent-fastify) - Component used to quickly deploy Fastify.js-based backend services in SCF
- [@twn39/tencent-php-slim](https://github.com/twn39/tencent-php-slim) - Component used to quickly deploy backend services based on Slim PHP microframework in SCF

In addition, you can view all Serverless Components in the [GitHub repository](https://github.com/serverless-components?q=tencent). Be sure to switch to the **v2** version when viewing the components.
![](https://main.qcloudimg.com/raw/8d30e522c8a8d3e46a8b057eaa161a13.png)
