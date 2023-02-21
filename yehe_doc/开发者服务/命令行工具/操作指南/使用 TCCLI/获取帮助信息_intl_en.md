This document describes how to use TCCLI to view the help information about products and their APIs.

## Directions

### Viewing brief help information
- Run the following command to view supported Tencent Cloud products. You can also view the products at [APIs](https://www.tencentcloud.com/document/api).
```bash
tccli help
```
- Taking Cloud Virtual Machine (CVM) as an example, run the following command to view the CVM APIs that support TCCLI:
```bash
tccli cvm help
```
- Taking the DescribeDisks API of Cloud Block Storage (CBS) as an example, run the following command to view the parameters of the API. For parameter descriptions and API information, see the corresponding API documentation at the Tencent Cloud website.
```bash
tccli cbs DescribeDisks help
```

### Viewing detailed help information
TCCLI displays brief help information by default. To view detailed information, use the `--detail` option.
- Run the following command to view the detailed information about supported Tencent Cloud products:
```bash
tccli help --detail
```
- Taking CVM as an example, run the following command to view the detailed information about the CVM APIs that support TCCLI:
```bash
tccli cvm help --detail
```
- Taking the CBS DescribeDisks API as an example, run the following command to view the detailed information and use cases of the input and output parameters of the API:
```bash
tccli cbs DescribeDisks help --detail
```
