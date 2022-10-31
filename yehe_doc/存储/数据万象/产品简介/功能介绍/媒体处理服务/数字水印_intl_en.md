## Overview

CI can hide images and strings in a video or image in a way they can hardly be detected or modified, without compromising the integrity and layout of the video or image. By identifying the watermark hidden in the content, you can confirm the content creator, copyright owner, and spreaders and check whether the video content is tampered with.



## Use Cases

#### Copyright protection

CI's digital watermark integrates transparency, robustness, security, and identification, making it a must-have feature for creators. Such watermarks can resist various attacks such as cropping, transcoding, special effect, rotation, and filter. By identifying the watermark hidden in the content, you can confirm the content creator, copyright owner, and spreaders and check whether the video content is tampered with.


## Directions

You can use the digital watermark feature through jobs or workflows.

### Through job

You can add a digital watermark to an existing video stored in COS by enabling video watermark when creating an audio/video transcoding job or by creating an independent digital watermark job through the console or API.

- Console: You can create an audio/video transcoding or digital watermark extracting job visually in the CI console as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
- API: You can create a digital watermark job through API as instructed in [Submitting Digital Watermark Extracting Job](https://intl.cloud.tencent.com/document/product/1045/48931).


### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, digital watermark operations will be automatically performed on files uploaded to the bucket or path.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Creating, deleting, querying, and updating workflow through API

You can create, delete, query, and update a workflow through API as instructed in [Creating Workflow](https://intl.cloud.tencent.com/document/product/1045/43733), [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Updating Workflow](https://intl.cloud.tencent.com/document/product/1045/43738) respectively.

