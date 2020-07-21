## Operation Scenarios

The Layer component is one of the basic components in the `serverless-tencent` component library. Through this component, you can create, configure, and manage SCF layer resources with speed and ease. 

## Prerequisites

You have installed [Node.js](https://nodejs.org/en/) (v8.6 or above; v10.0 or above is recommended).

## Directions

### Installation

Install Serverless through npm:

```console
npm install -g serverless
```

If you have already installed Serverless Framework, you can run the following command to upgrade it to the latest version: 

```console
npm update -g serverless
```

### Configuration

Create the `serverless.yml` file locally and configure it as follows:

```console
touch serverless.yml
```

```yml
# serverless.yml

component: layer
name: layerDemo
org: orgDemo
app: appDemo
stage: dev

inputs:
  region: ap-guangzhou
  name: layerDemo
  src: ./layer-folder
  runtimes:
    - Nodejs10.15

```
[Detailed Configuration >>](https://github.com/serverless-components/tencent-layer/blob/master/docs/configure.md)


### Deployment

 Run the following command to deploy by scanning code: 

```console
sls deploy
```

>?To grant persistent permission, please see [Account Configuration](#account).

### Removal

 You can run the following command to remove the deployed service: 

```
sls remove
```

<span id="account"></span>
### Account configuration (optional)

Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:

```console
touch .env # Tencent Cloud configuration information
```

Configure Tencent Cloud's `SecretId` and `SecretKey` information in the `.env` file and save it:
```
# .env
TENCENT_SECRET_ID=123
TENCENT_SECRET_KEY=123
```
>?
> - If you don't have a Tencent Cloud account yet, please [sign up](https://intl.cloud.tencent.com/register) first.
> - If you already have a Tencent Cloud account, you can get `SecretId` and `SecretKey` in [API Key Management](https://console.cloud.tencent.com/cam/capi).
