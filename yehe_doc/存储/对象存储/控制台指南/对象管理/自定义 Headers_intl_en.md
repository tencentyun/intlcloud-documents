## Overview
An HTTP header of an object is a string sent by the server over HTTP before it sends HTML data to the browser. By modifying HTTP headers, you can modify how the webpage responds as well as certain configurations, such as caching time. Modifying an object's HTTP headers does not modify the object itself.

For example, if the `Content-Encoding` header is modified to `gzip`, but the file itself was not compressed using gzip, a decoding error will occur.

>?Note that custom headers are not supported for archived objects.

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar. Click the specific bucket and enter the bucket details page.
2. In this example, select a single object that you want to customize under the **File List** tab, and go to **More Actions** > **Custom Header** under **Operation** to add custom headers. You can also select multiple objects and add custom headers to all of them by going to **More Actions** > Custom Header** at the top.
![](https://main.qcloudimg.com/raw/88779600818f3670df2f7df62fd1b3a0.png)
3. In the pop-up window, click **Add Header**. Select a parameter type, and enter a value for it. COS provides six HTTP headers to choose from. Once the configuration is complete, click **OK**.
![](https://main.qcloudimg.com/raw/191fbd1b903069b5e546bb237b050ee2.png)
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
      <td>UTF-8</td>
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

Assume that a bucket named "examplebucket-1250000000" was created under account APPID 1250000000, and an object “exampleobject.txt” was uploaded to the bucket’s root directory.

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
![](https://main.qcloudimg.com/raw/2474d24e7d1d365e0c736572aae8f652.png)
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

