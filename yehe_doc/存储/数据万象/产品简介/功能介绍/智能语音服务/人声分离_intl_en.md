## Overview

The voice/sound separation feature separates the voice from the background sound in a video material to generate a new independent audio file. Then, you can apply artistic processing of other styles to the material without accompaniment and noise.

## Use Cases

#### Post audio mixing

Diverse stylistic and artistic processing operations can be performed on voices, background sounds, and accompaniments after separation, such as voice changing and audio mixing.

#### Video promotion

Voices can be quickly separated, and then different background sounds can be added to mix materials for targeted marketing to user groups with different interests.

## Directions

You can use the voice/sound separation feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can customize voice/sound separation templates as follows:

Custom templates: You can create a template in the console as instructed in [Template](https://intl.cloud.tencent.com/document/product/1045/43606). You can also create, modify, find, and delete a template through API as instructed in [Creating Voice/Sound Separation Template](https://intl.cloud.tencent.com/document/product/1045/49916), [Updating Voice/Sound Separation Template](https://intl.cloud.tencent.com/document/product/1045/49930), [DescribeMediaTemplates](https://intl.cloud.tencent.com/document/product/1045/49919), and [DeleteMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49918) respectively.


### Through job

You can create a voice/sound separation job through the console or API for existing data stored in COS.

- Console: You can create a voice/sound separation job visually in the CI console as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
- API: You can create a voice/sound separation job through API as instructed in [Submitting Voice/Sound Separation Job](https://intl.cloud.tencent.com/document/product/1045/48946).


### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, voice/sound separation will be automatically performed on files uploaded to the bucket or path, and the output audio files will be saved in the specified location.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Deleting, querying, and searching for workflow

You can delete, query, and test a workflow through API as instructed in [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Testing Workflow](https://intl.cloud.tencent.com/document/product/1045/50340) respectively.
