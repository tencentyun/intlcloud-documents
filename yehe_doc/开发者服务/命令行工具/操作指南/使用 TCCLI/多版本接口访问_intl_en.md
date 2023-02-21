
By default, TCCLI accesses the latest version of APIs. However, some products have multiple versions of APIs. To access an API of a specific earlier version, refer to this document.

## Directions
- Taking Cloud Virtual Machine (CVM) as an example, run the following command to set the default API version to `2017-03-12`:
```
tccli configure set cvm.version 2017-03-12
```
- Run the following commands to specify the API version in real time:
```
tccli cvm help --version 2017-03-12
tccli cvm DescribeZones help --version 2017-03-12
tccli cvm DescribeZones --version 2017-03-12
```
