## Overview

By leveraging AI technologies to comprehensively analyze and assess video content, the video enhancement feature provides details enhancement, color enhancement, SDR to HDR, and super resolution features, which improve the video quality from all aspects.

>? Watermarks can be added to video files during video enhancement. For detailed directions, see [Template](https://intl.cloud.tencent.com/document/product/1045/43606).
>

## Use Cases

#### Video remastering

TV series and movies in SDR or with a low resolution or image quality can be remastered to generate HDR videos with more color and brightness details.

#### Image enhancement

Due to camera or environment restrictions, some videos may have low definition and dark image. Such videos can be processed by CI's SDR to HDR, details enhancement, color enhancement, and super resolution features to deliver a better watch experience on HD devices.


## Directions

You can use the video enhancement feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can customize templates as follows:

Custom templates: You can create a template in the console as instructed in [Template](https://intl.cloud.tencent.com/document/product/1045/43606). You can also create, modify, find, and delete a template through API as instructed in [Creating Video Enhancement Template](https://intl.cloud.tencent.com/document/product/1045/49915), [Updating Video Enhancement Template](https://intl.cloud.tencent.com/document/product/1045/49929), [DescribeMediaTemplates](https://intl.cloud.tencent.com/document/product/1045/49919), [DeleteMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49918) respectively.


### Through job

You can create a video enhancement job through the console or API for existing data stored in COS.

- Console: You can create a video enhancement or SDR-to-HDR job visually in the CI console as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
- API: You can create a video enhancement job through API as instructed in [Submitting Video Enhancement Job](https://intl.cloud.tencent.com/document/product/1045/48944).


### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, video enhancement will be automatically performed on files uploaded to the bucket or path, and the files with an optimized image quality will be saved in the specified location.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Creating, deleting, querying, and updating workflow through API

You can create, delete, query, and update a workflow through API as instructed in [Creating Workflow](https://intl.cloud.tencent.com/document/product/1045/43733), [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Updating Workflow](https://intl.cloud.tencent.com/document/product/1045/43738) respectively.
