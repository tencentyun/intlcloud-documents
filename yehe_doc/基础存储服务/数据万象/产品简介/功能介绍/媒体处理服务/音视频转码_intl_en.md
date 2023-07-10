## Overview

The audio/video transcoding feature converts an audio/video file bitstream. It changes parameters of the source bitstream, such as codec, resolution, and bitrate, to adapt to different devices and network conditions.

>?
> - Audio/Video transcoding is a paid feature. For billing details, see [Media Processing Fees](https://intl.cloud.tencent.com/document/product/1045/49489).
> - For a video file, you can add a watermark to the video during transcoding. For details, see [video watermark](https://intl.cloud.tencent.com/document/product/1045/43606).
> - You can toggle on the accelerated transcoding option for the audio/video transcoding job. After you do this, the job is added to an accelerated transcoding queue and its speed can reach more than 5 times of the regular transcoding speed.
> 



## Use Cases

#### Multi-device adaptability

As content platforms are generally intended for multiple types of devices, they need to provide media files in different formats for different users. CI's file transcoding feature provides a variety of transcoding parameters for most transcoding requirements. It also supports automatic triggering of transcoding during media file upload, so as to quickly meet the format requirements of different terminals.

#### Reduced space and traffic usage

For media resources such as images, the file transcoding feature can adjust their bitrates and provide diverse compression capabilities to increase the compression efficiency and downsize files. This reduces lags, storage space usage, and traffic fees.

#### Sync watermarking

CI can add multiple watermarks to media resources synchronously. This feature enhances the brand awareness and reduces the possibility of media file theft. In addition, it supports many watermark formats such as static and dynamic image as well as text, fully meeting your watermark needs in different scenarios.

#### Parallel processing of large-scale long videos

CI supports accelerated transcoding, which can implement rapid parallel processing of a large number of long videos, for example, movies and TV series.

## How to Use

You can use the file transcoding feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can use preset or custom template as follows:
- Preset template: Currently, CI provides a variety of preset templates for most file transcoding use cases. You can view all such templates in the [CI console](https://console.cloud.tencent.com/ci).
- Custom templates: You can create templates in the [console](https://intl.cloud.tencent.com/document/product/1045/43606). You can also [create](https://intl.cloud.tencent.com/document/product/1045/49911), [modify](https://intl.cloud.tencent.com/document/product/1045/49925), [find](https://intl.cloud.tencent.com/document/product/1045/49919), and [delete](https://intl.cloud.tencent.com/document/product/1045/49918) templates through APIs.


### Through job

You can create a file transcoding job through the console or API for existing data in COS.

- Console: You can create a transcoding job visually on the CI console as instructed in [file transcoding](https://intl.cloud.tencent.com/document/product/1045/48064).
- API: You can create a transcoding job through API as instructed in [Submitting Audio/Video Transcoding Job](https://intl.cloud.tencent.com/document/product/1045/48941).



### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, transcoding will be automatically performed on files uploaded to the bucket or path, and the transcoded files will be saved in the specified location.

#### Creating a workflow

You can create a workflow using the CI console. For more information, see [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Creating, deleting, querying, and searching for workflow through API

You can [create a workflow](https://intl.cloud.tencent.com/document/product/1045/43733), [delete a workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [search for specified workflows](https://intl.cloud.tencent.com/document/product/1045/50339), and [update a workflow](https://intl.cloud.tencent.com/document/product/1045/43738) through APIs.
