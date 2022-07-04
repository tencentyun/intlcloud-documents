语音识别（ASR）支持按标签授权。
- 按标签授权：您可以通过给资源标记标签，实现给子账号对应的标签下资源的管理权限。


## 接口级授权的 API 列表
针对支持操作级权限的 API 操作，您仍可以向用户授予使用该操作的权限，但是策略语句的资源元素必须指定为 * 。

| API 名 | API 描述 |
|---------|---------|
| CreateAsrUser | 为用户开通 ASR 服务 |
| DescribeResource | 查询资源包 |
| DescribeStatistics | 查询统计数据 |
| DescribeUserStatus | 查询用户 ASR 服务开通状态 |
| RealtimeRecognition | 实时识别 |
| StartStreamTranscription | 国际语音识别 |
