## Overview

This API (`CreateDocProcessJobs`) is used to submit a file transcoding job.

>!
>- Currently supported input file types include:
>  - Presentation files: PPTX, PPT, POT, POTX, PPS, PPSX, DPS, DPT, PPTM, POTM, PPSM.
>  - Text files: DOC, DOT, WPS, WPT, DOCX, DOTX, DOCM, DOTM.
>  - Spreadsheet files: XLS, XLT, ET, ETT, XLSX, XLTX, CSV, XLSB, XLSM, XLTM, ETS.
      A spreadsheet file may be split into multiple pages, with multiple images generated.
>  - Other files: PDF, LRC, C, CPP, H, ASM, S, JAVA, ASP, BAT, BAS, PRG, CMD, RTF, TXT, LOG, XML, HTM, HTML.
>- The input file size cannot exceed 200 MB.
>- The number of pages in the input file cannot exceed 5,000.
>- Job records are retained for one month. Save them in time. We recommend you configure callbacks to query job results.


## Request

#### Sample request

```shell
POST /doc_jobs HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
  <Tag></Tag>
  <Input>
    <Object></Object>
  </Input>
  <Operation>
    <Output>
      <Region></Region>
      <Bucket></Bucket>
      <Object></Object>
    </Output>
    <DocProcess>
       <StartPage></StartPage>
       <EndPage></EndPage>
       <TgtType></TgtType>
    </DocProcess>
  </Operation>
  <QueueId></QueueId>
</Request>
```

The nodes are described as follows:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>API Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>Request</td>
      <td>N/A</td>
      <td>Request container</td>
      <td>Container</td>
      <td>Supported</td>
   </tr>
</table>


`Request` has the following sub-nodes:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>API Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>Tag</td>
      <td>Request</td>
      <td>Job type, which currently can only be `DocProcess`.</td>
      <td>String</td>
      <td>Supported</td>
   </tr>
   <tr>
      <td>Input</td>
      <td>Request</td>
      <td>The object to be processed</td>
      <td>Container</td>
      <td>Supported</td>
   </tr>
   <tr>
      <td>Operation</td>
      <td>Request</td>
      <td>Operation rule</td>
      <td>Container</td>
      <td>Supported</td>
   </tr>
   <tr>
      <td>QueueId</td>
      <td>Request</td>
      <td>Queue ID of the job, which is automatically generated after the preview service is activated. Use the API for <a href="https://intl.cloud.tencent.com/document/product/1045/47935">querying file transcoding queue</a> to get it, or query it in the bucket in the <a href="https://console.cloud.tencent.com/ci">CI console</a>.</td>
      <td>String</td>
      <td>Supported</td>
   </tr>
</table>


`Input` has the following sub-nodes:

<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>API Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>Object</td>
      <td>Request.Input</td>
      <td>File URL in COS. `Bucket` is specified by `Host`.</td>
      <td>String</td>
      <td>Supported</td>
   </tr>
</table>




`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | --------------------------------------------- | --------- | -------- |
| DocProcess         | Request.Operation | Task type parameter, which takes effect only if `Tag` is `DocProcess`. | Container | Yes       |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |


`DocProcess` has the following sub-nodes:

#### Common request parameters

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :--------------------------- | ------------------------------------------------------------ | ------ | -------- |
| SrcType            | Request.Operation.DocProcess | Source data type. Currently, the file conversion feature determines the source data type according to the file extension of the COS object. If the object has no extension, you can set this value. | String | Yes       |
| TgtType            | Request.Operation.DocProcess | Type of the output target file. Valid values: jpg, png, pdf. If the input file format cannot be recognized, the `jpg` format will be used by default. You cannot specify pages for the `pdf` format. | String | No |
| StartPage          | Request.Operation.DocProcess | Starts conversion from page X. A spreadsheet file may be split into multiple pages, with multiple images generated, and `StartPage` indicates to start the conversion from page X of the specified `SheetId`. Default value: 1. | Int    | No       |
| EndPage            | Request.Operation.DocProcess | Ends conversion on page X. A spreadsheet file may be split into multiple pages, with multiple images generated, and `EndPage` indicates to end the conversion on page X of the specified `SheetId`. Default value: -1 (converting all pages). | Int    | No       |

#### Parameters for spreadsheet files (Excel)

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :--------------------------- | ------------------------------------------------------------ | ---- | -------- |
| SheetId            | Request.Operation.DocProcess | Sheet parameter, indicating to convert the xth sheet. Default value: 0 (converting all sheets). | Int  | No       |
| PaperDirection     | Request.Operation.DocProcess | Paper orientation of the spreadsheet. 0: vertical; other values: horizontal. Default value: 0. | Int  | No       |
| PaperSize          | Request.Operation.DocProcess | Page (canvas) size. Valid values: 0 (A4), 1 (A2), 2 (A0). Default value: 0. | Int  | No       |

#### Parameters for transcoding to .png/.jpg images

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :--------------------------- | ------------------------------------------------------------ | ------ | -------- |
| ImageParams        | Request.Operation.DocProcess | Processing parameters for the output image. All parameters of [basic image processing](https://www.tencentcloud.com/document/product/1045/33694) are supported. To specify multiple parameters, separate them by [pipeline operator](https://intl.cloud.tencent.com/document/product/1045/33727). In this way, the image can be processed by multiple parameters in sequence in the same request. | String | No       |
| Quality            | Request.Operation.DocProces  | Quality of the generated preview image. Value range: [1-100]. Default value: 100. For example, if the value is 100, the quality of the generated image will be 100%.                | Int  | No       |
| Zoom               | Request.Operation.DocProces  | Scaling parameter of the preview image. Value range: [10-200]. Default value: 100. For example, if the value is 200, the image will be scaled up (enlarged) by 200%.                | Int  | No       |
| ImageDpi           | Request.Operation.DocProcess | Renders the image according to the specified DPI. This parameter works together with `Zoom`. Value range: 96–600. Default value: 96. The width of the output image must be less than 65500 px. | Int | No |
| PicPagination      | Request.Operation.DocProcess | Whether to convert to a single long image. When this parameter is set to 1, up to 20 standard pages can be converted to a single long image, and more pages will cause an error. The page range can be controlled by `StartPage` and `EndPage`. The default value is 0, indicating to output images by page. This parameter will take effect only if `TgtType` is `png` or `jpg`. | Int | No |


`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | -------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Output file path. <br/>**For non-spreadsheet files, the output file name must include the `${Number}` or `${Page}` parameter.** If there are multiple output files, `${Number}` indicates that serial numbers start from 1, and `${Page}` indicates that serial numbers are the same as preview page numbers. <li>`${Number}` indicates that serial numbers start from 1 for multiple output files; for example, if the input parameter is `abc_${Number}.jpg` to preview pages 5–6 in the file, then output file names will be `abc_1.jpg` and `abc_2.jpg`. <li>`${Page}` indicates that serial numbers are the same as preview page numbers for multiple output files; for example, if the input parameter is `abc_${Page}.jpg` to preview pages 5–6 in the file, then the output file names will be `abc_5.jpg` and `abc_6.jpg`. <br/>**For spreadsheet files, the output file path must include the `${SheetID}` placeholder, and the output file name must include the `${Number}` parameter.** <li>For example, if the input parameter is `/${SheetID}/abc_${Number}.jpg`, then the corresponding number of folders will be generated first according to the number of Excel sheets to be converted, and then the corresponding number of image files will be generated in these folders.</li> | String  | Yes |



## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
        <JobsDetail>
                <Code></Code>
                <CreationTime></CreationTime>
                <EndTime></EndTime>
                <Input>
                    <Object></Object>
                </Input>
                <JobId></JobId>
                <Message/>
                <Operation>
                    <DocProcess>
                        <SrcType></SrcType>
                        <TgtType></TgtType>
                        <StartPage></StartPage>
                        <EndPage></EndPage>
                        <ImageParams></ImageParams>
                    </DocProcess>
                    <Output>
                        <Bucket></Bucket>
                        <Object></Object>
                        <Region></Region>
                    </Output>
                </Operation>
                <QueueId></QueueId>
                <State></State>
                <Tag></Tag>
        </JobsDetail>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| JobsDetail | Response | Job details |  Container |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag | Response.JobsDetail | Job type: DocProcess | String |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| QueueId            | Response.JobsDetail | Queue ID of the job                       | String    |
| Input              | Response.JobsDetail | Input file path of the job                   | Container |
| Operation          | Response.JobsDetail | Operation rule. Up to 6 operation rules are supported.                           | Container |

`Input` has the following sub-nodes:
Same as the `Request.Input` node in the request.

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :--------------- | :-------- |
| DocProcess         | Response.JobsDetail.Operation | File preview job parameter | Container |
| Output             | Response.JobsDetail.Operation | File output address   | Container |

`DocProcess` has the following sub-nodes:
Same as the `Request.Operation.DocProcess` node in the request.

`Output` has the following sub-nodes:
Same as the `Request.Operation.Output` node in the request.


#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Examples

#### Request

```plaintext
POST /doc_jobs HTTP/1.1
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: cos-python-sdk-v5.3.2
Host: examplebucket-1250000000.ci.ap-chongqing.myqcloud.com
Content-Type: application/xml
Content-Length: 546
Authorization: Authorization

<?xml version="1.0" encoding="UTF-8" ?>

<Request>
    <Input>
        <Object>1.doc</Object>
    </Input>
    <Operation>
      <Output>
          <Region>ap-chongqing</Region>
          <Object>big/test-${Number}</Object>
          <Bucket>examplebucket-1250000000</Bucket>
      </Output>
      <DocProcess>
          <TgtType>png</TgtType>
          <StartPage>1</StartPage>
          <EndPage>-1</EndPage>
	      <ImageParams>watermark/1/image/aHR0cDovL3Rlc3QwMDUtMTI1MTcwNDcwOC5jb3MuYXAtY2hvbmdxaW5nLm15cWNsb3VkLmNvbS8xLmpwZw==/gravity/southeast</ImageParams>
      </DocProcess>
    </Operation>
    <Tag>DocProcess</Tag>
    <QueueId>p532fdead78444e649e1a4467c1cd19d3</QueueId>
</Request>[!http]
```

#### Response

```plaintext
HTTP/1.1 200 OK
Date: Mon, 27 Jul 2020 07:20:08 GMT
Content-Type: application/xml
Content-Length: 863
Connection: keep-alive
Server: tencent-ci
x-ci-request-id: NWYxZTgwMjhfYzc2OTQzNjRfMzUx****

<?xml version="1.0" encoding="utf-8"?>
<Response>
        <JobsDetail>
                <Code>Success</Code>
                <CreationTime>2020-07-27T15:20:08+0800</CreationTime>
                <EndTime>-</EndTime>
                <Input>
                        <Object>1.doc</Object>
                </Input>
                <JobId>d99b3127ecfd911eab5e60dedb7c395dd</JobId>
                <Message/>
                <Operation>
                        <DocProcess>
                                <EndPage>5001</EndPage>
                                <ImageParams>watermark/1/image/aHR0cDovL3Rlc3QwMDUtMTI1MTcwNDcwOC5jb3MuYXAtY2hvbmdxaW5nLm15cWNsb3VkLmNvbS8xLmpwZw==/gravity/southeast</ImageParams>
                                <SrcType/>
                                <StartPage>1</StartPage>
                                <TgtType>png</TgtType>
                        </DocProcess>
                        <Output>
                                <Bucket>examplebucket-1250000000</Bucket>
                                <Object>big/test-${Number}</Object>
                                <Region>ap-chongqing</Region>
                        </Output>
                </Operation>
                <QueueId>p532fdead78444e649e1a4467c1cd19d3</QueueId>
                <State>Submitted</State>
                <Tag>DocProcess</Tag>
        </JobsDetail>
</Response>
```

