## Overview
An HTTP header (metadata header) of an object is a string sent by the server over HTTP before it sends HTML data to the browser. By modifying HTTP headers (metadata headers), you can modify how the webpage responds as well as certain configurations, such as caching time. Modifying an object's HTTP headers does not modify the object itself.

For example, if the `Content-Encoding` header is modified to `gzip`, but the file itself was not compressed using gzip, a decoding error will occur.

>?Note that custom headers are not supported for archived objects.
>

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left sidebar.
5. Find the object for which to customize a header and click **More Actions** > **Custom Header** in the **Operation** column on its right.
![](https://main.qcloudimg.com/raw/b424c94ad7dddd58dd6489cbb7cc43ee.png)
To customize headers for multiple objects, select multiple objects and click **More Actions** > **Custom Header** at the top.
![](https://main.qcloudimg.com/raw/88779600818f3670df2f7df62fd1b3a0.png)
6. In the pop-up window, select the parameter type of the metadata header to be set, enter the metadata value, and click **OK**.
COS provides the following six types of object HTTP headers for configuration:
![](https://main.qcloudimg.com/raw/cc85c6702c81f1af770dc04a23ae4bb7.png)
<table>
   <tr>
      <th>HTTP Header</th>
      <th>Description</th>
      <th>Example</th>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>MIME information of the file</td>
      <td>image/jpeg</td>
   </tr>
   <tr>
      <td>Cache-Control</td>
      <td>File caching mechanism</td>
      <td>no-cache;max-age=200</td>
   </tr>
   <tr>
      <td>Content-Disposition</td>
      <td>MIME type extension</td>
      <td>attachment;filename="fname.ext"</td>
   </tr>
   <tr>
      <td>Content-Encoding</td>
      <td>File encoding format</td>
      <td>gzip</td>
   </tr>
   <tr>
      <td>Expires</td>
      <td>Controls the expiration date of cache</td>
      <td>Wed, 21 Oct 2015 07:28:00 GMT</td>
   </tr>
   <tr>
      <td>x-cos-meta-[custom suffix]</td>
      <td>User-defined header</td>
      <td>x-cos-meta-via: homepage</td>
   </tr>
</table>


## Examples

Assume that a bucket named "examplebucket-1250000000" was created under account APPID 1250000000, and an object "exampleobject.txt" was uploaded to the bucket's root directory.

The sample below shows the headers returned for a request to download this object through a browser or client if no custom HTTP headers are specified.
#### Request
```sh
GET /exampleobject.txt HTTP/1.1
Host: examplebucket-1250000000.file.myqcloud.com
Accept: */*
```

#### Response
```http
HTTP/1.1 200 OK
Content-Language:zh-CN
Content-Type: text/plain
Content-Disposition: attachment; filename*="UTF-8''exampleobject.txt"
Access-Control-Allow-Origin: *
Last-Modified: Tue, 11 Jul 2017 15:30:35 GMT 
```

If you add custom headers as follows:
![](https://main.qcloudimg.com/raw/3df9e3628c6d8b429842807771ff547e.jpg)
then the headers returned for new requests will be as follows:

#### Request
```sh
GET /exampleobject.txt HTTP/1.1
Host: examplebucket-1250000000.file.myqcloud.com
Accept: */*
```

#### Response
```http
HTTP/1.1 200 OK
Content-Language:zh-CN
Cache-Control: no-cache
Content-Type: image/jpeg
Content-Disposition: attachment; filename*="abc.txt"
x-cos-meta-md5: 1234
Access-Control-Allow-Origin: *
Last-Modified: Tue, 11 Jul 2017 15:30:35 GMT
```

