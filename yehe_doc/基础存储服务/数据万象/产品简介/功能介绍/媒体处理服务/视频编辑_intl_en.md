## Overview

The video clipping feature allows you to clip and splice videos stored in COS.

- **Video clipping**: Clips the specified segment of a video file to generate a new video.
- **Video splicing**: Splices several files to generate a new video.
- **Video clipping and splicing**: Clips multiple files and then splices them to generate a new video.

## Directions

You can use the video clipping feature through **jobs** or **workflows**. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can customize transcoding templates and audio/video splicing templates as follows:

Custom templates: You can create a template in the console as instructed in [Template](https://intl.cloud.tencent.com/document/product/1045/43606). You can also create, modify, find, and delete a template through API as instructed in [Creating Splicing Template](https://intl.cloud.tencent.com/document/product/1045/49907), [Updating Splicing Template](https://intl.cloud.tencent.com/document/product/1045/49921), [DescribeMediaTemplates](https://intl.cloud.tencent.com/document/product/1045/49919), and [DeleteMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49918) respectively.
1. To implement video clipping, you can specify the time points for video clipping in the custom transcoding duration in the transcoding template as described in [Template](https://intl.cloud.tencent.com/document/product/1045/43606#.E9.9F.B3.E8.A7.86.E9.A2.91.E8.BD.AC.E7.A0.81) and then apply the template when creating a transcoding job or workflow.
2. To implement audio/video splicing, you can specify the locations of source files as well as the container format, frame rate, and other parameters of the output file in the splicing template as describes in [Template](https://intl.cloud.tencent.com/document/product/1045/43606#.E9.9F.B3.E8.A7.86.E9.A2.91.E6.8B.BC.E6.8E.A5) and then apply the template when creating a splicing job or workflow.

### Job

You can create an audio/video transcoding or splicing job for existing data stored in COS.

#### Creating job

- Console: You can create an audio/video transcoding or splicing job visually in the CI console as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
- API: You can create an audio/video transcoding or splicing job through API as instructed in [Submitting Audio/Video Transcoding Job](https://intl.cloud.tencent.com/document/product/1045/48941) and [Submitting Video Splicing Job](https://intl.cloud.tencent.com/document/product/1045/48929).

#### Deleting, querying, and searching for job

You can delete, query, and search for a job by filters through API as instructed in [CancelMediaJob](https://intl.cloud.tencent.com/document/product/1045/49512), [DescribeMediaJob](https://intl.cloud.tencent.com/document/product/1045/50355), and [DescribeMediaJobs](https://intl.cloud.tencent.com/document/product/1045/50356) respectively.

### Workflow

With a media processing workflow in CI, you can quickly and flexibly create video processing flows as needed. A workflow is bound to a path of an input bucket. When a video file is **uploaded** to the path, the media workflow will be **automatically triggered** to perform the specified operation, with the processing result automatically saved to the specified path of the output bucket. You can create an **audio/video transcoding** and **splicing** workflow to clip and splice newly uploaded video files.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Deleting, querying, and testing workflow

You can delete, query, and test a workflow through API as instructed in [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Testing Workflow](https://intl.cloud.tencent.com/document/product/1045/50340) respectively.
