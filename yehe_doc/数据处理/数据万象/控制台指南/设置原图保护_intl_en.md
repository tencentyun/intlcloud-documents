## Description

Original image protection is a Cloud Infinite (CI) feature that protects source files from being accessed directly by users. This feature should be used along with Styles. For more information, refer to [Setting Styles](https://intl.cloud.tencent.com/document/product/1045/33443). Once original image protection is enabled, users can only access a stylized version of the original image through a special URL. The original image is safely stored in the bucket.

For example, the URL to the original image is `http://examplebucket-1250000000.picsh.myqcloud.com/picture.jpg`, and you have set `style1` for the bucket `examplebucket-1250000000`. Once original image protection is enabled, the URL to the original image is no longer accessible. Users need to use `http://examplebucket-1250000000.picsh.myqcloud.com/picture.jpg?style1` to access the image.

>
> - This feature is mostly used to prevent hot linking or anti-cheating. For example, you can save your watermarks as a style and use it along with original image protection. Users will see a watermarked version of the image instead of the original version.
> - You can also use [APIs](https://intl.cloud.tencent.com/document/product/1045/33711) to enable original image protection.



## Directions

1. Log in to [CI Console](https://console.cloud.tencent.com/ci/index), and click **Bucket Management** in the left sidebar.
2. Go to the bucket management page and click on the name of the desired bucket.
3. In the bucket details page, click **Bucket Configurations**.
4. Locate the configuration item called **Original image protection** and click **Edit**. Click the toggle to enable it.
5. Click **Save** to enable original image protection. 

