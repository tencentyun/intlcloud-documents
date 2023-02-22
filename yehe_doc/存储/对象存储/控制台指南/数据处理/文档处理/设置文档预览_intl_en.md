## Overview

The COS console allows you to preview documents in a bucket. This document describes how to use the document preview feature in the console. For information on document preview, see [Document Preview Overview](https://intl.cloud.tencent.com/document/product/436/49159).


>!
>- The document preview feature is available in public cloud regions in the Chinese mainland and Silicon Valley, Virginia, Frankfurt, and Singapore. Currently, only document-to-image conversion preview is supported in Singapore and Silicon Valley.
> - Document preview is charged by CI. For detailed pricing, see [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).


## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar, and then click the bucket for which you want to enable the document preview feature.
3. Click **Data Processing** > **Document Processing**. In the **Document Preview** area, click **Edit** and toggle on the status
4. To preview a document, add parameters to the document URL. The parameters are described as follows:
```plaintext
<BucketName-APPID>.cos.<Region>.myqcloud.com/<objectkey>?ci-process=doc-preview&page=<page>&srcType=<srcType>
```
 - objectkey: Object key, which can be understood as a file path.
 - ci-process: CI's processing capability, which is fixed at `doc-preview` for document preview.
 - page: Number of the page to be converted, which is counted from 1.
 - srcType: Source data type. Currently, the file conversion feature determines the source data type according to the file extension of the COS object. If the object has no extension, you can set this value.


>! If you use the URL mode, only a single-page document or the first page of a multi-page document can be processed. If you want to preview more content, use [Document Preview API](https://intl.cloud.tencent.com/document/product/436/49404).
>
