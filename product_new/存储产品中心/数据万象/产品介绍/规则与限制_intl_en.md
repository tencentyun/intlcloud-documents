| Feature | Limits |
|-------|---------|
| Image processing |<li>Supported formats: this feature can process images in JPG, BMP, GIF, PNG, WEBP, SVG, and PSD formats, and transcode and process HEIF images.<li>Size: the maximum image size is limited to 20 MB, with both the height and width less than 9,999 pixels. |
| [Format conversion](https://intl.cloud.tencent.com/document/product/1045/33716) | JPG, BMP, GIF, PNG, WEBP, and YJPEG formats are supported. The default format is the original image format. |
| [Quality conversion](https://intl.cloud.tencent.com/document/product/1045/33717) | Only JPG and WEBP formats are supported. |
| [Progressive display](https://intl.cloud.tencent.com/document/product/1045/33716) | Only the JPG format is supported. If the output image format is not JPG, this parameter is ignored. |
| [Gaussian blurring](https://intl.cloud.tencent.com/document/product/1045/33718) | The GIF format is not supported. |
| [Pipeline operators](https://intl.cloud.tencent.com/document/product/1045/33727) | This feature allows you to perform multiple types of image processing sequentially. Currently, up to three layers of pipelines are supported. |


>Cloud Infinite (CI) is based on Cloud Object Storage (COS). For information about storage and limits on upload specifications, see [COS Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).