## 服务端录制回调说明[](id:date)

### 说明
受网络影响，您的服务器收到的通知顺序和事件发生的顺序可能不完全一致。  
我们的服务有重试机制，但仍不能保证所有的消息都能到达。  
考虑到以上两点，不建议您业务的核心业务逻辑依赖消息通知服务。

### 网络协议

如果在控制台配置了回调地址，即一个 HTTP(S) 协议接口的 URL，则需要支持 POST 方法，传输数据编码采用 UTF-8。

### HTTP 头参数

<table>
<tr><th>名称</th><th>类型</th><th>是否必需</th><th>描述</th></tr>
<tr>
<td>Signature</td>
<td>string</td>
<td>是</td>
<td>签名，具体见下方 <a href="#Signature">签名生成</a> 说明</td>
</tr></table>

### 签名生成[](id:Signature)

Signature = HMAC-SH1 ( strContent, SecretKey )

- **strContent**：签名原文串，为 body 的整个 JSON 内容（长度以 Content-Length 为准）。
- **body**：回调给业务的 JSON 内容，下方 [回调示例](#example) 中的全部内容即为 body。
- **SecretKey**：密钥，为应用的权限密钥，可通过 [控制台 > 应用详情](https://console.tencentcloud.com/gamegme) 查看。
- **HMAC-SH1**：签名算法。


### 回调参数

<table>
<thead><tr>
<th width="20%">名称</th>
<th width="20%">类型</th>
 <th width="60%">描述</th>  
</tr></thead>
<tbody><tr>
<td>BizID</td>
<td>Integer</td> 
<td>应用的AppID，可通过<a href="https://console.tencentcloud.com/gamegme">控制台 > 应用详情</a> 查看。</td> 
</tr>
<tr>
<td>RoomID</td>
<td>String</td> 
<td>房间ID</td> 
</tr>
<tr>
<td>UserID</td>
<td>String</td> 
<td>用户ID</td> 
</tr>
<tr>
<td>RecordMode</td>
<td>Integer</td> 
<td >录制模式<ul style="margin:0">
	<li/>0: 单流
	<li/>1: 混流
</ul ></td>
</tr>
<tr>
<td>Timestamp</td>
<td>Integer</td> 
<td>发送回调时的时间戳（s）</td> 
</tr>
<tr>
<td>TaskID</td>
<td>Integer</td> 
<td>云录制服务分配的任务 ID。任务 ID 是对一次录制生命周期过程的唯一标识，结束录制时会失去意义。当您使用自定义录制模式时，
任务 ID可以在开始录制时通过响应参数获取，需要业务保存下来，作为下次针对这个录制任务操作的请求参数。</td> 
</tr>
<tr>
<td>EventType</td>
<td>Integer</td> 
<td>事件类型</td> 
</tr>
</tr>
<tr>
<td>Detail</td>
<td><a href="#EventDetail">EventDetail</a></td> 
<td>事件详情，由EventType决定格式</td> 
</tr>
</table>



### EventDetail事件详情说明[](id:EventDetail)

| EventType | 说明             | Detail                                                         |
| --------- | --------------- | ------------------------------------------------------------ |
| 1         | 音频文件启动录制   | <ul><li>SeqNo: Number，分片序号</li><li> FileName: String，文件名</li></ul> |
| 2         | 音频文件完成录制   | <ul><li>SeqNo: Number，分片序号</li><li> FileName: String，文件名</li></ul> |
| 3         | 音频文件上传完成   | <ul><li>SeqNo: Number，分片序号</li><li> FileName: String，文件名</li></ul> |


### 回调示例[](id:example)

```json
{
    "BizID":1400000000,
    "RoomID":"100",
    "UserID":"999",
    "TaskID":446946705284000000,
    "RecordMode":1,
    "Timestamp":1675930605,
    "EventType":1,
    "Detail":{
    	"SeqNo":0,
    	"FileName":"1400000000_100_999/2023-02-09-16-16-45_446946705284000000_audio.mp3"
    }
}
```