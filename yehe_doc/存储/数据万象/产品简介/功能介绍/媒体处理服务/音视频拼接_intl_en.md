## Overview

The video/audio splicing feature adds the specified video/audio segment at the beginning or end of a video/audio file to generate a new one.
>? Audio/Video splicing is billed by the output file size under the billable item of file transcoding. For more information, see Media Processing Fees.
>


## Use Cases

CI's audio/video splicing feature is suitable for various scenarios, such as adding opening and ending credits, advertising, marketing, and video production.

## How to Use

You can use the audio/video splicing feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can customize audio/video splicing templates as follows:
- Custom templates: You can create templates in the console. You can also [create](https://intl.cloud.tencent.com/document/product/1045/43647), [modify](https://intl.cloud.tencent.com/document/product/1045/43650), [find](https://intl.cloud.tencent.com/document/product/1045/43649), and [delete](https://intl.cloud.tencent.com/document/product/1045/43648) templates through APIs.


### Job

You can create an audio/video splicing job for existing data stored in COS.

#### Creating job

- Console: You can create jobs visually in the CI console as instructed in the audio/video splicing job documentation.
- API: You can create audio/video splicing jobs through APIs as instructed in [Submitting Splicing Job](https://intl.cloud.tencent.com/document/product/1045/43703).

#### Deleting, querying, and searching for job

You can [delete](https://intl.cloud.tencent.com/document/product/1045/43702), [query](https://intl.cloud.tencent.com/document/product/1045/43704), and [search for](https://intl.cloud.tencent.com/document/product/1045/43705) jobs by filters through APIs.

### Workflow

With a media processing workflow in CI, you can quickly and flexibly create video processing flows as needed. A workflow is bound to a path of an input bucket. When a video file is **uploaded** to the path, the media workflow will be **automatically triggered** to perform the specified processing operation, with the processing result automatically saved to the specified path of the output bucket. You can set **audio/video splicing**, **file transcoding**, **video frame capturing**, **video conversion to animated image**, and **intelligent thumbnail** jobs in a workflow.
#### Creating workflow

You can create a workflow in the CI console as instructed in Creating Workflow.

#### Deleting, querying, and searching for workflow

You can [delete workflows](https://intl.cloud.tencent.com/document/product/1045/43734), [search for specified workflows](https://intl.cloud.tencent.com/document/product/1045/43735), [get workflow details](https://intl.cloud.tencent.com/document/product/1045/43736), and [get the list of workflow instances](https://intl.cloud.tencent.com/document/product/1045/43737) through APIs.
