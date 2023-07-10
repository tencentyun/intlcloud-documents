## Overview

This document provides an overview of APIs and SDK code samples related to Image Advanced Compression.


| API | Description |
| :--------------- |  :--------------------- |
| [Image Advanced Compression](https://intl.cloud.tencent.com/document/product/436/40119) | Image Advanced Compression allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transmission time, loading time, and the use of bandwidth and traffic. |

#### Sample code

[//]: # ".cssg-snippet-process-with-pic-operation"
```java
GetObjectRequest getObj = new GetObjectRequest(bucketName, key);
// The following are parameters for image compression. For more information, please see the API description of CI.
String compress = "imageMogr2/format/tpg";
getObj.putCustomQueryParameter(compress, null);
```