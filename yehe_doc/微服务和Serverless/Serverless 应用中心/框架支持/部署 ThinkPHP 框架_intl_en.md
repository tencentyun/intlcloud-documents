## Overview
Tencent Cloud [ThinkPHP](https://github.com/top-think/think) Serverless Component supports deploying RESTful API services based on ThinkPHP 6.x or above.

## Prerequisites
#### Initializing ThinkPHP project
1. The PHP environment has been set up locally. The recommended version is PHP 7.1 or above (ThinkPHP 6 is recommended).
2. Install Composer: ThinkPHP uses Composer to manage dependencies. For the installation method, please see [here](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos).

After the above two steps are completed, use Composer to initialize a `ThinkPHP` project:
```bash
composer create-project topthink/think serverless-thinkphp
```

## Operation Guide
### 1. Install

Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:

```bash
npm install -g serverless
```

### 2. Configure
Create a `serverless.yml` file in the project root directory:
```bash
$ touch serverless.yml
```

Configure `serverless.yml` as follows:
```yml
# serverless.yml
app: appDemo
stage: dev
component: thinkphp
name: thinkphpDemo

inputs:
  src:
    src: ./
    exclude:
      - .env
  region: ap-guangzhou
  runtime: Php7
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```

[More configuration items >>](https://github.com/serverless-components/tencent-thinkphp/tree/master/docs/configure.md)

### 3. Deploy

>!Before deployment, you need to run `php think clear` to clear the locally running configuration cache.

Deploy by running the `sls` command, and you can add the `--debug` parameter to view the information during the deployment process:
```bash
$ sls deploy --debug
```

### 4. Remove

You can run the following command to remove the deployed ThinkPHP project:

```bash
$ sls remove --debug
```

### Account configuration (optional)

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:
```shell
touch .env # Tencent Cloud configuration information
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

### More components

You can view more component information in the repository of [Serverless Components](https://github.com/serverless-components).
