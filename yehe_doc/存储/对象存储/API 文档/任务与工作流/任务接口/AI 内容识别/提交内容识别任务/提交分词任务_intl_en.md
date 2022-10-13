## Feature Description

This API is used to submit a word segmentation job.

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
POST /ai_jobs HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/49351).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>WordsGeneralize</Tag>
    <Input>
        <Object>text.txt</Object>
    </Input>
    <Operation>
        <WordsGeneralize>
            <NerMethod>DL</NerMethod>
            <SegMethod>Mix</SegMethod>
        </WordsGeneralize>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None     | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Job tag: WordsGeneralize                                   | String    | Yes   |
| Input              | Request | Information of the object to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Job callback address, which has a higher priority than that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default value). It has a higher priority than that of the queue. | String | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | --------------- | ------ | ---- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| WordsGeneralize     | Request.Operation | Word segmentation parameter                                             | Container | Yes   |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0`, `1`, `2`. Default value: `0`. | String | No |

`WordsGeneralize` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | :------------------------ | -------------------------------------- | --------- | ---- |---- |
| NerMethod          | Request.Operation.WordsGeneralize | NER method. Default value: `DL`. | String | No   |  `NerBasic` or `DL`  |
| SegMethod          | Request.Operation.WordsGeneralize | Word segmentation granularity. Default value: `MIX`. | String | No  |   `SegBasic` or `MIX` |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>ac7c990a00bf211ed946af9e0691f2b7a</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T14:44:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
        <Tag>WordsGeneralize</Tag>
        <Input>
            <Object>text.txt</Object>
        </Input>
        <Operation>
            <WordsGeneralize>
                <NerMethod>DL</NerMethod>
                <SegMethod>Mix</SegMethod>
            </WordsGeneralize>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

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
| Tag | Response.JobsDetail | Job tag: WordsGeneralize | String |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | ID of the queue which the job is in                       | String    |
| Input              | Response.JobsDetail | Same as the `Request.Input` node in the request                              | Container |
| Operation          | Response.JobsDetail | Operation rule                           | Container |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------ | :---------------------------- | :----------------------------------------------------------- | :-------- |
| WordsGeneralize | Response.JobsDetail.Operation | Same as `Request.Operation.WordsGeneralize` in the request                   | Container |
| UserData           | Response.JobsDetail.Operation | The user information passed through                      | String |
| JobLevel    | Response.JobsDetail.Operation | Job priority                                                         | String |
| WordsGeneralizeResult  | Response.JobsDetail.Operation | Word segmentation result, which will be returned if the job is executed successfully.                              | Container |

`WordsGeneralizeResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------ | :---------------------------- | :----------------------------------------------------------- | :-------- |
| WordsGeneralizeLable | Response.JobsDetail.Operation.WordsGeneralizeResult | Smart categorization result | Container array |
| WordsGeneralizeToken | Response.JobsDetail.Operation.WordsGeneralizeResult | Detailed word segmentation result | Container array |

`WordsGeneralizeLable` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------ | :---------------------------- | :----------------------------------------------------------- | :-------- |
| Category | Response.JobsDetail.Operation.WordsGeneralizeResult.WordsGeneralizeLable | Category | string |
| Word     | Response.JobsDetail.Operation.WordsGeneralizeResult.WordsGeneralizeLable | Word | string |

`WordsGeneralizeToken` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------ | :---------------------------- | :----------------------------------------------------------- | :-------- |
| Word   | Response.JobsDetail.Operation.WordsGeneralizeResult.WordsGeneralizeToken | Word | string |
| Offset | Response.JobsDetail.Operation.WordsGeneralizeResult.WordsGeneralizeToken | Offset | string |
| Length | Response.JobsDetail.Operation.WordsGeneralizeResult.WordsGeneralizeToken | Word length | string |
| Pos    | Response.JobsDetail.Operation.WordsGeneralizeResult.WordsGeneralizeToken | Part of speech | string |

See the subscript for the part of speech:

| Value | Description |
| :------ | :---- |
|A| Adjective |
|AD| Adverbial adjective |
|AN| Nominal adjective |
|B| Distinguishing word |
|C| Conjunction |
|D| Adverb |
|E| Interjection |
|F| Locality word |
|G| Morpheme |
|H| Preceding component |
|I| Idiom |
|J| Abbreviation |
|K| Trailing component |
|L| Idiom |
|M| Numeral |
|N| Noun |
|NR| Person name |
|NRF| Surname |
|NRG| First name |
|NS| Place name |
|NT| Organization |
|NZ| Other proper names |
|NX| Non-Chinese string |
|O| Onomatopoeia |
|P| Preposition |
|Q| Quantifier |
|R| Pronoun |
|S| Location word |
|T| Time word |
|U| Particle |
|V| Verb |
|VD| Adverbial verb |
|VN| Nominal verb |
|W| Punctuation |
|X| Non-morpheme word |
|Y| Modal particle |
|Z| State word |
|AG| Adjective morpheme |
|BG| Distinguishing morpheme |
|DG| Adverbial morpheme |
|MG| Numeral morpheme |
|NG| Nominal morpheme |
|QG| Quantifying morpheme |
|RG| Pronominal morpheme |
|TG| Verbal morpheme |
|VG| Quantifying morpheme |
|YG| Modal morpheme |
|ZG| State morpheme |
|UNK| Unknown |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request

```shell
POST /ai_jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: test-123456789.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>WordsGeneralize</Tag>
    <Input>
        <Object>text.txt</Object>
    </Input>
    <Operation>
        <WordsGeneralize>
            <NerMethod>DL</NerMethod>
            <SegMethod>Mix</SegMethod>
        </WordsGeneralize>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
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
        <JobId>ac7c990a00bf211ed946af9e0691f2b7a</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T14:44:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
        <Tag>WordsGeneralize</Tag>
        <Input>
            <Object>text.txt</Object>
        </Input>
        <Operation>
            <WordsGeneralize>
                <NerMethod>DL</NerMethod>
                <SegMethod>Mix</SegMethod>
            </WordsGeneralize>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```
