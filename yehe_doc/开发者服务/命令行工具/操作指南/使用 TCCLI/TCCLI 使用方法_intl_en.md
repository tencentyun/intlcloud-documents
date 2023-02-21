

## Overview
This document describes how to use the basic features of TCCLI.

TCCLI integrates all Tencent Cloud products that support TencentCloud API, and allows you to configure and manage the products. For example, you can use TCCLI to create and operate a Cloud Virtual Machine (CVM) instance, create a Cloud Block Storage (CBS) disk and view its usage, and create a Virtual Private Cloud (VPC) and add resources to it. All operations that can be performed on console pages can be performed by running commands in TCCLI. Examples:

* Run the `tccli cvm DescribeInstances` command to view CVM instances under the current account.
* Run the `tccli cbs DescribeDisks` command to view the list of CBS disks.



## Basic Feature Usage

<dx-alert infotype="explain" title="">
The following examples are based on Linux. Structures in the examples must be in standard JSON format.
</dx-alert>


### Using TCCLI to create a CVM instance
Run the following command to create a CVM instance:
```bash
tccli cvm RunInstances
--InstanceChargeType POSTPAID_BY_HOUR
--InstanceChargePrepaid '{"Period":1,"RenewFlag":"DISABLE_NOTIFY_AND_MANUAL_RENEW"}'
--Placement '{"Zone":"ap-guangzhou-2"}'
--InstanceType S1.SMALL1
--ImageId img-8toqc6s3
--SystemDisk '{"DiskType":"CLOUD_BASIC", "DiskSize":50}'
--InternetAccessible '{"InternetChargeType":"TRAFFIC_POSTPAID_BY_HOUR","InternetMaxBandwidthOut":10,"PublicIpAssigned":true}' 
--InstanceCount 1
--InstanceName TCCLI-TEST
--LoginSettings '{"Password":"TCCLI"}'
--SecurityGroupIds '["sg-0rszg2vb"]'
--HostName TCCLI-HOST-NAME1
```


### Using standard input to transfer binary files
TCCLI allows you to call APIs with the content type octet-stream. When calling such APIs, you can use standard input `< /path/to/file` to transfer binary files. Example:
```bash
# Taking the CLS UploadLog API as an example, you can use the following command to upload logs:
tccli cls UploadLog --TopicId xxx < /path/to/file
```

###  --cli-unfold-argument
If the API to call uses any structures, you can add `--cli-unfold-argument` in the command to use a dot (.) as the concatenation operator for structure input. In this case, you can use the autocomplete feature of TCCLI to make the input process easier. Example:
```bash
tccli cvm RunInstances --cli-unfold-argument \
--Placement.Zone ap-guangzhou-3 \
--ImageId img-8toqc6s3 \
--DryRun True
```
<dx-alert infotype="explain" title="">
- You can press the Tab key to complete `--cli-unfold-argument`. For details, see [Using the Autocomplete Feature](https://www.tencentcloud.com/document/product/1013/52423).
- You can specify `--cli-unfold-argument` in the command only when using TCCLI `3.0.273.1` or later.
</dx-alert>


### --generate-cli-skeleton
You can use `--generate-cli-skeleton` to generate a parameter skeleton in JSON format. Example:
```bash
# You can also input the generated JSON skeleton into a JSON file.
# $ tccli cvm DescribeInstances --generate-cli-skeleton > /home/test.json
tccli cvm DescribeInstances --generate-cli-skeleton
```
The output is as follows:
```json
{
    "Limit": "Integer", 
    "Filters": [
        {
            "Values": [
                "String"
            ], 
            "Name": "String"
        }
    ], 
    "InstanceIds": [
        "String"
    ], 
    "Offset": "Integer"
}
```
<dx-alert infotype="explain" title="">
- You can press the Tab key to complete `--generate-cli-skeleton`. For more information, see [Using the Autocomplete Feature](https://www.tencentcloud.com/document/product/1013/52423).
- You can specify `--generate-cli-skeleton` in the command only when using TCCLI `3.0.273.1` or later.
</dx-alert>

### --cli-input-json
If there are too many input parameters, you can add `--cli-input-json` in the command to support input through a JSON file. (Add `file://file directory` after `--cli-input-json`.) You can use `--generate-cli-skeleton` to generate the corresponding JSON file. After specifying parameters in the JSON file, you can use the file to call an API. Example:
```bash
tccli cvm DescribeInstances --cli-input-json file:///home/test.json
```
<dx-alert infotype="explain" title="">
- You can press the Tab key to complete `--cli-input-json`. For more information, see [Using the Autocomplete Feature](https://www.tencentcloud.com/document/product/1013/52423).
- You can specify `--cli-input-json` in the command only when using TCCLI `3.0.250.2` or later.
</dx-alert>

