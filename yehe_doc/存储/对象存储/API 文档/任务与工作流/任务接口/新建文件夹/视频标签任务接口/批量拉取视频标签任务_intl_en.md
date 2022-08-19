## Feature Description

The API (`DescribeMediaJobs`) is used to pull jobs that meet specified conditions.

## Request

#### Sample request

```shell
GET /jobs?size=&states=&queueId=&startCreationTime=&endCreationTime= HTTP/1.1
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

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:-- |:--|:--|:--|
| queueId | None | ID of the queue from which jobs are pulled | String | Yes |
| tag | None | Job type: VideoTag | String | Yes |
| orderByTime | None | `Desc` (default) or `Asc` | String | No |
| nextToken | None | Context token for pagination | String | No |
| size | None | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100. | Integer | No |
| States | None | Status of the jobs to pull. If you enter multiple job statuses, separate them with commas (,). Valid values: All (default), Submitted, Running, Success, Failed, Pause, Cancel | String | No |
| startCreationTime | None | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`. | String | No |
| endCreationTime | None | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | String | No |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <JobsDetail>
  </JobsDetail>
  <NextToken></NextToken>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| JobsDetail | Response | Job details. Same as `Response.JobsDetail` in `DescibeMediaJob`. |  Container |
| NextToken             | Response | Context token for pagination | String    |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Samples

#### Request

```shell
GET /jobs?queueId=aaaaaaaaaaa&tag=VideoTag HTTP/1.1
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
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=

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


