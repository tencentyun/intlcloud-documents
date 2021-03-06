## 简介
API 返回 CosResult 结构，如果成功可以获取对应 Response 结构中的数据，失败可以通过 CosResult 获取详细信息。

## 服务端异常

CosResult 封装了请求出错时返回的错误码和对应错误信息，详情请参阅 [错误码](https://intl.cloud.tencent.com/document/product/436/7730)。

>!SDK 内部封装的请求均会返回 CosResult 对象，每次调用完成后，均要使用 IsSucc() 成员函数判断本次调用是否成功。

#### 成员函数

<table>
   <tr>
      <th>函数</th>
      <th>函数描述</th>
   </tr>
   <tr>
      <td>bool isSucc()</td>
      <td>返回本次调用成功或失败<br>当返回 false 时：后续的 CosResult 成员函数才有意义<br>当返回 True 时：可以从 OperatorResp 中获取具体返回内容</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetErrorCode()</td>
      <td>获取 COS 返回的错误码，用来确定错误场景</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetErrorMsg()</td>
      <td>包含具体的错误信息</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetResourceAddr()</td>
      <td>资源地址，Bucket 地址或 Object 地址</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetXCosRequestId()</td>
      <td>当请求发送时，服务端将会自动为请求生成一个唯一的 ID。使用遇到问题时，request-id 能更快地协助 COS 定位问题</td>
   </tr>
   <tr>
      <td>string GetXCosTraceId()</td>
      <td>当请求出错时，服务端将会自动为这个错误生成一个唯一的 ID，trace-id 与 request-id 一一对应。使用遇到问题时，trace-id 能更快地协助 COS 定位问题</td>
   </tr>
   <tr>
      <td>string GetErrorInfo()</td>
      <td>获取 SDK 内部错误信息</td>
   </tr>
   <tr>
      <td>int GetHttpStatus()</td>
      <td>获取 HTTP 状态码</td>
   </tr>
</table>


#### 请求和响应基类

BaseReq、BaseResp 封装了请求和返回， 调用者只需要根据不同的操作类型生成不同的 OperatorReq，并填充 OperatorReq 的内容即可。
函数返回后，调用对应 BaseResp 的成员函数获取请求结果。

- 对于 Request，如无特殊说明，仅需要关注 Request 的构造函数。
- 对于 Response，所有方法的 Response 均有获取公共返回头部的成员函数。Response 的公共成员函数如下，具体字段含义请参阅 [公共返回头部](https://intl.cloud.tencent.com/document/product/436/7729)，此处不再赘述。

```
uint64_t GetContentLength();
std::string GetContentType();
std::string GetEtag();
std::string GetConnection();
std::string GetDate();
std::string GetServer();
std::string GetXCosRequestId();
std::string GetXCosTraceId();
```
