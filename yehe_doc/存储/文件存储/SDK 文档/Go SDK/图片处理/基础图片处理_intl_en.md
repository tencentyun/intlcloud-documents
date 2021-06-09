
## Overview

This document provides an overview of APIs and SDK code samples related to basic image processing.

| API | Operation |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Scaling](https://intl.cloud.tencent.com/document/product/436/36366) | Scales up/down an image |
| [Cropping](https://intl.cloud.tencent.com/document/product/436/36367) | Crops an image, including regular cropping, scaling and cropping, inscribed circle cropping, rounded corner cropping, and smart cropping |
| [Rotation](https://intl.cloud.tencent.com/document/product/436/36368) | Rotates an image, including common rotation and adaptive rotation |
| [Format conversion](https://intl.cloud.tencent.com/document/product/436/36369) | Converts the format of an image, optimizes GIF format, and performs progressive display |
| [Quality conversion](https://intl.cloud.tencent.com/document/product/436/36370) | Adjusts the quality of an image |
| [Gaussian blurring](https://intl.cloud.tencent.com/document/product/436/36371) | Blurs an image by a Gaussian function |
| [Sharpening](https://intl.cloud.tencent.com/document/product/436/36372) | Sharpens an image |
| [Image watermarks](https://intl.cloud.tencent.com/document/product/436/36373) | Adds a watermark to an image |
| [Text watermarks](https://intl.cloud.tencent.com/document/product/436/36374) | Adds a real-time text watermark to an image |
| [Obtaining basic image information](https://intl.cloud.tencent.com/document/product/436/36375) | Obtains the basic information (such as format, length, and height) about an image |
| [Obtaining image EXIF data](https://intl.cloud.tencent.com/document/product/436/36376) | Obtains the EXIF data of an image |
| [Obtaining the image average hue](https://intl.cloud.tencent.com/document/product/436/36377) | Obtains the average hue of an image |
| [Removing metadata](https://intl.cloud.tencent.com/document/product/436/36378) | Removes the image metadata, including the EXIF data |
| [Quick thumbnail template](https://intl.cloud.tencent.com/document/product/436/36379) | Provides an image processing template to generate thumbnails |
| [Pipeline operator](https://intl.cloud.tencent.com/document/product/436/36380) | Performs multiple operations on images in sequence |

## Scaling

#### Feature description 

Tencent Cloud’s CI uses the `imageMogr2` API to scale images.

#### Method prototype
```go
func (s *CIService) Get(ctx context.Context, key string, operation string, opt *ObjectGetOptions, id ...string) (*Response, error)

func (s *CIService) GetToFile(ctx context.Context, key, localpath, operation string, opt *ObjectGetOptions, id ...string) (*Response, error)
```

#### Sample request 
```go
name := "test.jpg"
// Sample 1. Obtain the object from the response body.
resp, err := c.CI.Get(context.Background(), name, "imageMogr2/thumbnail/!50px", nil)
if err != nil {
	//ERROR
}
defer resp.Body.Close()
ioutil.ReadAll(resp.Body)

// Sample 2. Download the object.
filepath := "test.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/thumbnail/!50px", nil)
```

#### Parameter description

| Parameter | Description | Type | Required |
| :--------------- | :----------------------------------------------------------- | :----- | :------- |
| key  | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | string | Yes |
| operation | Image processing operation, including scaling, cropping, rotating, converting formats, changing quality, and more | string | Yes |
| ObjectGetOptions | Object download parameters. For more information, please see [Object Operations](https://intl.cloud.tencent.com/document/product/436/31526). | string | No |
| id  | `VersionId` of the object | string | No |

## Cropping

#### Feature description 

CI uses the `imageMogr2` API to crop images, such as regular cropping, scaling and cropping, inscribed circle cropping, rounded corner cropping, and smart cropping.

#### Sample request 

```go
name := "test.jpg"
filepath := "test.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/cut/600x600x100x10", nil)
```

## Other Basic Image Processing Operations

#### Feature description 

You can perform other basic processing operations on images by changing the value of the `operation` parameter. For example, you can rotate the image clockwise by 90 degrees as follows:
```go
name := "test.jpg"
filepath := "test.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/rotate/90", nil)
```

