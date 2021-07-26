### How do I configure and limit the allowlist if multiple endpoints are requested in the Mini Program or the bucket name is uncertain?

When you instantiate the SDK, use `ForcePathStyle:true` to enable the suffix style. If you make a suffix style request in a URL formatted as `https://cos-ap-beijing.myqcloud.com/<BucketName-APPID>/<Key>`, the bucket name `/<BucketName-APPID>` will also be added to the signature calculation.

### How do I save an image in a Mini Program to my device?

First, obtain the image URL using `cos.getObjectUrl`. Then, call `wx.downloadFile` to download the image to obtain the temporary path. When the **Save Image** button appears, click the button to call `wx.saveImageToPhotosAlbum` to save the image to your album.


### Can QQ Mini Programs use the Mini Program SDK to upload files to COS?

COS currently supports only WeChat Mini Programs, and WeChat Mini Programs is not interconnected with QQ Mini Programs. Therefore, the Mini Program SDK cannot be used.

### What does the `getAuthorization` function do when Mini Programs use cos-wx-sdk-v5 to upload files to buckets?

The backend uses the `getAuthorization` function in the Mini Program SDK to get a temporary key and sends it to the frontend for signature calculation. Then users can perform operations such as upload and deletion on the files. We recommend that you use the temporary key mode to prevent disclosure of your key. For more information, see [Mini Program SDK use case: Create a COS SDK instance](https://intl.cloud.tencent.com/document/product/436/30609).

### How do I configure and limit the allowlist if multiple endpoints are requested in the COS Mini Program or the bucket name is uncertain?

When you instantiate the SDK, use `ForcePathStyle:true` to enable the suffix style. If you make a suffix style request in a URL in the following format, the bucket name `/<BucketName-APPID>` will also be added to the signature calculation.
```
https://cos-ap-beijing.myqcloud.com/<BucketName-APPID>/<Key>
```
