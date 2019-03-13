## Product Introduction

The HTTP header of an object is a string sent by the server over HTTP protocol before it sends HTML data to browser. By modifying the HTTP header, you can change the response form of the page or communicate configuration information, such as modifying the caching time. Modifying an object's HTTP header does not modify the object itself.
For example, if the Content-Encoding in Header is modified to gzip, but the file itself has not been compressed to .gz file in advance, a decoding error will occur.

## Header Configurations

COS provides five object HTTP header identifiers for configuration:

|       HTTP Header       |     Description      |               Example                |
| :-----------------: | :---------: | :-----------------------------: |
|    Cache-Control    |            Caching mechanism of file           |       no-cache;max-age=200       |
|    Content-Type     |             MIME information of file           |            text/html             |
| Content-Disposition | Extension of MIME protocol | attachment; filename="fname.ext" |
| Content-Language   |                Language of file                 |              zh-CN               |
|  Content-Encoding   |  Encoding format of file   | UTF-8 |
|  x-cos-meta-[custom content]  |   Custom content    |              Custom content               |

## Configuration Steps

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos4/index), and select **Bucket List**  from the left side bar to access the Bucket List page. Click the bucket (such as example) you want to configure back-to-origin for and enter the bucket.
   ![](//mc.qcloudimg.com/static/img/b51d5a77d53c3416324ea3eb283c788c/image.png)
2. Locate the object you want to set header for (such as example.exe), and click **More** on the right side of object, then click **Set Header** to pop up the head setting dialog box.
   ![](//mc.qcloudimg.com/static/img/5edf2ba97d32dd82b9c1be1e59379deb/image.png)
3. Click **+Add Parameter**, then choose the type of parameter you want to set (enter the custom name for custom content), enter the corresponding value and click **OK** to save.
   ![](//mc.qcloudimg.com/static/img/2a2ee4acd84b10baaa4c27a5b3118ebc/image.png)

## Example

Under APPID 123456790, a bucket named " example" is created. The object example.txt is uploaded under the bucket root directory.

If you do not customize the HTTP header for the object, the browser or client will get the following Object headers during download:

```http
> GET /example.txt HTTP/1.1
> Host: example-1234567890.file.myqcloud.com
> Accept: */*

< HTTP/1.1 200 OK
< Content-Language:zh-CN
< Content-Type: text/plain
< Content-Disposition: attachment; filename*="UTF-8''example.txt"
< Access-Control-Allow-Origin: *
< Last-Modified: Tue, 11 Jul 2017 15:30:35 GMT 
```

Add the following configurations:
![](//mc.qcloudimg.com/static/img/0d8bb1be135a68204f19f3ea187a75ab/image.png)
When you send a request again, the browser or the client will get the following object headers:

```http
> GET /example.txt HTTP/1.1
> Host: example-1234567890.file.myqcloud.com
> Accept: */*

< HTTP/1.1 200 OK
< Content-Language:zh-CN
< Cache-Control: no-cache
< Content-Type: image/jpeg
< Content-Disposition: attachment; filename*="abc.txt"
< x-cos-meta-md5: 1234
< Access-Control-Allow-Origin: *
< Last-Modified: Tue, 11 Jul 2017 15:30:35 GMT
```
