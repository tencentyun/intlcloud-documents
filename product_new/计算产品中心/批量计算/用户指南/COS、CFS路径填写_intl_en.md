## Overview
You need to enter COS and CFS paths for execution logs (`StdOut` and `StdErr`) and remote storage mappings in Batch, which is slightly different from access to COS buckets or files in HTTP mode.

##  COS Path Description

### Only Endpoints of COS XML API Format
For Batch path, only endpoints in the XML API format are supported. See the figure below:
![](https://main.qcloudimg.com/raw/f96cd300eaa28ba674ef9d3ab6362b0a.png)



### Prefixed with cos://
The acquired COS endpoint is shown in the following figure.
![](https://main.qcloudimg.com/raw/f96cd300eaa28ba674ef9d3ab6362b0a.png)
Prefix batch paths with `cos://` and suffix them with `/`. 
``` 
cos://batchdemo-125178xxxx.cos.ap-guangzhou.myqcloud.com/
```



### Mounting a Subdirectory
Add subdirectories to a bucket path as common file directories. The following figure shows the subdirectories created in the bucket.
![](https://main.qcloudimg.com/raw/0add1b49c44f4b2740ddc44e3164216b.png)
For directory mounting, the COS paths are as follows:
``` 
cos://batchdemo-125178xxxx.cos.ap-guangzhou.myqcloud.com/logs/
cos://batchdemo-125178xxxx.cos.ap-guangzhou.myqcloud.com/input/
cos://batchdemo-125178xxxx.cos.ap-guangzhou.myqcloud.com/output/
```

### Supporting Intra-Region Buckets
COS has regional attributes. Data transmission between the storage server and Cloud Virtual Machine (CVM) is efficient only when your batch job and COS bucket are in the same region.

## CFS Path Description
In remote storage mappings, you can configure CFS/NAS paths to automatically mount to a local path. See the figure below:
![](https://main.qcloudimg.com/raw/414ac8013f2f31587d75420ec0dc700f.png)

### Prefixed with cfs:// or nfs://
An example of an acquired CFS path is `10.66.xxx.xxx`. Prefix a Batch path with `cfs://` or `nfs://`.
>Suffix a Batch path with `/` and ensure that your CFS/NAS and Batch job configuration are on the same network.
>
``` 
cfs://10.66.xxx.xxx/ 
```









