
## Overview

This document provides an overview of APIs and SDK code samples related to Image Advanced Compression.


| API | Description |
| :--------------- |  :--------------------- |
| [Image Advanced Compression](https://intl.cloud.tencent.com/document/product/436/40119) | Image Advanced Compression allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transmission time, loading time, and the use of bandwidth and traffic. |


#### Sample request 

```
// Convert the image into TPG format.
name := "test.png"
filepath := "test.tpg"
_, err := c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/format/tpg", nil)
if err != nil {
	// ERROR
}

// Convert the image into HEIF format.
filepath = "test.heif"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/format/heif", nil)
if err != nil {
	// ERROR
}
```
