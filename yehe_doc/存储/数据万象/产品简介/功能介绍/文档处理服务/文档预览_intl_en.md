## Overview

The file preview feature allows you to preview files of nearly 30 types online through image or HTML, with the source file style preserved as much as possible. This addresses the lack of support for certain file formats on different devices and enables easy online file preview on PC, app, and other terminals.

>?
> - File preview is a paid feature. For billing details, see File Processing Fees.
> 



## Use Cases

#### Online education

The file preview feature enables viewing various types of files such as courseware and handouts in online education, which delivers an easier user experience.

#### Enterprise OA

As more and more companies allow employees to work remotely in different places, the demand for file preview on multiple terminals is soaring. CI can help you implement online file preview on PC, app, and other terminals with speed and ease.

#### Online file storage

CI's file preview feature can solve the problem with online display of file content while preserving the source file style to the greatest extent. This meets the needs of browsing files in online file storage services on PC, app, and other terminals.

#### Website transcoding

The display of file content at websites is subject to browser rules. The file preview feature of CI allows generating images from multiple types of files for preview. This addresses the display problems of file content on webpages.

## Directions

### Changing service status

- Enable/Disable the service: You can enable/disable the file preview feature visually in the console. For more information, see [File Preview](https://intl.cloud.tencent.com/document/product/1045/48064).
- Query the status: You can check the file preview feature status of the specified bucket through APIs. For more information, see the API documentation.

### Processing during download

You can use the file preview API to preview a file when downloading it. For more information, see the [API documentation](https://intl.cloud.tencent.com/document/product/1045/47929).

### Job

#### Creating job

- Console: You can create file preview jobs visually in the CI console as instructed in [File Preview](https://intl.cloud.tencent.com/document/product/1045/48064).
- API: You can use APIs to create file preview jobs as instructed in the [API documentation](https://intl.cloud.tencent.com/document/product/1045/47932).

#### Querying/Pulling job

- Console:
  You can view the execution status of jobs and find/pull specified jobs on the file preview page in the CI console. For detailed directions, see [File Preview](https://intl.cloud.tencent.com/document/product/1045/48064).

- API:
 - Query job: You can use the file preview API to query the specified job as instructed in the API documentation.
 - Pull job: You can use the file preview API to pull all tasks that meet the conditions as instructed in the API documentation.

### Queue

- Query: You can use the file preview API to query the queue as instructed in the API documentation.
- Update: You can use the file preview API to update the file preview queue as instructed in the API documentation.
