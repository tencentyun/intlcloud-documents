## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-07-25T16:35:39+0800</CreationTime>
        <EndTime>2022-07-25T16:35:43+0800</EndTime>
        <Input>
            <Object>text.txt</Object>
            <BucketId>test-123456789</BucketId>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>ac34be3aa0bf411ed9ce39d7cc972e427</JobId>
        <Message>Success</Message>
        <Operation>
            <JobLevel>0</JobLevel>
            <WordsGeneralize>
                <NerMethod>DL</NerMethod>
                <SegMethod>MIX</SegMethod>
            </WordsGeneralize>
            <WordsGeneralizeResult>
                <WordsGeneralizeLable>
                    <Category>Mobility</Category>
                    <Word>Taxi</Word>
                </WordsGeneralizeLable>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>0</Offset>
                    <Pos>t</Pos>
                    <Word>Today</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>2</Offset>
                    <Pos>v</Pos>
                    <Word>Taxi</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>1</Length>
                    <Offset>4</Offset>
                    <Pos>v</Pos>
                    <Word>Cost</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>5</Offset>
                    <Pos>nx</Pos>
                    <Word>60</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>1</Length>
                    <Offset>7</Offset>
                    <Pos>q</Pos>
                    <Word>CNY</Word>
                </WordsGeneralizeToken>
            </WordsGeneralizeResult>
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
| EventName          | Response | Fixed value: `TaskFinish`.    | String |
| JobsDetail | Response | Job details |  Container |

`JobsDetail` has the following sub-nodes:
<a href="https://intl.cloud.tencent.com/document/product/1045/49790#jobsDetail" target="_blank">Same as `Response.JobsDetail` in the word segmentation job submitting API.</a>

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
        <CreationTime>2022-07-25T16:35:39+0800</CreationTime>
        <EndTime>2022-07-25T16:35:43+0800</EndTime>
        <Input>
            <Object>text.txt</Object>
            <BucketId>test-123456789</BucketId>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>ac34be3aa0bf411ed9ce39d7cc972e427</JobId>
        <Message>Success</Message>
        <Operation>
            <JobLevel>0</JobLevel>
            <WordsGeneralize>
                <NerMethod>DL</NerMethod>
                <SegMethod>MIX</SegMethod>
            </WordsGeneralize>
            <WordsGeneralizeResult>
                <WordsGeneralizeLable>
                    <Category>Mobility</Category>
                    <Word>Taxi</Word>
                </WordsGeneralizeLable>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>0</Offset>
                    <Pos>t</Pos>
                    <Word>Today</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>2</Offset>
                    <Pos>v</Pos>
                    <Word>Taxi</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>1</Length>
                    <Offset>4</Offset>
                    <Pos>v</Pos>
                    <Word>Cost</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>2</Length>
                    <Offset>5</Offset>
                    <Pos>nx</Pos>
                    <Word>60</Word>
                </WordsGeneralizeToken>
                <WordsGeneralizeToken>
                    <Length>1</Length>
                    <Offset>7</Offset>
                    <Pos>q</Pos>
                    <Word>CNY</Word>
                </WordsGeneralizeToken>
            </WordsGeneralizeResult>
        </Operation>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback in JSON format triggered by a job API

```plaintext
{
	"Response": {
		"EventName": "TaskFinish",
		"JobsDetail": {
			"Code": "Success",
			"CreationTime": "2022-07-25T16:35:39+0800",
			"EndTime": "2022-07-25T16:35:43+0800",
			"Input": {
				"Object": "text.txt",
				"BucketId": "test-123456789",
				"Region": "ap-chongqing"
			},
			"JobId": "ac34be3aa0bf411ed9ce39d7cc972e427",
			"Message": "Success",
			"Operation": {
				"JobLevel": "0",
				"WordsGeneralize": {
					"NerMethod": "DL",
					"SegMethod": "MIX"
				},
				"WordsGeneralizeResult": {
					"WordsGeneralizeLable": {
						"Category": "Mobility",
						"Word": "Taxi"
					},
					"WordsGeneralizeToken": [{
							"Length": "2",
							"Offset": "0",
							"Pos": "t",
							"Word": "Today"
						},
						{
							"Length": "2",
							"Offset": "2",
							"Pos": "v",
							"Word": "Taxi"
						},
						{
							"Length": "1",
							"Offset": "4",
							"Pos": "v",
							"Word": "Cost"
						},
						{
							"Length": "2",
							"Offset": "5",
							"Pos": "nx",
							"Word": "60"
						},
						{
							"Length": "1",
							"Offset": "7",
							"Pos": "q",
							"Word": "CNY"
						}
					]
				}
			}
		}
	}
}
```
