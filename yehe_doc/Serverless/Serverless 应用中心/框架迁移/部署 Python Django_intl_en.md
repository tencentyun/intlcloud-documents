## Overview
**Tencent Cloud Django component** uses [Tencent Serverless Framework](https://github.com/serverless/components/tree/cloud). Based on serverless services (such as COS) in the cloud, it can implement "zero" configuration, convenient development, and rapid deployment of your Django webpage applications.

Django features:
- **"Zero" configuration**: you only need to write project code and then deploy it, and the Serverless Framework will take care of all the configuration work.
- **Pay-as-you-go billing**: fees are charged based on the request usage, and you don't need to pay anything if there is no request.
- **Fast deployment**: you can deploy your entire webpage application in just a few seconds.
- **Convenient collaboration**: the development mode and in-cloud debugging are supported to facilitate team collaboration.
- **Rich extensions**: RESTful API services can be deployed.


## Directions
### 1. Install Serverless CLI

Install the latest version of Serverless CLI through npm:
```
$ npm install -g serverless
```

### 2. Initialize the Django template project (optional)
If you don't have a local Django project, you can initialize a Django project with the following commands (if you already have one, you can ignore this step):
```
serverless init django-starter --name example
cd example
```

### 3. Install project dependencies
If you want to create a project by yourself, please install the dependencies required by Python in the project directory. For example, Django is needed in this example, and you can run `pip` to install it:
```
pip install Django -t ./
```

### 4. Configure the .yml file
Create a `serverless.yml` file in the project root directory:
```sh
touch serverless.yml
```
Paste the following configuration template into the file to implement basic project configuration.
>?You can add more configuration items in `serverless.yml` based on your actual deployment needs. For more information on the configuration of the .yml file, please see [Django Component Configuration](https://github.com/serverless-components/tencent-django/blob/master/docs/configure.md).
```yml
#serverless.yml
component: django
name: djangoDemo
org: orgDemo
app: appDemo
stage: dev

inputs:
  region: ap-guangzhou
  djangoProjectName: mydjangocomponent
  src: ./src
  functionConf:
    timeout: 10
    memorySize: 256
  apigatewayConf:
    protocols:
      - https
    environment: release
```


### 5. Deploy the application
Deploy by running the `sls deploy` command, and you can add the `--debug` parameter to view the information during the deployment process:

```
sls deploy --debug
```
After the deployment is completed, access the application by accessing the output API Gateway link.


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
>?
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>- If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
