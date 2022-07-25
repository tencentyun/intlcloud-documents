
## Overview

This document provides an overview of APIs and SDK code samples for basic image processing.

| API | Description    |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [Scaling](https://intl.cloud.tencent.com/document/product/436/36366) | Scales up/down an image. |
| [Cropping](https://intl.cloud.tencent.com/document/product/436/36367) | Crops an image, including regular cropping, scaling and cropping, cropping to circle, rounded corner cropping, and smart face cropping. |
| [Rotation](https://intl.cloud.tencent.com/document/product/436/36368) | Rotates an image, including regular rotation and adaptive rotation. |
| [Format conversion](https://intl.cloud.tencent.com/document/product/436/36369) | Converts the format of an image, optimizes the GIF format, and performs progressive display. |
| [Quality change](https://intl.cloud.tencent.com/document/product/436/36370) | Adjusts the quality of an image. |
| [Gaussian blurring](https://intl.cloud.tencent.com/document/product/436/36371) | Blurs an image by a Gaussian function. |
| [Sharpening](https://intl.cloud.tencent.com/document/product/436/36372) | Sharpens an image. |
| [Image watermark](https://intl.cloud.tencent.com/document/product/436/36373) | Adds a watermark to an image. |
| [Text watermark](https://intl.cloud.tencent.com/document/product/436/36374) | Adds a real-time text watermark to an image. |
| [Basic image information acquisition](https://intl.cloud.tencent.com/document/product/436/36375) | Queries the basic information of an image, such as format, width, and height. |
| [Image EXIF data acquisition](https://intl.cloud.tencent.com/document/product/436/36376) | Queries the EXIF data of an image. |
| [Image average hue acquisition](https://intl.cloud.tencent.com/document/product/436/36377) | Queries the average hue of an image. |
| [Metadata removal](https://intl.cloud.tencent.com/document/product/436/36378) | Removes the image metadata, including the EXIF data. |
| [Quick thumbnail template](https://intl.cloud.tencent.com/document/product/436/36379) | Generates a thumbnail through an image processing template.                           |
| [Pipeline operator](https://intl.cloud.tencent.com/document/product/436/36380) | Performs multiple operations on an image in sequence. |

## Scaling

#### Feature description

CI uses the **imageMogr2** API to scale images.

#### Method prototype
```go
func (s *CIService) Get(ctx context.Context, key string, operation string, opt *ObjectGetOptions, id ...string) (*Response, error)

func (s *CIService) GetToFile(ctx context.Context, key, localpath, operation string, opt *ObjectGetOptions, id ...string) (*Response, error)
```

#### Sample request
```go
name := "test.jpg"
// Sample 1. Get an object from the response body
resp, err := c.CI.Get(context.Background(), name, "imageMogr2/thumbnail/!50px", nil)
if err != nil {
	//ERROR
}
defer resp.Body.Close()
ioutil.ReadAll(resp.Body)

// Sample 2. Download an object
filepath := "test.jpg"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/thumbnail/!50px", nil)
```

#### Parameter description

| Parameter | Description | Type | Required |
| :--------------- | :----------------------------------------------------------- | :----- | :------- |
| key  | Unique identifier of the object in the bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | string | Yes |
| operation | Image processing operation, such as scaling, cropping, rotation, format conversion, and quality change. | string | Yes |
| ObjectGetOptions | Object download parameters. For more information, see [Object Operations](https://intl.cloud.tencent.com/document/product/436/43549). | string | No |
| id  | Object `VersionId` | string | No |

## Cropping

#### Feature description

CI uses the **imageMogr2** API to crop images, including regular cropping, scaling and cropping, cropping to circle, rounded corner cropping, and smart face cropping.

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

