## Overview

The audio/video segmentation feature can divide an audio or video into several segments of the specified duration to improve the efficiency of postproduction. It allows you to change the container format of the audio or video segments during segmentation.

>? When you use the audio/video segmentation feature, if only segmentation is performed, no fees will be incurred. If the container format is changed, remuxing fees under the audio/video transcoding billable item will be charged by the output file length. For more information, see [Media Processing Fees](https://intl.cloud.tencent.com/document/product/1045/49489).
>

## Use Cases

The audio/video segmentation feature is suitable for scenarios where large media files need to be segmented.

## Directions

You can use the audio/video segmentation feature through jobs or workflows.

### Through job

You can create an audio/video segmentation job through the console or API for existing data stored in COS.

#### Creating job

- Console: You can create an audio/video segmentation job visually in the CI console as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
- API: You can create an audio/video segmentation job through API as instructed in [Submitting Remuxing Job](https://intl.cloud.tencent.com/document/product/1045/48936).

#### Deleting, querying, and searching for job

You can delete, query, and search for a job by filters through API as instructed in [CancelMediaJob](https://intl.cloud.tencent.com/document/product/1045/49512), [DescribeMediaJob](https://intl.cloud.tencent.com/document/product/1045/50355), and [DescribeMediaJobs](https://intl.cloud.tencent.com/document/product/1045/50356) respectively.

### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, audio/video segmentation will be automatically performed on files uploaded to the bucket or path, and the audio/video segments will be saved in the specified location.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Creating, deleting, querying, and updating workflow through API

You can create, delete, query, and update a workflow through API as instructed in [Creating Workflow](https://intl.cloud.tencent.com/document/product/1045/43733), [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Updating Workflow](https://intl.cloud.tencent.com/document/product/1045/43738) respectively.
