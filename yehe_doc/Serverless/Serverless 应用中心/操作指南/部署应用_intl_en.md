## Overview
After developing your project locally, you can quickly deploy the application, view deployment information, and perform function debugging.

## Prerequisites
You have developed your project locally (for more information, please see [Project Development](https://intl.cloud.tencent.com/document/product/1040/38289)).

## Directions
### Quick deployment
Serverless Framework enables you to quickly deploy your project in the cloud by following the steps below:
```sh
sls deploy
```
After you enter this command, Serverless Framework CLI will perform the following operations:

#### 1. Scan QR code to authorize
You can authorize by scanning the QR code. After that, the CLI tool will write the generated temporary key information into the `.env` file in the current directory. The temporary key is valid for 2 hours. After it expires, you will be asked to scan the QR code again to authorize for deployment purposes.

If you don't want to scan the QR code repeatedly, you can also configure a permanent key in the `.env` file in the project directory:
```
# .env
TENCENT_SECRET_ID=xxxxxxxxxx # `SecretId` of your account
TENCENT_SECRET_KEY=xxxxxxxx # `SecretKey` of your account
```

You can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi). 

#### 2. Package and upload
After authorization is completed, Serverless Framework CLI will automatically package and upload your project according to the project code path configured in the `serverless.yml` file.

#### 3. Deploy in the cloud 
Resources will be created in the cloud for the uploaded project according to the parameters configured in the `.yml` file. After the deployment is completed, the command line will output the resource information.


### Advanced capabilities
- View specific log information during deployment:
```
sls deploy --debug
```

- Switch the specified traffic to the `$latest` function version during multi-version deployment and the rest traffic to the last published function version for grayscale release:
```
sls deploy --inputs traffic=0.1 public=true
```

- There are multiple Serverless instances in the application directory, and you want to update the specified project only:
```
sls deploy --target xxx
```
For example, in the project root directory, you can run the `sls deploy --target ./cos` command to update the COS instance only without affecting other instances.
```
.
├── src
│   ├── serverless.yml 
│   └── index1.js 
├── cos
│   └── serverless.yml 
├── db
│   └── serverless.yml 
└── .env 
```

### Viewing deployment information

After completing the deployment, you can run the following command to view the configuration information of the project:
```
sls info
```

### Debugging function
>?Currently, this command is supported only for function projects deployed through the [Serverless Framework SCF component](https://github.com/serverless-components/tencent-scf). It will be gradually supported for other components in the future.

The Serverless Framework SCF component supports triggering functions with the `invoke` command for debugging. For a function successfully deployed by running `sls deploy`, enter the project directory and run the function invocation command to remotely debug the function resources in the cloud. The debugging result will be output on the command line:

```
sls invoke  --inputs function=functionName  clientContext='{"weights":{"2":0.1}}'
```

- The `invoke` command must be executed in the same directory as the `serverless.yml` file deployed for the function.
- `clientContext` is the JSON string passed when the function is triggered. You can simulate different triggering events according to the JSON string format in the [triggering event template](https://intl.cloud.tencent.com/document/product/583/14572).

## FAQs
If a proxy is configured in your environment, the following problems may occur:

- Problem 1: the wizard does not pop up by default when `serverless` is entered.
  Solution: make sure that your IP is in the Chinese mainland and add the `SERVERLESS_PLATFORM_VENDOR=tencent` configuration item to the `.env` file.

- Problem 2: after `sls deploy` is entered, the deployment reports a network error.
  Solution: add the following proxy configuration to the `.env` file.
  ```
  HTTP_PROXY=http://127.0.0.1:12345 # Replace "12345" with your proxy port
  HTTPS_PROXY=http://127.0.0.1:12345 # Replace "12345" with your proxy port
  ```
