
This document provides two ways to load TPG images: loading online and using the TPG module.

### Option 1. Loading online TPG image

1. Integrate `CloudInfinite`.

   ```
   pod 'CloudInfinite'
   ```

2. Build a link requesting TPG images in the `CloudInfinite` module, and then use it with SDWebImage to load online TPG images.
    **Objective-C**
    ```
    // Instantiate `CloudInfinite` to build an image request link;
    CloudInfinite * cloudInfinite = [CloudInfinite new];
   
    // Build `CIImageLoadRequest` according to the basic feature options of CI you select;
    CITransformation * transform = [CITransformation new];
    [transform setFormatWith:CIImageTypeTPG options:CILoadTypeUrlFooter];
   
    // Build the image `CIImageLoadRequest`
    [cloudInfinite requestWithBaseUrl:@"image link" transform:transform request:^(CIImageLoadRequest * _Nonnull request) {
        // Request the successfully built `CIImageLoadRequest` instance.
    }];
    ```

    **swift**
    ```
    // Instantiate `CloudInfinite` to build an image request link;
    let cloudInfinite = CloudInfinite();
   
    // Build `CIImageLoadRequest` according to the basic feature options of CI you select;
    let transform = CITransformation();
    transform.setFormatWith(CIImageFormat.typeTPG, options: CILoadTypeEnum.urlFooter);
    
    // Build the image `CIImageLoadRequest`
    cloudInfinite.request(withBaseUrl: "image link", transform: transform) { (request) in
        // Request the successfully built `CIImageLoadRequest` instance.
    }  
    ```

### Option 2. Using TPG module to load TPG image

You can use the TPG module to load TPG image data, which supports TPG animated images with no additional processing needed.

1. Integrate the TPG module.
   ```
   pod 'CloudInfinite/TPG'
   ```
2. If the TPG image data has been obtained, directly use the UIImageView+TPG class of the TPG module to decode and display the image.

    **Objective-C**
    ```
        [self.tpgImageView setTpgImageWithData:data loadComplete:^(NSData * _Nullable data, UIImage * _Nullable image, NSError * _Nullable error) {

        }];
    ```
    **swift**
    ```
        imageView.setTpgImageWith(data) { (data, image, error) in

        }
    ```



