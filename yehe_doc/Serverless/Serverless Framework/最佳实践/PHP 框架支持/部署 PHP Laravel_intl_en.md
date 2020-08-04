## Operation Scenarios
 Tencent Cloud [Laravel](https://github.com/laravel/laravel) Serverless Component supports Laravel v6.0 and above. 

## Prerequisites
### Initializing Laravel project
Before using this component, you need to initialize a `laravel` project first:
```shell
composer create-project --prefer-dist laravel/laravel serverless-laravel
```
>!Laravel uses Composer to manage dependencies, so you need to install Composer first. For more information, please see [here](https://getcomposer.org/doc/00-intro.md#installation-linux-unix-macos).

### Modifying Laravel project
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
### Installation
Use npm to install [Serverless CLI](https://github.com/serverless/serverless) globally:
```shell
npm install -g serverless
```

### Configuration
Create a `serverless.yml` file in the project root directory:
```shell
touch serverless.yml
```

Configure `serverless.yml` as follows:
```yml
# serverless.yml

component: laravel
name: laravelDemo
org: orgDemo
app: appDemo
stage: dev

inputs:
  src: ./
  region: ap-guangzhou
  runtime: Php7
  apigatewayConf:
    protocols:
      - http
      - https
    environment: release
```

[Detailed Configuration >>](https://github.com/serverless-components/tencent-laravel/blob/master/docs/configure.md)

### Deployment

Run the following command to deploy by scanning code:

```console
sls deploy
```

>?
>-  **Before deployment, you need to clear the local configuration cache by running `php artisan config:clear`.** 
>- To grant persistent permission, please see [Account Configuration](#account).

### Removal

You can run the following command to remove the deployed service:

```console
sls remove
```

<span id="account"></span>
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

