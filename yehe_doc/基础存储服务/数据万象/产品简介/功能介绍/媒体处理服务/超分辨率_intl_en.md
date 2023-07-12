## Overview

The super resolution feature reconstructs the details and local features of a video by recognizing its content and contour so as to generate a high-resolution video image through a series of low-resolution video images. It can be used in combination with video enhancement to remaster old videos.

>? Watermarks can be added to video files during super resolution processing. For detailed directions, see [Template](https://intl.cloud.tencent.com/document/product/1045/43606).
>

## Use Cases

#### Resolution enhancement

Videos in SDR or with low resolution or image quality can be enhanced to generate HD/4K videos with a higher resolution.

#### Image quality increase

Due to camera or environment restrictions, some videos may have a low definition. Such videos can be processed by CI's super resolution feature to increase the resolution, recreate image details, and deliver a better watch experience on HD devices.


## Directions

You can use the super resolution feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can customize templates as follows:

Custom templates: You can create a template in the console as instructed in [Template](https://intl.cloud.tencent.com/document/product/1045/43606). You can also create, modify, find, and delete a template through API as instructed in [Creating Super Resolution Template](https://intl.cloud.tencent.com/document/product/1045/49910), [Updating Super Resolution Template](https://intl.cloud.tencent.com/document/product/1045/49924), [DescribeMediaTemplates](https://intl.cloud.tencent.com/document/product/1045/49919), and [DeleteMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49918) respectively.


### Through job

You can create a super resolution job through the console or API for existing data stored in COS.

- Console: You can create a super resolution job visually in the CI console as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
- API: You can create a super resolution job through API as instructed in [Submitting Super Resolution Job](https://intl.cloud.tencent.com/document/product/1045/48940).


### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, super resolution operations will be automatically performed on files uploaded to the bucket or path, and the output files will be saved in the specified location.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Creating, deleting, querying, and updating workflow through API

You can create, delete, query, and update a workflow through API as instructed in [Creating Workflow](https://intl.cloud.tencent.com/document/product/1045/43733), [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Updating Workflow](https://intl.cloud.tencent.com/document/product/1045/43738) respectively.
