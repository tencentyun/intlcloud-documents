## Overview
PostgreSQL for Serverless (ServerlessDB) is a database product that allocates resources on demand based on PostgreSQL. Its database automatically allocates resources based on your actual number of requests. With PostgreSQL for Serverless, you can create a database instance for easy use without caring about the instance specifications. You only need to pay for the actual usage when the database is active.

Through the PostgreSQL for Serverless component, you can create, configure, and manage PostgreSQL instances with speed and ease.

Features:

- **Pay-as-you-go billing**: fees are charged based on the request usage, and you don't need to pay anything if there is no request.
- **Zero configuration**: the default configuration will be done by Serverless.
- **Fast deployment**: you can create or update your database in just a few seconds.
- **Convenient collaboration**: the database status information and deployment logs in the cloud make multi-person collaborative development easier.

## Directions
#### Installation
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:

```shell
$ npm install -g serverless
```

#### Account configuration

Create the `.env` file locally:

```bash
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

#### Configuration

Create a directory and enter it:
```
$ mkdir tencent-postgreSQL && cd tencent-postgreSQL
```

Create a `serverless.yml` file in a new directory:

```shell
$ touch serverless.yml
```
Configure `serverless.yml` as follows:
```yml
# serverless.yml
component: postgresql # Name of the imported component, which is required. The `postgresql` component is used in this example
name: serverlessDB # Name of the instance created by this component, which is required
org: test # Organization information, which is optional. The default value is the `appid` of your Tencent Cloud account
app: serverlessDB # SQL application name, which is optional
stage: dev # Information for identifying environment, which is optional. The default value is `dev`

inputs:
  region: ap-guangzhou  # Valid values: ap-guangzhou, ap-shanghai, ap-beijing
  zone: ap-guangzhou-2  # Valid values: ap-guangzhou-2, ap-shanghai-2, ap-beijing-3
  dBInstanceName: serverlessDB
  vpcConfig:
    vpcId: vpc-xxxxxxx
    subnetId: subnet-xxxxxx
  extranetAccess: false
```
The PostgreSQL component supports "zero" configuration deployment, that is, it can be deployed directly through the default values in the configuration file. Nonetheless, you can also modify more optional configuration items to further customize your project.

[Detailed Configuration >>](https://github.com/serverless-components/tencent-postgresql/blob/master/docs/configure.md)

>!Currently, PostgreSQL for Serverless is available for creation and deployment only in **Beijing Zone 3**, **Guangzhou Zone 2**, and **Shanghai Zone 2**. Therefore, when entering the region and AZ information in the `yaml` file, please be sure to use the correct region and corresponding VPC and subnet information.

#### Deployment

Deploy by running the `sls` command, and you can add the `--debug` parameter to view the information during the deployment process:
>?`sls` is short for the `serverless` command.

```bash
$ sls deploy
```

#### Removal
You can run the following commands to remove the deployed database instance:

```bash
$ sls remove
```

## Best Practice

After deploying the PostgreSQL Serverless database, you can refer to [Deploying Full-Stack Website with Vue + Express + PostgreSQL](https://intl.cloud.tencent.com/document/product/1040/36989) to use this database instance.

## More Components
You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).




