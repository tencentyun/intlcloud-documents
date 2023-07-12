## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-07-01T10:05:48+0800</CreationTime>
        <EndTime>2022-07-01T10:06:02+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j535b10a4f8e211ec9452c1c27f56a659</JobId>
        <Message>Success</Message>
        <Operation>
            <UserData>This is my VideoTag job.</UserData>
            <VideoTag>
                <Scenario>Stream</Scenario>
            </VideoTag>
            <VideoTagResult>
                <StreamData>
                    <Data>
                        <ActionTags>
                            <EndTime>11</EndTime>
                            <StartTime>0</StartTime>
                            <Tags>
                                <Confidence>0.421531</Confidence>
                                <Tag>Speak</Tag>
                                <TagCls>Speak</TagCls>
                            </Tags>
                        </ActionTags>
                        <ActionTags>
                            <EndTime>12.88</EndTime>
                            <StartTime>11.04</StartTime>
                            <Tags/>
                        </ActionTags>
                        <ObjectTags>
                            <Objects>
                                <BBox>
                                    <X1>0.10181817412376404</X1>
                                    <X2>0.8069194555282593</X2>
                                    <Y1>0.6880248785018921</Y1>
                                    <Y2>0.8779844045639038</Y2>
                                </BBox>
                                <Confidence>0.808393</Confidence>
                                <Name>Keyboard</Name>
                            </Objects>
                            <TimeStamp>11</TimeStamp>
                        </ObjectTags>
                        <PersonTags/>
                        <PlaceTags>
                            <ClipFrameResult>Office: 0.55</ClipFrameResult>
                            <ClipFrameResult>Office: 0.55</ClipFrameResult>
                            <ClipFrameResult>Office: 0.59</ClipFrameResult>
                            <ClipFrameResult>Office: 0.54</ClipFrameResult>
                            <ClipFrameResult>Office: 0.42</ClipFrameResult>
                            <ClipFrameResult>Office: 0.43</ClipFrameResult>
                            <ClipFrameResult>Office: 0.33</ClipFrameResult>
                            <ClipFrameResult>Office: 0.29</ClipFrameResult>
                            <ClipFrameResult>Office: 0.15</ClipFrameResult>
                            <ClipFrameResult>Entertainment venue: 0.42</ClipFrameResult>
                            <ClipFrameResult>Office: 0.33</ClipFrameResult>
                            <EndIndex>275</EndIndex>
                            <EndTime>11</EndTime>
                            <StartIndex>0</StartIndex>
                            <StartTime>0</StartTime>
                            <Tags>
                                <Confidence>0.591724</Confidence>
                                <Tag>Office</Tag>
                                <TagCls>Work</TagCls>
                            </Tags>
                            <Tags>
                                <Confidence>0.175342</Confidence>
                                <Tag>Supermarket/Convenience store/Store</Tag>
                                <TagCls>Business</TagCls>
                            </Tags>
                        </PlaceTags>
                        <PlaceTags>
                            <ClipFrameResult>Other: 0.09</ClipFrameResult>
                            <ClipFrameResult>Other: 0.21</ClipFrameResult>
                            <ClipFrameResult>Other: 0.19</ClipFrameResult>
                            <ClipFrameResult>Sky: 0.28</ClipFrameResult>
                            <ClipFrameResult>Sky: 0.25</ClipFrameResult>
                            <ClipFrameResult>Other: 0.30</ClipFrameResult>
                            <ClipFrameResult>Other: 0.28</ClipFrameResult>
                            <ClipFrameResult>Other: 0.49</ClipFrameResult>
                            <ClipFrameResult>Other: 0.56</ClipFrameResult>
                            <ClipFrameResult>Other: 0.58</ClipFrameResult>
                            <EndIndex>322</EndIndex>
                            <EndTime>12.88</EndTime>
                            <StartIndex>276</StartIndex>
                            <StartTime>11.04</StartTime>
                            <Tags>
                                <Confidence>0.581444</Confidence>
                                <Tag>Other</Tag>
                                <TagCls>Other</TagCls>
                            </Tags>
                            <Tags>
                                <Confidence>0.283301</Confidence>
                                <Tag>Sky</Tag>
                                <TagCls>Nature/Outdoor</TagCls>
                            </Tags>
                        </PlaceTags>
                        <Tags>
                            <Confidence>0.355083</Confidence>
                            <Tag>MOBA - Arena of Valor</Tag>
                        </Tags>
                        <Tags>
                            <Confidence>0.587103</Confidence>
                            <Tag>Game</Tag>
                        </Tags>
                        <Tags>
                            <Confidence>0.544651</Confidence>
                            <Tag>Office</Tag>
                        </Tags>
                        <Tags>
                            <Confidence>0.182886</Confidence>
                            <Tag>Supermarket/Convenience store/Store</Tag>
                        </Tags>
                    </Data>
                    <SubErrCode>0</SubErrCode>
                    <SubErrMsg>ok</SubErrMsg>
                </StreamData>
            </VideoTagResult>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-07-01T10:05:50+0800</StartTime>
        <State>Success</State>
        <Tag>VideoTag</Tag>
        <VideoTag/>
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
| EventName          | Response | Fixed value: `TaskFinish`.    | String |
| JobsDetail | Response | Job details |  Container |

`JobsDetail` has the following sub-nodes:
<a href="https://intl.cloud.tencent.com/document/product/1045/48945" target="_blank">Same as `Response.JobsDetail` in the video tagging job submitting API.</a>

**If the job is triggered by a workflow, `Response.JobsDetail.Input` will also contain a `CosHeaders` node of the container array type.**

`CosHeaders` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------- | :------------------ | :----- |
| Key                | Response.JobsDetail.Input.CosHeaders | Name of the custom header  | String |
| Value              | Response.JobsDetail.Input.CosHeaders | Value of the custom header | String |

**If the job is triggered by a workflow, `Response.JobsDetail` will also contain a `Workflow` node of the container type.**

`Workflow` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ----------------------------------------- | -------------------------------------- | ------ |
| RunId              | Response.Workflow | Workflow instance ID                    | String |
| WorkflowId         | Response.Workflow | Workflow ID                       | String |
| WorkflowName       | Response.Workflow | Workflow name                      | String |
| Name               | Response.Workflow | Workflow node name                   | String |

## Samples

### Sample 1: Job callback triggered by a job API

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-07-01T10:05:48+0800</CreationTime>
        <EndTime>2022-07-01T10:06:02+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j535b10a4f8e211ec9452c1c27f56a659</JobId>
        <Message>Success</Message>
        <Operation>
            <UserData>This is my VideoTag job.</UserData>
            <VideoTag>
                <Scenario>Stream</Scenario>
            </VideoTag>
            <VideoTagResult>
                <StreamData>
                    <Data>
                        <ActionTags>
                            <EndTime>11</EndTime>
                            <StartTime>0</StartTime>
                            <Tags>
                                <Confidence>0.421531</Confidence>
                                <Tag>Speak</Tag>
                                <TagCls>Speak</TagCls>
                            </Tags>
                        </ActionTags>
                        <ActionTags>
                            <EndTime>12.88</EndTime>
                            <StartTime>11.04</StartTime>
                            <Tags/>
                        </ActionTags>
                        <ObjectTags>
                            <Objects>
                                <BBox>
                                    <X1>0.10181817412376404</X1>
                                    <X2>0.8069194555282593</X2>
                                    <Y1>0.6880248785018921</Y1>
                                    <Y2>0.8779844045639038</Y2>
                                </BBox>
                                <Confidence>0.808393</Confidence>
                                <Name>Keyboard</Name>
                            </Objects>
                            <TimeStamp>11</TimeStamp>
                        </ObjectTags>
                        <PersonTags/>
                        <PlaceTags>
                            <ClipFrameResult>Office: 0.55</ClipFrameResult>
                            <ClipFrameResult>Office: 0.55</ClipFrameResult>
                            <ClipFrameResult>Office: 0.59</ClipFrameResult>
                            <ClipFrameResult>Office: 0.54</ClipFrameResult>
                            <ClipFrameResult>Office: 0.42</ClipFrameResult>
                            <ClipFrameResult>Office: 0.43</ClipFrameResult>
                            <ClipFrameResult>Office: 0.33</ClipFrameResult>
                            <ClipFrameResult>Office: 0.29</ClipFrameResult>
                            <ClipFrameResult>Office: 0.15</ClipFrameResult>
                            <ClipFrameResult>Entertainment venue: 0.42</ClipFrameResult>
                            <ClipFrameResult>Office: 0.33</ClipFrameResult>
                            <EndIndex>275</EndIndex>
                            <EndTime>11</EndTime>
                            <StartIndex>0</StartIndex>
                            <StartTime>0</StartTime>
                            <Tags>
                                <Confidence>0.591724</Confidence>
                                <Tag>Office</Tag>
                                <TagCls>Work</TagCls>
                            </Tags>
                            <Tags>
                                <Confidence>0.175342</Confidence>
                                <Tag>Supermarket/Convenience store/Store</Tag>
                                <TagCls>Business</TagCls>
                            </Tags>
                        </PlaceTags>
                        <PlaceTags>
                            <ClipFrameResult>Other: 0.09</ClipFrameResult>
                            <ClipFrameResult>Other: 0.21</ClipFrameResult>
                            <ClipFrameResult>Other: 0.19</ClipFrameResult>
                            <ClipFrameResult>Sky: 0.28</ClipFrameResult>
                            <ClipFrameResult>Sky: 0.25</ClipFrameResult>
                            <ClipFrameResult>Other: 0.30</ClipFrameResult>
                            <ClipFrameResult>Other: 0.28</ClipFrameResult>
                            <ClipFrameResult>Other: 0.49</ClipFrameResult>
                            <ClipFrameResult>Other: 0.56</ClipFrameResult>
                            <ClipFrameResult>Other: 0.58</ClipFrameResult>
                            <EndIndex>322</EndIndex>
                            <EndTime>12.88</EndTime>
                            <StartIndex>276</StartIndex>
                            <StartTime>11.04</StartTime>
                            <Tags>
                                <Confidence>0.581444</Confidence>
                                <Tag>Other</Tag>
                                <TagCls>Other</TagCls>
                            </Tags>
                            <Tags>
                                <Confidence>0.283301</Confidence>
                                <Tag>Sky</Tag>
                                <TagCls>Nature/Outdoor</TagCls>
                            </Tags>
                        </PlaceTags>
                        <Tags>
                            <Confidence>0.355083</Confidence>
                            <Tag>MOBA - Arena of Valor</Tag>
                        </Tags>
                        <Tags>
                            <Confidence>0.587103</Confidence>
                            <Tag>Game</Tag>
                        </Tags>
                        <Tags>
                            <Confidence>0.544651</Confidence>
                            <Tag>Office</Tag>
                        </Tags>
                        <Tags>
                            <Confidence>0.182886</Confidence>
                            <Tag>Supermarket/Convenience store/Store</Tag>
                        </Tags>
                    </Data>
                    <SubErrCode>0</SubErrCode>
                    <SubErrMsg>ok</SubErrMsg>
                </StreamData>
            </VideoTagResult>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-07-01T10:05:50+0800</StartTime>
        <State>Success</State>
        <Tag>VideoTag</Tag>
        <VideoTag/>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback in JSON format triggered by a job API

```plaintext
{
    "EventName": "TaskFinish",
    "JobsDetail": {
        "Code": "Success",
        "CreationTime": "2022-07-01T10:05:48+0800",
        "EndTime": "2022-07-01T10:06:02+0800",
        "Input": {
            "BucketId": "test-123456789",
            "Object": "input/demo.mp4",
            "Region": "ap-chongqing"
        },
        "JobId": "j535b10a4f8e211ec9452c1c27f56a659",
        "Message": "Success",
        "Operation": {
            "UserData": "This is my VideoTag job.",
            "VideoTag": {
                "Scenario": "Stream"
            },
            "VideoTagResult": {
                "StreamData": {
                    "Data": {
                        "ActionTags": [{
                                "EndTime": "11",
                                "StartTime": "0",
                                "Tags": {
                                    "Confidence": "0.421531",
                                    "Tag": "Speak",
                                    "TagCls": "Speak"
                                }
                            },
                            {
                                "EndTime": "12.88",
                                "StartTime": "11.04"
                            }
                        ],
                        "ObjectTags": {
                            "Objects": {
                                "BBox": {
                                    "X1": "0.10181817412376404",
                                    "X2": "0.8069194555282593",
                                    "Y1": "0.6880248785018921",
                                    "Y2": "0.8779844045639038"
                                },
                                "Confidence": "0.808393",
                                "Name": "Keyboard"
                            },
                            "TimeStamp": "11"
                        },
                        "PlaceTags": [{
                                "ClipFrameResult": [
                                    "Office: 0.55",
                                    "Office: 0.55",
                                    "Office: 0.59",
                                    "Office: 0.54",
                                    "Office: 0.42",
                                    "Office: 0.43",
                                    "Office: 0.33",
                                    "Office: 0.29",
                                    "Office: 0.15",
                                    "Entertainment venue: 0.42",
                                    "Office: 0.33"
                                ],
                                "EndIndex": "275",
                                "EndTime": "11",
                                "StartIndex": "0",
                                "StartTime": "0",
                                "Tags": [{
                                        "Confidence": "0.591724",
                                        "Tag": "Office",
                                        "TagCls": "Work"
                                    },
                                    {
                                        "Confidence": "0.175342",
                                        "Tag": "Supermarket/Convenience store/Store",
                                        "TagCls": "Business"
                                    }
                                ]
                            },
                            {
                                "ClipFrameResult": [
                                    "Other: 0.09",
                                    "Other: 0.21",
                                    "Other: 0.19",
                                    "Sky: 0.28",
                                    "Sky: 0.25",
                                    "Other: 0.30",
                                    "Other: 0.28",
                                    "Other: 0.49",
                                    "Other: 0.56",
                                    "Other: 0.58"
                                ],
                                "EndIndex": "322",
                                "EndTime": "12.88",
                                "StartIndex": "276",
                                "StartTime": "11.04",
                                "Tags": [{
                                        "Confidence": "0.581444",
                                        "Tag": "Other",
                                        "TagCls": "Other"
                                    },
                                    {
                                        "Confidence": "0.283301",
                                        "Tag": "Sky",
                                        "TagCls": "Nature/Outdoor"
                                    }
                                ]
                            }
                        ],
                        "Tags": [{
                                "Confidence": "0.355083",
                                "Tag": "MOBA - Arena of Valor"
                            },
                            {
                                "Confidence": "0.587103",
                                "Tag": "Game"
                            },
                            {
                                "Confidence": "0.544651",
                                "Tag": "Office"
                            },
                            {
                                "Confidence": "0.182886",
                                "Tag": "Supermarket/Convenience store/Store"
                            }
                        ]
                    },
                    "SubErrCode": "0",
                    "SubErrMsg": "ok"
                }
            }
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-07-01T10:05:50+0800",
        "State": "Success",
        "Tag": "VideoTag"
    }
}
```
