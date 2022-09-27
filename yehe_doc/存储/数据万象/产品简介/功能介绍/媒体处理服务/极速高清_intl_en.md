## Overview

The top speed codec transcoding feature integrates image quality repair and enhancement, adaptive parameter selection, and V265 encoder among other video processing features. It makes videos clearer yet smaller and requires only low consumption of network resources while delivering a better watch experience.

>?
> - Watermarks can be added to video files during transcoding. For detailed directions, see [Template](https://intl.cloud.tencent.com/document/product/1045/43606).
> - Both top speed codec and audio/video transcoding features contain the HDR to SDR feature, which can convert high dynamic range (HDR) videos to standard dynamic range (SDR) videos. CI changes the dynamic range conversion policy based on the video scene, so that the image details of the output video are as close as possible to those of the input video.
> 

## Use Cases

#### Image quality enhancement

CI can enhance the subjective image quality by integrating adaptive parameter selection and V265 encoder among other video processing features. It makes videos clearer yet smaller and requires only low consumption of network resources while delivering a better watch experience.

#### Reduced space and traffic usage

For media resources such as images, the top speed codec transcoding feature can lower their bitrates and increase their definitions. It provides diverse compression capabilities to increase the compression efficiency, downsize files, and mitigate the bandwidth pressure. This reduces lags, storage space usage, and traffic fees.

## Directions

You can use the top speed codec transcoding feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can customize top speed codec transcoding templates as follows:

Custom templates: You can create a template in the console as instructed in [Template](https://intl.cloud.tencent.com/document/product/1045/43606). You can also create, modify, find, and delete a template through API as instructed in [Creating Top Speed Codec Transcoding Template](https://intl.cloud.tencent.com/document/product/1045/49908), [Updating Top Speed Codec Transcoding Template](https://intl.cloud.tencent.com/document/product/1045/49922), [DescribeMediaTemplates](https://intl.cloud.tencent.com/document/product/1045/49919), and [DeleteMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49918) respectively.


### Through job

You can create a top speed codec transcoding job through the console or API for existing data stored in COS.

- Console: You can create a top speed codec transcoding job visually in the CI console as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
>? You can enable HDR to SDR through the advanced settings in the audio/video transcoding or top speed codec transcoding template.
>
- API: You can create a top speed codec transcoding job through API as instructed in [Submitting SDR-to-HDR Job](https://intl.cloud.tencent.com/document/product/1045/48935).
>? You can create a transcoding template through API and enable HDR to SDR in the template as instructed in [Creating Professional Transcoding Template](https://intl.cloud.tencent.com/document/product/1045/49912).
>

### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, transcoding will be automatically performed on files uploaded to the bucket or path, and the output files will be saved in the specified location.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Creating, deleting, querying, and updating workflow through API

You can create, delete, query, and update a workflow through API as instructed in [Creating Workflow](https://intl.cloud.tencent.com/document/product/1045/43733), [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Updating Workflow](https://intl.cloud.tencent.com/document/product/1045/43738) respectively.

