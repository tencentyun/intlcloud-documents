## 简介

本文档提供关于媒体截图接口的 API 概览和 SDK 示例代码。

>! 需要 COS PYTHON SDK v5.1.9.11 及以上版本。

| API                        |             操作名                     | 操作描述                                               |
| ------------------------------------------------------------ | --------------------------|---------------------------- |
| [GetSnapshot](https://intl.cloud.tencent.com/document/product/436/46912) | 查询截图	 | 用于查询媒体文件在某个时间的截图 |

>! 使用此接口前，请确保已打开官网控制台中数据处理下的媒体处理开关，否则会报错`media bucket unbinded, bucket's host is unavailable`。详情请参见 [开通媒体处理](https://intl.cloud.tencent.com/document/product/436/46275)。

## 查询截图

#### 功能说明

用于查询媒体文件在某个时间的截图。

#### 方法原型

```py
def get_snapshot(Bucket, Key, Time, Width=None, Height=None, Format='jpg', Rotate='auto', Mode='exactframe', **kwargs)
```

#### 请求示例
```py
response = client.get_snapshot(
    Bucket='examplebucket-1250000000',
    Key='demo.mp4',
    Time='1.5',
    Width='480',
    Format='png'
)
print(response)
response['Body'].get_stream_to_file('snapshot.jpg')
```

#### 参数说明


| 参数名称 | 参数描述                                                     | 是否必填 | 类型   |
| ------- | ----------------------------------------------------------- | ------- | ----- |
| Bucket        | 存储桶名称，格式为 BucketName-APPID ，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312) | 是 | String     |
| Key     | 对象键（Key）是对象在存储桶中的唯一标识 | 是       | String   |
| Time   | 截图的时间点，单位为秒，可以支持小数点        | 是       | String  |
| Width | 截图的宽。默认为0         | 否       | String    |
| Height | 截图的高。默认为0 当 width 和 height 都为0时，表示使用视频的宽高；如果单个为0，则以另外一个值按视频宽高比例自动适应 | 否       | String    |
| Format | 截图的格式，支持 jpg 和 png，默认 jpg    | 否     | String |
| Rotate | 图片旋转方式 auto：按视频旋转信息进行自动旋转off：不旋转，默认值为 auto | 否       | String |
| Mode   | 截帧方式 keyframe：截取指定时间点之前的最近的一个关键帧exactframe：截取指定时间点的帧，默认值为 exactframe | 否       | String |
