## Overview
The HTTP header of an object is a string sent by the server over HTTP protocol before it sends HTML data to browser. By modifying the HTTP header, you can change the response form of the page or communicate configuration information, such as modifying the caching time. Modifying an object's HTTP header does not modify the object itself.

For example, if the Content-Encoding in Header is modified to gzip, but the file itself has not been compressed to .gz file in advance, a decoding error will occur.

>Note that archived objects do not support custom headers.

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5), and then select the **Bucket List** in the left pane to go to the Bucket List page. Click the bucket of the object to enter the bucket.
![](https://main.qcloudimg.com/raw/8dccbc7b536de784e46edbd8de3c2464.jpg)
2. Locate the object for which you want to set headers, and click **Details** on the right.
![](https://main.qcloudimg.com/raw/160b6e921d1e79de7b36f6533f4910c6.jpg)
3. Go to the **Custom Headers** section, and click **Add Header**. Select a parameter type (enter custom content in the custom field), and enter a value. COS provides the following 6 HTTP headers for objects. Once the configuration is complete, click **Save**.

![](https://main.qcloudimg.com/raw/babe4e3591b0d63a866537a34de12d94.jpg)

<table>
   <tr>
      <th>HTTP Header</th>
      <th>Remarks</th>
      <th>Example</th>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>MIME information of file</td>
      <td>image/jpeg</td>
   </tr>
   <tr>
      <td>Cache-Control</td>
      <td>File caching mechanism</td>
      <td>no-cache;max-age=200</td>
   </tr>
   <tr>
      <td>Content-Disposition</td>
      <td>Extension with a MIME type</td>
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
      <td>x-cos-meta-[custom content]</td>
      <td>Custom content</td>
      <td>x-cos-meta-via: homepage</td>
   </tr>
</table>
4. If you need to add custom headers for more than one object, you can select the objects, and click **Custom Header** under **More Actions**.

![](https://main.qcloudimg.com/raw/f3c395a4cf1a8e29375c1722688642f3.png)

## Samples

Under APPID 1250000000, a bucket named " example" is created. The object exampleobject.txt is uploaded under the bucket root directory.

If you do not customize the HTTP header for the object, the browser or client will get the following Object headers during download:
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

Add the following configurations:
![](https://main.qcloudimg.com/raw/3df9e3628c6d8b429842807771ff547e.jpg)
When you send a request again, the browser or the client will get the following object headers:

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
