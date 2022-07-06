## Overview

Image compression is the process of downsizing an image as much as possible without sacrificing quality so that it can be stored at a lower cost and accessed more quickly.

COS offers a variety of image compression options based on [CI](https://intl.cloud.tencent.com/document/product/1045/33422) for your choice based on your business scenario. Available compression options are as follows:

- **WebP compression:** Converts images to the .webp format, which is superior to .jpg in terms of compression. A .webp image is over 25% smaller than a .jpg image with the same quality. This format is suitable for multi-terminal use cases.
- **HEIF compression:** Converts images to the .heif format, which has a super high compression ratio. A .webp image is over 80% smaller than a .jpg image with the same quality. iOS adopts .heif as the default format for photos, and Android P natively supports .heif.
- **TPG compression:** Converts images to the .tpg format, which is a proprietary image format launched by Tencent and supports animated images. Currently, QQ Browser, Qzone, and other Tencent products support .tpg by default. A .tpg image is over 90% or 50% smaller than a .gif or .png image with the same quality, respectively.
- **AVIF compression:** Converts images to the .avif format, which is a new image format launched by Netflix based on AV1 in February 2020 and currently is supported by browsers such as Chrome and Firefox.

>? Image compression is a paid service charged by CI. For detailed pricing, see the image processing prices of CI.
>

## Use Cases

The image compression feature meets the needs of image compression on various terminals such as PC and app in diverse use cases like ecommerce and media. This effectively reduces the transmission time, loading time, and use of bandwidth and traffic.

Different compression features have different compatibility with existing image formats and browser environments as detailed below:

| Feature | Supported Formats | Supported Browsers and Systems | Compatibility | Compression Effect | Compression Speed |
| :-------- | :----------------------------------------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- |
| WebP compression | .jpg, .png, .bmp, .gif, .heif, .tpg, and .avif | More than 95% of browsers and systems such as Edge, Firefox, Chrome, Safari, Android, iOS, and WeChat | Strong | Average | Fast |
| HEIF compression | .jpg, .png, .bmp, .webp, and .avif | Not supported in browsers but natively supported on iOS 11 or later and Android P | Weak | Strong | Fast |
| TPG compression | .jpg, .png, .bmp, .gif, .heif, .webp, and .avif | Only a few browsers such as QQ Browser as special decoders are required  | Weak | Strong | Fast |
| AVIF compression | .jpg, .png, .bmp, .gif, .heif, .webp, and .tpg | A few browsers and systems such as Firefox, Chrome, and Android | Weak | Very strong | Slow |


>? To use the TPG format, ensure that **the environment where images are loaded supports TPG decoding**. CI provides the TPG decoder-integrated SDKs for [iOS](https://intl.cloud.tencent.com/document/product/1045/47707), [Android](https://intl.cloud.tencent.com/document/product/1045/45575), and [Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) to facilitate quick integration with TPG.
>

## How to Use

You can use the above compression features through the format conversion capabilities of basic image processing. To do so, set the `format` parameter to the desired compression format. Specific parameters are as follows:

| Parameter | Description |
| :----- | :----------------------------------------- |
| webp | Converts the original image to .webp format for compression. |
| heif | Converts the original image to .heif format for compression. |
| tpg | Converts the original image to .tpg format for compression. |
| avif | Converts the original image to .avif format for compression. |

## Compression Examples

The following examples convert the original image in .png format at `https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png` to .jpeg, .webp, .heif, .tpg, and .avif formats respectively. The effects are as follows:

![img](https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png)

### Example 1. Convert to .jpeg format

Final request URL:
```
https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png?imageMogr2/format/jpeg
```

### Example 2. Convert to .webp format

Final request URL:

```
https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png?imageMogr2/format/webp
```

### Example 3. Convert to .heif format

Final request URL:

```
https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png?imageMogr2/format/heif
```

### Example 4. Convert to .tpg format

Final request URL:

```
https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png?imageMogr2/format/tpg
```

### Example 5. Convert to .avif format

Final request URL:

```
https://ci-avif-demo-1258125638.cos.ap-guangzhou.myqcloud.com/test-png.png?imageMogr2/format/avif
```

The following table lists the compression ratio comparison of different image compression options:

| Format | Size |
| :---------- | :----------------- |
| .png (original image) | 465 KB |
| .jpeg | 114 KB (75.5% smaller) |
| .webp | 64 KB (86.2% smaller) |
| .heif | 54 KB (88.4% smaller) |
| .tpg | 56 KB (88.0% smaller) |
| .avif | 32 KB (93.1% smaller) |

