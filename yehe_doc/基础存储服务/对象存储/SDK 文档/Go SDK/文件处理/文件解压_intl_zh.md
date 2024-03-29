
## 简介

本文档提供关于数据万象文件解压的 API 概览以及 SDK 示例代码。

| API                 | 操作描述            |
| ------------------- | ------------------------ |
| [提交文件解压任务](https://intl.cloud.tencent.com/document/product/436/53993)   | 以提交任务的方式进行文件解压任务        |
| [查询文件解压结果](https://intl.cloud.tencent.com/document/product/436/53994)  | 主动查询指定的文件解压任务结果 |



## 提交文件解压任务

#### 功能说明

以提交任务的方式进行文件解压缩，异步返回压缩包内被解压出来的文件。

#### 方法原型
```go
func (s *CIService) CreateFileProcessJob(ctx context.Context, opt *FileProcessJobOptions) (*FileProcessJobResult, *Response, error)
```

#### 请求示例
```go
createJobOpt := &cos.FileProcessJobOptions{
	Tag: "FileUncompress",
	Input: &cos.FileProcessInput{
		Object: "294028.zip",
	},
	Operation: &cos.FileProcessJobOperation{
		FileUncompressConfig: &cos.FileUncompressConfig{
            Prefix:         "uncomp",
            PrefixReplaced: "1",
		},
		Output: &cos.FileProcessOutput{
			Region: "ap-beijing",
			Bucket: "test-1250000000",
		}
	},
	QueueId: "p111a8dd208104ce3b11c78398f658ca8",
}
res, _, err := c.CI.CreateFileProcessJob(context.Background(), createJobOpt)
```

#### 参数说明

```go
type FileProcessJobOptions struct {
	XMLName          xml.Name
	Tag              string
	Input            *FileProcessInput
	Operation        *FileProcessJobOperation
	QueueId          string
	CallBackFormat   string
	CallBackType     string
	CallBack         string
	CallBackMqConfig *NotifyConfigCallBackMqConfig
}
type FileProcessInput struct {
	Region string
	Bucket string
	Object string
}
type FileProcessJobOperation struct {
	FileHashCodeConfig   *FileHashCodeConfig
	FileHashCodeResult   *FileHashCodeResult
	FileUncompressConfig *FileUncompressConfig
	FileUncompressResult *FileUncompressResult
	FileCompressConfig   *FileCompressConfig
	FileCompressResult   *FileCompressResult
	Output               *FileProcessOutput
	UserData             string
}
type FileHashCodeConfig struct {
	Type        string
	AddToHeader bool
}
type FileHashCodeResult struct {
	MD5          string
	SHA1         string
	SHA256       string
	FileSize     int
	LastModified string
	Etag         string
}
type FileUncompressConfig struct {
	Prefix         string
	PrefixReplaced string
}
type FileUncompressResult struct {
	Region    string
	Bucket    string
	FileCount string
}
type FileCompressConfig struct {
	Flatten string
	Format  string
	UrlList string
	Prefix  string
	Key     string
}
type FileCompressResult struct {
	Region string
	Bucket string
	Object string
}
type FileProcessOutput struct {
	Region string
	Bucket string
	Object string
}
type NotifyConfigCallBackMqConfig struct {
	MqMode   string
	MqRegion string
	MqName   string
}
```

| 参数名称  | 描述                                   | 类型      | 是否必选 |
| --------- | -------------------------------------- | --------- | --------- |
| Tag       | 创建任务的 Tag，目前仅支持：FileUncompress | String    | 是         |
| Input     | 待操作的文件对象。详情见 [Input](https://www.tencentcloud.com/document/product/436/53993) | Container | 是         |
| Operation | 操作规则                               | Container | 是         |
| Operation.FileUncompressConfig | 指定文件解压的处理规则。详情见 [FileUncompressConfig](https://intl.cloud.tencent.com/document/product/436/53993) | Container | 是         |
| Operation.FileUncompressResult | 文件解压的结果，任务未完成时不返回。详情见 [FileUncompressResult](https://intl.cloud.tencent.com/document/product/436/53993) | Container | 否         |
| Operation.Output | 指定文件处理后的文件保存的地址信息。详情见 [Output](https://intl.cloud.tencent.com/document/product/436/53995) | Container | 是         |
| Operation.UserData | 透传用户信息, 可打印的 ASCII 码, 长度不超过1024                               | String | 否         |
| QueueId   | 任务所在的队列 ID                      | String    | 是         |
| CallBackFormat | 任务回调格式，JSON 或 XML，默认 XML，优先级高于队列的回调格式。 | String    | 否         |
| CallBackType | 任务回调类型，Url 或 TDMQ，默认 Url，优先级高于队列的回调类型。 | String    | 否         |
| CallBack   | 任务回调的地址，优先级高于队列的回调地址。 | String    | 否         |
| CallBackMqConfig | 任务回调 TDMQ 配置，当 CallBackType 为 TDMQ 时必填。详情见 [CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945) | Container | 否         |

#### 返回结果说明

```go
type FileProcessJobResult struct {
    JobsDetail FileProcessJobResult
}
type FileProcessJobResult struct {
    Code         string
    Message      string
    JobId        string
    Tag          string
    State        string
    CreationTime string
	StartTime    string
	EndTime      string
    QueueId      string
    Input        *FileProcessInput
    Operation    *FileProcessJobOperation
}
```

| 参数名称   | 描述           | 类型      |
| ---------- | -------------- | --------- |
| JobsDetail | 任务的详细信息 | Container |
| Code         | 错误码，只有 State 为 Failed 时有意义                        | String |
| Message      | 错误描述，只有 State 为 Failed 时有意义                      | String |
| JobId        | 新创建任务的 ID                                              | String |
| Tag          | 新创建任务的 Tag：FileUncompress | String |
| State        | 任务的状态，为 Submitted、Running、Success、Failed、Pause、Cancel 其中一个 | String |
| CreationTime | 任务的创建时间                                               | String |
| StartTime    | 任务的开始时间                                               | String |
| EndTime      | 任务的结束时间                                               | String |
| QueueId      | 任务所属的队列 ID                                            | String |
| Input        | 该任务的输入文件路径，详情请参见 FileProcessJobOptions.Input | Container |
| Operation    | 该任务的规则，详情请参见 FileProcessJobOptions.Operation | Container |



## 查询文件解压结果

#### 功能说明

查询一个文件处理任务,根据任务 ID 查询任务详情。

#### 方法原型
```go
func (s *CIService) DescribeFileProcessJob(ctx context.Context, jobid string) (*FileProcessJobResult, *Response, error)
```

#### 请求示例

```go
jobid := "<jobid>"
res, _, err := c.CI.DescribeFileProcessJob(context.Background(), jobid)
```

#### 参数说明
| 参数名称 | 描述           | 类型   | 是否必选 |
| -------- | -------------- | ------ | --------- |
| jobid    | 文件处理任务 ID | String | 是         |

#### 返回结果说明

```go
type FileProcessJobResult struct {
	JobsDetail *FileProcessJobsDetail
}
```

| 参数名称       | 描述                                                         | 类型      |
| -------------- | ------------------------------------------------------------ | --------- |
| JobsDetail     | 任务的详细信息， 同 CreateFileProcessJob 接口的 Response.JobsDetail 节点 | Container |

