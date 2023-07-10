## Overview

To make it easier and faster for you to use CI's basic image processing features and CDN's image delivery features, we provide the following five modules for your choice as needed:

|Module|Feature
|:--:|:--
|CloudInfinite (default module)|This module contains CI's basic image processing operations and supports freely combining various operations to build URLs for network requests.
|Loader |This module uses the `CIImageLoadRequest` instance to request online images and return image data.
|TPG|This module decodes and displays general images and TPG images.
|AVIF|This module decodes and displays general images and AVIF images (on v1.3.8 or later).
|SDWebImage-CloudInfinite|This module provides CI's basic image processing features based on the SDWebImage and CloudInfinite modules.


>?
>- For more information on TPG, see [TPG Compression](https://intl.cloud.tencent.com/document/product/1045/42363).
> - For more information on AVIF, see [AVIF Compression](https://intl.cloud.tencent.com/document/product/1045/43028).

## Resources

- For SDK source codes and demos, see [CI iOS SDK](https://github.com/tencentyun/cloud-Infinite-sdk-ios.git).
- For SDK APIs and parameters, see [SDK API](https://intl.cloud.tencent.com/document/product/1045/33713).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cloud-Infinite-sdk-ios#changelog).

## Preparations

1. Prepare an iOS application; this can be an existing project or a new empty project.
2. Make sure that the application is built using an SDK running on iOS 8.0 or above.

## Step 1. Install the SDK CloudInfinite module

Main features of the CloudInfinite module:
- It contains CI's basic image processing operations, such as image scaling, cropping, rotation, format conversion, quality change, Gaussian blur, sharpening, watermarking, and image theme color acquisition.
- It encapsulates each operation as a TransformItem and supports freely combining basic operations to build URLs for direct network requests.

**Integration via CocoaPods**

>? We recommend you use the CocoaPods method. The steps for integrating related modules are the same and will not be repeated.

1. Add the module to your project's Podfile:
```
    pod 'CloudInfinite'
```
2. Run the installation command in the terminal:
```
    pod install
```

## Step 2. Start using

#### Importing header files

**Objective-C**
```
#import <CloudInfinite.h>
```
**swift**
Add project name-Bridging-Header in the bridging file.
```
#import <CloudInfinite.h>
```

#### Build the CIImageLoadRequest instance
1. When using CloudInfinite to build a CI-enabled image URL, you first need to instantiate the CloudInfinite class.

**Objective-C**
```
    CloudInfinite * cloudInfinite = [CloudInfinite new];
```
**swift**
```
let cloudInfinite = CloudInfinite();
```
2. Instantiate the image transformation class `CITransformation` and set related operations. The following takes TPG as an example. For more features, see [Basic Image Processing](https://www.tencentcloud.com/document/product/1045/45588).

**Objective-C**
```
    CITransformation * transform = [CITransformation new];
    [transform setFormatWith:CIImageTypeTPG options:CILoadTypeUrlFooter];
```
**swift**
```
    let transform = CITransformation();
    transform.setFormatWith(CIImageFormat.typeTPG, options: CILoadTypeEnum.urlFooter);
```
3. Use the CloudInfinite instance to construct a CI-enabled image URL.
 - Build synchronously

**Objective-C**
```
    CIImageLoadRequest * imageloadRequest = [cloudInfinite requestWithBaseUrl:@"Image URL" transform:transform];
    // Image URL
    NSURL * imageURL = imageloadRequest.url;
    // Header parameter
    NSString * heaer = imageloadRequest.header;
```

**swift**
```
    let imageloadRequest = cloudInfinite.request(withBaseUrl: "Image URL", transform: transform);
    // Image URL
    let imageURL = imageloadRequest.url;
    // Header parameter
    let heaer = imageloadRequest.header;
```
 - Build asynchronously

**Objective-C**
```
    [cloudInfinite requestWithBaseUrl:@"image link" transform:transform request:^(CIImageLoadRequest * _Nonnull request) {
        // Image URL
        request.url;
        // Header parameter
        request.header;
    }];
```
**swift**
```
    cloudInfinite.request(withBaseUrl: "", transform: transform) { (request) in
        // Image URL
        request.url;
        // Header parameter
        request.header;
    };
```

>?
- The header parameter of `CIImageLoadRequest` is valid only when image format conversion is performed and `options` is set to `loadtypeacceptheader`.
- When using a custom loader to request an image, if the header needs to be used, concatenate it as follows:

```
NSDictionary * header = @{@"accept":[NSString stringWithFormat:@"image/%@",request.header]};
```

## Step 3. Load an image

After successfully constructing a `CIImageLoadRequest` instance, use the CloudInfinite/Loader module to load images. Integrate the CloudInfinite/Loader module as follows:

```
pod 'CloudInfinite/Loader' 
```

#### Requesting image data

Request the image `NSData`, which is suitable for requesting TPG images (with the TPG decoding module required) or images that require additional processing of binary data.
**Objective-C**
```
// `request` is the `CIImageLoadRequest` instance successfully constructed in the previous step.
[[CIImageLoader shareLoader] loadData:request loadComplete:^(NSData * _Nullable data, NSError * _Nullable error) {
    // `data` is the obtained image data.
}];
```
**swift**
```
// `request` is the `CIImageLoadRequest` instance successfully constructed in the previous step.
CIImageLoader.share().loadData(request) { (data, error) in
    // `data` is the obtained image data.
};
```

#### Loading general image

 **Objective-C**
```
// Pass in the image control `imageView` and the successfully constructed `CIImageLoadRequest` instance
[[CIImageLoader shareLoader]display:imageView loadRequest:request placeHolder:nil loadComplete:^(NSData * _Nullable data, NSError * _Nullable error) {
		// `data` is the obtained image data.
}];
```
**swift**

```
// Pass in the image control `imageView` and the successfully constructed `CIImageLoadRequest` instance
CIImageLoader.share().display(imageView, loadRequest: request, placeHolder: nil) { (data, error) in
		// `data` is the obtained image data.
};
```
