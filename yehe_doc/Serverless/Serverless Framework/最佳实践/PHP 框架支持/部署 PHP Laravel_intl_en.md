## Operation Scenarios
Tencent Cloud [Laravel](https://github.com/laravel/laravel) Serverless Component supports deploying RESTful API services.

## Prerequisites
#### Initializing Laravel project
Before using this component, you need to initialize a `laravel` project first:
```shell
php composer create-project --prefer-dist laravel/laravel serverless-laravel
```
>!Laravel uses Composer to manage dependencies, so you need to install Composer first. For more information, please see [here](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos).

#### Modifying Laravel project
When a function is executed, only `/tmp` is readable/writable; therefore, you need to write the `storage` directory of the `laravel` framework runtime into this directory by modifying the `bootstrap/app.php` file and adding the following content after `$app = new Illuminate\Foundation\Application`:
```php
$app->useStoragePath($_ENV['APP_STORAGE'] ?? $app->storagePath());
```

Then, add the following configuration to the `.env` file in the root directory:
```dotenv
# View file compilation path
VIEW_COMPILED_PATH=/tmp/storage/framework/views

# Because it is a serverless function, it is impossible to store sessions on the disk. If sessions are not needed, you can use `array`
# If necessary, you can store the session in a cookie or database
SESSION_DRIVER=array

# You are recommended to output the error log to the console for easier viewing in the cloud
LOG_CHANNEL=stderr

# The application storage directory must be `/tmp`
APP_STORAGE=/tmp
```

## Directions
#### Installation
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:
```shell
$ npm install -g serverless
```

#### Configuration
Create a `serverless.yml` file in the project root directory:
```shell
$ touch serverless.yml
```

Configure `serverless.yml` as follows:
```yml
# serverless.yml

MyComponent:
  component: "@serverless/tencent-laravel"
  inputs:
    region: ap-guangzhou 
    functionName: laravel-function
    code: ./
    functionConf:
      timeout: 10
      memorySize: 128
      environment:
        variables:
          TEST: vale
      vpcConfig:
        subnetId: ''
        vpcId: ''
    apigatewayConf:
      protocol: https
      environment: release
```

[Detailed Configuration >>](https://github.com/serverless-components/tencent-laravel/tree/master/docs/configure.md)

#### Deployment



Deploy by running the `sls` command and add the `--debug` parameter to view the information during the deployment process:
>? `sls` is short for the `serverless` command.

```shell
$ sls --debug

  DEBUG ─ Resolving the template's static variables.
  DEBUG ─ Collecting components from the template.
  DEBUG ─ Downloading any NPM components found in the template.
  DEBUG ─ Analyzing the template's components dependencies.
  DEBUG ─ Creating the template's components graph.
  DEBUG ─ Syncing template state.
  DEBUG ─ Executing the template's components graph.
  DEBUG ─ Compressing function laravel-function file to /Users/Downloads/serverless-laravel/.serverless/laravel-function.zip.
  DEBUG ─ Compressed function laravel-function file successful
  DEBUG ─ Uploading service package to cos[sls-cloudfunction-ap-guangzhou-code]. sls-cloudfunction-default-laravel-function-1581888194.zip
  DEBUG ─ Uploaded package successful /Users/Downloads/serverless-laravel/.serverless/laravel-function.zip
  DEBUG ─ Creating function laravel-function
  DEBUG ─ Created function laravel-function successful
  DEBUG ─ Setting tags for function laravel-function
  DEBUG ─ Creating trigger for function laravel-function
  DEBUG ─ Deployed function laravel-function successful
  DEBUG ─ Starting API-Gateway deployment with name MyComponent.TencentApiGateway in the ap-guangzhou region
  DEBUG ─ Service with ID service-ok334ism created.
  DEBUG ─ API with id api-l7cppn6s created.
  DEBUG ─ Deploying service with id service-ok334ism.
  DEBUG ─ Deployment successful for the api named MyComponent.TencentApiGateway in the ap-guangzhou region.

  MyComponent: 
    region:              ap-guangzhou
    functionName:        laravel-function
    apiGatewayServiceId: service-ok334ism
    url:                 http://service-ok334ism-1258834142.gz.apigw.tencentcs.com/release/

  192s › MyComponent › done
```

#### Removal

You can run the following commands to remove the deployed service:
```shell
$ sls remove --debug

  DEBUG ─ Flushing template state and removing all components.
  DEBUG ─ Removing function
  DEBUG ─ Request id
  DEBUG ─ Removed function laravel-function successful
  DEBUG ─ Removing any previously deployed API. api-l7cppn6s
  DEBUG ─ Removing any previously deployed service. service-ok334ism

  18s › MyComponent › done
  
```

#### Account configuration (optional)

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:

Configure Tencent Cloud's `SecretId` and `SecretKey` information in the `.env` file and save it:
```text
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```

>?
>- If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
>-  If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
