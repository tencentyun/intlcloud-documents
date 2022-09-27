## Overview

By leveraging the multimodal content understanding technology, this feature recognizes and aggregates the video content, postures, and scenes to quickly and professionally generate highlights such as shots in games, choruses of songs, and hilarious moments in variety shows, making it suitable for sports events, variety shows, galas, and many other scenarios.

## Use Cases

#### Game replay

Exciting moments like shooting and scoring during sports events and games can be quickly clipped to generate highlights for replay.

#### Video promotion

Official promotional materials and highlights can be automatically generated for targeted marketing to user groups with different interests.

## Directions

You can use the video montage feature through jobs or workflows. In order to improve the operational efficiency and reduce repetitive operations, CI offers the template feature, which is a configuration item in jobs and workflows. You can save common parameter combinations as templates and reuse them directly in subsequent operations, with no need to set the parameters every time you start a job. You can customize video montage templates as follows:

Custom templates: You can create a template in the console as instructed in [Template](https://intl.cloud.tencent.com/document/product/1045/43606). You can also create, modify, find, and delete a template through API as instructed in [Creating Video Montage Template](https://intl.cloud.tencent.com/document/product/1045/49914), [Updating Video Montage Template](https://intl.cloud.tencent.com/document/product/1045/49928), [DescribeMediaTemplates](https://intl.cloud.tencent.com/document/product/1045/49919), and [DeleteMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/49918) respectively.


### Through job

You can create a video montage job through the console or API for existing data stored in COS.

- Console: You can create a video montage job visually in the CI console as instructed in [Job](https://intl.cloud.tencent.com/document/product/1045/43605).
- API: You can create a video montage job through API as instructed in [Submitting Video Montage Job](https://intl.cloud.tencent.com/document/product/1045/48943).

### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, video montage operations will be automatically performed on files uploaded to the bucket or path, and the generated highlights will be saved in the specified location.

#### Creating workflow

You can create a workflow in the CI console as instructed in [Workflow](https://intl.cloud.tencent.com/document/product/1045/43604).

#### Deleting, querying, and testing workflow

You can delete, query, and test a workflow through API as instructed in [Deleting Workflow](https://intl.cloud.tencent.com/document/product/1045/43734), [Querying Workflow](https://intl.cloud.tencent.com/document/product/1045/50339), and [Testing Workflow](https://intl.cloud.tencent.com/document/product/1045/50340) respectively.

