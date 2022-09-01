
This document describes how to load online and local TPG images.


### Installing TPG SDK

```
implementation 'com.qcloud.cos:tpg:1.3.2'    
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

### Option 1. Loading online TPG image

1. Integrate the CI SDK.
```
implementation 'com.qcloud.cos:cloud-infinite:1.2.1'    
```
2. Build a link requesting TPG images in the CI SDK, and then use it with Glide to load online TPG images.
```
// Instantiate `CloudInfinite` to build an image request link;
CloudInfinite cloudInfinite = new CloudInfinite();
// Perform transformation according to the basic feature options of CI you select;
CITransformation transform = new CITransformation();
transform.format(CIImageFormat.TPG, CIImageLoadOptions.LoadTypeUrlFooter);
// Build the image `CIImageLoadRequest`
CIImageLoadRequest request = cloudInfinite.requestWithBaseUrlSync(url, transform);
```

### Option 2. Loading local TPG image

You can use the TPG format for the application's built-in resources, such as assets, drawable, and raw can reduce the size of the installation package.

```
// Load TPG images in `Assets`
TpgImageLoader.displayWithAssets(imageview, assetsName);
// Load TPG images in `Resource`
TpgImageLoader.displayWithResource(imageview, R.drawable.tpg);
// Load TPG images in local files
TpgImageLoader.displayWithFileUri(imageview, fileUri);
```
