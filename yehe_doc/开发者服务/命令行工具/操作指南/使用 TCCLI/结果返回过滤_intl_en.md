Some commands return much information in the output. You can filter the information as required.

## Directions
This document describes how different filtering methods are used and their corresponding outcomes. The DescribeZones API of Cloud Virtual Machine (CVM) is used as an example in this document.

- View the unfiltered output.
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
- View a specified field.
```bash
[root@VM_180_248_centos ~]# tccli cvm DescribeZones  --filter TotalCount
4
```
- View the Nth sub-object of a specified object in array type.
<dx-alert infotype="notice" title="">
On macOS, the error `zsh: no matches found: xxx` may be returned after you run the following command. To resolve this issue, enclose the filter in single quotes.
</dx-alert>
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
- Filter the sub-objects in an array and display them with a new name.
<dx-alert infotype="notice" title="">
The filter must be enclosed in single quotes.
</dx-alert>
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
