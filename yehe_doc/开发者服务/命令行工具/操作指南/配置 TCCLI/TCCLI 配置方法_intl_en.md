This document describes how to initialize the configuration of Tencent Cloud Command Line Interface (TCCLI) in interactive and command line modes, and how to switch between accounts.


## Prerequisites
You have installed TCCLI. For more information, see [Installing TCCLI](https://www.tencentcloud.com/document/product/1013/33464).

## Directions

Before using TCCLI, you must initialize its configuration to ensure that the prerequisites for using TencentCloud API are met.


<dx-alert infotype="explain" title="">
The secretId, secretKey, and region used in this document are only examples. Replace them with actual information.
</dx-alert>


#### Interactive mode

You can enter the interactive mode for quick configuration by running the `tccli configure` command.
```bash
$ tccli configure
TencentCloud API secretId [*afcQ]:AKIDz8krbsJ5yKBZQpn74WFkmLPx3*******
TencentCloud API secretKey [*ArFd]:Gu5t9xGARNpq86cd98joQYCN3*******
region: ap-guangzhou
output[json]:
```
- **secretId**: the SecretId of your TencentCloud API key, which can be obtained at [Manage API Key](https://console.cloud.tencent.com/cam/capi).
- **secretKey**: the SecretKey of your TencentCloud API key, which can be obtained at [Manage API Key](https://console.cloud.tencent.com/cam/capi).
- **region**: the region where your Tencent Cloud product resides. Go to [APIs](https://www.tencentcloud.com/document/api/213) and obtain available regions from the page of your Tencent Cloud product. For example, you can obtain [Region List](https://www.tencentcloud.com/document/product/213/31574) from the page of Cloud Virtual Machine (CVM).
- **output**: the output format of the request return packet, which is optional. Valid values: json, table, text. Default value: json.
	For more information, run the `tccli configure help` command.
	

	
#### Command line mode
In command line mode, you can configure the information in an automated script.
```bash
# The `set` subcommand is used to configure one or more items.
$ tccli configure set secretId AKIDz8krbsJ5yKBZQpn74WFkmLPx3*******
$ tccli configure set region ap-guangzhou  output json
# The `get` subcommand is used to obtain configuration information.
$ tccli configure get secretKey
secretKey = Gu5t9xGARNpq86cd98joQYCN3*******
# The `list` subcommand is used to print all configuration information.
$ tccli configure list
credential:
secretId =  AKIDz8krbsJ5yKBZQpn74WFkmLPx3*******
secretKey =  Gu5t9xGARNpq86cd98joQYCN3*******
configure:
region =  ap-guangzhou
output =  json
# Specify the values of secretId and secretKey in the command line. For example, you can use the following command to query the CVM instance information:
$ tccli cvm DescribeInstances --secretId AKIDz8krbsJ5yKBZQpn74WFkmLPx3****** --secretKey Gu5t9xGARNpq86cd98joQYCN3*******
```

#### Supporting multiple accounts
TCCLI supports multiple accounts, making it easier for you to use multiple configurations at the same time.
```bash
# Specify the account name `test` in interactive mode.
$ tccli configure --profile test
TencentCloud API secretId [*BCDP]:AKIDz8krbsJ5yKBZQpn74WFkmLPx3*******
TencentCloud API secretKey [*ArFd]:Gu5t9xGARNpq86cd98joQYCN3*******
region: ap-guangzhou
output[json]:
# Specify the account name `test` for set/get/list subcommands.
$ tccli configure set region ap-guangzhou  output json  --profile test
$ tccli configure get secretKey      --profile test
$ tccli configure list      --profile test
# Use the `remove` subcommand to delete the configuration file of the specified account. If no account is specified, the default configuration file is deleted.
$ tccli configure remove -profile test
# Specify an account when calling an API such as the DescribeZones API of CVM.
$ tccli cvm DescribeZones --profile test
```

#### TCCLI configuration file
 - After you run the `tccli configure`command, the `default.configure` and `default.credential` files for TCCLI are generated under the `~/.tccli` directory. Content in the two files is in JSON format.
 The `default.configure` file records the version (the latest version by default) of the API to call, the endpoint (the nearest endpoint by default), the default output format, and the specified region. The `default.credential` file records your key pairs. Example:
```bash
# Format of the default.configure file: (The following takes CVM as an example. By default, the version of CVM APIs to call is 2017-03-12, and the endpoint for calling CVM APIs is cvm.tencentcloudapi.com.)
{
	...
	"cvm": {
	"endpoint": "cvm.tencentcloudapi.com",
	"version": "2017-03-12"
	},
	...
	"output": "json",
	"region": "ap-guanzhou",
	...
}
# Format of the default.credential file:
{
  "secretId": "AKIDz8krbsJ5yKBZQpn74WFkmLPx3*******",
  "secretKey": "Gu5t9xGARNpq86cd98joQYCN3*******"
}
```
 - If you specified an account name in the configuration command, the configuration files corresponding to the account name are generated. For example, after you run the `tccli configure --profile test` command, the `test.configure` and `test.credential` files are generated.
 - To modify content in the configuration files, you can directly edit the files or use the `set` subcommand. For example, you can run the `tccli configure set cvm.version 2017-03-12` command to set the version of CVM APIs to call to the default version 2017-03-12.


#### Configuring environment variables
TCCLI supports configuring TencentCloud API key pairs in environment variables to ensure the security of your information. For example, in Linux, you can configure a key pair in the following ways:
<dx-tabs>
::: Use `export` command (temporary)
```bash
# Set a TencentCloud API key SecretId.
$ export TENCENTCLOUD_SECRET_ID=AKIDz8krbsJ5yKBZQpn74WFkmLPx3*******
# Set a TencentCloud API key SecretKey.
$ export TENCENTCLOUD_SECRET_KEY=Gu5t9xGARNpq86cd98joQYCN3*******
# Set the region of a Tencent Cloud product.
$ export TENCENTCLOUD_REGION=ap-guangzhou
```

:::
::: Write into profile file (permanent)
```bash
# Edit the /etc/profile file, and write the following content into the file:
export TENCENTCLOUD_SECRET_ID=AKIDz8krbsJ5yKBZQpn74WFkmLPx3*******
export TENCENTCLOUD_SECRET_KEY=Gu5t9xGARNpq86cd98joQYCN3*******
export TENCENTCLOUD_REGION=ap-guangzhou
# Then run the following command for the environment variables to take effect:
$ source /etc/profile
```
:::
</dx-tabs>

<dx-alert infotype="explain" title="">
If you specify the same information in the command, configuration file, and environment variables, the priority order in TCCLI is command > configuration file > environment variables.
</dx-alert>

## Other configurations
- TCCLI supports authentication through Cloud Access Management (CAM) roles. For more information, see [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420).
```bash
# CAM role configuration is not available in interactive mode. Use the non-interactive mode instead:
$ tccli configure set role-arn qcs::cam::uin/***********/**** role-session-name ****
```
The `role-arn` and `role-session-name` fields support the `get` and `list` subcommands of `configure`. You can write values into the configuration file, or specify values in the command line, in the same way that you configure `secretId` and `secretKey`, as shown below:
```bash
# Use the `get` subcommand to obtain configuration information.
$ tccli configure get role-arn
role-arn = qcs::cam::uin/***********/****
# Use the `list` subcommand to print all configuration information.
$ tccli configure list
credential:
role-arn = qcs::cam::uin/***********/****
role-session-name = ****
# Write the configuration information into environment variables.
$ export TENCENTCLOUD_ROLE_ARN=qcs::cam::uin/***********/****
$ export TENCENTCLOUD_ROLE_SESSION_NAME=****
# Specify the `role-arn` and `role-session-name` fields in the command line. The following example is for calling the DescribeZones API:
$ tccli cvm DescribeZones --role-arn qcs::cam::uin/***********/**** --role-session-name ****
```
- If your instance is bound to a role, you can use the role for authentication, without providing `secretId` and `secretKey`. You can use `--use-cvm-role` to call APIs through the role.
```bash
#  Use a role to call the DescribeZones API.
$ tccli cvm DescribeZones --use-cvm-role
```
<dx-alert infotype="notice" title="">
This method applies only to instances bound to a role. For more information, see [Managing Roles](https://intl.cloud.tencent.com/document/product/213/45917).
</dx-alert>


