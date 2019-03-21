## Overview

The HTTP header of an object is a string sent by the server over HTTP protocol before it sends HTML data to browser. By modifying the HTTP header, you can change the response form of the page or communicate configuration information, such as modifying the caching time. Modifying an object's HTTP header does not modify the object itself.
For example, if the Content-Encoding in Header is modified to gzip, but the file itself has not been compressed to .gz file in advance, a decoding error will occur.


## Configuration Steps

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos4/index), and select **Bucket List**  from the left side bar to access the Bucket List page. Click the bucket (such as example) you want to configure origin-pull for and enter the bucket.
   ![](https://main.qcloudimg.com/raw/f9537c1e5103b41f20a69072abfeec5a.png)
2. Locate the object you want to set header for (such as example.exe), and click **More** on the right side of object, then click **Set Header** to pop up the head setting dialog box.
   ![](https://main.qcloudimg.com/raw/197467f1e0eaa6176ae4fb7e36b99289.png)
3. Click **+Add Parameter**, then choose the type of parameter you want to set (enter the custom name for custom content), enter the corresponding value and click **OK** to save.COS provides six object HTTP header identifiers for configuration:

|       HTTP Header       |     Description      |               Example                |
| :-----------------: | :---------: | :-----------------------------: |
|    Cache-Control    |            Caching mechanism of file           |       no-cache;max-age=200       |
|    Content-Type     |             MIME information of file           |            text/html             |
| Content-Disposition | Extension of MIME protocol | attachment; filename="fname.ext" |
|  Content-Encoding   |  Encoding format of file   | UTF-8 |
|Expires	|The expiration date used to control the cache|	Wed, 21 Oct 2015 07:28:00 GMT|
|  x-cos-meta-[custom content]  |   Custom content    |              Custom content               |

![](https://main.qcloudimg.com/raw/191fbd1b903069b5e546bb237b050ee2.png)

## Example

Under APPID 1250000000, a bucket named " examplebucket" is created. The object example.txt is uploaded under the bucket root directory.

If you do not customize the HTTP header for the object, the browser or client will get the following Object headers during download:

**request**

```http
GET /example.txt HTTP/1.1
Host: examplebucket-1250000000.file.myqcloud.com
Accept: */*
```

**response**

```
HTTP/1.1 200 OK
Content-Type: text/plain
Content-Disposition: attachment; filename*="UTF-8''example.txt"
Access-Control-Allow-Origin: *
Last-Modified: Tue, 11 Jul 2017 15:30:35 GMT 
```

Add the following configurations:
![](https://main.qcloudimg.com/raw/2474d24e7d1d365e0c736572aae8f652.png)
When you send a request again, the browser or the client will get the following object headers:

**request**

```http
GET /example.txt HTTP/1.1
Host: examplebucket-1250000000.file.myqcloud.com
Accept: */*
```

**response**

```
HTTP/1.1 200 OK
Cache-Control: no-cache
Content-Type: image/jpeg
Content-Disposition: attachment; filename*="abc.txt"
x-cos-meta-md5: 1234
Access-Control-Allow-Origin: *
Last-Modified: Tue, 11 Jul 2017 15:30:35 GMT
```
