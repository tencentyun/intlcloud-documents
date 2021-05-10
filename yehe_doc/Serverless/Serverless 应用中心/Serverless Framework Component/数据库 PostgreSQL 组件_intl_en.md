## Operation Scenarios
PostgreSQL for Serverless (ServerlessDB) is a PostgreSQL-based database product that enables on-demand allocation of resources. It can automatically allocate resources according to the actual number of requests. You can simply create a database instance to use PostgreSQL for Serverless without caring about instance specification, and you only need to pay for resource usage during active period of the instance.

Through the PostgreSQL ServerlessDB component, you can create, configure, and manage Tencent Cloud PostgreSQL instances with speed and ease.

Features:

- **Pay per use**: fees are charged based on the request usage, and you don't need to pay anything if there is no request.
- **Zero configuration**: the default configuration is implemented by Serverless.
- **Fast deployment**: you can create or update your database in a matter of seconds.
- **Convenient collaboration**: the status information and deployment logs of the database in the cloud make multi-person collaborative development easier.

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

Create a `serverless.yml` file in the new directory:

```shell
$ touch serverless.yml
```
Configure `serverless.yml` as follows:
```yml
# serverless.yml
component: postgresql # (Required) Name of the imported component. The `postgresql` component is used in this example
name: serverlessDB # (Required) Name of the instance created by the `postgresql` component
org: test # (Optional) Organization information. The default value is the `appid` of your Tencent Cloud account.
app: serverlessDB # (Optional) SQL application name
stage: dev # (Optional) Information for identifying environment. The default value is `dev`.

inputs:
  region: ap-guangzhou  # You can select `ap-guangzhou`, `ap-shanghai`, or `ap-beijing`
  zone: ap-guangzhou-2  # You can select `ap-guangzhou-2`, `ap-shanghai-2`, or `ap-beijing-3`
  dBInstanceName: serverlessDB
  vpcConfig:
    vpcId: vpc-xxxxxxx
    subnetId: subnet-xxxxxx
  extranetAccess: false
```
The PostgreSQL ServerlessDB component supports "zero" configuration deployment, that is, it can be deployed directly through the default values in the configuration file. Nonetheless, you can also modify more optional configuration items to further customize your project.

[Detailed Configuration >>](https://github.com/serverless-components/tencent-postgresql/blob/master/docs/configure.md)

>!Currently, PostgreSQL for Serverless instances can be created and deployed only in **Beijing Zone 3**, **Guangzhou Zone 2**, and **Shanghai Zone 2**. Therefore, when entering the region and AZ in the YAML file, please be sure to enter a correct region and corresponding VPC and subnet information.

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

## More Components
You can view more component information in the repository of [Serverless Components](https://github.com/serverless/components).

