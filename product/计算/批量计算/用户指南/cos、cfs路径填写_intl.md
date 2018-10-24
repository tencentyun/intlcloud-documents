## Summary

Execution logs (StdOut, StdErr) and remote storage mapping in Batch involve entering the COS/CFS path which is slightly different from that when accessing a COS bucket or file through HTTP. See below for details.

## 1. COS Path Description

### Only COS XML API access domain name is supported

![](https://mc.qcloudimg.com/static/img/9e0e71c620551fd4271f5e026978d068/1.png)

The access domain names supported by COS include those applicable to XML API and JSON API, but when entered in Batch, only domain name in the XML API form is supported as shown in the red box above.

### The path has to begin with cos://

![](https://mc.qcloudimg.com/static/img/9e0e71c620551fd4271f5e026978d068/1.png)

For example, when entered as a path in Batch, the address in the figure above requires a cos:// prefix. For details, see below:

``` 
cos://testbatch-1252462967.cos.ap-beijing-1.myqcloud.com/ 
```

``Note: The path has to end with /``

### Mounting a subdirectory

![](https://mc.qcloudimg.com/static/img/5dfebdda44fa0417c03090675a58a099/2.png)

Subdirectories can be added directly after the bucket's domain name as a regular directory. For example, a folder in the bucket above can be entered as the following path when mounted:

``` 
cos://testbatch-1252462967.cos.ap-beijing-1.myqcloud.com/testdir/ 
```

### Only bucket in the same region is supported

COS is region-specific, and you need to ensure that your Batch jobs are in the same region as the COS bucket, so that data can be transferred between the storage and Cloud Virtual Machine (CVM) most efficiently.

## 2. CFS Path Description

In remote storage mapping, you can configure to automatically mount a CFS/NAS path to the local path.

![](https://mc.qcloudimg.com/static/img/7721d8b14f775055615d430528008cb9/3.png)

### The path has to begin with cfs:// or nfs://

For example, when entered as a path in Batch, the address in the figure above requires a cfs:// or nfs:// prefix. For details, see below:

``` 
cfs://10.66.140.208/ 
```

``Note: The path has to end with /. Please make sure your CFS/NAS and Batch jobs are configured in the same network. ``







