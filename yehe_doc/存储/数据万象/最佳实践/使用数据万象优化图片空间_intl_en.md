## Overview

As your business grows, the used storage space and traffic of [COS](https://intl.cloud.tencent.com/document/product/436) increase rapidly, especially for image services, the most critical part of the web. Due to the sync loading feature of HTML, an image is usually loaded only after the previous image is fully loaded, yet lowering the resolution locally will lose most of the details in images. [CI](https://intl.cloud.tencent.com/document/product/1045) provides the extremely cost-effective [image compression](https://intl.cloud.tencent.com/document/product/1045/40107) feature to greatly reduce the image size. This document takes HEIF as an example.

For billing details, see Image Advanced Compression Fees.

 The HEIF compression feature can convert images into the HEIF format. HEIF offers over 80% smaller file sizes at the same quality compared with JPG and has the highest compression speed.

AVIF is a new compressed image format based on AV1, which can only be viewed in newer browsers.

Image compatibility is as follows:
<table>
<tr><th>Format</th><th>Android 12</th><th>iOS 15.4</th><th>Windows 11</th><th>Compression</th></tr>
<tr><td>PNG</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>None</td></tr>
<tr><td>JPG</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>None</td></tr>
<tr><td>AVIF</td><td>×</td><td>×</td><td>Extension required</td><td>↓ 50+%</td></tr>
<tr><td>HEIF</td><td>&#10003;</td><td>&#10003;</td><td>Extension required</td><td>↓ 30+%</td></tr>
<tr><td>TPG</td><td>QQ Browser only</td><td>QQ Browser only</td><td>QQ Browser only</td><td>↓ 50+%</td></tr>
<tr><td>WebP</td><td>&#10003;</td><td>&#10003;</td><td>&#10003;</td><td>↓ 20+%</td></tr>
</table>

## Prerequisites

- You have logged in to the [CI console](https://console.cloud.tencent.com/ci) and activated the CI service.
- You have created and bound a storage bucket. For more information, see [Configuring Buckets](https://intl.cloud.tencent.com/document/product/1045/33440).
- You have activated [image advanced compression](https://intl.cloud.tencent.com/document/product/1045/40106).

## Directions
### Processing existing data

#### Processing through job

1. Create a template as instructed in Image Processing.
The main parameters are as follows:
 - Resize Mode: Select **No-scaling**.
 - Output Format: Select **AVIF** or **HEIF**.
2. Create a job as instructed in Creating Image Processing Job.

>? The operations are tedious if you need to batch process data. In this case, we recommend you [process data through a workflow](#ProcessWorkflow).
>

<span id="ProcessWorkflow"></span>
#### Processing through workflow

1. Create a template as instructed in Image Processing.
The main parameters are as follows:
 - Resize Mode: Select **No-scaling**.
 - Output Format: Select **AVIF** or **HEIF**.
2. Create an image workflow as instructed in Creating Workflow.
The main parameters are as follows:
 - Input Bucket Name: Select the bound bucket.
 - Format Match: Select **Image file**.
 - Configure Workflow: Select **Image processing**.
3. On the workflow management page, find the newly created workflow and click **Run Workflow**.
4. Set the scanning mode to **Run workflow for multiple files**, configure other parameters as needed, and click **Run workflow**. For detailed directions, see Triggering Workflow.



### Processing uploaded data

#### Data workflow (recommended)

On the workflow management page, find the newly created workflow and set **Run upon Upload** to **Enabled**.


#### API method

Images are only processed in real time and cannot be stored as files through the API method. Therefore, you need to keep adding parameters during image upload to have images automatically stored. For more information, see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695).
Here, you need to customize the `rules` parameter, which can be viewed in the image processing section of the workflow details.


## Summary

### Image size comparison

The following is an example:

| Original Image (MB) | HEIF (MB)  | AVIF (MB)  |
|---------|---------|---------|
| 7.91 | 3.2 | 1.8 |
| 18 | 13 | 3.2 |
| 30 | 14 | 6.9 |

As can be clearly seen, HEIF and AVIF greatly reduce the size of the original JPG or PNG image. If there are 100,000 10 MB images in a folder, AVIF can save more than 300 GB space, which reduces storage fees and traffic fees by 24 USD and 102 USD respectively every month in a STANDARD storage pack for regions in the Chinese mainland.


### Strengths and shortcomings


| Type | Advanced Compression | Traditional Compression |
|---------|---------|---------|
| Speed | Fast processing in the cloud | Local processing subject to device conditions |
| Definition | Almost lossless | Lossy |
| Compression ratio | Very high | General |
| Cost | Low | Subject to device conditions |
| Compatibility | Medium | Very high |

We recommend you use the HEIF format on iOS and use WebP or AVIF format on Windows.

## FAQs

### What should I do if processing fails for large images?

Size limit:
- The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels respectively, and the total number of pixels not exceeding 250 million.
- The width and height of the output image cannot exceed 9,999 pixels respectively.
- For an animated input image, the total number of pixels (width * height * number of frames) cannot exceed 250 million.

If the above limits are exceeded, processing will fail. We recommend you use Photoshop or other software tools to reduce the image size before processing.

### What should I do if processing cannot start?

Check whether you have activated the CI service and enabled the image advanced compression feature and whether your account balance is sufficient.


### What should I do if processing takes too long?

Generally speaking, it takes 10 minutes to process an image. If processing takes a longer time, restart the job. If the problem persists, check whether the image content is too complex and optimize it if so.
If the problem persists, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.



