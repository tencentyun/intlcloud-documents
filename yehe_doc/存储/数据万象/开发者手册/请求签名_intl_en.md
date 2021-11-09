CI uses signatures to verify the validity of requests. The developer authorizes a signature to the client for it to upload, download, and manage the specified resources.

When using CI, you can call RESTful APIs to initiate anonymous or signed HTTP requests. For signed requests, the server will validate the identity of the requester.

- Anonymous request: an HTTP request that does not carry any authentication information, and is sent using RESTful APIs.
- Signed request: an HTTP request that carries a signature. The server will authenticate requesters and only execute requests initiated by authenticated ones. If the authentication fails, the server will return an error message and deny the request.

CI uses the same signature algorithm as [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/zh/document/product/436) and uses Hash-based message authentication code (HMAC) custom solutions for identity verification.

### Signature algorithm

Currently, CI has integrated with COS, meaning that you can use a COS domain to process images. The signature version required is different for CI and COS domains.

- **CI domain**: formatted as `<BucketName-APPID>.<picture region>.myqcloud.com/<picture name>` (for example, `examplebucket-1250000000.picsh.myqcloud.com/picture.jpeg`). It uses **JSON** signatures.
- **COS domain**: formatted as `<BucketName-APPID>.cos.<Region>.myqcloud.com` (for example, `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg`). It uses **XML** signatures. For more information about XML signatures, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

### Signature scenarios

<table>
   <tr>
      <th colspan="2">Scenario</th>
      <th>Applicable Signature</th>
   </tr>
   <tr>
      <td rowspan=2>Processing data upon download</td>
      <td>Hotlink protection not enabled</td>
      <td>No signature verification</td>
   </tr>
   <tr>
      <td>Hotlink protection enabled</td>
      <td>Signature verification</td>
   </tr>
   <tr>
      <td>Processing data upon upload</td>
      <td>Persistent processing</td>
      <td>XML signatures</td>
   </tr>
   <tr>
      <td>Bucket API calls </td>
      <td>Query, activation, deletion, etc.</td>
      <td>XML signatures</td>
   </tr>
   <tr>
      <td>Content recognition</td>
      <td>Detecting pornographic, political, or violent/terror content</td>
      <td>XML signatures</td>
   </tr>
</table>


### Signature tools

To generate a signature, you need the `APPID` (e.g., 1250000000), bucket name (e.g., `examplebucket-ci`), as well as the `SecretID` and `SecretKey` of the project.

The following describes how to obtain the information above:
1. Log in to the [CI console](https://console.cloud.tencent.com/ci/index) and click **Bucket Management** on the left sidebar.
2. Click the name of the desired bucket.
3. Click **Bucket Configuration** to view the bucket name and bucket ID. If there is no bucket created for the current project, you can create one by referring to [Creating Buckets](https://intl.cloud.tencent.com/document/product/1045/33436).
3. Log in to the [CAM console](https://console.cloud.tencent.com/cam/capi) and go to **Manage API Key** to get `SecretID` and `SecretKey`.



The signature calculation process of CI is the same as that of COS. You can use a COS signature tool to generate a signature version you need according to the **signature scenario**.


### Using a signature

Signed HTTP requests sent via RESTful APIs can pass the signature in the following ways:

1. Pass through a standard HTTP `Authorization` header, such as `Authorization: q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753;1557996953&...&q-signature=...`
2. Pass as an HTTP request parameter (be sure to URL-encode), such as `/exampleobject?q-sign-algorithm=sha1&q-ak=...&q-sign-time=1557989753%3B1557996953&...&q-signature=...`


>!In the example above, `...` are the signatures.



