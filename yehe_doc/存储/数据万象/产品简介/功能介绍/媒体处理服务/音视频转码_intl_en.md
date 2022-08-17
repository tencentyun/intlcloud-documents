## Overview

The file transcoding feature converts an audio/video file bitstream. It changes parameters of the source bitstream, such as codec, resolution, and bitrate, to adapt to different devices and network conditions.

>?
> - File transcoding is a paid feature. For billing details, see Media Processing Fees.
> - Watermarks can be added to video files during transcoding. For detailed directions, see Video Watermark.
> 




## Use Cases

#### Multi-device adaptability

As content platforms are generally intended for multiple types of devices, they need to provide media files in different formats for different users. CI's file transcoding feature provides a variety of transcoding parameters for most transcoding requirements. It also supports automatic triggering of transcoding during media file upload, so as to quickly meet the format requirements of different terminals.

#### Reduced space and traffic usage

For media resources such as images, the file transcoding feature can adjust their bitrates and provide diverse compression capabilities to increase the compression efficiency and downsize files. This reduces lags, storage space usage, and traffic fees.

#### Sync watermarking

CI can add multiple watermarks to media resources synchronously. This feature enhances the brand awareness and reduces the possibility of media file theft. In addition, it supports many watermark formats such as static and dynamic image as well as text, fully meeting your watermark needs in different scenarios.

## Directions

You can use the file transcoding feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can use preset or custom templates as follows:
- Preset templates: Currently, CI provides a variety of preset templates for most file transcoding use cases. You can view all such templates in the [CI console](https://console.cloud.tencent.com/ci).
- Custom templates: You can create templates in the console. You can also create, modify, find, or delete templates through APIs as instructed in [Creating Transcoding Template](https://intl.cloud.tencent.com/document/product/1045/43643), [Updating Transcoding Template](https://intl.cloud.tencent.com/document/product/1045/43646), [Searching for Transcoding Template](https://intl.cloud.tencent.com/document/product/1045/43645), and [Deleting Transcoding Template](https://intl.cloud.tencent.com/document/product/1045/43644) respectively.


### Through job

You can create file transcoding jobs through the console or APIs to transcode existing files in COS.

- Console: You can create a job visually in the CI console as instructed in the file transcoding job documentation.
- API: You can use APIs to create file transcoding jobs as instructed in [Transcoding Job APIs](https://www.tencentcloud.com/document/product/1045/43676).



### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, transcoding will be automatically performed on files uploaded to the bucket or path, and the output files will be saved in the specified location.

#### Creating workflow

You can create a workflow in the CI console as instructed in Creating Workflow.

#### Deleting, querying, and searching for workflow

You can delete, search for, get details of, and get the list of instances of workflows through APIs as instructed in [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Searching for Workflow](https://intl.cloud.tencent.com/document/product/1045/43735), [Getting Workflow Instance Details](https://intl.cloud.tencent.com/document/product/1045/43736), and [Getting Workflow Instance List](https://intl.cloud.tencent.com/document/product/1045/43737) respectively.
