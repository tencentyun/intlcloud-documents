## Feature Overview

This API is used to submit a video object detection job.

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
>
> Authorization: Auth String. For more information, see [Request Signature](https://www.tencentcloud.com/document/product/436/7778).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://www.tencentcloud.com/document/product/1045/49896).


#### Request headers

This API only uses [Common Request Headers](https://www.tencentcloud.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>VideoTargetRec</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
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
| ------------------ | ------- | ------------------------------------------------------------ | --------- | -------- |
| Tag                | Request | Job type: `VideoTargetRec`                                   | String    | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default value). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default value) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address, which takes priority over that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |


`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | ------------------------------------------------------------ | ------ | -------- |
| Object             | Request.Input | Media filename. At least one of `Object` and `Url` must be passed in. If both parameters are passed in, `Object` is preferred. | String | No       |
| Url                | Request.Input | Media access URL. At least one of `Url` and `Object` must be passed in. If both parameters are passed in, `Object` is preferred. | String | No       |

<span id="operation"></span>
`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | -------- |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| VideoTargetRec     | Request.Operation | Video object detection parameter, which is the same as <a href="https://cloud.tencent.com/document/product/436/84736#VideoTargetRec " target="_blank">Request.VideoTargetRec</a> in the API for creating a video object detection template | Container | No       |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0` (default), `1`, `2`. | String | No |

>!At least one of `TemplateId` and `VideoTargetRec` must be passed in. `TemplateId` is used first. If `TemplateId` is unavailable, `VideoTargetRec` is used.

## Response

#### Response headers

This API only returns [Common Response Headers](https://www.tencentcloud.com/document/product/1045/43610).

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
        <Tag>VideoTargetRec</Tag>
        <Operation>
            <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
            <TemplateName>video_target_rec_demo</TemplateName>
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
| JobsDetail | Response | Job details |  Container |

<span id="jobsDetail"></span>
`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag                | Response.JobsDetail | Job type: `VideoTargetRec`                               | String    |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime          | Response.JobsDetail | Job start time                                               | String    |
| EndTime          | Response.JobsDetail | Job end time                                               | String    |
| QueueId            | Response.JobsDetail | ID of the queue where the job is in                                             | String    |
| Operation          | Response.JobsDetail | Task rule                           | Container |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------- | :---------------------------- | :------------------------------------------ | :-------- |
| TemplateId         | Response.JobsDetail.Operation | Job template ID                     | String    |
| TemplateName         | Response.JobsDetail.Operation | Job template name, which is returned when `TemplateId` exists    | String    |
| VideoTargetRec | Response.JobsDetail.Operation | Same as `Request.Operation.VideoTargetRec` in the request |  Container |
| VideoTargetRecResult     | Response.JobsDetail.Operation | Video object detection result |  Container |
| UserData           | Response.JobsDetail.Operation | The user information passed through                      | String |
| JobLevel    | Response.JobsDetail.Operation | Job priority                                                         | String |

`VideoTargetRecResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :------------------------------------------------- | ------------ | ------------- |
| BodyRecognition    | Response.JobsDetail.Operation.VideoTargetRecResult | Human body detection result | Container array |
| PetRecognition     | Response.JobsDetail.Operation.VideoTargetRecResult | Pet detection result | Container array |
| CarRecognition     | Response.JobsDetail.Operation.VideoTargetRecResult | Vehicle detection result | Container array |

`BodyRecognition` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :----------------------------------------------------------- | ------------------------ | ------------- |
| Time               | Response.JobsDetail.Operation.VideoTargetRecResult.BodyRecognition | Screenshot time point in seconds   | String        |
| Url                | Response.JobsDetail.Operation.VideoTargetRecResult.BodyRecognition | Screenshot URL                  | String        |
| BodyInfo           | Response.JobsDetail.Operation.VideoTargetRecResult.BodyRecognition | Human body detection result. Multiple human bodies may be detected. | Container array |

`PetRecognition` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :----------------------------------------------------------- | ---------------------------- | ------------- |
| Time               | Response.JobsDetail.Operation.VideoTargetRecResult.PetRecognition | Screenshot time point in seconds   | String        |
| Url                | Response.JobsDetail.Operation.VideoTargetRecResult.PetRecognition | Screenshot URL                  | String        |
| PetInfo            | Response.JobsDetail.Operation.VideoTargetRecResult.PetRecognition | Pet detection result. Multiple pets may be detected. | Container array |

`CarRecognition` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :----------------------------------------------------------- | ------------------------ | ------------- |
| Time               | Response.JobsDetail.Operation.VideoTargetRecResult.CarRecognition | Screenshot time point in seconds   | String        |
| Url                | Response.JobsDetail.Operation.VideoTargetRecResult.CarRecognition | Screenshot URL                  | String        |
| CarInfo            | Response.JobsDetail.Operation.VideoTargetRecResult.CarRecognition | Vehicle detection result. Multiple vehicles may be detected. | Container array |

`BodyInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :----------------------------------------------------------- | ------------------------------------------------- | --------- |
| Name               | Response.JobsDetail.Operation.VideoTargetRecResult.BodyRecognition.BodyInfo | Detection type                                          | String    |
| Score              | Response.JobsDetail.Operation.VideoTargetRecResult.BodyRecognition.BodyInfo | Confidence level of the detected object. Value range: [0-100]. The higher the score, the more likely the image contains the target object. | Int       |
| Location           | Response.JobsDetail.Operation.VideoTargetRecResult.BodyRecognition.BodyInfo | Coordinates of the human body detected in the image                              | Container |

`Location` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :----------------------------------------------------------- | ----------------- | ------ |
| X                  | Response.JobsDetail.Operation.VideoTargetRecResult.BodyRecognition.BodyInfo.Location | X coordinate              | String |
| Y                  | Response.JobsDetail.Operation.VideoTargetRecResult.BodyRecognition.BodyInfo.Location | Y coordinate             | String |
| Height             | Response.JobsDetail.Operation.VideoTargetRecResult.BodyRecognition.BodyInfo.Location | Height  | String |
| Width              | Response.JobsDetail.Operation.VideoTargetRecResult.BodyRecognition.BodyInfo.Location | Width | String |

`PetInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :----------------------------------------------------------- | ------------------------------------------------- | --------- |
| Name               | Response.JobsDetail.Operation.VideoTargetRecResult.PetRecognition.PetInfo | Detection type                                          | String    |
| Score              | Response.JobsDetail.Operation.VideoTargetRecResult.PetRecognition.PetInfo | Confidence level of the detected object. Value range: [0-100]. The higher the score, the more likely the image contains the target object. | Int       |
| Location           | Response.JobsDetail.Operation.VideoTargetRecResult.PetRecognition.PetInfo | Coordinates of the pet detected in the image                              | Container |

`Location` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :----------------------------------------------------------- | ----------------- | ------ |
| X                  | Response.JobsDetail.Operation.VideoTargetRecResult.PetRecognition.PetInfo.Location | X coordinate              | String |
| Y                  | Response.JobsDetail.Operation.VideoTargetRecResult.PetRecognition.PetInfo.Location | Y coordinate             | String |
| Height             | Response.JobsDetail.Operation.VideoTargetRecResult.PetRecognition.PetInfo.Location | Height  | String |
| Width              | Response.JobsDetail.Operation.VideoTargetRecResult.PetRecognition.PetInfo.Location | Width | String |

`CarInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :----------------------------------------------------------- | ------------------------------------------------- | --------- |
| Name               | Response.JobsDetail.Operation.VideoTargetRecResult.CarRecognition.CarInfo | Detection type                                          | String    |
| Score              | Response.JobsDetail.Operation.VideoTargetRecResult.CarRecognition.CarInfo | Confidence level of the detected object. Value range: [0-100]. The higher the score, the more likely the image contains the target object. | Int       |
| Location           | Response.JobsDetail.Operation.VideoTargetRecResult.CarRecognition.CarInfo | Coordinates of the vehicle detected in the image                              | Container |

`Location` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | :----------------------------------------------------------- | ----------------- | ------ |
| X                  | Response.JobsDetail.Operation.VideoTargetRecResult.CarRecognition.CarInfo.Location | X coordinate              | String |
| Y                  | Response.JobsDetail.Operation.VideoTargetRecResult.CarRecognition.CarInfo.Location | Y coordinate             | String |
| Height             | Response.JobsDetail.Operation.VideoTargetRecResult.CarRecognition.CarInfo.Location | Height  | String |
| Width              | Response.JobsDetail.Operation.VideoTargetRecResult.CarRecognition.CarInfo.Location | Width | String |

#### Error codes

No special error message will be returned for this request. For the common error messages, see [Error Codes](https://www.tencentcloud.com/document/product/1045/33700).

## Examples

#### Request 1: Using a video object detection template ID

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>VideoTargetRec</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

#### Response 1

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
        <Tag>VideoTargetRec</Tag>
        <Operation>      
            <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
            <TemplateName>video_target_rec_demo</TemplateName>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```

#### Request 2: Using the video object detection parameter

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>VideoTargetRec</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <VideoTargetRec>
            <Body>true</Body>
            <Car>true</Car>
            <Pet>true</Pet>
        </VideoTargetRec>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

#### Response 2

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
        <Tag>VideoTargetRec</Tag>
        <Operation>
            <VideoTargetRec>
                <Body>true</Body>
                <Car>true</Car>
                <Pet>true</Pet>
            </VideoTargetRec>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```

