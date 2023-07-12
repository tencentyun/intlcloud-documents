## Overview

The file preview feature leverages CI's capabilities to transcode files into images, PDFs, or HTML5 pages. It addresses the display problems of file content on webpages and enables easy **online file preview** on PC, app, and other terminals. It is widely suitable for diverse business scenarios, such as online education, enterprise OA, and website transcoding.

>?
>- Currently supported input file types include:
  - Presentation files: PPTX, PPT, POT, POTX, PPS, PPSX, DPS, DPT, PPTM, POTM, PPSM.
  - Text files: DOC, DOT, WPS, WPT, DOCX, DOTX, DOCM, DOTM.
  - Spreadsheet files: XLS, XLT, ET, ETT, XLSX, XLTX, CSV, XLSB, XLSM, XLTM, ETS.
  - Other files: PDF, LRC, C, CPP, H, ASM, S, JAVA, ASP, BAT, BAS, PRG, CMD, RTF, TXT, LOG, XML, HTM, HTML.
>- Currently, the above file types can be transcoded to JPG, PNG, PDF, or HTML formats.
>- The input file cannot exceed 200 MB in size or 5,000 pages.



## Architecture

Currently, the file preview feature provides two modes: sync transcoding and async transcoding.

### Sync transcoding

<img src="https://qcloudimg.tencent-cloud.cn/raw/8841b09bf41ea16ae0f4b58c71dc43ba.png" width="550px"  />

### Async transcoding
<img src="https://main.qcloudimg.com/raw/13028a5d31b0f35ae7994e9373f60014.png" width="550px" />

## Use Cases

This feature addresses the display problems of file content on webpages and enables easy online file preview on PC, app, and other terminals. It is widely suitable for diverse business scenarios, such as online education, enterprise OA, and website transcoding.


## Directions

### Through the COS console

To use the file preview feature, you need to activate the file preview service first in the console as instructed in Enabling File Preview.

#### Async transcoding

You can asynchronously transcode files for preview in the COS console as instructed in [Configuring Job](https://intl.cloud.tencent.com/document/product/436/46409).

### Through RESTful APIs

#### Sync transcoding

You can use APIs to transcode files in your bucket for preview in real time:

- To use non-HTML5 preview, see Sync Request API.
- To use HTML5 preview, see Getting Started.
