## Overview

The audio noise cancellation feature removes device noise, ambient noise, and other noises for an audio in course recording, outdoor shooting post-production, or other scenarios.

>? The input file is a video file.
>

## Use Cases

#### Post-optimization of online courses/conferences

Noise cancellation and gain processing are performed on an audio recorded in unfavorable environment or by an unfavorable device, so that the audio information in the course can be accurately transmitted.

#### UGC creation

Audio noise is removed and the accuracy of speech recognition is improved to reduce the amount of automatic subtitle modification and optimize the audio quality of the finished content.


## How to Use

You can use the audio noise cancellation feature through jobs or workflows.


### Through job

You can create an audio noise cancellation job through the console or API for existing data stored in COS.


- API: You can create an audio noise cancellation job through API as instructed in [Submitting Audio Noise Cancellation Job](https://intl.cloud.tencent.com/document/product/1045/48933) in the API documentation.


### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, audio noise cancellation will be automatically performed on files uploaded to the bucket or path, and the muxed files will be saved in the specified location.

#### Creating a workflow

You can create a workflow using the CI console. For more information, see [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Creating, deleting, querying, and updating a workflow through API

You can [create a workflow](https://intl.cloud.tencent.com/document/product/1045/43733), [delete a workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [query workflows](https://intl.cloud.tencent.com/document/product/1045/50339), and [update a workflow](https://intl.cloud.tencent.com/document/product/1045/43738) through APIs.
