## Single-Connection Bandwidth Limit

COS supports traffic control for file uploads and downloads to guarantee normal network bandwidth for your other applications. You can add the `x-cos-traffic-limit` parameter in a request for [PutObject](https://intl.cloud.tencent.com/document/product/436/7749), [PostObject](https://intl.cloud.tencent.com/document/product/436/14690), [GetObject](https://intl.cloud.tencent.com/document/product/436/7753), or [UploadPart](https://intl.cloud.tencent.com/document/product/436/7750) and set a speed limit value. Then, COS will control the network bandwidth for the request accordingly.

## Instructions

- You can put a traffic limit on a request by specifying the `x-cos-traffic-limit` in your PUT Object, POST Object, GET Object, or Upload Part request. This parameter can be used as a request header, request parameter, or a HTML form field for POST Object requests.
- The value of the `x-cos-traffic-limit` parameter must be a number and the unit is bit/s by default.
- The speed limit value range is 819200–838860800, i.e, 100 KB/s–100 MB/s. If the range is exceeded, a 400 error will be returned.
>?1 MByte = 1,024 KByte = 1,048,576 Byte = 8,388,608 bit.

## API Use Case

The following is a sample request for the simple upload API with a speed limit of 1048576 bit/s (128 KB/s):

```sh
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Content-Length: 13
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109068;1561116268&q-key-time=1561109068;1561116268&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=998bfc8836fc205d09e455c14e3d7e623bd2****
x-cos-traffic-limit: 1048576
```

