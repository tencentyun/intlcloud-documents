## Overview

The text to speech feature converts text to natural-sounding and smooth speeches in a variety of voices through advanced deep learning technology. It comes with various features such as speech speed, voice, and volume adjustment. It is suitable for diverse scenarios, including smart customer service, voice interaction, audiobook, and accessible broadcasting.

## Use Cases

#### Smart customer service

The text to speech feature works with speech recognition and natural language processing modules to close the loop of human-machine interaction in customer service bot and task service robot use cases. The highly natural bot voices make human-machine interaction more natural.

#### Audiobook

Electronic courseware, novels, and other types of text can be converted to audios of different voices to create audiobooks that can be listened to at any time.

## How to Use

You can use the text to speech feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can customize text-to-speech templates as follows:

Custom templates: You can create templates in the [console](https://cloud.tencent.com/document/product/460/46490). You can also [create](https://intl.cloud.tencent.com/document/product/1045/48126), [modify](https://intl.cloud.tencent.com/document/product/1045/48129), [find](https://intl.cloud.tencent.com/document/product/1045/48128), and [delete](https://intl.cloud.tencent.com/document/product/1045/48127) templates through APIs.


### Through job

You can create text-to-speech jobs through the console or APIs to convert text to speech for existing data in COS.

- Console: You can create a job visually in the CI console as instructed in the text-to-speech job documentation.
- API: You can use APIs to create text-to-speech jobs as instructed in the [API documentation](https://intl.cloud.tencent.com/document/product/1045/48147).

### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, text to speech will be automatically performed on files uploaded to the bucket or path, and the generated audio files will be saved in the specified location.

#### Creating workflow

You can create a workflow in the CI console as instructed in Creating Workflow.

#### Deleting, querying, and searching for workflow

You can [delete workflows](https://intl.cloud.tencent.com/document/product/1045/43734), [search for specified workflows](https://intl.cloud.tencent.com/document/product/1045/43735), [get workflow details](https://intl.cloud.tencent.com/document/product/1045/43736), and [get the list of workflow instances](https://intl.cloud.tencent.com/document/product/1045/43737) through APIs.

