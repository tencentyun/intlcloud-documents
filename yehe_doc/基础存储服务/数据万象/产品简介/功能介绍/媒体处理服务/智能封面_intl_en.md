## Overview

CI's intelligent thumbnail feature intelligently analyzes the quality, brilliance, and content relevance of video frames by understanding the video content with Tencent Media Lab's advanced AI technologies. Then, it extracts optimal frames to generate thumbnails to make the content more engaging.

>?
>
>- The intelligent thumbnail feature is a paid service and billed by the video duration. For billing details, see [Media Processing Fees](https://intl.cloud.tencent.com/document/product/1045/49489).
>- Three optimal keyframes will be output through smart analysis of each video file.



## Use Cases

#### Video platform

For traditional video platforms, reviewers need to watch videos and then manually select thumbnails, which is labor consuming and slows down video release. The intelligent thumbnail feature can quickly select the most striking frames as thumbnails, which saves labor resources and accelerates video release.

#### Family album

At present, most family album services can display only images in loop. For video files in smart albums, the intelligent thumbnail feature can be used to automatically generate album thumbnails for loop display, thereby increasing the richness and utilization of family albums.

## Directions

### Workflow

CI provides the workflow service, which can automatically process videos when they are uploaded and save the processing results in a specified location.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Creating, deleting, querying, and updating workflow through API

You can create, delete, query, and update a workflow through API as instructed in [Creating Workflow](https://intl.cloud.tencent.com/document/product/1045/43733), [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Updating Workflow](https://intl.cloud.tencent.com/document/product/1045/43738) respectively.



### Job

You can create an intelligent thumbnail job for existing data stored in COS.

#### Creating job

- Console: You can create an intelligent thumbnail job visually in the [CI console](https://console.cloud.tencent.com/ci) as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
- API: You can create an intelligent thumbnail job through API as instructed in [Submitting Intelligent Thumbnail Job](https://intl.cloud.tencent.com/document/product/1045/48937).

#### Deleting, querying, and searching for job

You can delete, query, and search for a job by filters through API as instructed in [CancelMediaJob](https://intl.cloud.tencent.com/document/product/1045/49512), [DescribeMediaJob](https://intl.cloud.tencent.com/document/product/1045/50355), and [DescribeMediaJobs](https://intl.cloud.tencent.com/document/product/1045/50356) respectively.

