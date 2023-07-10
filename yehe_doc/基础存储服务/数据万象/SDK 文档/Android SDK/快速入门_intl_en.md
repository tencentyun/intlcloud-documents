## Overview

To make it easier and faster for you to use CI's basic image processing features and CDN's image delivery features, we provide the following five modules for your choice as needed:

|Module|Feature
|:--:|:--
|cloud-infinite (default module)|This module contains CI's basic image processing operations and supports freely combining various operations to build URLs for network requests.
|cloud-infinite-loader |This module uses the `CIImageLoadRequest` instance to request online images and return image data.
|TPG|This module decodes and displays general images and TPG images.
|AVIF|This module decodes and displays general images and AVIF images.
|cloud-infinite-glide|This module depends on the `glide` and `cloud-infinite` modules to provide CI's basic image processing features.


>?
>- For more information on TPG, see [TPG Compression](https://intl.cloud.tencent.com/document/product/1045/42363).

## Resources

- For the SDK source code and demo, see [here](https://github.com/tencentyun/cloud-Infinite-sdk-android.git).
- For SDK APIs and parameters, see [Scaling](https://intl.cloud.tencent.com/document/product/1045/33713).
- For SDK release notes, see [Changelog](https://github.com/tencentyun/cloud-Infinite-sdk-android#%E6%9B%B4%E6%96%B0%E6%97%A5%E5%BF%97).

## Prerequisites

1. You need an Android app, which can be one of your existing projects or a new one.
2. Make sure that the application is built by using an SDK running on Android 4.0.3 or later.

## Step 1. Install the cloud-infinite SDK

The `cloud-infinite` module has the following main features:

- It contains CI's basic image processing operations, such as image scaling, cropping, rotation, format conversion, quality change, Gaussian blur, sharpening, watermarking, and image theme color acquisition.
- It encapsulates each operation as a CITransform and supports freely combining basic operations to build URLs for direct network requests.

**Use Gradle for integration**
>? As the Bintray repository is no longer available, CI's SDKs have been migrated to Maven Central. The import path is different, so you need to use the new import path during the update.
>

Add the following code to the project-level `build.gradle` file (usually in the root directory):
```
repositories {
    google()
    // Add the following line
    mavenCentral() 
}
```

Add the following to the `build.gradle` of your app or other class libraries:
```
 implementation 'com.qcloud.cos:cloud-infinite:1.2.1'			
```

## Step 2. Start using

#### Build the CIImageLoadRequest instance
1. When using CloudInfinite to build a CI-enabled image URL, you first need to instantiate the CloudInfinite class.
```
CloudInfinite cloudInfinite = new CloudInfinite();
```
2. Instantiate the image transformation class `CITransformation` and set related operations. The following takes TPG as an example. For more features, see [Basic Image Processing](https://intl.cloud.tencent.com/document/product/1045/43513).
```
CITransformation transform = new CITransformation();
transform.format(CIImageFormat.TPG, CIImageLoadOptions.LoadTypeUrlFooter)
```
3. Use the CloudInfinite instance to build a CI-enabled image URL.
 - Build synchronously
```
CIImageLoadRequest request = cloudInfinite.requestWithBaseUrlSync(objectUrl, transform);
// Image URL
URL imageURL = request.getUrl();
// Header parameter
Map<String, List<String>> heaers = request.getHeaders();
```
 - Build asynchronously
```
cloudInfinite.requestWithBaseUrl(objectUrl, transform, new CloudInfiniteCallback() {
        @Override
        public void onImageLoadRequest(@NonNull final CIImageLoadRequest request) {
            // Image URL
            URL imageURL = request.getUrl();
            // Header parameter
            Map<String, List<String>> heaers = request.getHeaders();
        }
    });
```

>?The header parameter of CIImageLoadRequest is valid only when image format conversion is performed and `options` is set to `LoadTypeAcceptHeader`.

## Step 3. Load an image

After successfully building the CIImageLoadRequest instance, use the cloud-infinite-loader SDK to load an image.
1. Integrate the cloud-infinite-loader SDK.
```
implementation 'com.qcloud.cos:cloud-infinite-loader:1.2.1'
```
2. Add the INTERNET permission.
```
<uses-permission android:name="android.permission.INTERNET" />
```
3. Load the image.
 - Directly load ImageView
```
CIImageLoader ciImageLoader = new CIImageLoader();
ciImageLoader.display(request, imageview);
```
 - Request image data
```
CIImageLoader ciImageLoader = new CIImageLoader();
ciImageLoader.loadData(request, new CIImageLoadDataCallBack() {
    @Override
    public void onLoadData(byte[] bytes) {
        // Use the pseudocode to set bytes data for the imageview
        //imageview.setBytes(bytes);
    }

    @Override
    public void onFailure(QCloudClientException clientException, QCloudServiceException serviceException) {

    }
});
```
