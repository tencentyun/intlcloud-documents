## Overview

Image compression is the process of downsizing an image as much as possible without sacrificing quality so that it can be stored at a lower cost and accessed more quickly.

COS offers a variety of image compression options based on [CI](https://www.tencentcloud.com/document/product/1045/33422) for your choice based on your business scenario. Available compression options are as follows:

- **AVIF compression**: Converts images to the .avif format, which is a new image format launched by Netflix based on AV1 in February 2020 and currently is supported by browsers such as Chrome and Firefox.

- **WebP compression**: Converts images to the .webp format, which is superior to .jpg in terms of compression. A .webp image is over 25% smaller than a .jpg image with the same quality. This format is suitable for multi-terminal use cases.

- **HEIF compression**: Converts images to the .heif format, which has a super high compression ratio. A .webp image is over 80% smaller than a .jpg image with the same quality. iOS adopts .heif as the default format for photos, and Android P natively supports .heif.

- **TPG compression**: Converts images to the .tpg format, which is a proprietary image format launched by Tencent and supports animated images. Currently, QQ Browser, Qzone, and other Tencent products support .tpg by default. A .tpg image is over 90% or 50% smaller than a .gif or .png image with the same quality, respectively.

- **Smart image compression**: Intelligently determines the subjective quality of an image and automatically adjusts it. It significantly reduces the image size without changing the original format, and delivers a visual effect as closest to the original image as possible.

  

>? 
>
>- Image compression is a paid service charged by CI. For detailed pricing, see [Image Processing Fees](https://intl.cloud.tencent.com/document/product/1045/45582).
> - Currently, the smart image compression service is available only in Beijing and Shanghai regions.

## Use Cases

The image compression feature meets the needs of image compression on various terminals such as PC and app in diverse use cases like ecommerce and media. This effectively reduces the transmission time, loading time, and use of bandwidth and traffic.

Different compression features have different compatibility with existing image formats and browser environments as detailed below:

| Feature | Supported Formats | Supported Browsers and Systems | Compatibility | Compression Effect | Compression Speed |
| :-------- | :----------------------------------------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- |
| AVIF compression | .jpg, .png, .bmp, .gif, .heif, .webp, and .tpg | A few browsers and systems such as Firefox, Chrome, and Android | Average | Very good | Fast |
| WebP compression | .jpg, .png, .bmp, .gif, .heif, .tpg, and .avif | More than 95% of browsers and systems such as Edge, Firefox, Chrome, Safari, Android, iOS, and Weixin | Strong | Average | Fast |
| HEIF compression | .jpg, .png, .bmp, .webp, and .avif | Not supported in browsers but natively supported on iOS 11 or later and Android P | Weak | Good | Fast |
| TPG compression | .jpg, .png, .bmp, .gif, .heif, .webp, and .avif | Only a few browsers such as QQ Browser as special decoders are required  | Weak | Good | Fast |
| Smart image compression | .jpg and .png (without changing the format of the original image) | All | Very strong | Good | Fast|


>? CI provides [Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) SDK that integrates TPG and AVIF decoders, so you only need to integrate it into your client to decode and preview TPG and AVIF images.

## How to Use

### AVIF, HEIF, and TPG compression

These three are advanced image formats, and you need to enable the [image advanced compression](https://intl.cloud.tencent.com/document/product/436/40117) feature first before you can use them.

After enabling the advanced compression feature, you can use it by setting the image [format conversion parameter](https://intl.cloud.tencent.com/document/product/436/36369) to the desired compression format. Specific parameters are as follows:

| Parameter | Description |
| :--------------------- | :----------------------------------------- |
| imageMogr2/format/avif | Converts the original image to .avif format for compression. |
| imageMogr2/format/heif | Converts the original image to .heif format for compression. |
| imageMogr2/format/tpg  | Converts the original image to .tpg format for compression. |

### WEBP compression

You can directly use the WEBP compression feature through the format conversion capabilities of basic image processing. Specific parameters are as follows:

| Parameter | Description |
| :--------------------- | :----------------------------------------- |
| imageMogr2/format/webp | Converts the original image to .webp format for compression. |

### Smart image compression

The smart image compression feature automatically compresses the images in matching formats, without changing the way you access your images and requiring additional compression parameters.

You need to [enable the smart image compression feature]() using the console. After the feature is enabled, you can access images in the same way as before, and images will be automatically compressed.

## Compression Examples

Perform all the above compression operations on the original .png image. Assume the link of the original image is:

https://examples-125xxxxx.cos.ap-shanghai.myqcloud.com/test.png

### Example 1. Convert to .jpeg format

Final request URL:

```
https://examples-125xxxxx.cos.ap-shanghai.myqcloud.com/test.png?imageMogr2/format/jpeg
```

### Example 2. Convert to .webp format

Final request URL:

```
https://examples-125xxxxx.cos.ap-shanghai.myqcloud.com/test.png?imageMogr2/format/webp
```

### Example 3. Convert to .heif format

Final request URL:

```
https://examples-125xxxxx.cos.ap-shanghai.myqcloud.com/test.png?imageMogr2/format/heif
```

### Example 4. Convert to .tpg format

Final request URL:

```
https://examples-125xxxxx.cos.ap-shanghai.myqcloud.com/test.png?imageMogr2/format/tpg
```

### Example 5. Convert to .avif format

Final request URL:

```
https://examples-125xxxxx.cos.ap-shanghai.myqcloud.com/test.png?imageMogr2/format/avif
```

### Example 6. Perform smart image compression

Final request URL:

```
https://examples-125xxxxx.cos.ap-shanghai.myqcloud.com/test.png
```



The following table compares the compression ratio of different image compression options (the values are for reference only):

| Format | Size |
| :---------- | :----------------- |
| .png (original image) | 465 KB |
| .jpeg | 114 KB (75.5% smaller) |
| .avif | 32 KB (93.1% smaller) |
| .webp | 64 KB (86.2% smaller) |
| .heif | 54 KB (88.4% smaller) |
| .tpg | 56 KB (88.0% smaller) |
| Smart image compression | 59 KB (87.3% smaller) |
