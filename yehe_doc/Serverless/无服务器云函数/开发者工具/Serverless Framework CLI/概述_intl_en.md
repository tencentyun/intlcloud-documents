## Overview
Well-received in the industry, Serverless Framework allows you to deploy a complete and available serverless application framework without having to care about underlying resources. It features resource orchestrating, auto scaling, and event driving and covers the full development lifecycle from coding and debugging to testing and deploying, helping you quickly build serverless applications with the aid of Tencent Cloud resources.

## SCF Component
Serverless Framework provides an SCF component, which can be used to quickly package and deploy SCF projects. You can familiarize yourself with and use the component by following the steps below:
1. Get started with Serverless Framework CLI as instructed in [Creating and Deploying Functions](https://intl.cloud.tencent.com/document/product/583/36707).
2. Learn how to use Serverless Framework to develop and debug SCF functions as instructed in [Development Mode and In-cloud Debugging](https://intl.cloud.tencent.com/document/product/583/36268).
3. Learn how to perform project management and resource orchestration for multiple SCF functions as instructed in [Project Application](https://intl.cloud.tencent.com/document/product/583/38850).


## Best Practices
Serverless Framework provides the SCF component to implement resource creation and orchestration for SCF. In addition, it provides more encapsulated components and best practices for some typical use cases, such as Express framework support and website deployment. For more information, please see the [Serverless Components project](https://github.com/serverless/components/blob/master/README.cn.md) on GitHub.
<table>
<tr>
<th>Item</th><th>Description</th>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1040/36748">Deploying static websites</a></td>
<td>Use the `Serverless Website` component to quickly host a static website.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1040/37354">Deploying Express.js applications</a></td>
<td>Use the `Serverless SCF` component to quickly construct an Express.js project.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1040/36989">Deploying full-stack websites with Vue + Express + PostgreSQL</a></td>
<td>Use Vue as the frontend and Express framework as the backend to deploy a serverless full-stack application through multiple Serverless Components.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/1040/37355">Deploying Nuxt.js applications</a></td>
<td>Use the `Serverless Components Nuxt.js` component to quickly deploy an SSR project based on Nuxt.js.</td>
</tr>
</table>
