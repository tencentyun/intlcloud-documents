# Using Advanced Features

## Operation Scenarios

This document describes how to use the advanced features of TCCLI International Version, including multi-version API access, nearest access point specifying, and return result filtering.

## Directions

### Multi-version API access

Some products may have multiple versions of APIs, and TCCLI accesses the latest version by default. If you want to access a specific legacy version, you can do so in the following way (with CVM as an example).

```bash
# Set the default version of the CVM product: 2017-03-12
tccli configure set cvm.version 2017-03-12

# Specify the version number in real time when using
tccli cvm help --version 2017-03-12
tccli cvm DescribeZones help --version 2017-03-12
tccli cvm DescribeZones --version 2017-03-12
```

### Specify the nearest access point (Endpoint)

By default, TCCLI requests the nearest endpoint for accessing a service. You can also specify your own endpoint for a product (with CVM as an example).

```bash
# Set the default endpoint of the CVM product
tccli configure set cvm.endpoint cvm.ap-guangzhou.tencentcloudapi.com

# Specify in real time when calling
tccli cvm DescribeZones --endpoint cvm.ap-guangzhou.tencentcloudapi.com
```

### Filtering return results

1. Output without any filtering (with the return result of CVM DescribeZones API as an example):

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
    "RequestId": "4fd313a6-155f-4c7a-bf86-898c02fcae02"
   }
   ```

2. View a specified field:

   ```bash
   [root@VM_180_248_centos ~]# tccli cvm DescribeZones  --filter TotalCount
   4
   ```

3. View the information of the Nth sub-object of a specified object in array type.

   ```bash
   [root@VM_180_248_centos ~]# tccli cvm DescribeZones  --filter ZoneSet[0]
   {
    "ZoneState": "AVAILABLE",
    "ZoneId": "100001",
    "Zone": "ap-guangzhou-1",
    "ZoneName": "Guangzhou Zone 1"
   }
   ```

4. View a certain field of all the sub-objects with a certain name under the specified object in array type.

   ```bash
[root@VM_180_248_centos ~]# tccli cvm DescribeZones  --filter ZoneSet[*].ZoneName
   [
    "Guangzhou Zone 1",
    "Guangzhou Zone 2",
    "Guangzhou Zone 3",
    "Guangzhou Zone 4"
   ]
   ```
   
5. Filter the sub-objects in the array and then present them under a new name:

   > Note:
   >
   > The content that defines the filtering behavior needs to be marked with single quotes.

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