## Overview

CI's video frame capturing feature captures the frames of a video at specified time points during upload or after storage. You can customize the start time point of frame capturing, frame capturing interval, number of frames to be captured, and output image size and format to meet your diversified needs.

>? Video frame capturing is a paid feature. For billing details, see [Media Processing Fees](https://intl.cloud.tencent.com/document/product/1045/49489).
>


## Use Cases

CI's video frame capturing feature is suitable for various scenarios, such as video sampling, specific frame capturing, and random frame capturing.


## Directions

You can use the video frame capturing feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can use a preset or custom template as follows:
- Preset templates: Currently, CI provides a variety of preset templates for most video frame capturing use cases. You can view all such templates in the [CI console](https://console.cloud.tencent.com/ci).
- Custom templates: You can create a template in the console as instructed in [Template](https://intl.cloud.tencent.com/document/product/1045/43606). You can also create, modify, find, and delete a template through API as instructed in [Creating Screenshot Template](https://intl.cloud.tencent.com/document/product/1045/49909), [Updating Screenshot Template](https://intl.cloud.tencent.com/document/product/1045/49923), [DescribeMediaTemplates](https://intl.cloud.tencent.com/document/product/1045/49919), and [DeleteMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49918) respectively.


### Job

You can create a video frame capturing job for existing data stored in COS.

- Console: You can create a video frame capturing job visually in the CI console as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
- API: You can create a video frame capturing job through API as instructed in [Submitting Screenshot Job](https://intl.cloud.tencent.com/document/product/1045/48938).


### Workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, frame capturing will be automatically performed on videos uploaded to the bucket or path, and the screenshots will be saved in the specified location.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Creating, deleting, querying, and updating workflow through API

You can create, delete, query, and update a workflow through API as instructed in [Creating Workflow](https://intl.cloud.tencent.com/document/product/1045/43733), [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Updating Workflow](https://intl.cloud.tencent.com/document/product/1045/43738) respectively.
