Tencent Cloud Infinite (CI) verifies the validity of requests through signatures. Developers grant a signature to the client to allow it to upload, download, and manage specific resources.

With CI, an anonymous HTTP request or signed HTTP request can be made by using the RESTful API. For a signature request, the server will authenticate the initiator.

- Anonymous request: the HTTP request does not include any identity or authentication information, and the HTTP request is made through the RESTful API.
- Signature request: a signature is included in the HTTP request, and authentication is performed after the server receives the request. The request is approved and executed after a successful authentication, otherwise it is discarded with an error message.

Cloud Infinite uses the same signature algorithm as [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436) on which it is based. It performs authentication using a custom scheme based on HMAC (Hash Message Authentication Code).

### Signature Algorithm

There are XML and JSON signatures:

- Use **JSON** signatures for **downloading** operations.
- Use **XML** signatures for the **uploading** and **bucket API** operations. For more information, see XML [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

>
- The host in the downloading request header looks like `<BucketName-APPID>.<picture region>.myqcloud.com/<picture name>`, for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`.
- The host in the uploading request header looks like `<BucketName-APPID>.pic.<Region>.myqcloud.com`, for example `examplebucket-1250000000.pic.ap-shanghai.myqcloud.com/picture.jpeg`.

### Scenarios

<table>
   <tr>
      <th colspan=2>Scenario</th>
      <th>Applicable Signature</th>
   </tr>
   <tr>
      <td rowspan=2>Processing during data downloading</td>
      <td>Hotlink protection is disabled</td>
      <td>No signature verification</td>
   </tr>
   <tr>
      <td>Hotlink protection is enabled</td>
      <td>JSON signature</td>
   </tr>
   <tr>
      <td>Processing during data uploading</td>
      <td>Persistence processing</td>
      <td>XML signature</td>
   </tr>
   <tr>
      <td>Bucket API operations</td>
      <td>Query, enable, delete, and others</td>
      <td>XML signature</td>
   </tr>
   <tr>
      <td>Content recognition</td>
      <td>Detect content related to pornography, politics, violence, and terrorism</td>
      <td>XML signature</td>
   </tr>
</table>

### Signature Tool

The information that is required for generating a signature includes the APPID (such as 1250000000), bucket name (such as examplebucket-ci), and SecretID and SecretKey of the project.

The preceding information can be obtained as follows:
1. Log in to [CI Console](https://console.cloud.tencent.com/ci/index), and click **Bucket Management** in the left sidebar.
2. Click the bucket that you want to manage to go to the bucket management page.
3. Click **Bucket Configuration** to view the bucket name and bucket ID. Create a bucket if the current project does not contain one yet. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/1045/33436).
4. Go to the API key management page in [CAM](https://console.cloud.tencent.com/cam/capi) to get the SecretID and SecretKey.



CI follows the same process for computing a signature as COS.


### Using Signatures

Signed HTTP requests initiated through RESTful APIs can pass signatures in the following ways:

1. Pass through a standard HTTP Authorization header, such as `Authorization: q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753;1557996953&...&q-signature=...`
2. Pass as an HTTP request parameter (be sure to implement UrlEncode), such as `/exampleobject?q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753%3B1557996953&...&q-signature=...`


>In the preceding example, `...` is used to substitute the specific signing information.

