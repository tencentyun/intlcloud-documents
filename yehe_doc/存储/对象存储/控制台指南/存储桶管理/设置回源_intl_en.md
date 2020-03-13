## Overview
You can configure origin-pull rules for buckets on COS Console. If the object you request does not exist in the bucket, or a specific request needs to be redirected, you can configure origin-pull rules to access corresponding data via COS. Origin-pull configurations are mainly used for data hot migration, redirection of specific requests, and other scenarios.

>The success rate of data origin-pull depends on network environment.


<img src="https://main.qcloudimg.com/raw/f63a74cf70a9f6582e52e13a2b16e72a.png" width="90%">



## Steps
1. Log into the [COS Console](https://console.cloud.tencent.com/cos5), select **Bucket List** in the left pane to enter the Bucket List page. Click the bucket for which you want to configure CORS to enter the bucket details page.
![](https://main.qcloudimg.com/raw/3797a80a4d8ec0d49d64754530f8fe4d.png)
2. Click **Basic Configuration** on the left to enter the basic configuration page of the bucket.
3. Scroll down to find the [Origin-Pull Configurations] item, change the current status to On, and enter the origin-pull address. The configuration items are described as follows:
 - **Origin-Pull Address**: Enter the domain name or IP address without the `http://` or `https` prefix. You can also add the port number after the domain name or IP address.
 - **Origin-Pull Protocol**: The HTTP protocol when COS accesses the origin server you have specified. The options are Force HTTPS, Force HTTP, and Follow Request Protocol.
	 - If you select Force HTTPS/HTTP, COS will access your origin server using HTTPS/HTTP protocol.
	 - If you select Follow Request Protocol, COS will access your origin server with the protocol you use to request COS.
 - **Origin-Pull Parameter**: Specify whether to pass in request parameters used when accessing the COS to the origin server.
 - **3xx Following Policy**: When the origin server returns a 3XX redirect status code, COS by default will follow 3XX to pull data from another origin server again. If you select **Off**, resources will not be pulled.
 - **Add Origin-Pull Header**: When COS accesses your origin server, it can carry the newly added header you have specified for access. Currently, up to 10 new custom headers can be added. 
Example of a correct address:
```shell
abc.example.com
abc.example.com:8080
10.10.10.10
10.10.10.10:8080
```
5. Click **Save**.


#### Samples
**Background**
A user whose APPID is 1250000000 created a bucket named "examplebucket-1250000000", and enabled CDN accelerated domain name:
```shell
examplebucket-1250000000.file.myqcloud.com
```

Configure the origin-pull address of the bucket to:
```shell
abc.example.com
```
Store the image picture.jpg at the origin server `http://abc.example.com`.

**Initial access from the client**:
```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
``` 
When COS finds that the object cannot be hit, it returns the HTTP status code 302 to the client and is redirected to the following address:
```shell
http://abc.example.com/picture.jpg
``` 
The origin server then provides the object to the client to ensure access, and COS copies picture.jpg from the origin server and saves it to the root directory of the bucket "example".

**The second access**:
```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
``` 
COS directly hits the picture.jpg object in the root directory and returns it to the client.
