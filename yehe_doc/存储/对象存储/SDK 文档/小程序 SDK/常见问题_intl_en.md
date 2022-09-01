### What should I do if error 403 is reported when I perform operations with a temporary key?

Check whether the `action` and `allowPrefix` you entered when applying for the temporary key are correct.
1. For example, if you call `cos.putObject()`, but the `action` does not contain **name/cos:PutObject**, then there is no `putObject` permission, resulting in the error 403.
2. For example, if the key for the operation is `1.jpg`, but the `allowPrefix` is entered as `test/*` (only allowing operations on the `test/*` path), then there is no operation permission for the corresponding path, resulting in the error 403.

If both `action` and `allowPrefix` are correct, see [Generating and Using Temporary Keys](https://intl.cloud.tencent.com/document/product/436/14048) and [403 Error for COS Access](https://intl.cloud.tencent.com/document/product/436/40105).
Field description: STS SDKs for different languages use different fields for `action` and `allowPrefix`, such as `allowActions` and `allowPrefixes` in the STS Java SDK. Be sure to check the examples in the STS SDK.

### How do I configure and limit the allowlist if multiple domain names are requested in the mini program or the bucket name is unknown?

When the SDK is instantiated, `ForcePathStyle:true` can be used to enable suffixed request, and then only the URL of the real request is needed, which is in the following format:
```
https://cos-ap-beijing.myqcloud.com/<BucketName-APPID>/<Key>
```
When a suffixed request is signed, the bucket name `/<BucketName-APPID>` will also be used in the signature calculation.

### How do I save an image in a mini program to my device?

1. Get the image URL through `cos.getObjectUrl`.
2. Call `wx.downloadFile` to download the image and get the temporary path.
3. Click **Save** and call `wx.saveImageToPhotosAlbum` to save the image to the album.


### Can I upload files to COS by using the Mini Program SDK for QQ mini programs?

COS currently supports only WeChat mini programs, but WeChat mini programs do not interconnect with QQ mini programs. Therefore, the Mini Program SDK cannot be used.

### What does the `getAuthorization` function do when mini programs use cos-wx-sdk-v5 to upload files to buckets?

The backend uses the `getAuthorization` function in the Mini Program SDK to get a temporary key and sends it to the frontend for signature calculation. Then, you can perform operations such as upload and deletion on the files according to the signature calculation result. We recommend you use a temporary key to prevent disclosure of your key. For more information, see [Getting Started](https://intl.cloud.tencent.com/document/product/436/30609).

