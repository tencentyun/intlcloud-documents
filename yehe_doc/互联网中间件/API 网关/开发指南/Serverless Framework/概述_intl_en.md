## Overview

Well-received in the industry, Serverless Framework allows you to deploy a complete, available serverless application framework without the need to care about underlying resources. It features resource orchestrating, auto scaling, and event driving and covers the full development lifecycle from coding and debugging to testing and deploying, helping you quickly build serverless applications with the aid of Tencent Cloud resources.

## Serverless Framework Components

Serverless Components is a scenario-based solution that supports orchestration and organization of multiple cloud resources for different use cases such as Express framework integration and website deployment. It can greatly simplify the configuration and management of cloud resources while interconnecting Tencent Cloud products such as API Gateway, COS, and CAM, so that you can focus more on your business development. For more information, please see [Serverless Components](https://github.com/serverless/components/blob/master/README.cn.md) on GitHub.

### Benefits and features

- **Ease of use**
  Serverless Components is built around your scenarios (e.g., websites, blogs, payment systems, and image services). It abstracts underlying infrastructure configuration and enables you to implement your business scenarios with simple configurations.
- **Reusability**
  A serverless component can be easily created and deployed through a very simple `serverless.yml` file. Plus, its JavaScript library `serverless.js` supports extension and reuse with simple syntax.
- **Fast deployment**
  The deployment of most serverless components is about 20 times faster than traditional configuration tools. They allow rapid deployment and remote verification which help effectively reduce the workload of local emulation and debugging.

### API Gateway component

The API Gateway component is one of the basic components provided by [Tencent Serverless Framework](https://github.com/serverless/components/tree/cloud). Through this component, you can create, configure, and manage API gateways with speed and ease.

## Best Practice



You can start using Serverless Framework CLI through the following practices:

<table>
<tr>
<th>Item</th><th>Description</th>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1040/37354">Deploying Express.js application</a></td>
<td>Use the `Serverless SCF` component to quickly construct an Express.js project.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1040/36989">Deploying full-stack website with Vue + Express + PostgreSQL</a></td>
<td>Use Vue as the frontend and Express framework as the backend to deploy a serverless full-stack application through multiple Serverless Components.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1040/37355">Deploying Nuxt.js application</a></td>
<td>Use the `Serverless Components Nuxt.js` component to quickly deploy an SSR project based on Nuxt.js.</td>
</tr>
</table>