
## Overview

This document provides an overview of APIs and SDK code samples for image advanced compression.


| API | Description |
| :--------------- |  :--------------------- |
| [Image advanced compression](https://intl.cloud.tencent.com/document/product/1045/40108) | Allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transfer time, loading time, and the use of bandwidth and traffic. |


#### Sample request

```
// Convert the input image to TPG format
name := "test.png"
filepath := "test.tpg"
_, err := c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/format/tpg", nil)
if err != nil {
	// ERROR
}

// Convert the input image to HEIF format
filepath = "test.heif"
_, err = c.CI.GetToFile(context.Background(), name, filepath, "imageMogr2/format/heif", nil)
if err != nil {
	// ERROR
}
```
