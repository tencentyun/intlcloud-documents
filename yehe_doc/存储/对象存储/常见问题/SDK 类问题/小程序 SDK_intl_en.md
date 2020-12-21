### How do I configure and limit the allowlist if multiple endpoints are requested in the Mini Program or the bucket name is uncertain?

When you instantiate the SDK, use `ForcePathStyle:true` to enable the suffix style. If you make a suffix style request in a URL formatted as `https://cos-ap-beijing.myqcloud.com/<BucketName-APPID>/<Key>`, the bucket name `/<BucketName-APPID>` will also be added to the signature calculation.

### How do I save an image in a Mini Program to my device?

First, obtain the image URL using `cos.getObjectUrl`. Then, call `wx.downloadFile` to download the image to obtain the temporary path. When the **Save Image** button appears, click the button to call `wx.saveImageToPhotosAlbum` to save the image to your album.
