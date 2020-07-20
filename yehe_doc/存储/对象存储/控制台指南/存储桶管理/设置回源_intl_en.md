### Introduction
You can configure origin-pull rules for buckets on the COS Console. If the object you request does not exist in the bucket, or a specific request needs to be redirected, you can configure origin-pull rules to access corresponding data via COS. Origin-pull configurations are mainly used for hot data migration, redirecting specific requests, and other relevant scenarios.

>The success rate of data origin-pull depends on your network environment.


<img src="https://main.qcloudimg.com/raw/f63a74cf70a9f6582e52e13a2b16e72a.png" width="90%">



### Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the Bucket List page. Click the bucket for which you want to configure the origin-pull to enter the bucket details page.
![](https://main.qcloudimg.com/raw/3797a80a4d8ec0d49d64754530f8fe4d.png)
2. Click **Basic Configuration** on the left sidebar to enter the bucket’s basic configuration page.
3. Scroll down to find the [Origin-Pull Configurations] item, change the current status to “On”, and enter the origin-pull address. Configure the following as described below:
 - **Origin-Pull Address**: Enter the domain name or IP address without the `http://` or `https` prefix. You can also add the port number after the domain name or IP address.
 - **Origin-Pull Protocol**: The HTTP protocol when COS accesses the specified origin server. The options are Force HTTPS, Force HTTP, and Follow Request Protocol.
	 - If you select Force HTTPS/HTTP, COS will access the origin server using HTTPS/HTTP protocol.
	 - If you select Follow Request Protocol, COS will access the origin server with the protocol used in the request.
 - **Origin-Pull Parameter**: Specify whether to pass in COS request parameters when accessing the origin server.
 - **3xx Following Policy**: When the origin server returns a 3XX redirect status code, COS will follow the code by default and pull data from another origin server. If you select **Off**, resources will not be pulled.
 - **Add Origin-Pull Header**: When COS accesses the origin server, it can carry newly added headers you have specified for access. Currently, up to 10 new custom headers can be added. 

Example of a correct address:
```shell
abc.example.com
abc.example.com:8080
10.10.10.10
10.10.10.10:8080
```
4. Click **Save**.


#### Examples
**Background**
A user whose APPID is 1250000000 created a bucket named "examplebucket-1250000000", and enabled CDN acceleration endpoint domain name:
```shell
examplebucket-1250000000.file.myqcloud.com
```

Configure the origin-pull address of the bucket to be:
```shell
abc.example.com
```
Store the image picture.jpg at the origin server `http://abc.example.com`.

**Initial access on the client-end**:
```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```
When COS finds that the object cannot be hit, it returns HTTP status code `302` to the client and is redirected to the following address:
```shell
http://abc.example.com/picture.jpg
```
The origin server then provides the object to the client to ensure access, and COS copies picture.jpg from the origin server and saves it to the root directory of the bucket "example".

**Second-time access**:
```shell
http://examplebucket-1250000000.file.myqcloud.com/picture.jpg
```
COS directly hits the picture.jpg object in the root directory and returns it to the client.
