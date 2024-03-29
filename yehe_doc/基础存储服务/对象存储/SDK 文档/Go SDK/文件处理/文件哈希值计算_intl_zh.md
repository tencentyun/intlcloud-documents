
## 简介

本文档提供关于数据万象文件哈希值计算的 API 概览以及 SDK 示例代码。

| API                 | 操作描述            |
| ------------------- | -------------------- |
| [哈希值计算同步请求](https://intl.cloud.tencent.com/document/product/436/53990)   | 以同步请求的方式进行文件哈希值计算，实时返回计算得到的哈希值   |
| [提交哈希值计算任务](https://intl.cloud.tencent.com/document/product/436/53991)   | 以提交任务的方式进行文件哈希值计算任务        |
| [查询哈希值计算结果](https://intl.cloud.tencent.com/document/product/436/53992)  | 主动查询指定的文件哈希值计算任务结果 |



## 哈希值计算同步请求

#### 功能说明

以同步请求的方式进行文件哈希值计算，返回得到的哈希值。

#### 方法原型
```go
func (s *CIService) GetFileHash(ctx context.Context, name string, opt *GetFileHashOptions) (*GetFileHashResult, *Response, error)
```

#### 请求示例
```go
opt := &cos.GetFileHashOptions{
    CIProcess: "filehash",
    Type:      "md5",
}
res, _, err := c.CI.GetFileHash(context.Background(), "test.jpg", opt)
```

#### 参数说明

```go
type GetFileHashOptions struct {
	CIProcess   string
	Type        string
	AddToHeader bool
}
```

| 参数名称  | 描述                                   | 类型      | 是否必选 |
| --------- | -------------------------------------- | --------- | --------- |
| name        | 执行操作的文件全路径                                            | String    | 是         |
| CIProcess   | 操作类型，哈希值计算固定为：filehash                         | String | 是         |
| Type        | 支持的哈希算法类型，有效值：md5、sha1、sha256                               | String | 是         |
| AddToHeader | 是否将计算得到的哈希值，自动添加至文件的自定义header，格式为：x-cos-meta-md5/sha1/sha256; 有效值： true、false，不填则默认为false。 | Bool | 否         |

#### 返回结果说明

```go
type GetFileHashResult struct {
	FileHashCodeResult *FileHashCodeResult
	Input              *FileProcessInput
}
```

| 参数名称   | 描述           | 类型      |
| ---------- | -------------- | --------- |
| FileHashCodeResult | 文件哈希值的结果。详情请参见 FileProcessJobOptions.Input | Container |
| Input              | 输入文件的基本信息。详情请参见 FileProcessJobOptions.Operation.FileHashCodeResult | Container |



## 提交哈希值计算任务

#### 功能说明

以提交任务的方式进行文件哈希值计算，异步返回计算得到的哈希值。

#### 方法原型
```go
func (s *CIService) CreateFileProcessJob(ctx context.Context, opt *FileProcessJobOptions) (*FileProcessJobResult, *Response, error)
```

#### 请求示例
```go
createJobOpt := &cos.FileProcessJobOptions{
	Tag: "FileHashCode",
	Input: &cos.FileProcessInput{
		Object: "294028.zip",
	},
	Operation: &cos.FileProcessJobOperation{
		FileHashCodeConfig: &cos.FileHashCodeConfig{
            Type:        "sha1",
            AddToHeader: true,
		},
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
| Tag       | 创建任务的 Tag，目前仅支持：FileHashCode | String    | 是         |
| Input     | 待操作的文件对象。详情见 [Input](https://intl.cloud.tencent.com/document/product/436/53991) | Container | 是         |
| Operation | 操作规则                               | Container | 是         |
| Operation.FileHashCodeConfig | 指定哈希值计算的处理规则。详情见 [FileHashCodeConfig](https://intl.cloud.tencent.com/document/product/436/53991) | Container | 是         |
| Operation.FileHashCodeResult | 计算得到的文件 hash 值信息，任务未完成时不返回。详情见 [FileHashCodeResult](https://intl.cloud.tencent.com/document/product/436/53991) | Container | 否         |
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
| Tag          | 新创建任务的 Tag：FileHashCode | String |
| State        | 任务的状态，为 Submitted、Running、Success、Failed、Pause、Cancel 其中一个 | String |
| CreationTime | 任务的创建时间                                               | String |
| StartTime    | 任务的开始时间                                               | String |
| EndTime      | 任务的结束时间                                               | String |
| QueueId      | 任务所属的队列 ID                                            | String |
| Input        | 该任务的输入文件路径，详情请参见 FileProcessJobOptions.Input | Container |
| Operation    | 该任务的规则，详情请参见 FileProcessJobOptions.Operation | Container |



## 查询哈希值计算结果

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
| 参数名称 | 描述           | 类型   |
| -------- | -------------- | ------ |
| jobid    | 文件处理任务 ID | String |

#### 返回结果说明

```go
type FileProcessJobResult struct {
	JobsDetail *FileProcessJobsDetail
}
```

| 参数名称       | 描述                                                         | 类型      | 是否必选 |
| -------------- | ------------------------------------------------------------ | --------- | --------- |
| JobsDetail     | 任务的详细信息， 同 CreateFileProcessJob 接口的 Response.JobsDetail 节点 | Container | 是         |
