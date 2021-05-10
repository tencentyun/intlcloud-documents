## Operation Scenarios
The CDN component is one of the basic components in the `serverless-tencent` component library. Through this component, you can create, configure, and manage CDN services with speed and ease.

## Prerequisites

- You have installed [Node.js](https://nodejs.org/en/) (v8.6 or above; v10.0 or above is recommended).
- You have activated [CDN](https://console.cloud.tencent.com/cdn).

## Directions

#### Installation

Install Serverless through npm:

```console
npm install -g serverless
```

If you have already installed Serverless Framework, you can run the following command to upgrade it to the latest version: 

```console
npm update -g serverless
```

#### Configuration

Create the `serverless.yml` file locally:
```shell
touch serverless.yml
```
Configure `serverless.yml` as follows:
```yml
# serverless.yml

component: cdn
name: cdnDemo
app: appDemo
stage: dev

inputs:
  area: overseas
  domain: mysite.com # Domain name
  origin:
    origins:
      - xxx.cos.ap-guangzhou.myqcloud.com  # Origin server, which can be a domain name or an IP
    originType: cos
    originPullProtocol: https
  serviceType: web
  forceRedirect:
    switch: on
    redirectType: https
    redirectStatusCode: 301
  https:
    switch: on
    http2: on
    certInfo:
      certId: 'abc'
      # certificate: 'xxx'
      # privateKey: 'xxx'
```

[Detailed Configuration >>](https://github.com/serverless-components/tencent-cdn/blob/master/docs/configure.md)

#### Deployment

Run the following command to deploy by scanning code:
```console
sls deploy
```

>?
>- Make sure that you have activated [CDN](https://console.cloud.tencent.com/cdn).
>- To grant persistent permission, please see [Account Configuration](#account).

#### Removal

Run the following command to remove the deployed CDN configuration:
```console
sls remove
```

<span id="account"></span>
#### Account configuration (optional)
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

