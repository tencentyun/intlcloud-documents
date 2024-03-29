

## 简介
本文档提供关于文档预览队列接口的 API 概览以及 SDK 示例代码。

| API            | 操作名       | 操作描述     |
| --------------- | ------------ | -------- |
| DescribeDocProcessQueues  |     查询文档预览队列     | 查询文档预览队列信息 |
| UpdateDocProcessQueue    |   更新文档预览队列       | 更新文档预览队列信息 |


## 查询文档预览队列

#### 功能说明

DescribeDocProcessQueues 接口用于查询文档预览队列。

#### 方法原型
```go
func (s *CIService) DescribeDocProcessQueues(ctx context.Context, opt *DescribeDocProcessQueuesOptions) (*DescribeDocProcessQueuesResult, *Response, error)
```

#### 请求示例
```go
DescribeQueueOpt := &cos.DescribeDocProcessQueuesOptions{
	QueueIds: "p111a8dd208104ce3b11c78398f658ca8,p4318f85d2aa14c43b1dba6f9b78be9b3,aacb2bb066e9c4478834d4196e76c49d3",
	PageNumber: 1,
	PageSize:   2,
}
res, _, err := c.CI.DescribeDocProcessQueues(context.Background(), DescribeQueueOpt)
```

#### 参数说明

```go
type DescribeDocProcessQueuesOptions struct {
    QueueIds   string `url:"queueIds,omitempty"`
    State      string `url:"state,omitempty"`
    PageNumber int    `url:"pageNumber,omitempty"`
    PageSize   int    `url:"pageSize,omitempty"`
}
```

| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| QueueIds | 队列 ID，以“,”符号分割字符串 | String             |
| State | 1. Active 表示队列内的作业会被文档预览服务调度执行 2. Paused 表示队列暂停，作业不再会被文档预览服务调度执行，队列内的所有作业状态维持在暂停状态，已经处于执行中的任务将继续执行，不受影响 | String      |
| PageNumber | 第几页 | int |
| PageSize | 每页个数 | int |

#### 返回结果说明

```go
type DescribeDocProcessQueuesResult struct {
    XMLName      xml.Name          
    RequestId    string            
    TotalCount   int
    PageNumber   int
    PageSize     int
    QueueList    []DocProcessQueue 
    NonExistPIDs []string
}
type DocProcessQueue struct { 
    QueueId       string
    Name          string
    State         string
    MaxSize       int
    MaxConcurrent int
    UpdateTime    string
    CreateTime    string
    NotifyConfig  *DocProcessQueueNotifyConfig
}
type DocProcessQueueNotifyConfig struct { 
    Url   string
    State string
    Type  string
    Event string
}
```

| 参数名称     | 描述                            | 类型       |
| :----------- | :------------------------------ | :--------- |
| RequestId    | 请求的唯一 ID                   | String     |
| TotalCount   | 队列总数                        | Int        |
| PageNumber   | 当前页数，同请求中的 pageNumber | Int        |
| PageSize     | 每页个数，同请求中的 pageSize   | Int        |
| QueueList    | 队列数组                        | Container  |
| NonExistPIDs | 不存在的队列 ID 列表            | String 数组 |
| QueueId       | 队列 ID                      | String    |
| Name          | 队列名字                     | String    |
| State         | 当前状态，Active 或者 Paused | String    |
| NotifyConfig  | 回调配置                     | Container |
| MaxSize       | 队列最大长度                 | Int       |
| MaxConcurrent | 当前队列最大并行执行的任务数 | Int       |
| UpdateTime    | 更新时间                     | String    |
| CreateTime    | 创建时间                     | String    |
| Url      | 回调地址              | String |
| State    | 开关状态，On 或者 Off | String |
| Type     | 回调类型，Url         | String |
| Event    | 触发回调的事件        | String |


## 更新文档预览队列

#### 功能说明

UpdateDocProcessQueue 接口用于更新文档预览队列。

#### 方法原型

```go
func (s *CIService) UpdateDocProcessQueue(ctx context.Context, opt *UpdateDocProcessQueueOptions) (*UpdateDocProcessQueueResult, *Response, error)
```

#### 请求示例
```go
updateQueueOpt := &cos.UpdateDocProcessQueueOptions{
	Name:    "queue-doc-process-1",
	QueueID: "p111a8dd208104ce3b11c78398f658ca8",
	State:   "Active",
	NotifyConfig: &cos.DocProcessQueueNotifyConfig{
		State: "Off",
	},
}
res, _, err := c.CI.UpdateDocProcessQueue(context.Background(), updateQueueOpt)
```
#### 参数说明

```go
type UpdateDocProcessQueueOptions struct {
    XMLName      xml.Name
    Name         string
    QueueID      string
    State        string
    NotifyConfig *DocProcessQueueNotifyConfig
}
```

| 参数名称| 描述  | 类型  |
| ----| ---- | ---- |
| Name | 队列名称 | String             |
| QueueID | 队列 ID | String      |
| State | 队列状态 | String |
| NotifyConfig | 通知渠道，详情请参见 DocProcessQueue.NotifyConfig | Container |

#### 返回结果说明

```go
type UpdateDocProcessQueueResult struct {
    XMLName   xml.Name
    RequestId string
    Queue     *DocProcessQueue
}
```

| 参数名称  | 描述                                                         | 类型   |
| --------- | ------------------------------------------------------------ | ------ |
| RequestId | 请求的唯一 ID                                                | Struct |
| Queue     | 队列信息，详情请参见 DescribeDocProcessQueuesResult.QueueList | Struct |



