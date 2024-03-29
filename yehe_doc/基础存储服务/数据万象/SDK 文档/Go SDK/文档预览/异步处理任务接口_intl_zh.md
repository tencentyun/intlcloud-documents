
## 简介

本文档提供关于文档预览任务接口的 API 概览以及 SDK 示例代码。

| API                 | 操作名        | 操作描述            |
| ------------------- | -------------- | --------------------- |
|  CreateDocProcessJobs   | 提交文档预览任务 | 用于提交一个文档预览任务        |
|DescribeDocProcessJob  | 查询指定的文档预览任务 | 用于查询指定的文档预览任务 |
| DescribeDocProcessJobs| 拉取符合条件的文档预览任务 | 用于拉取符合条件的文档预览任务             |


## 提交文档预览任务

#### 功能说明

CreateDocProcessJobs 接口用于提交一个文档预览任务。

#### 方法原型
```go
func (s *CIService) CreateDocProcessJobs(ctx context.Context, opt *CreateDocProcessJobsOptions) (*CreateDocProcessJobsResult, *Response, error)
```

#### 请求示例
```go
createJobOpt := &cos.CreateDocProcessJobsOptions{
	Tag: "DocProcess",
	Input: &cos.DocProcessJobInput{
		Object: "form.pdf",
	},
	Operation: &cos.DocProcessJobOperation{
		Output: &cos.DocProcessJobOutput{
			Region: "ap-guangzhou",
			Object: "test-doc${Number}",
			Bucket: "examplebucket-1250000000",
		},
		DocProcess: &cos.DocProcessJobDocProcess{
			TgtType:     "png",
			StartPage:   1,
			EndPage:     -1,
			ImageParams: "watermark/1/image/aHR0cDovL3Rlc3QwMDUtMTI1MTcwNDcwOC5jb3MuYXAtY2hvbmdxaW5nLm15cWNsb3VkLmNvbS8xLmpwZw==/gravity/southeast",
		},
	},
	QueueId: "p111a8dd208104ce3b11c78398f658ca8",
}
res, _, err := c.CI.CreateDocProcessJobs(context.Background(), createJobOpt)
```

#### 参数说明

```go
type CreateDocProcessJobsOptions struct {
    XMLName   xml.Name
    Tag       string
    Input     *DocProcessJobInput
    Operation *DocProcessJobOperation
    QueueId   string
}
type DocProcessJobInput struct {
    Object string
}
type DocProcessJobOperation struct {
    Output           *DocProcessJobOutput
    DocProcess       *DocProcessJobDocProcess
    DocProcessResult *DocProcessJobDocProcessResult
}
type DocProcessJobOutput struct {
    Region string
    Bucket string
    Object string
}
type DocProcessJobDocProcess struct {
    SrcType        string
    TgtType        string
    SheetId        int
    StartPage      int
    EndPage        int
    ImageParams    string
    DocPassword    string
    Comments       int
    PaperDirection int
    Quality        int
    Zoom           int
}
```

| 参数名称  | 描述                                   | 类型      |
| --------- | -------------------------------------- | --------- |
| Tag       | 创建任务的 Tag，目前仅支持：DocProcess | String    |
| Input     | 待操作的文件对象                       | Container |
| Operation | 操作规则                               | Container |
| QueueId   | 任务所在的队列 ID                      | String    |
| Object    | 文件在 COS 上的文件路径，Bucket 由 Host 指定 | String    |
| Output     | 结果输出地址                                  | Container |
| DocProcess | 当 Tag 为 DocProcess 时有效，指定该任务的参数 | Container |
| Region   | 存储桶的地域                                                 | String |
| Bucket   | 存储结果的存储桶                                             | String |
| Object   | 输出文件路径。 **非表格文件输出文件名需包含${Number}或${Page}参数。**多个输出文件，${Number} 表示序号从1开始，${Page}表示序号与预览页码一致。${Number} 表示多个输出文件，序号从1开始，例如输入 abc\_${Number}.jpg，预览某文件5-6页，则输出文件名为 abc\_1.jpg，abc\_2.jpg${Page}表示多个输出文件，序号与预览页码一致，例如输入 abc\_${Page}.jpg，预览某文件5-6页，则输出文件名为 abc\_5.jpg，abc\_6.jpg。**表格文件输出路径需包含${SheetID}占位符，输出文件名必须包含${Number}参数。**例如 /${SheetID}/ abc\_${Number}.jpg，先根据 excel 转换的表格数，生成对应数量的文件夹，再在对应的文件夹下，生成对应数量的图片文件 | String |
| SrcType        | 源数据的后缀类型。当前文档转换根据 COS 对象的后缀名来确定源数据类型，当 COS 对象没有后缀名时，可以设置该值 | String |
| TgtType        | 转换输出目标文件类型，png 表示转换成 png 格式的图片文件；jpg 表示转换成 jpg 格式的图片文件；pdf 表示转换成 pdf 格式的图片文件。如果传入的格式未能识别，默认使用 jpg 格式 | String |
| SheetId        | 表格文件参数，转换第 x 个表，默认为1；设置 SheetId 为0，即转换文档中全部表格 | Int    |
| StartPage      | 从第 x 页开始转换；在表格文件中，一张表可能分割为多页转换，生成多张图片。StartPage 表示从指定 SheetId 的第 x 页开始转换。默认为1 | Int    |
| EndPage        | 转换至第 x 页；在表格文件中，一张表可能分割为多页转换，生成多张图片。EndPage 表示转换至指定 SheetId 的第 x 页。默认为-1，即转换全部页 | Int    |
| ImageParams    | 转换后的图片处理参数，支持 [基础图片处理](https://www.tencentcloud.com/document/product/436/36365) 所有处理参数，多个处理参数可通过 [管道操作符](https://intl.cloud.tencent.com/document/product/436/36380) 分隔，从而实现在一次访问中按顺序对图片进行不同处理 | String |
| DocPassword    | Office 文档的打开密码，如果需要转换有密码的文档，请设置该字段 | String |
| Comments       | 是否隐藏批注和应用修订，默认为 0。 0：隐藏批注，应用修订；1：显示批注和修订 | Int    |
| PaperDirection | 表格文件转换纸张方向，0代表垂直方向，非0代表水平方向，默认为0 | Int    |
| Quality        | 生成预览图的图片质量，取值范围：[1-100]，默认值100。 例如：值为100，代表生成图片质量为100% | Int    |
| Zoom           | 预览图片的缩放参数，取值范围：[10-200]，默认值100。 例如：值为200，代表图片缩放比例为200% 即放大两倍 | Int    |

#### 返回结果说明

```go
type CreateDocProcessJobsResult struct {
    JobsDetail DocProcessJobDetail
}
type DocProcessJobDetail struct { 
    Code         string
    Message      string
    JobId        string
    Tag          string
    State        string
    CreationTime string
    QueueId      string
    Input        *DocProcessJobInput
    Operation    *DocProcessJobOperation
}
```

| 参数名称   | 描述           | 类型      |
| ---------- | -------------- | --------- |
| JobsDetail | 任务的详细信息 | Container |
| Code         | 错误码，只有 State 为 Failed 时有意义                        | String |
| Message      | 错误描述，只有 State 为 Failed 时有意义                      | String |
| JobId        | 新创建任务的 ID                                              | String |
| Tag          | 新创建任务的 Tag：DocProcess                                 | String |
| State        | 任务的状态，为 Submitted、Running、Success、Failed、Pause、Cancel 其中一个 | String |
| CreationTime | 任务的创建时间                                               | String |
| QueueId      | 任务所属的队列 ID                                            | String |
| Input        | 该任务的输入文件路径，详情请参见CreateDocProcessJobsOptions.Input | Container |
| Operation    | 该任务的规则，详情请参见CreateDocProcessJobsOptions.Operation | Container |



## 查询指定文档预览任务

#### 功能说明

DescribeDocProcessJob 用于查询指定的文档预览任务。

#### 方法原型
```go
func (s *CIService) DescribeDocProcessJob(ctx context.Context, jobid string) (*DescribeDocProcessJobResult, *Response, error)
```

#### 请求示例

```go
jobid := "<jobid>"
res, _, err := c.CI.DescribeDocProcessJob(context.Background(), jobid)
```

#### 参数说明
| 参数名称 | 描述           | 类型   |
| -------- | -------------- | ------ |
| jobid    | 文档预览任务 ID | String |

#### 返回结果说明

```go
type DescribeDocProcessJobResult struct {
    JobsDetail     *DocProcessJobDetail 
    NonExistJobIds string
}
```

| 参数名称       | 描述                                                         | 类型      |
| -------------- | ------------------------------------------------------------ | --------- |
| JobsDetail     | 任务的详细信息， 同 CreateDocProcessJobs 接口的 Response.JobsDetail 节点 | Container |
| NonExistJobIds | 查询的 ID 中不存在的任务，所有任务都存在时不返回             | String    |


## 拉取符合条件的文档预览任务 

#### 功能说明

DescribeDocProcessJobs 用于拉取符合条件的文档预览任务。

#### 方法原型
```go
func (s *CIService) DescribeDocProcessJobs(ctx context.Context, opt *DescribeDocProcessJobsOptions) (*DescribeDocProcessJobsResult, *Response, error)
```

#### 请求示例
```go
DescribeJobsOpt := &cos.DescribeDocProcessJobsOptions{
	QueueId: "p111a8dd208104ce3b11c78398f658ca8",
	Tag:     "DocProcess",
}
res, _, err := c.CI.DescribeDocProcessJobs(context.Background(), DescribeJobsOpt)
```

#### 参数说明

```go
type DescribeDocProcessJobsOptions struct {
    QueueId           string
    Tag               string
    OrderByTime       string
    NextToken         string
    Size              int
    States            string
    StartCreationTime string
    EndCreationTime   string
}
```

| 参数名称          | 描述                                                         | 类型   |
| ----------------- | ------------------------------------------------------------ | ------ |
| QueueId           | 拉取该队列 ID 下的任务                                     | String |
| Tag               | 任务的 Tag：DocProcess                                     | String |
| OrderByTime       | Desc 或者 Asc。默认为 Desc                                 | String |
| NextToken         | 请求的上下文，用于翻页。上次返回的值                       | String |
| Size              | 拉取的最大任务数。默认为10，最大值为100                      | Int    |
| States            | 拉取该状态的任务，以`,`分割，支持多状态：All、Submitted、Running、Success、Failed、Pause、Cancel。默认为 All | String |
| StartCreationTime | 拉取创建时间大于该时间的任务。格式为：`%Y-%m-%dT%H:%m:%S%z`  | String |
| EndCreationTime   | 拉取创建时间小于该时间的任务。格式为：`%Y-%m-%dT%H:%m:%S%z`  | String |


#### 返回结果说明

```go
type DescribeDocProcessJobsResult struct {
    JobsDetail []DocProcessJobDetail
    NextToken  string
}
```

| 参数名称   | 描述                                                         | 类型      |
| ---------- | ------------------------------------------------------------ | --------- |
| JobsDetail | 任务的详细信息，同 CreateDocProcessJobs 接口中的 Response.JobsDetail 节点 | Container |
| NextToken  | 翻页的上下文 Token                                           | String    |
