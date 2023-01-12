## Feature Overview
An HTTP header (metadata header) of an object is a string sent by the server over HTTP before it sends HTML data to the browser. By modifying HTTP headers (metadata headers), you can modify how the webpage responds as well as certain configurations, such as caching time. Modifying an object's HTTP headers does not modify the object itself.

For example, if the `Content-Encoding` header is changed to `gzip`, but the file itself was not compressed using gzip, a decoding error will occur.

>?Custom headers are not supported for archived objects.
>

## How It Works

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the object resides and click the bucket name.
4. Click **File List** on the left sidebar.
5. Locate the object for which a header is to be customized and click **More Actions** > **Custom Header** in the **Operation** column on its right. To customize headers for multiple objects, select multiple objects and click **More Actions** > **Custom Header** at the top.
6. In the pop-up window, select the parameter type of the metadata header to be set, enter the metadata value, and click **OK**.
COS provides the following six types of object HTTP headers for configuration:
<table>
   <tr>
      <th>HTTP Header</th>
      <th>Remarks</th>
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


## License request example

Assume that a bucket named "examplebucket-1250000000" was created under account APPID 1250000000, and an object "exampleobject.txt" was uploaded to the bucket's root directory.

The sample below shows the headers returned for a request to download this object through a browser or client if no custom HTTP headers are specified.

#### Request

```plaintext
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:16 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511316;1586518516&q-key-time=1586511316;1586518516&q-header-list=date;host&q-url-param-list=&q-signature=1bd1898e241fb978df336dc68aaef4c0acae****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: text/plain
Content-Disposition: attachment; filename*="UTF-8''exampleobject.txt"
Access-Control-Allow-Origin: *
Last-Modified: Fri, 10 Apr 2020 09:35:05 GMT 
```

If you add custom headers as follows:

then the headers returned for new requests will be as follows:

#### Request

```plaintext
GET /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Apr 2020 09:35:16 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1586511316;1586518516&q-key-time=1586511316;1586518516&q-header-list=date;host&q-url-param-list=&q-signature=1bd1898e241fb978df336dc68aaef4c0acae****
Connection: close
```

#### Response

```plaintext
HTTP/1.1 200 OK
Cache-Control: no-cache
Content-Type: image/jpeg
Content-Disposition: attachment; filename*="abc.txt"
x-cos-meta-md5: 1234
Access-Control-Allow-Origin: *
Last-Modified: Fri, 10 Apr 2020 09:35:05 GMT 
```

