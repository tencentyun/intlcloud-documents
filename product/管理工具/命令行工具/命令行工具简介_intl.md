
Tencent Cloud Command Line Interface (TCCLI) is a unified tool for managing Tencent cloud resources. With TCCLI, you can quickly and easily call Tencent Cloud API to manage your Tencent Cloud resources. You can also achieve automation and script processing based on TCCLI and thus mix and reuse the functions in multiple ways. Please note that this product is not yet available on the International Console. 

## Installing TCCLI
1. Before installing CLI, make sure your system has already installed Python environment and Pip tool.
>**Note: Python must be version 2.7 or higher**. For more information, see [Python's official website](https://www.python.org/) and [Pip's official website](https://pypi.org/project/pip/).

2. TCCLI is dependent on TencentCloudApi Python SDK. **If the version number of the TencentCloudApi Python SDK is lower than that of the TCCLI to be installed, the TencentCloudApi Python SDK will be automatically upgraded when TCCLI is installed.**
3. Install TCCLI by executing the following command:
```bash
pip install tccli
```
4. After the installation is completed, execute the "tccli version" command to check whether the installation is successful.
5. If your environment is Linux, you can enable auto-completion with the following command:
```bash
complete -C 'tccli_completer' tccli
```

## Configuring TCCLI
To use TCCLI, you need to complete its initial configuration so that it meets the prerequisites of using Cloud API.
1. You can enter the interactive mode for quick configuration using the "tccli configure" command.
```bash
$  tccli configure
TencentCloud API secretId [*afcQ]:AKIDwLw1234MMfPRle2g9nR2OTI787aBCDP
TencentCloud API secretKey [*ArFd]:OxXj7khcV1234dQSSYNABcdCc1LiArFd
region: ap-guangzhou
output[json]:
```
secretId: Cloud API key's secretId.
secretKey: Cloud API key's secretKey.
region: Cloud product region. Please go to the corresponding product page for information about available regions.
output: Optional parameter; output format of the request return packet; [json, table and text] are supported; default value: json.
For more information, execute the "tccli configure help" command.
2. In command line mode, you can configure the information in an automated script.
```bash
# The "set" subcommand can set a certain configuration or multiple configurations simultaneously.
tccli configure set secretId AKIDwLw1234MMfPRle2g9nR2OTI787aBCDP
tccli configure set region ap-guangzhou  output json
# The "get" subcommand is used to obtain configuration information.
tccli configure get secretKey
secretKey = OxXj7khcV1234dQSSYNABcdCc1LiArFd
# The "list" subcommand prints all configuration information.
tccli configure list
credential:
secretId =  AKIDwLw1234MMfPRle2g9nR2OTI787aBCDP
secretKey =  OxXj7khcV1234dQSSYNABcdCc1LiArFd
configure:
region =  ap-guangzhou
output =  json
```
For more information, execute the "tccli configure [list get set] help" command.
3. TCCLI supports multiple accounts, making it easier to use multiple configurations at the same time.
```bash
Specify the account name "test" in interactive mode.
$  tccli configure --profile test
TencentCloud API secretId [*BCDP]:AKIDwLw1234MMfPRle2g9nR2OTI787aBCDP
TencentCloud API secretKey [*ArFd]:OxXj7khcV1234dQSSYNABcdCc1LiArFd
region: ap-guangzhou
output[json]:
# Specify the account name "test" for set/get/list subcommands
tccli configure set region ap-guangzhou  output json  --profile test
tccli configure get secretKey      --profile test
tccli configure list      --profile test
Specify the account when calling the API (with cvm DescribeZones as an example).
tccli cvm DescribeZones --profile test
```


## Using TCCLI
TCCLI integrates all Tencent Cloud products that support TencentCloud API and allows for configuration and management of such products. For example, you can use TCCLI to create and manage a CVM instance, create a CBS disk and view its usage and create a VPC and add resources to it. All operations that can be done on the console pages can be performed by executing commands in TCCLI.
* Use the "tccli cvm DescribeInstances" command to see CVM instances under the current account.
* Use the "tccli cbs DescribeDisks" command to view the list of CBS disks.

Take creating a CVM instance as an example (**please note that the non-simple parameters in the demo must be in standard json format**):
```bash
tccli cvm RunInstances --InstanceChargeType POSTPAID_BY_HOUR --InstanceChargePrepaid '{"Period":1,"RenewFlag":"DISABLE_NOTIFY_AND_MANUAL_RENEW"}'
 --Placement '{"Zone":"ap-guangzhou-2"}' --InstanceType S1.SMALL1 --ImageId img-8toqc6s3 --SystemDisk '{"DiskType":"CLOUD_BASIC", "DiskSize":50}'
--InternetAccessible '{"InternetChargeType":"TRAFFIC_POSTPAID_BY_HOUR","InternetMaxBandwidthOut":10,"PublicIpAssigned":true}' --InstanceCount 1
--InstanceName TCCLI-TEST --LoginSettings '{"Password":"isd@cloud"}' --SecurityGroupIds '["sg-0rszg2vb"]' --HostName TCCLI-HOST-NAME1
```
For details of more functions, you can view the supported products by executing the "tccli help" command, view the supported APIs by executing the "tccli cvm help" command (with CVM as an example) and view the parameters supported by the API by executing the "tccli cbs DescribeDisks help" command (with the DescribeDisks API of CBS as an example).

## Advanced Functions
### Multi-version API Access
Some products may have multiple versions of APIs, and TCCLI accesses the latest version by default. If you want to access a specific old version, you can do so in the following way (with CVM as an example).
```bash
# Set the default version of the CVM product: 2017-03-12.
tccli configure set cvm.version 2017-03-12

# Specify the version number in real time when using.
tccli cvm help --version 2017-03-12
tccli cvm DescribeZones help --version 2017-03-12
tccli cvm DescribeZones --version 2017-03-12
```

### Specifying the Nearest Endpoint
By default, TCCLI requests the nearest endpoint for accessing the service. You can also specify your own endpoint for a product (with CVM as an example).
```bash
# Set the default endpoint of the CVM product.
tccli configure set cvm.endpoint cvm.ap-guangzhou.tencentcloudapi.com

# Specify in real time when calling.
tccli cvm DescribeZones --endpoint cvm.ap-guangzhou.tencentcloudapi.com
```
### Filtering Returned Results
1. Output without any filtering (with the return of the cvm DescribeZones API as an example).
```bash
[root@VM_180_248_centos ~]# tccli cvm DescribeZones
{
    "TotalCount": 4,
    "ZoneSet": [
        {
            "ZoneState": "Available",
            "ZoneId": "100001",
            "Zone": "ap-guangzhou-1",
            "ZoneName": "Guangzhou Zone 1"
        },
        {
            "ZoneState": "Available",
            "ZoneId": "100002",
            "Zone": "ap-guangzhou-2",
            "ZoneName": "Guangzhou Zone 2"
        },
        {
            "ZoneState": "Available",
            "ZoneId": "100003",
            "Zone": "ap-guangzhou-3",
            "ZoneName": "Guangzhou Zone 3"
        },
        {
            "ZoneState": "Available",
            "ZoneId": "100004",
            "Zone": "ap-guangzhou-4",
            "ZoneName": "Guangzhou Zone 4"
        }
    ],
    "RequestId": "4fd313a6-155f-4c7a-bf86-898c02fcae02"
}
```
2. View a specified field.
```bash
[root@VM_180_248_centos ~]# tccli cvm DescribeZones  --filter TotalCount
4
```
3. View the information of the Nth sub-object of a specified array-type object.
```bash
[root@VM_180_248_centos ~]# tccli cvm DescribeZones  --filter ZoneSet[0]
{
    "ZoneState": "Available",
    "ZoneId": "100001",
    "Zone": "ap-guangzhou-1",
    "ZoneName": "Guangzhou Zone 1"
}
```
4. View a certain field of all the sub-objects with a certain name under a specified array-type object.
```bash
[root@VM_180_248_centos ~]# tccli cvm DescribeZones  --filter ZoneSet[*].ZoneName
[
    "Guangzhou Zone 1",
    "Guangzhou Zone 2",
    "Guangzhou Zone 3",
    "Guangzhou Zone 4"
]
```
5. Filter the sub-objects in the array and then present them under a new name.
Note: The content that defines the filtering behavior needs to be marked with single quotes.
```bash
[root@VM_180_248_centos ~]# tccli cvm DescribeZones  --filter 'ZoneSet[*].{name:ZoneName, id:ZoneId}'
[
    {
        "name": "Guangzhou Zone 1",
        "id": "100001"
    },
    {
        "name": "Guangzhou Zone 2",
        "id": "100002"
    },
    {
        "name": "Guangzhou Zone 3",
        "id": "100003"
    },
    {
        "name": "Guangzhou Zone 4",
        "id": "100004"
    }
]
```
