## Overview

The text to speech feature converts text to natural-sounding and smooth speeches in a variety of voices in PCM, WAV, or MP3 format through advanced deep learning technology. It comes with various features such as speech speed, voice, and volume adjustment. It is suitable for diverse scenarios, including smart customer service, voice interaction, audiobook, and accessible broadcasting.

## Use Cases

#### Smart customer service

The text to speech feature works with speech recognition and natural language processing modules to close the loop of human-machine interaction in customer service bot and task service robot use cases. The highly natural bot voices make human-machine interaction more natural.

#### Audiobook

Electronic courseware, novels, and other types of text can be converted to audios of different voices to create audiobooks that can be listened to at any time.

## Directions

You can use the text to speech feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can customize text-to-speech templates as follows:

Custom templates: You can create a template in the console as instructed in [Template](https://intl.cloud.tencent.com/document/product/1045/43606). You can also create, modify, find, and delete a template through API as instructed in [Creating Text-to-Speech Template](https://intl.cloud.tencent.com/document/product/1045/49913), [Updating Text-to-Speech Template](https://intl.cloud.tencent.com/document/product/1045/49927), [DescribeMediaTemplates](https://intl.cloud.tencent.com/document/product/1045/49919), and [DeleteMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49918) respectively.

### Voice description

| Name | Voice Parameter Value | Type | Use Case | Supported Languages | Voice Quality |
|---------|---------|---------|---------|---------|---------|
| Ruxue | ruxue | Standard female voice | General | Chinese, Chinese-English mix | Standard |
| Aixiaonan | aixiaonan | Sweet female voice | General, social | Chinese, Chinese-English mix | Premium |
| Aixiaoxing | aixiaoxing | Commentary male voice | General, commentary | Chinese, Chinese-English mix | Premium |
| Alice | alice | Standard female voice | General | English | Premium |

### Multi-sentiment voice description

| Name | Voice Parameter Value | Sentiment Category |
|---------|---------|---------|
| Aixiaoxing | aixiaoxing | Neutral, broadcasting, calm, excited |

>? Text to speech supports async and sync modes. If the input text is short, such as in the one-sentence scenario, the sync mode is recommended.
>

### Through job

You can create a text-to-speech job through the console or API for existing data stored in COS.

- Console: You can create a text-to-speech job visually in the CI console as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
- API: You can create a text-to-speech job through API as instructed in [Submitting Text-to-Speech Job](https://intl.cloud.tencent.com/document/product/1045/48942).

### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, text to speech will be automatically performed on files uploaded to the bucket or path, and the generated audio files will be saved in the specified location.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Creating, deleting, querying, and updating workflow through API

You can create, delete, query, and update a workflow through API as instructed in [Creating Workflow](https://intl.cloud.tencent.com/document/product/1045/43733), [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Updating Workflow](https://intl.cloud.tencent.com/document/product/1045/43738) respectively.

