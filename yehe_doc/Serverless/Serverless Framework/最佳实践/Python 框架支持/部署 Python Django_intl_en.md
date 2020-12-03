## Operation Scenarios
**Tencent Cloud Django component** uses [Tencent Serverless Framework](https://github.com/serverless/components/tree/cloud). Based on serverless services (such as COS) in the cloud, it can implement "zero" configuration, convenient development, and rapid deployment of your Django webpage applications.

Django features:
- **"Zero" configuration**: you only need to write project code and then deploy it, and the Serverless Framework will take care of all the configuration work.
- **Pay-as-you-go billing**: fees are charged based on the request usage, and you don't need to pay anything if there is no request.
- **Fast deployment**: you can deploy your entire webpage application in just a few seconds.
- **Convenient collaboration**: the development mode and in-cloud debugging are supported to facilitate team collaboration.
- **Rich extensions**: RESTful API services can be deployed.


## Directions
### 1. Install

Install the latest version of Serverless Framework through npm:
```
$ npm install -g serverless
```

### 2. Create

Create a directory and enter it:
```
$ mkdir myDjangoDemo && cd myDjangoDemo
```

Use the following command and template link to quickly create a static website hosting application:
```
$ serverless create --template-url https://github.com/serverless-tencent/tencent-django/tree/master/example
$ cd example
```

### 3. Configure
Create the `serverless.yml` file locally:
```shell
$ touch serverless.yml
```

Configure `serverless.yml` as follows:
```yml
component: django # (required) name of the component. In that case, it's express.
name: mydjangoDemo # (required) name of your express component instance.
org: mydjangoDemo # (optional) serverless dashboard org. default is the first org you created during signup.
app: mydjangoDemo # (optional) serverless dashboard app. default is the same as the name property.
stage: dev # (optional) serverless dashboard stage. default is dev.

inputs:
  region: ap-guangzhou
  functionName: DjangoFunction 
  djangoProjectName: mydjangocomponent # Name of your project folder
  src:
    bucket: enter the name of the bucket into which you upload your project
    src: ./src
  functionConf:
    timeout: 10
    memorySize: 256
    environment:
      variables:
        TEST: vale
    vpcConfig:
      subnetId: ''
      vpcId: ''
  apigatewayConf:
    protocols:
      - https
    environment: release

```
>
If you want to create a project by yourself, please install the dependencies required by Python in the project directory. For example, `Django` is needed in this example, and you can run `pip` to install it:
```
pip install Django -t ./
```

### 4. Deploy

If you have not [logged in to](https://intl.cloud.tencent.com/login) or [signed up for](https://intl.cloud.tencent.com/register) a Tencent Cloud account:

Deploy by running the `sls` command, and you can add the `--debug` parameter to view the information during the deployment process:

```shell
$ sls deploy --debug
```

### 5. Remove
You can run the following commands to remove the deployed service:
```shell
$ sls remove --debug
```

### Account configuration (optional)
Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:
```shell
$ touch .env # Tencent Cloud configuration information
```

Configure Tencent Cloud's `SecretId` and `SecretKey` information in the `.env` file and save it:
```text
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
>
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
