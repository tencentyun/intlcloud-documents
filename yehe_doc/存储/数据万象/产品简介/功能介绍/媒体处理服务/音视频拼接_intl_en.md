## Overview

The video/audio splicing feature adds the specified video/audio segment at the beginning or end of a video/audio file to generate a new one.
>? Audio/Video splicing is billed by the output file size under the file transcoding billable item. For more information, see [Media Processing Fees](https://intl.cloud.tencent.com/document/product/1045/49489).
>


## Use Cases

CI's audio/video splicing feature is suitable for various scenarios, such as adding opening and closing credits, advertising, marketing, and video production.

## Directions

You can use the audio/video splicing feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can customize audio/video splicing templates as follows:
- Custom templates: You can create a template in the console as instructed in [Template](https://intl.cloud.tencent.com/document/product/1045/43606). You can also create, modify, find, and delete a template through API as instructed in [Creating Splicing Template](https://intl.cloud.tencent.com/document/product/1045/49907), [Updating Splicing Template](https://intl.cloud.tencent.com/document/product/1045/49921), [DescribeMediaTemplates](https://intl.cloud.tencent.com/document/product/1045/49919), and [DeleteMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49918) respectively.


### Job

You can create an audio/video splicing job for existing data stored in COS.

#### Creating job

- Console: You can create an audio/video splicing job visually in the CI console as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
- API: You can create an audio/video splicing job through API as instructed in [Submitting Video Splicing Job](https://intl.cloud.tencent.com/document/product/1045/48929).

#### Deleting, querying, and searching for job

You can delete, query, and search for a job by filters through API as instructed in [CancelMediaJob](https://intl.cloud.tencent.com/document/product/1045/49512), [DescribeMediaJob](https://intl.cloud.tencent.com/document/product/1045/50355), and [DescribeMediaJobs](https://intl.cloud.tencent.com/document/product/1045/50356) respectively.

### Workflow

With a media processing workflow in CI, you can quickly and flexibly create video processing flows as needed. A workflow is bound to a path of an input bucket. When a video file is **uploaded** to the path, the media workflow will be **automatically triggered** to perform the specified operation, with the processing result automatically saved to the specified path of the output bucket. You can set **audio/video splicing**, **file transcoding**, **video frame capturing**, **video-to-animated image conversion**, and **intelligent thumbnail** jobs in a workflow.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Creating, deleting, querying, and updating workflow through API

You can create, delete, query, and update a workflow through API as instructed in [Creating Workflow](https://intl.cloud.tencent.com/document/product/1045/43733), [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Updating Workflow](https://intl.cloud.tencent.com/document/product/1045/43738) respectively.
