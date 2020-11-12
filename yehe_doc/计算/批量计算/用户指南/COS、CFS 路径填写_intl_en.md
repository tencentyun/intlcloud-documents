## Overview
You need to enter COS and CFS paths for execution logs (`StdOut` and `StdErr`) and remote storage mappings in BatchCompute, which is slightly different from access to COS buckets or files in HTTP mode.

## COS Path Description

### Only endpoints in COS XML API format
For BatchCompute paths, only endpoints in the XML API format are supported as shown below:
![](https://main.qcloudimg.com/raw/f96cd300eaa28ba674ef9d3ab6362b0a.png)



### Prefixed with cos://
The obtained COS endpoint is as shown below:
![](https://main.qcloudimg.com/raw/f96cd300eaa28ba674ef9d3ab6362b0a.png)
Prefix BatchCompute paths with `cos://` and suffix them with `/`.
``` 
cos://batchdemo-125178xxxx.cos.ap-guangzhou.myqcloud.com/
```



### Mounting subdirectory
Add subdirectories to a bucket path as common file directories. The following figure shows the subdirectories created in the bucket.
![](https://main.qcloudimg.com/raw/0add1b49c44f4b2740ddc44e3164216b.png)
For directory mounting, the COS paths are as follows:
``` 
cos://batchdemo-125178xxxx.cos.ap-guangzhou.myqcloud.com/logs/
cos://batchdemo-125178xxxx.cos.ap-guangzhou.myqcloud.com/input/
cos://batchdemo-125178xxxx.cos.ap-guangzhou.myqcloud.com/output/
```

### Supporting intra-region buckets
COS has regional attributes. Data transfer between the storage server and Cloud Virtual Machine (CVM) is efficient only when your BatchCompute job and COS bucket are in the same region.

## CFS Path Description
In remote storage mappings, you can configure CFS/NAS paths to automatically mount to a local path as shown below:
![](https://main.qcloudimg.com/raw/96194f01e1ac7e5fc86cda96c792e403.png)

### Prefixed with cfs:// or nfs://
An example of an obtained CFS path is `10.66.xxx.xxx`. Prefix a BatchCompute path with `cfs://` or `nfs://`.
>!Suffix the path with `/` and ensure that your CFS/NAS and BatchCompute job are on the same network.
>
``` 
cfs://10.66.xxx.xxx/ 
```









