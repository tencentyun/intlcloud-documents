
## 简介

本文档提供关于文档预览任务接口的 API 概览以及 SDK 示例代码。

| API                 | 操作名        | 操作描述            |
| ------------------- | -------------- | --------------------- |
|  [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49407)   | 提交文档预览任务 | 用于提交一个文档预览任务        |
|  [DescribeDocProcessJob](https://intl.cloud.tencent.com/document/product/436/49408)  | 查询指定的文档预览任务 | 用于查询指定的文档预览任务 |
|  [DescribeDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49409) | 拉取符合条件的文档预览任务 | 用于拉取符合条件的文档预览任务             |


## 提交文档预览任务

#### 功能说明

ci_create_doc_job 接口用于提交一个文档预览任务。

#### 方法原型
```py
def ci_create_doc_job(self, Bucket, QueueId, InputObject, OutputBucket, OutputRegion, OutputObject, SrcType=None, TgtType=None,
                          StartPage=None, EndPage=-1, SheetId=0, PaperDirection=0, PaperSize=0, DocPassword=None, Comments=None, PageRanges=None, ImageParams=None, Quality=100, Zoom=100, ImageDpi=96, PicPagination=0, **kwargs)
```

#### 请求示例
```py
def ci_create_doc_jobs():
    # 创建文档预览异步任务
    response = client.ci_create_doc_job(
        Bucket=bucket_name,
        QueueId='p4bdf22xxxxxxxxxxxxxxxxxxxxxxxxxf1',
        InputObject='normal.pptx',
        OutputBucket=bucket_name,
        OutputRegion='ap-chongqing',
        OutputObject='/test_doc/normal/abc_${Number}.jpg',
        # DocPassword='123',
        Quality=109,
        PageRanges='1,3',
    )
    print(response)
    return response
```

#### 参数说明

| 参数名称  | 描述                                   | 类型      |
| --------- | -------------------------------------- | --------- |
| Bucket    | 对象所在存储桶                      | String    |
| QueueId   | 任务所在的队列 ID                      | String    |
| InputObject    | 待操作的文件对象                       | Container |
| OutputRegion   | 存储桶的地域                                                 | String |
| OutputBucket   | 存储结果的存储桶                                             | String |
| OutputObject   | 输出文件路径。 **非表格文件输出文件名需包含${Number}或${Page}参数。**多个输出文件，${Number} 表示序号从1开始，${Page}表示序号与预览页码一致。${Number} 表示多个输出文件，序号从1开始，例如输入 abc\_${Number}.jpg，预览某文件5-6页，则输出文件名为 abc\_1.jpg，abc\_2.jpg${Page}表示多个输出文件，序号与预览页码一致，例如输入 abc\_${Page}.jpg，预览某文件5-6页，则输出文件名为 abc\_5.jpg，abc\_6.jpg。**表格文件输出路径需包含${SheetID}占位符，输出文件名必须包含${Number}参数。**例如 /${SheetID}/ abc\_${Number}.jpg，先根据 excel 转换的表格数，生成对应数量的文件夹，再在对应的文件夹下，生成对应数量的图片文件 | String |
| SrcType        | 源数据的后缀类型。当前文档转换根据 COS 对象的后缀名来确定源数据类型，当 COS 对象没有后缀名时，可以设置该值 | String |
| TgtType        | 转换输出目标文件类型，png 表示转换成 png 格式的图片文件；jpg 表示转换成 jpg 格式的图片文件；pdf 表示转换成 pdf 格式的图片文件。如果传入的格式未能识别，默认使用 jpg 格式 | String |
| StartPage      | 从第 x 页开始转换；在表格文件中，一张表可能分割为多页转换，生成多张图片。StartPage 表示从指定 SheetId 的第 x 页开始转换。默认为1 | Int    |
| EndPage        | 转换至第 x 页；在表格文件中，一张表可能分割为多页转换，生成多张图片。EndPage 表示转换至指定 SheetId 的第 x 页。默认为-1，即转换全部页 | Int    |
| SheetId        | 表格文件参数，转换第 x 个表，默认为1；设置 SheetId 为0，即转换文档中全部表格 | Int    |
| PaperDirection | 表格文件转换纸张方向，0代表垂直方向，非0代表水平方向，默认为0 | Int    |
| PaperSize      | 设置纸张（画布）大小，对应信息为： 0 → A4 、 1 → A2 、 2 → A0 ，默认 A4 纸张 | Int    |
| DocPassword    | Office 文档的打开密码，如果需要转换有密码的文档，请设置该字段 | String |
| Comments       | 是否隐藏批注和应用修订，默认为 0。 0：隐藏批注，应用修订；1：显示批注和修订 | Int    |
| PageRanges     | 自定义需要转换的分页范围，例如： "1,2-4,7" ，则表示转换文档的 1、2、3、4、7 页面 | String    |
| ImageParams    | 转换后的图片处理参数，支持 [基础图片处理](https://www.tencentcloud.com/document/product/436/36365) 所有处理参数，多个处理参数可通过 [管道操作符](https://intl.cloud.tencent.com/document/product/436/36380) 分隔，从而实现在一次访问中按顺序对图片进行不同处理 | String |
| Quality        | 生成预览图的图片质量，取值范围：[1-100]，默认值100。 例如：值为100，代表生成图片质量为100% | Int    |
| Zoom           | 预览图片的缩放参数，取值范围：[10-200]，默认值100。 例如：值为200，代表图片缩放比例为200% 即放大两倍 | Int    |
| ImageDpi       | 按指定 dpi 渲染图片，该参数与 Zoom 共同作用，取值范围 96-600 ，默认值为 96 。转码后的图片单边宽度需小于65500像素 | Int    |
| PicPagination  | 是否转换成单张长图，设置为 1 时，最多仅支持将 20 标准页面合成单张长图，超过可能会报错，分页范围可以通过 StartPage、EndPage 控制。默认值为 0 ，按页导出图片，TgtType="png"/"jpg" 时生效 | Int    |

#### 返回结果说明

```py
{
    'JobsDetail': {
        'Code': 'Success', 
        'CreationTime': '2022-09-14T00:00:00+0800', 
        'EndTime': '-', 
        'Input': {
            'BucketId': 'test-125xxxxxxxxxxx', 
            'Object': '1.txt', 
            'Region': 'ap-chongqing'
        }, 
        'JobId': 'dcf48xxxxxxxxxxxxxxxxxxxxxxxxxc523', 
        'Message': None, 
        'Operation': {
            'DocProcess': {
                'Comments': '1', 
                'DocPassword': None, 
                'EndPage': '-1', 
                'ImageDpi': '96', 
                'ImageParams': None, 
                'PageRanges': '1,3', 
                'PaperDirection': '0', 
                'PaperSize': '0', 
                'PicPagination': '0', 
                'Quality': '109', 
                'SheetId': '0', 
                'SrcType': None, 
                'StartPage': '0', 
                'TgtType': None, 
                'Zoom': '100'
            }, 
            'JobLevel': '0', 
            'Output': {
                'Bucket': 'test-125xxxxxxxxxxx', 
                'Object': '/test_doc/normal/abc_${Number}.jpg', 
                'Region': 'ap-chongqing'
            }
        }, 
        'QueueId': 'p4bxxxxxxxxxxxxxxxxxxxxxxxxxxxxx57f1', 
        'StartTime': '-', 
        'State': 'Submitted', 
        'Tag': 'DocProcess'
    }
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
| Input        | 该任务的输入文件路径 | Container |
| Operation    | 该任务的规则 | Container |



## 查询指定文档预览任务

#### 功能说明

ci_get_doc_job 用于查询指定的文档预览任务。

#### 方法原型
```py
def ci_get_doc_job(self, Bucket, JobID, **kwargs):
```

#### 请求示例

```py
def ci_get_doc_jobs():
    # 获取文档预览异步任务信息
    response = client.ci_get_doc_job(
        Bucket=bucket_name,
        JobID='d18a9xxxxxxxxxxxxxxxxxxxxff1aa',
    )
    print(response)
    return response
```

#### 参数说明
| 参数名称 | 描述           | 类型   |
| -------- | -------------- | ------ |
| Bucket   | 对象所在存储桶   | String |
| JobID    | 文档预览任务 ID  | String |

#### 返回结果说明

```py
{
    'JobsDetail': 
    [{
        'Code': 'Success', 
        'CreationTime': '2022-09-14T17:15:43+0800', 
        'EndTime': '2022-09-14T17:15:45+0800', 
        'Input': {'BucketId': 'testpic-1253960454', 'Object': '1.txt', 'Region': 'ap-chongqing'}, 
        'JobId': 'dcf488492340d11edb2a0e3aa2e38c523', 
        'Message': None, 
        'Operation': {
            'DocProcess': {'Comments': '1', 
                'DocPassword': None, 
                'EndPage': '-1', 
                'ImageDpi': '96', 
                'ImageParams': None, 
                'PageRanges': '1,3', 
                'PaperDirection': '0', 
                'PaperSize': '0', 
                'PicPagination': '0',
                'Quality': '109', 
                'SheetId': '0', 
                'SrcType': None, 
                'StartPage': '0', 
                'TgtType': None, 
                'Zoom': '100'
            }, 
            'DocProcessResult': {
                'FailPageCount': '0', 
                'PageInfo': [{'PageNo': '1', 'TgtUri': '/test_doc/normal/abc_1.jpg'}, {'PageNo': '3', 'TgtUri': '/test_doc/normal/abc_3.jpg'}], 
                'SuccPageCount': '2', 
                'TaskId': None, 
                'TgtType': None, 
                'TotalPageCount': '7'
            }, 
            'JobLevel': '0', 
            'Output': {'Bucket': 'testpic-1253960454', 'Object': '/test_doc/normal/abc_${Number}.jpg', 'Region': 'ap-chongqing'}
        }, 
        'QueueId': 'p4bdf22746b014a22a5a097b1f1d057f1', 
        'StartTime': '2022-09-14T17:15:44+0800', 
        'State': 'Success', 
        'Tag': 'DocProcess'
    }]
}

```

| 参数名称       | 描述                                                         | 类型      |
| -------------- | ------------------------------------------------------------ | --------- |
| JobsDetail     | 任务的详细信息， 同 [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49407#.E5.93.8D.E5.BA.94) 接口的 Response.JobsDetail 节点 | Container |
| NonExistJobIds | 查询的 ID 中不存在的任务，所有任务都存在时不返回             | String    |


## 拉取符合条件的文档预览任务 

#### 功能说明

ci_list_doc_jobs 用于拉取符合条件的文档预览任务。

#### 方法原型
```py
def ci_list_doc_jobs(self, Bucket, QueueId, StartCreationTime=None, EndCreationTime=None, OrderByTime='Desc', States='All', Size=10, NextToken='', **kwargs):

```

#### 请求示例
```py
def ci_list_doc_jobs():
    # 获取文档预览异步任务信息列表
    response = client.ci_list_doc_jobs(
        Bucket=bucket_name,
        QueueId='p4bdxxxxxxxxxxxxxxxxxxxx57f1',
        Size=10,
    )
    print(response)
    return response
```

#### 参数说明

| 参数名称          | 描述                                                         | 类型   |
| ----------------- | ------------------------------------------------------------ | ------ |
| Bucket            | 任务所在存储桶                                            | String |
| QueueId           | 拉取该队列 ID 下的任务                                     | String |
| OrderByTime       | Desc 或者 Asc。默认为 Desc                                 | String |
| NextToken         | 请求的上下文，用于翻页。上次返回的值                       | String |
| Size              | 拉取的最大任务数。默认为10，最大值为100                      | Int    |
| States            | 拉取该状态的任务，以`,`分割，支持多状态：All、Submitted、Running、Success、Failed、Pause、Cancel。默认为 All | String |
| StartCreationTime | 拉取创建时间大于该时间的任务。格式为：`%Y-%m-%dT%H:%m:%S%z`  | String |
| EndCreationTime   | 拉取创建时间小于该时间的任务。格式为：`%Y-%m-%dT%H:%m:%S%z`  | String |


#### 返回结果说明

```py
{
    'JobsDetail': [{
        'Code': 'Success', 
        'CreationTime': '2022-09-14T17:15:43+0800', 
        'EndTime': '2022-09-14T17:15:45+0800', 
        'Input': {'BucketId': 'testpic-1253960454', 'Object': '1.txt', 'Region': 'ap-chongqing'}, 
        'JobId': 'dcf488492340d11edb2a0e3aa2e38c523', 
        'Message': None, 
        'Operation': {
            'DocProcess': {
                'Comments': '1', 
                'DocPassword': None, 
                'EndPage': '-1', 
                'ImageDpi': '96', 
                'ImageParams': None, 
                'PageRanges': '1,3',
                'PaperDirection': '0', 
                'PaperSize': '0', 
                'PicPagination': '0', 
                'Quality': '109', 
                'SheetId': '0', 
                'SrcType': None, 
                'StartPage': '0', 
                'TgtType': None, 
                'Zoom': '100'
            }, 
            'DocProcessResult': {
                'FailPageCount': '0', 
                'PageInfo': [{'PageNo': '1', 'TgtUri': '/test_doc/normal/abc_1.jpg'}, {'PageNo': '3', 'TgtUri': '/test_doc/normal/abc_3.jpg'}], 
                'SuccPageCount': '2', 
                'TaskId': None, 
                'TgtType': None, 
                'TotalPageCount': '7'
            }, 
            'JobLevel': '0', 
            'Output': {'Bucket': 'testpic-1253960454', 'Object': '/test_doc/normal/abc_${Number}.jpg', 'Region': 'ap-chongqing'}
        }, 
        'QueueId': 'p4bdf22746b014a22a5a097b1f1d057f1', 
        'StartTime': '2022-09-14T17:15:44+0800', 
        'State': 'Success', 
        'Tag': 'DocProcess'
    }], 
    'NextToken': '75789'
}
```

| 参数名称   | 描述                                                         | 类型      |
| ---------- | ------------------------------------------------------------ | --------- |
| JobsDetail | 任务的详细信息，同 [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/436/49407#.E5.93.8D.E5.BA.94) 接口中的 Response.JobsDetail 节点 | Container |
| NextToken  | 翻页的上下文 Token                                           | String    |
