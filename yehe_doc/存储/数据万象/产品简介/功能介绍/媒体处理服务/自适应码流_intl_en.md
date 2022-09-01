## Overview

The adaptive bitrate streaming feature can generate multi-bitrate adaptive HLS or DASH target files from a single original video at one time, helping you quickly distribute video content in different network conditions.

## Use Cases

- Video website: The bitrate can be automatically switched according to network conditions without affecting the watch experience.
- Short video terminal: The bitrate can be automatically switched according to network conditions without affecting the watch experience.
- Online meeting and education: The bitrate can be adapted to network conditions to improve the communication quality.

## How to Use

You can use the adaptive bitrate streaming feature through a workflow.

### Through workflow

CI provides the workflow service. You can enable a workflow for a bucket or a specific path. Then, adaptive bitrate streaming will be automatically performed on files uploaded to the bucket or path, and the muxed files will be saved in the specified location.

You can create a workflow through the console or API:

- Console: You can create a workflow in the console to use the HLS adaptive muxing feature. For more information, see Workflow.
- API: You can use an API to create an HLS adaptive muxing workflow. For more information, see the [API documentation](https://intl.cloud.tencent.com/document/product/1045/43733).

