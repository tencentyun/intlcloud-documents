## Overview
**Tencent Cloud static website component** uses [Tencent Serverless Framework](https://github.com/serverless/components/tree/cloud). Based on serverless services (such as COS) in the cloud, it can implement "zero" configuration, convenient development, and rapid deployment of your static website. The static website component supports a rich set of configuration extensions such as custom domain name and CDN acceleration and provides the easiest-to-use, low-cost, and elastically scalable cloud-based static website development and hosting capabilities.


Features:

- **Pay-as-you-go billing**: fees are charged based on the request usage, and you don't need to pay anything if there is no request.
- **"Zero" configuration**: you only need to write project code and then deploy it, and the Serverless Framework will take care of all the configuration work.
- **Fast deployment**: you can deploy your static website in just a few seconds.
- **Real-time log**: you can view the business status through the output of the real-time log, which makes it easy for you to develop applications directly in the cloud.
- **Convenient collaboration**: the status information and deployment logs in the cloud make multi-person collaborative development easier.
- **CDN acceleration, SSL certificate configuration, and custom domain name**: you can configure CDN acceleration, custom domain names, and HTTPS access.





## Directions
#### 1. Install

Install the latest version of Serverless Framework through npm:
```
$ npm install -g serverless
```

#### 2. Create

Create a directory and enter it:
```
$ mkdir tencent-website && cd tencent-website
```

Use the following command and template link to quickly create a static website hosting application:
```
$ serverless init website-demo
$ cd website-demo
```

After download, the directory structure is as follows:
```
|- src
|   └── index.html
└──  serverless.yml
```

In the `src` directory, you can host both simple HTML files and complete React/Vue applications.

#### 3. Deploy

Run the following command in the directory under the `serverless.yml` file to deploy the static website. After the deployment is completed, you can view the URL address of your static website in the output on the command line. Then, you can click the address to visit the hosted website.

```
$ serverless deploy
```

If you want to view more information on the deployment process, you can run the `sls deploy --debug` command to view the real-time log information during the deployment process (`sls` is an abbreviation for the `serverless` command).



#### 4. Configure

The static website component supports "zero" configuration deployment, that is, it can be deployed directly through the default values in the configuration file. Nonetheless, you can also modify more optional configuration items to further customize your project.

The following describes certain configuration items in `serverless.yml` of the static website component:

```yml
# serverless.yml

component: website # Name of the imported component, which is required. The `tencent-website` component is used in this example
name: websitedemo # Name of the instance created by this `website` component, which is required
org: test # Organization information, which is optional. The default value is the `appid` of your Tencent Cloud account
app: websiteApp # Website application name, which is optional
stage: dev # Information for identifying environment, which is optional. The default value is `dev`

inputs:
  src:
    root: ./
    src: ./src
    hook: npm run build
    index: index.html
    websitePath: ./
  region: ap-guangzhou
  bucketName: my-bucket
  protocol: http
  hosts:
    - host: anycoder.cn
      https:
        certId: 123
```

View the [complete configuration and configuration description >>](https://github.com/serverless-components/tencent-website/blob/master/docs/configure.md)

After you update the configuration fields according to the configuration file, run `serverless deploy` or `serverless` again to update the configuration to the cloud.

#### 5. Debug

After the static website application is deployed, the project can be further developed through the debugging feature to create an application for the production environment. After modifying and updating the code locally, you don't need to run the `serverless deploy` command every time for repeated deployment. Instead, you can run the `serverless dev` command to directly detect and automatically upload changes in the local code.

You can enable debugging by running the `serverless dev` command in the directory where the `serverless.yml` file is located.

`serverless dev` also supports real-time outputting of cloud logs. After each deployment, you can access the project to output invocation logs in real time on the command line, which makes it easy for you to view business conditions and troubleshoot issues.

#### 6. Check status

In the directory where the `serverless.yml` file is located, run the following command to check the deployment status:

```
$ serverless info
```

#### 7. Remove

In the directory where the `serverless.yml` file is located, run the following command to remove the deployed static website service. After removal, this component will delete all related resources created during deployment in the cloud.

```
$ serverless remove
```

Similar to the deployment process, you can run the `sls remove --debug` command to view real-time log information during the removal process (`sls` is an abbreviation for the `serverless` command).

## Account Configuration

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:

```console
$ touch .env # Tencent Cloud configuration information
```

Configure Tencent Cloud's `SecretId` and `SecretKey` information in the `.env` file and save it:
```
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
>?
- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
