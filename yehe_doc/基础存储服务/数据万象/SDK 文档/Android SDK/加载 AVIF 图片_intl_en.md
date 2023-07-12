
This document describes how to load online and local AVIF images.


### Installing AVIF SDK

```
implementation 'com.qcloud.cos:avif:1.0.0'    
```

The .so libraries will be included automatically. We recommend you use the "abiFilter" configuration of the NDK in the module's `build.gradle` file to set the .so library frameworks that are supported.

```
defaultConfig {
    ndk {
        // Set the .so library frameworks that are supported
        abiFilters 'armeabi' //, 'x86', 'armeabi-v7a', 'x86_64', 'arm64-v8a'
    }
}
```

### Option 1. Loading online AVIF image

1. Integrate the CI SDK.
```
implementation 'com.qcloud.cos:cloud-infinite:1.2.1'    
```
2. Build a link requesting AVIF images in the CI SDK, and then use it with Glide to load online AVIF images as instructed in [Loading Image with Glide](https://intl.cloud.tencent.com/document/product/1045/45577).
```
// Instantiate `CloudInfinite` to build an image request link;
CloudInfinite cloudInfinite = new CloudInfinite();
// Perform transformation according to the basic feature options of CI you select;
CITransformation transform = new CITransformation();
transform.format(CIImageFormat.AVIF, CIImageLoadOptions.LoadTypeUrlFooter);
// Build the image `CIImageLoadRequest`
CIImageLoadRequest request = cloudInfinite.requestWithBaseUrlSync(url, transform);
```

### Option 2. Loading local AVIF image

You can use the AVIF format for the application's built-in resources, such as assets, drawable, and raw can reduce the size of the installation package.

```
// Load AVIF images in `Assets`
AVIFImageLoader.displayWithAssets(imageview, assetsName);
// Load AVIF images in `Resource`
AVIFImageLoader.displayWithResource(imageview, R.drawable.avif);
// Load AVIF images in local files
AVIFImageLoader.displayWithFileUri(imageview, fileUri);
```
