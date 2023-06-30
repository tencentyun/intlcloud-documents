
This document describes the COS access methods and the way to determine a private network access. It also provides the connectivity test sample to help you learn more about CVM access to COS.

## Access Methods
If you have deployed a service in Tencent Cloud to access COS, different access modes apply to as follows:
- **Intra-region access**: access within the same region will be automatically directed to a private network address. A private network connection is automatically used, incurring no traffic fees. Therefore, we recommend choosing the same region when you purchase different Tencent Cloud products to save on costs.
- **Cross-region access**: currently, cross-region requests do not support private network access and will be resolved to a public network address by default.

## Determining a Private Network Access
To determine whether a CVM accesses COS via a private network, perform the following steps.
Run the `nslookup` command on the CVM to resolve the COS domain name. If a private IP is returned, the access is over a private network; otherwise, it is over a public network.
1. Obtain and record the bucket access domain as instructed in [Bucket Overview](https://www.tencentcloud.com/document/product/436/38493).
2. Log in to the CVM instance and run the `nslookup` command. Assume that `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com` is the address of the destination bucket, run the following command.
```
nslookup examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
```
In the command output, the `10.148.214.13` and `10.148.214.14` IPs indicate that the access to COS is over a private network.
<dx-alert infotype="explain" title="">
Generally, a private IP address is in the format of `10.*.*.*` or `100.*.*.*`, while a VPC IP address `169.254.*.*`. Both IP formats are on the private network.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/49a7d7429ec2a96d271f6a63926286ea.png"/>

## Test Connectivity
See the “Testing connectivity” section in [Request Creation Overview](https://www.tencentcloud.com/document/product/436/30613) for the COS access samples through a public network, access through Tencent Cloud CVMs (classic network) within the same region and access through Tencent Cloud CVMs (VPC) within the same region.


## Relevant operations
- [Mounting COS to Windows Server as Local Drive](https://www.tencentcloud.com/document/product/436/40490)
- [Storing Remote WordPress Attachments to COS](https://www.tencentcloud.com/document/product/436/34082)


