## 操作场景
您可通过本文快速了解 Batch 的使用方法及计算能力。 

## 前提条件
请根据 [前置准备](http://intl.cloud.tencent.com/document/product/599/10548) 里的说明完成准备，并了解如何配置自定义信息里的通用部分。

### 查看 Demo
>请在 [前置准备](http://intl.cloud.tencent.com/document/product/599/10548) 中修改 `1_SimpleStart.py` 文件自定义信息的通用部分。
>
使用编辑器打开 `1_SimpleStart.py` 文件
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "LOCAL",
    "Command": " python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
```
自定义部分除 Application 以外，都已在前置准备中说明， Application 中配置请参考下表：

<table>
	<tr>
	<th>配置项</th>
	<th>描述</th>
	</tr>
	<tr>
	<td>DeliveryForm</td>
	<td>应用程序的交付方式，包括软件打包、容器镜像、CVM 内部直接运行三种，这里 LOCAL 代表的是 CVM 内部直接运行。</td>
	</tr>
	<tr>
	<td>Command</td>
	<td>任务启动命令，这里执行的是一段 Python 脚本。以1为起点，将斐波拉契数列的前20个数字求和并输出到 StdOutput 里。</td>
	</tr>
</table>

<span id="commit"></span>
### 提交作业
执行以下命令，执行 Python 脚本。
Demo 中已经通过 Python 脚本 + Batch 命令行工具的形式封装了提交作业流程。
```
python 1_SimpleStart.py
```
返回结果如下所示，则表示提交成功。
```
{
    "RequestId": "393292f4-5583-48ad-a9f5-f673138ea637", 
    "JobId": "job-o0xxxxxq7"
}
```
若未提交成功，请检查返回值排查错误，也可以通过 [联系我们](http://intl.cloud.tencent.com/document/product/599/10806) 。

### 查看状态
- 执行以下命令，通过 DescribeJob 查看执行状态：
```
$ tccli batch DescribeJob --version 2017-03-12 --JobId job-xxx
```
>--JobId 请替换成 [提交作业](#commit) 中的返回的 JobId。
>
返回信息如下（部分已省略）：
```
{
    "EndTime": "2019-10-08T04:06:58Z", 
    "JobState": "SUCCEED", 
    "TaskInstanceMetrics": {
        ...
    }, 
    "Zone": "ap-guangzhou-2", 
    "TaskMetrics": {
        ...
    }, 
    "JobName": "TestJob", 
    "Priority": 1, 
    "RequestId": "7a5f4c94-1357-486c-9c48-8286ba01b5b2", 
    "TaskSet": [
        ...
    ], 
    "StateReason": null, 
    "JobId": "job-o0xxxxxq7", 
    "DependenceSet": [], 
    "CreateTime": "2019-10-08T04:05:54Z"
}
```
- 返回信息包含下列常见执行状态：
 * STARTING：启动中
 * RUNNING：执行中
 * SUCCEED：执行成功
 * FAILED：执行失败

### 查看结果
1. 登录对象存储控制台，单击左侧导航栏中的**[存储桶列表](https://console.cloud.tencent.com/cos5/bucket)**。
2. 选择已创建的 **Bucket ID**>**文件列表**>**logs 文件**，执行结果均保存在 logs 文件中。如下图所示：
![](https://main.qcloudimg.com/raw/e6ffa709b7e843c44d00bedfd072f367.png)
 - 成功时请查看标准输出 stdout.job-xxx.xxxx.0.log，内容如下：
```
6765
```
 - 失败时请查看标准错误 stderr.job-xxx.xxxx.0.log，可能的内容如下：
```
/bin/sh: -c: line 0: syntax error near unexpected token `('
/bin/sh: -c: line 0: ` python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" '
```



