Serverless Framework is a popular serverless application framework service well recognized in the industry. It allows you to deploy completely available serverless application architectures without worrying about underlying resources. Its comprehensive capabilities including resource orchestration, auto scaling, and event-driven programming cover the entire application lifecycle from coding, debugging, and testing to deployment, enabling you to quickly build serverless applications by connecting to cloud-based resources.

Serverless Framework is a standardized, component-based serverless application development product as shown below:
![](https://main.qcloudimg.com/raw/30d9772cd859cfa24c14289098435c71.png)

## Features
#### Application-Level framework
Serverless Framework provides various frameworks suitable for different use cases. After selecting a framework as needed, you can focus on developing business logic without consideration of underlying resources.

#### Easy deployment
When you deploy an application, Serverless Framework will automatically deploy and configure SCF, API Gateway, COS, and other basic resources according to the application characteristics, eliminating the need for manual efforts.

#### One-Stop experience
Serverless Framework enables you to quickly create, debug, and deploy a serverless application, as well as to monitor its running status after launch and troubleshoot errors with speed.

## Serverless Framework Components
Serverless Components is a scenario-based solution that supports orchestration and organization of multiple cloud resources for different use cases such as Express framework integration and website deployment. It can greatly simplify the configuration and management of cloud resources while interconnecting Tencent Cloud products such as gateways, COS, and CAM, so that you can focus more on your business development.

For more information, please see [Serverless Components on GitHub](https://github.com/serverless/components/blob/master/README.cn.md).


### Benefits and features

- **Ease of use**
  Serverless Components is built around your scenarios (e.g., websites, blogs, payment systems, and image services). It abstracts underlying infrastructure configuration and enables you to implement your business scenarios with simple configurations.
- **Reusability**
  A serverless component can be easily created and deployed through a very simple `serverless.yml` file. Plus, its JavaScript library `serverless.js` supports extension and reuse with simple syntax.
- **Fast deployment**
  The deployment of most serverless components is about 20 times faster than traditional configuration tools. They allow rapid deployment and remote verification which help effectively reduce the workload of local emulation and debugging.



### Serverless Framework Components best practices

The following are common use case templates:

- [Deploying Hexo static blog](https://intl.cloud.tencent.com/document/product/1040/36749)
This example uses the Serverless Website component to quickly construct a serverless Hexo website:
```shell
serverless create --template-url https://github.com/serverless/components/tree/v1/templates/tencent-hexo-blog
```

- [Constructing RESTful API quickly](https://intl.cloud.tencent.com/document/product/1040/36747)
This example uses the Serverless SCF component to quickly construct a RESTful API application and perform `GET` and `PUT` operations.
```shell
serverless create --template-url https://github.com/serverless/components/tree/v1/templates/tencent-python-rest-api
```

- Deploy serverless full-stack web application (React.js)
This example uses React as the frontend and Express framework as the backend to deploy a serverless full-stack application through multiple Serverless Components.
```shell
serverless create --template-url https://github.com/serverless/components/tree/v1/templates/tencent-fullstack-react-application
```

- Deploy serverless full-stack web application (Vue.js)
This example uses Vue as the frontend and Express framework as the backend to deploy a serverless full-stack application through multiple Serverless Components.
```shell
serverless create --template-url https://github.com/serverless/components/tree/v1/templates/tencent-fullstack-vue-application
```

### Supported Serverless Components

Currently, Serverless Components supports a rich set of development frameworks and applications in various programming languages as detailed below:
![](https://main.qcloudimg.com/raw/8d30e522c8a8d3e46a8b057eaa161a13.png)

Basic components:
- [@serverless/tencent-postgresql](https://github.com/serverless-components/tencent-postgresql) - TencentDB for PostgreSQL serverless component
- [@serverless/tencent-apigateway](https://github.com/serverless-components/tencent-apigateway) - Tencent Cloud API Gateway component
- [@serverless/tencent-cos](https://github.com/serverless-components/tencent-cos) - Tencent Cloud COS component
- [@serverless/tencent-scf](https://github.com/serverless-components/tencent-scf) - Tencent Cloud SCF component
- [@serverless/tencent-cdn](https://github.com/serverless-components/tencent-cdn) - Tencent Cloud CDN component
- [@serverless/tencent-cam-role](https://github.com/serverless-components/tencent-cos) - Tencent Cloud COS component
- [@serverless/tencent-cam-policy](https://github.com/serverless-components/tencent-layer) - Tencent Cloud Layer component
- [@serverless/tencent-vpc](https://github.com/serverless-components/tencent-vpc) - Tencent Cloud VPC component
- [@serverless/tencent-ssl](https://github.com/serverless-tencent/tencent-ssl) - Tencent Cloud SSL certificate component



Advanced components:
- [@serverless/tencent-nextjs](https://github.com/serverless-components/tencent-nextjs) - Component used to quickly deploy Next.js-based applications in SCF
- [@serverless/tencent-nuxtjs](https://github.com/serverless-components/tencent-nuxtjs) - Component used to quickly deploy Nuxt.js-based applications in SCF
- [@serverless/tencent-express](https://github.com/serverless-components/tencent-express) - Component used to quickly deploy Express.js-based backend services in SCF
- [@serverless/tencent-egg](https://github.com/serverless-components/tencent-egg) - Component used to quickly deploy Egg.js-based backend services in SCF
- [@serverless/tencent-koa](https://github.com/serverless-components/tencent-koa) - Component used to quickly deploy Koa.js-based backend services in SCF
- [@serverless/tencent-flask](https://github.com/serverless-components/tencent-flask) - Tencent Cloud Python Flask RESTful API component
- [@serverless/tencent-django](https://github.com/serverless-tencent/tencent-django) - Tencent Cloud Python Django RESTful API component
- [@serverless/tencent-laravel](https://github.com/serverless-components/tencent-laravel) - Tencent Cloud PHP Laravel RESTful API component
- [@serverless/tencent-website](https://github.com/serverless-components/tencent-website) - Component used to quickly deploy static websites in SCF

Third-party components:
- [@authing/serverless-oidc](https://github.com/Authing/serverless-oidc) - Component used to quickly deploy Authing-based authentication
- [@twn39/tencent-fastify](https://github.com/twn39/tencent-fastify) - Component used to quickly deploy Fastify.js-based backend services in SCF
- [@twn39/tencent-php-slim](https://github.com/twn39/tencent-php-slim) - Component used to quickly deploy backend services based on Slim PHP microframework in SCF

In addition, you can view all Serverless Components in the [GitHub repository](https://github.com/serverless-components?q=tencent).
