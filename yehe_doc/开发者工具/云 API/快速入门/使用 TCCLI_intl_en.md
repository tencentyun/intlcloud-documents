Tencent Cloud Command Line Interface (TCCLI) is a unified tool for managing Tencent Cloud resources. With TCCLI, you can quickly and easily call Tencent Cloud APIs to manage your resources and automate them through scripts for diversified combination and reuse. 

The table below describes the basic and advanced TCCLI features:
<table>
<tr>
<th>Feature</th><th>Description</th>
</tr>
<tr>
<td><a href="#primaryfunction">Basic features</a></td>
<td>
<ul style="margin:0px">
<li>Configures TCCLI</li>
<li>Provides help information</li>
<li>Outputs results in JSON, table or text format</li>
</ul>
</td>
</tr>
<tr>
<td><a href="#sophisticatedfunctions">Advanced features</a></td>
<td>
<ul style="margin:0px">
<li>Supports multi-version API access</li>
<li>Specifies the nearest access point (Endpoint)</li>
<li>Filters return results</li>
<li>Outputs the input parameters structure to JSON</li>
<li>Reads and calls a JSON file</li>
<li>Calls complex type dot (.) expansion</li>
</ul>
</td>
</tr>
</table>

## Installing TCCLI
1. Before installing TCCLI, make sure that your system has the Python environment and pip tool installed. For more information, see [Python](https://intl.cloud.tencent.com/document/product/494/7244).
>!
>- Use Python 2.7 or a later version. For more information, please see [Python's official website](https://www.python.org/) and [pip's official website](https://pypi.org/project/pip/). 
>- TCCLI depends on the TencentCloudApi Python SDK. If the version number of the TencentCloudApi Python SDK is earlier than that of TCCLI to be installed, the TencentCloudApi Python SDK will be automatically upgraded when TCCLI is installed.
>
2. In Windows, press **Win+R**, enter `cmd` and click **OK**. This document uses the LinuxOS as an example.
3. Run the following command to install TCCLI.
```
pip install tccli
```
>! Run the following commands to upgrade TCCLI earlier than version 3.0.96.1:
```
sudo pip uninstall tccli jmespath
sudo pip install tccli
```
>
4. Run the following command to verify whether TCCLI is successfully installed:
```
tccli --version
```
If the following result is returned, it indicates that TCCLI has been successfully installed.

```bash
[root@VM_180_248_centos ~]# tccli --version
3.0.250.1
```

5. Run the following command to enable the autocomplete feature that also corrects uppercase/lowercase misuse.
```bash
complete -C 'tccli_completer' tccli
```
The following code snippets display the autocomplete process:

```bash
[root@VM_33_50_centos ~]# tccli c
cam          cbs          cdn          chdfs        ckafka       cloudhsm     cms          cr           cynosdb 
captcha      ccc          cds          cim          clb          cme          configure    cvm          
cat          cdb          cfs          cis          cloudaudit   cmq          cpdp         cws          
[root@VM_33_50_centos ~]# tccli cvm R
RebootInstances                      ResetInstance                        ResetInstancesType 
RenewHosts                           ResetInstancesInternetMaxBandwidth   ResizeInstanceDisks 
RenewInstances                       ResetInstancesPassword               RunInstances 
[root@VM_33_50_centos ~]# tccli cvm RunInstances --
--ActionTimer               --generate-cli-skeleton     --InstanceType              --SecurityGroupIds 
--ClientToken               --HostName                  --InternetAccessible        --SystemDisk 
--cli-input-json            --HpcClusterId              --LoginSettings             --TagSpecification 
--DataDisks                 --ImageId                   --output                    --timeout 
--DisasterRecoverGroupIds   --InstanceChargePrepaid     --Placement                 --UserData 
--DryRun                    --InstanceChargeType        --profile                   --version 
--endpoint                  --InstanceCount             --region                    --VirtualPrivateCloud 
--EnhancedService           --InstanceMarketOptions     --secretId                  
--filter                    --InstanceName              --secretKey                 
[root@VM_33_50_centos ~]# tccli cvm RunInstances --Placement 
```

## Configuring TCCLI
1. Run the following command to enter the interactive mode for quick configuration.
```bash
tccli configure
```
Configure the parameters as follows:
```bash
 TencentCloud API secretId [*afcQ]:
 TencentCloud API secretKey [*ArFd]:
 region: 
 output[json]:
```
 * **secretId**: SecretId of your TencentCloud API key, which can be obtained at [Manage API Key](https://console.cloud.tencent.com/cam/capi). A root account can apply for up to two API keys.
 * **secretKey**: SecretKey of your TencentCloud API key, which can be obtained at [Manage API Key](https://console.cloud.tencent.com/cam/capi).
 * **region**: the region of Tencent Cloud services. Use the relevant [APIs](https://intl.cloud.tencent.com/document/api) to obtain available regions, such as [Region List](https://intl.cloud.tencent.com/document/product/213/31574) for CVM.
 - **output:** optional, output format of the request return packet. Valid values: JSON, table, text. Default value: JSON.
     For more information, please run the `tccli configure help` command.
2. In command line mode, you can configure the information in an automated script: 
```bash
 # The `set` subcommand is used to configure one or more items.
 tccli configure set secretId AKIDwLw1234***********nR2OTI787aBCDP
 tccli configure set region ap-guangzhou  output json
 # The `get` subcommand is used to obtain configuration information.
 tccli configure get secretKey
 secretKey = OxXj7khcV1234*********dCc1LiArFd
 # The `list` subcommand is used to print out all configuration information.
 tccli configure list
 credential:
 secretId =  AKIDwLw1234**********nR2OTI787aBCDP
 secretKey =  OxXj7khcV1234*********dCc1LiArFd
 configure:
 region =  ap-guangzhou
 output =  json
```
Use the `tccli configure [list, get or set] help` command such as `tccli configure list help` to view more information. 
3. Configure multiple accounts for easy use. 
```bash
 # Specify the account name `test` in an interactive mode.
 $ tccli configure --profile test
 TencentCloud API secretId [*BCDP]:AKIDwLw1234***********R2OTI787aBCDP
 TencentCloud API secretKey [*ArFd]:OxXj7khcV1234*********dCc1LiArFd
 region: ap-guangzhou
 output[json]:
 # Specify the account name “test” for `set/get/list` subcommands. This command has the same effect as the previous one.
 $ tccli configure set region ap-guangzhou  output json secretId AKIDwLw1234***********R2OTI787aBCDP secretKey OxXj7khcV1234*********dCc1LiArFd --profile test
 # Modify a parameter (such as region) alone:
 $ tccli configure set region ap-beijing
 # View the key or configurations of the `test` user.
 $ tccli configure get secretKey --profile test
 $ tccli configure list --profile test
 # Specify an account when calling an API such as DescribeZones API for CVM.
 $ tccli cvm DescribeZones --profile test
```

## Using TCCLI
<span id ="primaryfunction"></span>
### Basic features
TCCLI supports custom configurations, provides help information, and outputs results in JSON, table or text.
>! The non-simple parameters in the examples must be in standard JSON format. 
>
TCCLI currently supports the following three calling methods:
* JSON strings
* JSON file --cli-input-json
* Complex type dot (.) expansion --cli-unfold-argument

#### Calling sample of JSON strings
- Run the following command to create a CVM instance.
```bash
$ tccli cvm RunInstances --InstanceChargeType POSTPAID_BY_HOUR --InstanceChargePrepaid '{"Period":1,"RenewFlag":"DISABLE_NOTIFY_AND_MANUAL_RENEW"}' --Placement '{"Zone":"ap-guangzhou-2"}' --InstanceType S1.SMALL1 --ImageId img-8toqc6s3 --SystemDisk '{"DiskType":"CLOUD_BASIC", "DiskSize":50}' --InternetAccessible '{"InternetChargeType":"TRAFFIC_POSTPAID_BY_HOUR","InternetMaxBandwidthOut":10,"PublicIpAssigned":true}' --InstanceCount 1 --InstanceName TCCLI-TEST --LoginSettings '{"Password":"isd@cloud"}' --SecurityGroupIds '["sg-0rszg2vb"]' --HostName TCCLI-HOST-NAME1
```
- Run the following command to obtain the CVM’s monitoring data.
```bash
[root@VM_33_50_centos ~]# tccli monitor GetMonitorData --Namespace "QCE/CVM" --Period 300 --MetricName "CPUUsage" --Instances '[{"Dimensions":[{"Name":"InstanceId","Value":"ins-cac6a4w8"}]}]'
```

#### Calling sample of JSON file (--cli-input-json)
1. Run the following command to output the input parameters to a JSON file.
```bash
[root@VM_33_50_centos ~]# tccli cvm RunInstances  --generate-cli-skeleton > /tmp/RunInstances.json
```
2. Replace with your actual values, and pass in the JSON file in the format of `--cli-input-json` followed by `file://+file path` as shown below:
```bash
[root@VM_33_50_centos ~]# tccli cvm RunInstances --cli-input-json file:///tmp/RunInstances.json
{
        "RequestId": "20e2b42d-3260-4750-9293-79116208330e", 
        "InstanceIdSet": null
}
```

#### Calling sample of complex type dot (.) expansion (--cli-unfold-argument)
This method expands and joins a complex type in dots to solve the input difficulties with the CLI autocomplete feature and avoid errors.
For example, `{"a":{"b": "c"}}` will be expanded to `--a.b c`. For a complex array, use `.0` and `.1` to represent the first and second elements of the array. For a simple array, separate multiple elements with spaces, such as `--Integer 10 20` and `--String str1 str2`.

Run the following command to create a CVM instance.
```bash
[root@VM_33_50_centos ~]# tccli cvm RunInstances --cli-unfold-argument --InstanceChargeType POSTPAID_BY_HOUR --InstanceChargePrepaid.Period 1 --InstanceChargePrepaid.RenewFlag DISABLE_NOTIFY_AND_MANUAL_RENEW --Placement.Zone ap-guangzhou-2 --InstanceType S1.SMALL1 --ImageId img-8toqc6s3 --SystemDisk.DiskType CLOUD_BASIC --SystemDisk.DiskSize 50 --InternetAccessible.InternetChargeType TRAFFIC_POSTPAID_BY_HOUR --InternetAccessible.InternetMaxBandwidthOut 10 --InternetAccessible.PublicIpAssigned True --InstanceCount 1 --InstanceName TCCLI-TEST --LoginSettings.Password isd@cloud --SecurityGroupIds sg-0rszg2vb --HostName TCCLI-HOST-NAME1
```


#### More use cases
Use the following commands to learn more about TCCLI:
- Run the `tccli help` command to learn all command usage.
```bash
[root@VM_33_50_centos ~]# tccli help
NAME
    tccli
DESCRIPTION
    tccli (Tencent Cloud Command Line Interface) is a tool to manage your Tencent Cloud services.
CONFIGURE
    Before using tccli, you should use the command(tccli configure) to configure your profile as the default For more in
    formation, please enter tccli configure help
USEAGE
    tccli [options] <service> [options] <action> [options] [options and parameters]
OPTIONS
    help
    show the tccli help info
    --version
    show the version of tccli
AVAILABLE SERVICES
    af
    Describes how to manage loan anti-fraud via APIs.
    afc
    Describes how to customize modeling via APIs.
    ame
    Describes how to operate genuine music library via APIs, including material acquisition, data reporting, etc.
    ......
```
- Run the `tccli cvm help` command to view supported APIs. This document uses CVM as an example.
```bash
[root@VM_33_50_centos ~]# tccli cvm help
NAME
    cvm
AVAILABLE VERSIONS
    2017-03-12
    Only the latest version will be displayed by default. Use `help --version xxxx-xx-xx` to check other versions.
DESCRIPTION
    cvm-2017-03-12
    Describes how to manage and operate CVM instances via APIs, including image, key, and other resources.
USEAGE
    tccli cvm <action> [--param...]
OPTIONS
    help
    show the tccli cvm help info
AVAILABLE ACTIONS
    AllocateHosts
    Creates a CDH instance
    AssociateInstancesKeyPairs
    Binds a key pair
    AssociateSecurityGroups
    Binds a security group
    ......
```
- Run the `tccli cbs DescribeDisks help` command to view the supported API parameters. This document uses DescribeDisks API for CBS as an example.
```bash
[root@VM_33_50_centos ~]# tccli cbs DescribeDisks help
NAME
    DescribeDisks
DESCRIPTION
    cbs-2017-03-12-DescribeDisks
    This API is used to query the list of cloud disks.
    * You can filter cloud disks by ID, type, status, etc. The relationship between different filters is logical `AND`. For more information on filters, see 
    `Filter`.
    * If the parameter is empty, a number (as specified by `Limit`; the default is 20) of cloud disk will be returned.
USEAGE
    tccli cbs DescribeDisks [--param...]
OPTIONS
    help
    show the tccli cbs DescribeDisks help info
    --region
    identify the region to which the instance you want to work with belongs.
    --timeout
    specify a request timeout
    --secretKey
    specify a SecretKey
    ......  
AVAILABLE PARAMS
    --Limit (Integer | Optional)
    The number of returned results. Default value: 20. Maximum value: 100. For more information on `Limit`, see the relevant sections in API [Introduction](https://intl.cloud.tencent.com/document/product/362/15633).
    --OrderField (String | Optional)
    Field by which the cloud disks are sorted in the response. Valid values: <br><li>CREATE_TIME: sort by creation time <br><li>DEADLINE: sort by expiration time
    <br>By default, the results are sorted by creation time.
    --Offset (Integer | Optional)
    The offset. Default value: 0. For more information on `Offset`, see the relevant sections in API [Introduction](https://intl.cloud.tencent.com/document/product/362/15633).
    ......
```
- Output results to JSON, table or text
  - **JSON**
```bash
[root@VM_33_50_centos ~]# tccli cvm DescribeRegions 
{
    "TotalCount": 20, 
    "RegionSet": [
        {
            "RegionState": "AVAILABLE", 
            "Region": "ap-beijing", 
            "RegionName": "North China (Beijing)"
        }, 
        {
            "RegionState": "AVAILABLE", 
            "Region": "ap-chengdu", 
            "RegionName": "Southwest China (Chengdu)"
        },
        {
            "RegionState": "AVAILABLE", 
            "Region": "ap-guangzhou", 
            "RegionName": "South China (Guangzhou)"
        }, 
        {
            "RegionState": "AVAILABLE", 
            "Region": "ap-hongkong", 
            "RegionName": "Hong Kong, Macao and Taiwan, China (Hong Kong)"
        },  
        {
            "RegionState": "AVAILABLE", 
            "Region": "ap-singapore", 
            "RegionName": "Southeast Asia (Singapore)"
        }, 
        {
            "RegionState": "AVAILABLE", 
            "Region": "ap-tokyo", 
            "RegionName": "Asia Pacific (Tokyo)"
        }, 
        {
            "RegionState": "AVAILABLE", 
            "Region": "eu-frankfurt", 
            "RegionName": "Europe (Frankfurt)"
        }, 
        ......
    ], 
    "RequestId": "e5125cf1-****-****-****-316f18eed021"
}
```
 - **Table**:

```bash
[root@VM_33_50_centos ~]# tccli cvm DescribeRegions --output table
--
|                        action                        |
+---------------------------------------+--------------+
|               RequestId               | TotalCount   |
+---------------------------------------+--------------+
|  1af5f2a0-****-****-****-462f0271a69f |  20          |
+---------------------------------------+--------------+
||                      RegionSet                     ||
|+-------------------+----------------+---------------+|
||      Region       |  RegionName    |  RegionState  ||
|+-------------------+----------------+---------------+|
||  ap-bangkok       |  Asia Pacific (Bangkok)      |  AVAILABLE    ||
||  ap-beijing       |  North China (Beijing)      |  AVAILABLE    ||
||  ap-chengdu       |  Southwest China (Chengdu)     |  AVAILABLE    ||
||  ap-chongqing     |  Southwest China (Chongqing)     |  AVAILABLE    ||
||  ap-guangzhou     |  South China (Guangzhou)      |  AVAILABLE    ||
||  ap-guangzhou-open|   South China (Guangzhou Open)  |  AVAILABLE    ||
||  ap-hongkong      |  Hong Kong, Macao, and Taiwan (Hong Kong, China)   |  AVAILABLE    ||
||  ap-mumbai        |  Asia Pacific (Mumbai)      |  AVAILABLE    ||
||  ap-nanjing       |  East China (Nanjing)      |  AVAILABLE    ||
||  ap-seoul         |  Asia Pacific (Seoul)      |  AVAILABLE    ||
||  ap-shanghai      |  East China (Shanghai)      |  AVAILABLE    ||
||  ap-singapore     |  Southeast Asia (Singapore)    |  AVAILABLE    ||
||  ap-tokyo         |  Asia Pacific (Tokyo)      |  AVAILABLE    ||
||  eu-frankfurt     |  Europe (Frankfurt)    |  AVAILABLE    ||
||  eu-moscow        |  Europe (Moscow)     |  AVAILABLE    ||
||  na-ashburn       |  Eastern US (Virginia)    |  AVAILABLE    ||
||  na-siliconvalley |  Western US (Silicon Valley)      |  AVAILABLE    ||
||  na-toronto       |  North America (Toronto)     |  AVAILABLE    ||
|+-------------------+----------------+---------------+|
```

 - **Text**:

```bash
[root@VM_33_50_centos ~]# tccli cvm DescribeRegions --output text
70bbd02f-****-****-****-afc5c34018ae    20
REGIONSET       ap-bangkok      Asia Pacific (Bangkok)   AVAILABLE
REGIONSET       ap-beijing      North China (Beijing)  AVAILABLE
REGIONSET       ap-chengdu      Southwest China (Chengdu)  AVAILABLE
REGIONSET       ap-chongqing    Southwest China (Chongqing)  AVAILABLE
REGIONSET       ap-guangzhou    South China (Guangzhou)   AVAILABLE
REGIONSET       ap-guangzhou-open       South China (Guangzhou Open)      AVAILABLE
REGIONSET       ap-hongkong     Hong Kong, Macao, and Taiwan (Hong Kong, China)    AVAILABLE
REGIONSET       ap-mumbai       Asia Pacific (Mumbai)  AVAILABLE
REGIONSET       ap-nanjing      East China (Nanjing)  AVAILABLE
REGIONSET       ap-seoul        Asia Pacific (Seoul)  AVAILABLE
REGIONSET       ap-shanghai     East China (Shanghai) AVAILABLE
REGIONSET       ap-singapore    Southeast Asia (Singapore)      AVAILABLE
REGIONSET       ap-tokyo        Asia Pacific (Tokyo)   AVAILABLE
REGIONSET       eu-frankfurt   Europe (Frankfurt)      AVAILABLE
REGIONSET       eu-moscow       Europe (Moscow)        AVAILABLE
REGIONSET       na-ashburn      Eastern US (Virginia)      AVAILABLE
REGIONSET       na-siliconvalley        Western US (Silicon Valley)   AVAILABLE
REGIONSET       na-toronto      North America (Toronto)        AVAILABLE
```
<span id ="sophisticatedfunctions"></span>
### Advanced features
This document uses CVM as an example to describe how to use TCCLI advanced features, including multi-version access, specifying nearest access point, filtering the return results, outputting input parameters to JSON, and passing in a JSON file.

#### Multi-version API access
Some products may have APIs in multiple versions, and TCCLI accesses the latest version by default. If you want to access a specific legacy version, you can do so in the following way:
- Method 1: use the default CVM version 2017-03-12
```bash
tccli configure set cvm.version 2017-03-12
```
- Method 2: specify the version number during use
```
tccli cvm help --version 2017-03-12
tccli cvm DescribeZones help --version 2017-03-12
tccli cvm DescribeZones --version 2017-03-12
```

#### Specifying the nearest access point (Endpoint)
By default, TCCLI requests the nearest endpoint for accessing a service. You can also specify the endpoint for a product.
- Set the default endpoint of the CVM product
```bash
tccli configure set cvm.endpoint cvm.ap-guangzhou.tencentcloudapi.com
```
- Specify the endpoint when calling
```
tccli cvm DescribeZones --endpoint cvm.ap-guangzhou.tencentcloudapi.com
```

#### Filtering return results
- Output without any filtering (using the return result of the CVM DescribeZones API as an example):
```bash
   [root@VM_180_248_centos ~]# tccli cvm DescribeZones
   {
    "TotalCount": 4,
    "ZoneSet": [
        {
            "ZoneState": "AVAILABLE",
            "ZoneId": "100001",
            "Zone": "ap-guangzhou-1",
            "ZoneName": "Guangzhou Zone 1"
        },
        {
            "ZoneState": "AVAILABLE",
            "ZoneId": "100002",
            "Zone": "ap-guangzhou-2",
            "ZoneName": "Guangzhou Zone 2"
        },
        {
            "ZoneState": "AVAILABLE",
            "ZoneId": "100003",
            "Zone": "ap-guangzhou-3",
            "ZoneName": "Guangzhou Zone 3"
        },
        {
            "ZoneState": "AVAILABLE",
            "ZoneId": "100004",
            "Zone": "ap-guangzhou-4",
            "ZoneName": "Guangzhou Zone 4"
        }
    ],
    "RequestId": "4fd313a6-****-****-****-898c02fcae02"
   }
```
- View a specified field
```bash
[root@VM_180_248_centos ~]# tccli cvm DescribeZones  --filter TotalCount
4
```
- View the information of the Nth sub-object of a specified object in array type
```bash
 [root@VM_180_248_centos ~]# tccli cvm DescribeZones  --filter ZoneSet[0]
 {
	"ZoneState": "AVAILABLE",
	"ZoneId": "100001",
	"Zone": "ap-guangzhou-1",
	"ZoneName": "Guangzhou Zone 1"
 }
```
- View a certain field of all the sub-objects with a certain name under the specified object in array type.
```bash
   [root@VM_180_248_centos ~]# tccli cvm DescribeZones  --filter ZoneSet[*].ZoneName
   [
    "Guangzhou Zone 1",
    "Guangzhou Zone 2",
    "Guangzhou Zone 3",
    "Guangzhou Zone 4"
   ]
```
- Filter the sub-objects in an array and display them with a new name 
>! The filter needs to be marked with single quotes.
>
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

## FAQs

#### How do I purchase TCCLI?

This service is free of charge. Please [submit a ticket](https://console.cloud.tencent.com/workorder/category) if you need any help.

#### How do I implement API authentication?
Select the **Making API Requests** > **Signature** directory of the product that supports API to authenticate access requests. For example, see [Signature](https://intl.cloud.tencent.com/document/product/213/31575) for CVM.

