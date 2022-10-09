## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-07-18T15:16:43+0800</CreationTime>
        <EndTime>2022-07-18T15:16:44+0800</EndTime>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/deer.jpg</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>c93984788066911ed89ed352d4d9d2084</JobId>
        <Message/>
        <Operation>
            <Output>
                <Bucket>test-1234567890</Bucket>
                <Object>output/out.jpg</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <PicProcessResult>
                <ObjectName>output/out.jpg</ObjectName>
                <OriginalInfo>
                    <Etag>"d5a491cd3d8d071e3212c3478e8e35a1"</Etag>
                    <ImageInfo>
                        <Ave>0xc64847</Ave>
                        <Format>JPEG</Format>
                        <Height>417</Height>
                        <Orientation>0</Orientation>
                        <Quality>68</Quality>
                        <Width>500</Width>
                    </ImageInfo>
                </OriginalInfo>
                <ProcessResult>
                    <Etag/>
                    <Format>JPEG</Format>
                    <Height>500</Height>
                    <Quality>68</Quality>
                    <Size>24911</Size>
                    <Width>417</Width>
                </ProcessResult>
            </PicProcessResult>
            <TemplateId>t10461fe2bd5a649db9022452ec71e0381</TemplateId>
            <TemplateName>test</TemplateName>
            <UserData>This is my PicProcess job.</UserData>
        </Operation>
        <QueueId>p2911917386e148639319e13c285cc774</QueueId>
        <StartTime>2022-07-18T15:16:44+0800</StartTime>
        <State>Success</State>
        <Tag>PicProcess</Tag>
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
<a href="https://intl.cloud.tencent.com/document/product/1045/49947#jobsDetail" target="_blank">Same as `Response.JobsDetail` in the image processing job submitting API</a>

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
        <CreationTime>2022-07-18T15:16:43+0800</CreationTime>
        <EndTime>2022-07-18T15:16:44+0800</EndTime>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/deer.jpg</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>c93984788066911ed89ed352d4d9d2084</JobId>
        <Message/>
        <Operation>
            <Output>
                <Bucket>test-1234567890</Bucket>
                <Object>output/out.jpg</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <PicProcessResult>
                <ObjectName>output/out.jpg</ObjectName>
                <OriginalInfo>
                    <Etag>"d5a491cd3d8d071e3212c3478e8e35a1"</Etag>
                    <ImageInfo>
                        <Ave>0xc64847</Ave>
                        <Format>JPEG</Format>
                        <Height>417</Height>
                        <Orientation>0</Orientation>
                        <Quality>68</Quality>
                        <Width>500</Width>
                    </ImageInfo>
                </OriginalInfo>
                <ProcessResult>
                    <Etag/>
                    <Format>JPEG</Format>
                    <Height>500</Height>
                    <Quality>68</Quality>
                    <Size>24911</Size>
                    <Width>417</Width>
                </ProcessResult>
            </PicProcessResult>
            <TemplateId>t10461fe2bd5a649db9022452ec71e0381</TemplateId>
            <TemplateName>test</TemplateName>
            <UserData>This is my PicProcess job.</UserData>
        </Operation>
        <QueueId>p2911917386e148639319e13c285cc774</QueueId>
        <StartTime>2022-07-18T15:16:44+0800</StartTime>
        <State>Success</State>
        <Tag>PicProcess</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback triggered by a workflow

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-07-18T15:16:43+0800</CreationTime>
        <EndTime>2022-07-18T15:16:44+0800</EndTime>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/deer.jpg</Object>
            <Region>ap-chongqing</Region>
            <CosHeaders>
                <Key>Content-Type</Key>
                <Value>image/jpeg</Value>
            </CosHeaders>
            <CosHeaders>
                <Key>x-cos-request-id</Key>
                <Value>NjJiZDYwYTFfNjUzYTYyNjRfZjEwZl8xMmZhYzY5</Value>
            </CosHeaders>
            <CosHeaders>
                <Key>EventName</Key>
                <Value>cos:ObjectCreated:Put</Value>
            </CosHeaders>
            <CosHeaders>
                <Key>Size</Key>
                <Value>1024</Value>
            </CosHeaders>
        </Input>
        <JobId>c93984788066911ed89ed352d4d9d2084</JobId>
        <Message/>
        <Operation>
            <Output>
                <Bucket>test-1234567890</Bucket>
                <Object>output/out.jpg</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <PicProcessResult>
                <ObjectName>output/out.jpg</ObjectName>
                <OriginalInfo>
                    <Etag>"d5a491cd3d8d071e3212c3478e8e35a1"</Etag>
                    <ImageInfo>
                        <Ave>0xc64847</Ave>
                        <Format>JPEG</Format>
                        <Height>417</Height>
                        <Orientation>0</Orientation>
                        <Quality>68</Quality>
                        <Width>500</Width>
                    </ImageInfo>
                </OriginalInfo>
                <ProcessResult>
                    <Etag/>
                    <Format>JPEG</Format>
                    <Height>500</Height>
                    <Quality>68</Quality>
                    <Size>24911</Size>
                    <Width>417</Width>
                </ProcessResult>
            </PicProcessResult>
            <TemplateId>t10461fe2bd5a649db9022452ec71e0381</TemplateId>
            <TemplateName>test</TemplateName>
            <UserData>This is my PicProcess job.</UserData>
        </Operation>
        <QueueId>p2911917386e148639319e13c285cc774</QueueId>
        <StartTime>2022-07-18T15:16:44+0800</StartTime>
        <State>Success</State>
        <Tag>PicProcess</Tag>
        <Workflow>
            <Name>PicProcess_1581665960537</Name>
            <RunId>ic90edd59f84f11ec9d4f525400a3c59f</RunId>
            <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
            <WorkflowName>workflow-test</WorkflowName>
        </Workflow>
    </JobsDetail>
</Response>
```

### Sample 3: Job callback in JSON format triggered by a workflow

```plaintext
{
	"EventName": "TaskFinish",
	"JobsDetail": {
		"Code": "Success",
		"CreationTime": "2022-07-18T15:16:43+0800",
		"EndTime": "2022-07-18T15:16:44+0800",
		"Input": {
			"BucketId": "test-1234567890",
			"Object": "input/deer.jpg",
			"Region": "ap-chongqing",
			"CosHeaders": [{
					"Key": "Content-Type",
					"Value": "image/jpeg"
				},
				{
					"Key": "x-cos-request-id",
					"Value": "NjJiZDYwYTFfNjUzYTYyNjRfZjEwZl8xMmZhYzY5"
				},
				{
					"Key": "EventName",
					"Value": "cos:ObjectCreated:Put"
				},
				{
					"Key": "Size",
					"Value": "1024"
				}
			]
		},
		"JobId": "c93984788066911ed89ed352d4d9d2084",
		"Operation": {
			"Output": {
				"Bucket": "test-1234567890",
				"Object": "output/out.jpg",
				"Region": "ap-chongqing"
			},
			"PicProcessResult": {
				"ObjectName": "output/out.jpg",
				"OriginalInfo": {
					"Etag": "\"d5a491cd3d8d071e3212c3478e8e35a1\"",
					"ImageInfo": {
						"Ave": "0xc64847",
						"Format": "JPEG",
						"Height": "417",
						"Orientation": "0",
						"Quality": "68",
						"Width": "500"
					}
				},
				"ProcessResult": {
					"Format": "JPEG",
					"Height": "500",
					"Quality": "68",
					"Size": "24911",
					"Width": "417"
				}
			},
			"TemplateId": "t10461fe2bd5a649db9022452ec71e0381",
			"TemplateName": "test",
			"UserData": "This is my PicProcess job."
		},
		"QueueId": "p2911917386e148639319e13c285cc774",
		"StartTime": "2022-07-18T15:16:44+0800",
		"State": "Success",
		"Tag": "PicProcess",
		"Workflow": {
			"Name": "PicProcess_1581665960537",
			"RunId": "ic90edd59f84f11ec9d4f525400a3c59f",
			"WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
			"WorkflowName": "workflow-test"
		}
	}
}
```
