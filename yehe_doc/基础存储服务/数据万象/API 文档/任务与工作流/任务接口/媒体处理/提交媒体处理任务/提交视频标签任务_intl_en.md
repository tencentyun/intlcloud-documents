## Feature Description

This API is used to submit a video tagging job.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateAnimationTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>



## Request

#### Sample request

```shell
POST /jobs HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>VideoTag</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <VideoTag>
            <Scenario>Stream</Scenario>
        </VideoTag>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | -------- |
| Request            | None     | Request container | Container | Yes       |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ------------------------------------------------------- | --------- | -------- |
| Tag                | Request | Job tag: VideoTag                                   | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default). It has a higher priority than that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It has a higher priority than that of the queue.                    | String | No |
| CallBack           | Request | Job callback address, which has a higher priority than that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure > CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | ------------------------------------------------------------ | ------ | -------- |
| Object             | Request.Input | Name of the media file on which to perform the video tagging job. Currently, .mp4, .avi, .mkv, .wmv, .rmvb, .flv, and .mov formats are supported. For videos longer than 30 minutes, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance. | String | Yes |

<span id="operation"></span>
`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------ | --------- | -------- |
| VideoTag            | Request.Operation | `VideoTag` job parameter                                             | Container | Yes  |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0` (default), `1`, `2`. | String | No |
| UserData           | Response.JobsDetail.Operation | The user information passed through.                      | String | No |

`VideoTag` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | :------------------------- | ------------------------------------------------------------ | ------ | -------- | -------------------------- |
| Scenario           | Request.Operation.VideoTag | Scenario type. You can select the application scenario of the video tag. The used algorithm, input, and output vary by scenario. | string | Yes | The current version is only adapted to the `Stream` scenario |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j8d121820f5e411ec926ef19d53ba9c6f</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>VideoTag</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <VideoTag>
                <Scenario>Stream</Scenario>
            </VideoTag>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| JobsDetail         | Response | Job details | Container |

<span id="jobsDetail"></span>
`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag                | Response.JobsDetail | Job tag: VideoTag                              | String    |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | ID of the queue which the job is in                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation          | Response.JobsDetail | Operation rule                           | Container |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------ | ---------------- | ------ |
| Region             | Response.JobsDetail.Input | Bucket region     | String |
| Bucket             | Response.JobsDetail.Input | Result storage bucket | String |
| Object             | Response.JobsDetail.Input | Output result filename | String |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :------------------------------------ | :-------- |
| VideoTag | Response.JobsDetail.Operation | Same as `Request.Operation.VideoTag` in the request. |  Container |
| VideoTagResult     | Response.JobsDetail.Operation | Video tag analysis result, which will not be returned when the job is not completed. |  Container |
| UserData           | Response.JobsDetail.Operation | The user information passed through.                      | String |
| JobLevel    | Response.JobsDetail.Operation | Job priority                                                         | String |

`VideoTagResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------------------- | :------------------------------ | :-------- |
| StreamData | Response.JobsDetail.Operation.VideoTagResult | Result of the video tagging job in the `Stream` scenario | Container |

`StreamData` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------------------------------ | :------------------------------------------- | :-------- |
| Data | Response.JobsDetail.Operation.VideoTagResult.StreamData | Result list of the video tagging job in the `Stream` scenario | Container |
| SubErrCode | Response.JobsDetail.Operation.VideoTagResult.StreamData | Algorithm status code. `0`: Success. Other values: Exception. | String |
| SubErrMsg | Response.JobsDetail.Operation.VideoTagResult.StreamData | Algorithm error message. `ok` indicates a success. If the request fails, the corresponding error is returned. | String |

`Data` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------------------- | :--------------------- | :-------- |
| Tags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data | Video tag and video category information |  Container |
| PersonTags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data | Person tag information |  Container array |
| PlaceTags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data | Scene tag information |  Container array |
| ActionTags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data | Action tag information |  Container array |
| ObjectTags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data | Object tag information |  Container array |

`Tags` (video tag) has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------------------------------ | :----- |
| Tag | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags | Tag name |  String |
| TagCls | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags | Tag category |  String |
| Confidence | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags | Tag model prediction score. Value range: [0, 1]. |  Float |

`Tags` (video category) has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------------------- | :------------------------------ | :----- |
| Tag | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags | Video category |  String |
| Confidence | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags | Tag model prediction score. Value range: [0, 1]. |  Float |

`PersonTags` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------------------- | :--------------------------------- | :-------- |
| Name | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags | Person name |  String |
| Confidence | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags | Tag model prediction score |  Float |
| Count | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags | Number of person appearances | String |
| DetailPerSecond | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags | Location and time of person appearance | Container array |

`DetailPerSecond` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------------------- | :--------------------------- | :-------- |
| TimeStamp | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond | Appearance time in seconds |  String |
| Confidence | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond | Tag model prediction score |  Float |
| BBox | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond | Relative coordinates of the object with top-left corner as the origin | Container array |

`BBox` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------------------- | :--------------- | :----- |
| X1 | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond.BBox | Relative position of coordinate X1 |  String |
| Y1 | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond.BBox | Relative position of coordinate Y1 |  String |
| X2 | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond.BBox | Relative position of coordinate X2 |  String |
| Y2 | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond.BBox | Relative position of coordinate Y2 |  String |

`PlaceTags` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------- |
| Tags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Video scene tag information, which may not be returned and is the same as `Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags`. |  Container array |
| StartTime | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Segment start time in seconds |  String |
| EndTime | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Segment end time in seconds |  String |
| StartIndex | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Segment start frame number |  String |
| EndIndex | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Segment end frame number |  String |
| ClipFrameResult | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Top 1 single frame recognition result |  String |

`ActionTags` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------- |
| Tags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ActionTags | Video action tag information, which may not be returned and is the same as `Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags`. |  Container array |
| StartTime | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ActionTags | Segment start time in seconds |  String |
| EndTime | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ActionTags | Segment end time in seconds |  String |

`ObjectTags` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------- |
| Objects | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ObjectTags | Video object tag information, which may not be returned and is the same as `Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags`. |  Container array |
| TimeStamp | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ObjectTags | Timestamp of the identified object in seconds |  String |


`Object` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :-------- |
| Name | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ObjectTags.Objects | Object name |  string |
| Confidence | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ObjectTags.Objects | Tag model prediction score. Value range: [0, 1]. |  Float |
| BBox | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ObjectTags.Objects | Relative coordinates of the object with top-left corner as the origin, which is the same as `Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond.BBox`. |  Container array |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Samples

#### Request

```shell
POST /jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>VideoTag</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <VideoTag>
            <Scenario>Stream</Scenario>
        </VideoTag>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j8d121820f5e411ec926ef19d53ba9c6f</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>VideoTag</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <VideoTag>
                <Scenario>Stream</Scenario>
            </VideoTag>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```
