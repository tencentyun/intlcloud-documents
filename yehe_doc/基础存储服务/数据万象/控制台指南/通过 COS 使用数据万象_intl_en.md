## Overview

CI depends on COS to process data. You can use the COS console/SDK to quickly use CI services such as content moderation and media processing. This document describes the precautions for using CI via COS and how to use it.

>? Using CI incurs data processing fees, and the storage and traffic fees incurred will be charged by COS. For detailed pricing, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/436/16871).
>

## Prerequisites

- You have activated COS and created a bucket. If you haven’t, go to the [COS console](https://console.cloud.tencent.com/cos5) to activate COS and create a bucket as instructed.
- You have activated CI. If you haven’t, go to the [CI console](https://console.cloud.tencent.com/ci) to activate it as instructed.


## Directions

1. [Create a bucket](https://intl.cloud.tencent.com/document/product/436/13309) via the COS console and [upload the files to process](https://intl.cloud.tencent.com/document/product/436/13321) to the bucket.
2. On the left sidebar of the COS console, click **Bucket List** and then click the name of the created bucket.
3. On the bucket management page, use the following full data processing capabilities of CI:
 - Content moderation
 - Data processing
 - Workflow
4. CI’s data processing capabilities have also been integrated into COS SDKs. For the calling directions, please see [SDK Overview](https://intl.cloud.tencent.com/document/product/436/6474).
