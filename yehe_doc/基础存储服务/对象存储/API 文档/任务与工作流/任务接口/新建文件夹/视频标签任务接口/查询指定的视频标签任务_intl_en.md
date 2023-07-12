## Feature Description

This API (`DescribeMediaJob`) is used to query a specified job.

## Request

#### Sample request

```shell
GET /jobs/<jobId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request does not have a request body.


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <JobsDetail>
  </JobsDetail>
  <NonExistJobIds></NonExistJobIds>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| JobsDetail | Response | Job details. Same as `Response.JobsDetail` in `CreateMediaJobs`. |  Container |
| NonExistJobIds | Response | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| VideoTag | Response.JobsDetail.Operation | Same as `Request.Operation.VideoTag` in `CreateMediaJobs`. |  Container |
| VideoTagResult | Response.JobSDetail.Operation | Returned video tagging job result details when the job type is `VideoTag` and the status is `success`. | Container |

`VideoTagResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| StreamData | Response.JobsDetail.Operation.VideoTagResult | Result of the video tagging job in the `Stream` scenario | Container |

`StreamData` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Data | Response.JobsDetail.Operation.VideoTagResult.StreamData | Result list of the video tagging job in the `Stream` scenario | Container |
| SubErrCode | Response.JobsDetail.Operation.VideoTagResult.StreamData | Algorithm status code. 0: success; other values: exception. | Container |
| SubErrMsg | Response.JobsDetail.Operation.VideoTagResult.StreamData | Algorithm error message. `ok` indicates a success. If the request fails, the corresponding error is returned. | Container |

`Data` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Tags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data | Video tag and video category information |  Container |
| PersonTags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data | Person tag information |  Container |
| PlaceTags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data | Scene tag information |  Container |
| ActionTags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data | Action tag information |  Container |
| ObjectTags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data | Object tag information |  Container |

`Tags` (video tag) has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Tag | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags | Tag name |  String |
| TagCls | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags | Tag category |  String |
| Confidence | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags | Tag model prediction score. Value range: [0, 1]. |  Float |

`Tags` (video category) has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Tag | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags | Video category |  String |
| Confidence | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags | Tag model prediction score. Value range: [0, 1]. |  Float |

`PersonTags` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Name | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags | Person name |  String |
| Confidence | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags | Tag model prediction score |  Float |
| Count | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags | Number of person appearances | String |
| DetailPerSecond | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags | Location and time of person appearance | Container |

`DetailPerSecond` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| TimeStamp | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond | Appearance time in seconds |  String |
| Confidence | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond | Tag model prediction score |  Float |
| BBox | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond | Relative coordinates of the object with top-left corner as the origin | Container |

`BBox` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| X1 | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond.BBox | Relative position of coordinate X1 |  String |
| Y1 | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond.BBox | Relative position of coordinate Y1 |  String |
| X2 | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond.BBox | Relative position of coordinate X2 |  String |
| Y2 | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond.BBox | Relative position of coordinate Y2 |  String |

`PlaceTags` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Tags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Video scene tag information, which may not be returned and is the same as `Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags`. |  Container |
| StartTime | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Segment start time in seconds |  String |
| EndTime | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Segment end time in seconds |  String |
| StartIndex | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Segment start frame number |  String |
| EndIndex | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Segment end frame number |  String |
| ClipFrameResult | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PlaceTags | Top 1 single frame recognition result |  String |

`ActionTags` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Tags | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ActionTags | Video action tag information, which may not be returned and is the same as `Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags`. |  Container |
| StartTime | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ActionTags | Segment start time in seconds |  String |
| EndTime | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ActionTags | Segment end time in seconds |  String |

`ObjectTags` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Objects | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ObjectTags | Video object tag information, which may not be returned and is the same as `Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.Tags`. |  Container |
| TimeStamp | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ObjectTags | Timestamp of the identified object in seconds |  String |


`Object` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Name | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ObjectTags.Objects | Object name |  Container |
| Confidence | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ObjectTags.Objects | Tag model prediction score. Value range: [0, 1]. |  Float |
| BBox | Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.ObjectTags.Objects | Relative coordinates of the object with top-left corner as the origin, which is the same as `Response.JobsDetail.Operation.VideoTagResult.StreamData.Data.PersonTags.DetailPerSecond.BBox`. |  Container |








#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
GET /jobs/jabcxxxxfeipplsdfwe HTTP/1.1
Accept: */*
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>jabcxxxxfeipplsdfwe</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>VideoTag<Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
      <VideoTag>
        <Scenario>Stream</Scenario>
      </VideoTag>
      <VideoTagResult>
        <StreamData>
          <Data>
            <Tags>
              <Confidence>0.939035</Confidence>
              <Tag>Natural scenery</Tag>
              <TagCls>Life</TagCls>
            </Tags>
            <Tags>
              <Confidence>0.884062</Confidence>
              <Tag>Snow mountain</Tag>
              <TagCls>Travel</TagCls>
            </Tags>
            <Tags>
              <Confidence>0.345798</Confidence>
              <Tag>Cloud</Tag>
              <TagCls>Travel</TagCls>
            </Tags>
            <Tags>
              <Confidence>0.997328</Confidence>
              <Tag>Natural scenery</Tag>
            </Tags>
            <Tags>
              <Confidence>0.997595</Confidence>
              <Tag>Travel</Tag>
            </Tags>
            <PersonTags>
              <Name>Cecilia Han</Name>
              <Confidence>0.985561</Confidence>
              <Count>3</Count>
              <DetailPerSecond>
                <TimeStamp>1</TimeStamp>
                <Confidence>0.8411815762519836</Confidence>
                <BBox>
                  <X1>0.29050925925925924</X1>
                  <Y1>0.257201646090535</Y1>
                  <X2>0.4652777777777778</X2>
                  <Y2>0.6584362139917695</Y2>
                </BBox>
              </DetailPerSecond>
              <DetailPerSecond>
                <TimeStamp>2</TimeStamp>
                <Confidence>0.9262690246105194</Confidence>
                <BBox>
                  <X1>0.3472222222222222</X1>
                  <Y1>0.03497942386831276</Y1>
                  <X2>0.6412037037037037</X2>
                  <Y2>0.7181069958847737</Y2>
                </BBox>
              </DetailPerSecond>
              <DetailPerSecond>
                <TimeStamp>3</TimeStamp>
                <Confidence>0.8933985382318497</Confidence>
                <BBox>
                  <X1>0.3576388888888889</X1>
                  <Y1>0.03497942386831276</Y1>
                  <X2>0.6631944444444444</X2>
                  <Y2>0.7366255144032922</Y2>
                </BBox>
              </DetailPerSecond>
            </PersonTags>
            <PersonTags>
              <Name>Gulnazar</Name>
              <Confidence>0.9010105729103088</Confidence>
              <Count>2</Count>
              <DetailPerSecond>
                <TimeStamp>18</TimeStamp>
                <Confidence>0.8933985382318497</Confidence>
                <BBox>
                  <X1>0.5567129629629629</X1>
                  <Y1>0.13991769547325103</Y1>
                  <X2>0.8078703703703703</X2>
                  <Y2>0.7469135802469136</Y2>
                </BBox>
              </DetailPerSecond>
              <DetailPerSecond>
                <TimeStamp>19</TimeStamp>
                <Confidence>0.8933985382318497</Confidence>
                <BBox>
                  <X1>0.5335648148148148</X1>
                  <Y1>0.21193415637860083</Y1>
                  <X2>0.7800925925925926</X2>
                  <Y2>0.8045267489711934</Y2>
                </BBox>
              </DetailPerSecond>              
            </PersonTags>
            <PlaceTags>
              <Tags>
                <Tag>Forest</Tag>
                <TagCls>Nature/Outdoor</TagCls>
                <Confidence>0.516961</Confidence>
              </Tags>
              <Tags>
                <Tag>Field/Park/Garden</Tag>
                <TagCls>Nature/Outdoor</TagCls>
                <Confidence>0.230019</Confidence>
              </Tags>
              <StartTime>0.0</StartTime>
              <EndTime>68.6</EndTime>
              <StartIndex>0</StartIndex>
              <EndIndex>1715</EndIndex>
              <ClipFrameResult>Forest: 0.37</ClipFrameResult>
              <ClipFrameResult>Forest: 0.22</ClipFrameResult>
              <ClipFrameResult>Field_Park_Garden: 0.19</ClipFrameResult>
              <ClipFrameResult>Orchard: 0.14</ClipFrameResult>
            </PlaceTags>
            <PlaceTags>
              <StartTime>68.64</StartTime>
              <EndTime>72.4</EndTime>
              <StartIndex>1716</StartIndex>
              <EndIndex>1810</EndIndex>
              <ClipFrameResult>Closeup: 0.23</ClipFrameResult>
              <ClipFrameResult>Glacier_Iceberg: 0.04</ClipFrameResult>
              <ClipFrameResult>Closeup: 0.06</ClipFrameResult>
              <ClipFrameResult>Closeup: 0.09</ClipFrameResult>
            </PlaceTags>
            <ActionTags>
              <StartTime>5.8</StartTime>
              <EndTime>8.56</EndTime>
              <Tags>
                <Tag>Speak</Tag>
                <TagCls>Speak</TagCls>
                <Confidence>0.90646</Confidence>
              </Tags>
              <Tags>
                <Tag>Toast</Tag>
                <TagCls>Toast</TagCls>
                <Confidence>0.91610</Confidence>
              </Tags>
            </ActionTags>
            <ObjectTags>
              <TimeStamp>62.0</TimeStamp>
              <Objects>
                <Name>Cake</Name>
                <Confidence>0.638210</Confidence>
                <BBox>
                  <X1>0.21793489158153534</X1>
                  <Y1>0.5634896159172058</Y1>
                  <X2>0.6121288537979126</X2>
                  <Y2>1.0</Y2>
                </BBox>
              </Objects>
              <Objects>
                <Name>Table</Name>
                <Confidence>0.67762</Confidence>
                <BBox>
                  <X1>0.06269711256027222</X1>
                  <Y1>0.6098541021347046</Y1>
                  <X2>0.9128285646438599</X2>
                  <Y2>0.9146066904067993</Y2>
                </BBox>
              </Objects>
            </ObjectTags>
          </Data>
          <SubErrCode>0</SubErrCode>
          <SubErrMsg>ok</SubErrMsg>
        </StreamData>
      </VideoTagResult>
    </Operation>
  </JobsDetail>
</Response>
```


