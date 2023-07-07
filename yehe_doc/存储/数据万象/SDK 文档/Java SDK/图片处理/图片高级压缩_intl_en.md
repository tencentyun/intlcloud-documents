## Overview

This document provides an overview of APIs and SDK code samples for image advanced compression.


<table>
<thead>
<tr>
<th align="left" width="15%">API</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody><tr>
<td align="left"><a href="https://www.tencentcloud.com/document/product/1045/42363">Image advanced compression</a></td>
<td align="left">The image advanced compression feature allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transmission time, loading time, and the use of bandwidth and traffic.</td>
</tr>
</tbody></table>

### Sample code

[//]: # ".cssg-snippet-process-with-pic-operation"
```java
GetObjectRequest getObj = new GetObjectRequest(bucketName, key);
// The following are sample parameters for image compression. For more information, see CI's API documentation.
String compress = "imageMogr2/format/tpg";
getObj.putCustomQueryParameter(compress, null);
```
