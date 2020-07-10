## Operation Scenarios
**Tencent Cloud SCF** uses [Tencent Serverless Framework](https://github.com/serverless/components/tree/cloud). Based on serverless services (functions, triggers, etc.) in the cloud, it can implement "zero" configuration, convenient development, and rapid deployment of your first function. It supports a rich set of configuration extensions and provides the easiest-to-use, low-cost, and elastically scalable cloud-based function development, configuration, and deployment capabilities.

SCF component features:

- **Pay-as-you-go billing**: fees are charged based on the request usage, and you don't need to pay anything if there is no request.
- **"Zero" configuration**: you only need to write project code and then deploy it, and the Serverless Framework will take care of all the configuration work.
- **Fast deployment**: you can deploy your entire SCF application in just a few seconds.
- **Real-time log**: you can view the business status through the output of the real-time log, which makes it easy for you to develop applications directly in the cloud.
- **Cloud debugging**: SCF supports quick cloud debugging for the Node.js framework, which shields differences in the local environment.
- **Convenient collaboration**: the status information and deployment logs in the cloud make multi-person collaborative development easier.

## Directions
#### 1. Install

Install the latest version of Serverless Framework through npm:
```
$ npm install -g serverless
```

#### 2. Create

Create a directory and enter it:
```
$ mkdir tencent-scf && cd tencent-scf
```

Use the following command and template link to quickly create an SCF application:
```
$ serverless create --template-url https://github.com/serverless-components/tencent-scf/tree/v2/example
$ cd example
```

After download, the directory structure is as follows:
```
|- src
|   └── index.py
└──  serverless.yml
```

#### 3. Deploy

Run `serverless deploy` in the directory under the `serverless.yml` file to deploy the function. After the deployment is completed, you can view the URL address provided by the corresponding gateway trigger of the function in the output on the command line. Then, you can click the address to view the deployment effect of the function.

If you want to view more information on the deployment process, you can run the `sls deploy --debug` command to view the real-time log information during the deployment process (`sls` is an abbreviation for the `serverless` command).


#### 4. Configure

Tencent Cloud SCF component supports "zero" configuration deployment, that is, it can be deployed directly through the default values in the configuration file. Nonetheless, you can also modify more optional configuration items to further customize your project.

The following is the complete configuration description for `serverless.yml` of the Tencent Cloud SCF component:

```yml
# serverless.yml

component: scf # (Required) Reference the name of the component, which is the `tencent-scf` component in this example
name: scfdemo # (Required) Name of the instance created by this component
org: test # (Optional) Used to record organization information. Default value: your Tencent Cloud account's `appid`
app: scfApp # (Optional) SCF application name
stage: dev # (Optional) Used to distinguish between environments. Default value: dev

inputs:
  name: scfFunctionName
  src: ./src
  runtime: Nodejs10.15 # Runtime environment of function. Valid values: Python2.7, Python3.6, Nodejs6.10, Nodejs8.9, Nodejs10.15, PHP5, PHP7, Golang1, Java8.
  region: ap-guangzhou
  handler: index.main_handler
  events:
    - apigw:
        name: serverless_api
        parameters:
          protocols:
            - http
            - https
          serviceName:
          description: The service of Serverless Framework
          environment: release
          endpoints:
            - path: /index
              method: GET
```

View the [complete configuration and configuration description >>](https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md).

After you update the configuration fields according to the configuration file, run `serverless deploy` or `serverless` again to update the configuration to the cloud.

#### 5. Debug

After the SCF application is deployed, the project can be further developed through the debugging feature to create an application for the production environment. After modifying and updating the code locally, you don't need to run the `serverless deploy` command every time for repeated deployment. Instead, you can run the `serverless dev` command to directly detect and automatically upload changes in the local code.

You can enable debugging by running the `serverless dev` command in the directory where the `serverless.yml` file is located.

`serverless dev` also supports real-time outputting of cloud logs. After each deployment, you can access the project to output invocation logs in real time on the command line, which makes it easy for you to view business conditions and troubleshoot issues.

Currently, in addition to real-time log output, for Node.js applications, cloud debugging is also supported. After the `serverless dev` command is started, it will automatically listen on the remote port and set the function timeout period to 900 seconds temporarily. At this point, you can find the remote debugging path by accessing `chrome://inspect/#devices` and directly debug the code with breakpoints. After the debugging mode ends, you need to deploy the function again to update the code and set the timeout period back to the original value.

#### 6. Check status

In the directory where the `serverless.yml` file is located, run the following command to check the deployment status:

```
$ serverless info
```

#### 7. Remove

In the directory where the `serverless.yml` file is located, run the following command to remove the deployed SCF application. After removal, this component will delete all related resources created during deployment in the cloud.

```
$ serverless remove
```

Similar to the deployment process, you can run the `sls remove --debug` command to view real-time log information during the removal process. `sls` is an abbreviation for the `serverless` command.

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
>
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
