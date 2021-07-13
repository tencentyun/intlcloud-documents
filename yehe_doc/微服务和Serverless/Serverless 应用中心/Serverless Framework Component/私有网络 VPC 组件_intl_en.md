## Operation Scenarios
Tencent Cloud VPC component supports configuring `serverless.yml` to quickly create VPCs and subnets with specified names and output `VPCID` and `SubnetID` in order to facilitate the configuration of network information required by other components.

## Directions
### Installation

 Install the latest version of Serverless Framework through npm: 

```shell
$ npm install -g serverless
```

### Configuration
Create a `vpcDemo` directory and create a `serverless.yml` file in it.

```shell
$ mkdir vpcDemo && cd vpcDemo
$ touch serverless.yml
```
Configure `serverless.yml` as follows:
```yml
# serverless.yml
org: orgDemo # Organization information, which is optional. The default value is the `appid` of your Tencent Cloud account.
app: appDemo # VPC application name, which is optional.
stage: dev # Information for identifying environment, which is optional. The default value is `dev`.

component: vpc # Name of the imported component, which is required. The `tencent-vpc` component is used in this example
name: vpcDemo # Name of the instance created by this component, which is required.

inputs:
  region: ap-guangzhou
  zone: ap-guangzhou-2
  vpcName: serverless
  subnetName: serverless
```
[Detailed Configuration >>](https://github.com/serverless-components/tencent-vpc/blob/master/docs/configure.md)

### Deployment

Run `sls deploy` to deploy:

```bash
$ sls deploy
serverless ⚡ framework
Action: "deploy" - Stage: "dev" - App: "appDemo" - Instance: "vpcDemo"

region:     ap-guangzhou
zone:       ap-guangzhou-2
vpcId:      vpc-xxxxxxxx
vpcName:    serverless
subnetId:   subnet-xxxxxxxx
subnetName: serverless


3s › vpcDemo › Success
```



>?`sls` is short for the `serverless` command.

### Information viewing

Run `sls info` to view the information of successful deployment:

```bash
$ sls info

serverless ⚡ framework

Status:       active
Last Action:  deploy (5 minutes ago)
Deployments:  2

region:     ap-guangzhou
zone:       ap-guangzhou-2
vpcId:      vpc-xxxxxxx
vpcName:    serverless
subnetId:   subnet-xxxxxxx
subnetName: serverless

vpcDemo › Info successfully loaded
```


### Removal

You can run the following commands to remove the deployed VPC:

```bash
$ sls remove

serverless ⚡ framework
Action: "remove" - Stage: "dev" - App: "appDemo" - Instance: "vpcDemo"

6s › vpcDemo › Success
```

### Account configuration (optional)
Currently, you can scan a QR code to log in to the CLI by default. If you want to configure persistent environment variables/key information, you can also create a local `.env` file:

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

