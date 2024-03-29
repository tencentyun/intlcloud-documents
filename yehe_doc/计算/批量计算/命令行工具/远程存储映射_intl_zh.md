## 操作场景
远程映射是 Batch 对存储使用相关的辅助功能，能够将 COS、CFS 等远程存储映射到本地的文件夹上。


##  前提条件
请根据 [前置准备](https://intl.cloud.tencent.com/document/product/599/10548) 里的说明完成准备，并了解如何配置自定义信息里的通用部分。

## 操作步骤
### 上传输入数据文件
1. 创建  `number.txt` 文件，内容如下：
```
1
2
3
4
5
6
7
8
9
```
2. 登录对象存储控制台，单击左侧导航栏中的**[存储桶列表](https://console.cloud.tencent.com/cos5/bucket)**。
3. 选择已创建的 Bucket ID>**文件列表**>input 文件，上传 `number.txt`。如下图所示：
![](https://main.qcloudimg.com/raw/82be55909b293aa026539d47c996a1c4.png)

### 查看和修改 Demo
>?请在 [前置准备](https://intl.cloud.tencent.com/document/product/599/10548) 中修改  `3_StoreMapping.py` 文件自定义信息的通用部分。
>
使用编辑器打开 `3_StoreMapping.py` 文件
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "PACKAGE",
    "Command": "python ./codepkg/sumnum.py",
    "PackagePath": "http://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com/codepkg/codepkg.tgz"
}
StdoutRedirectPath = "your cos path"
StderrRedirectPath = "your cos path"
InputMapping = {
    "SourcePath": "cos://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com/input/",
    "DestinationPath": "/data/input/"
}
OutputMapping = {
    "SourcePath": "/data/output/",
    "DestinationPath": "your output remote path"
}
```
与 [`2_RemoteCodePkg.py`](https://intl.cloud.tencent.com/document/product/599/10552) 相比，自定义部分中修改如下表：
<table>
	<tr>
	<th>配置项</th>
	<th>描述</th>
	</tr>
	<tr>
	<td>Application</td>
	<td>Command 改为执行 sumnum.py。 </td>
	</tr>
	<tr>
	<td>InputMapping</td>
	<td>	输入映射。
	<ul class="params">
	<li>SourcePath 远程存储地址：修改为前置准备里 input 文件夹的地址，请参考 <a href="https://intl.cloud.tencent.com/document/product/599/10548#.E8.8E.B7.E5.8F.96-cos-.E7.9B.B8.E5.85.B3.E8.AE.BF.E9.97.AE.E5.9F.9F.E5.90.8D">获取 COS 相关访问域名</a>。</li>
	<li>DestinationPath 本地目录：暂不修改。</li>
	</ul>
</td>
	</tr>
	<tr>
	<td>OutputMapping</td>
	<td>输出映射。
	<ul class="params">
	<li>SourcePath 本地目录：暂不修改。</li>
	<li>DestinationPath 远程存储地址：修改为前置准备里 output 文件夹的地址，请参考 <a href="https://intl.cloud.tencent.com/document/product/599/10548#.E8.8E.B7.E5.8F.96-cos-.E7.9B.B8.E5.85.B3.E8.AE.BF.E9.97.AE.E5.9F.9F.E5.90.8D">获取 COS 相关访问域名</a>。</li>
	</ul>
	</td>
	</tr>
</table>

sumnum.py 的内容如下：
打开文件 `input/number.txt`，并把每一行的数字相加，然后把结果写到 `output/result.txt` 里。
```
import os

inputfile = "/data/input/number.txt"
outputfile = "/data/output/result.txt"

def readFile(filename):
    total = 0
    fopen = open(filename, 'r')
    for eachLine in fopen:
        total += int(eachLine)
    fopen.close()
    print "total = ",total
    fwrite = open(outputfile, 'w')
    fwrite.write(str(total))
    fwrite.close()

print("Local input file is ",inputfile)
readFile(inputfile)
```


### 提交作业
执行以下命令，执行 Python 脚本。
Demo 中已经通过 Python 脚本 + Batch 命令行工具的形式封装了提交作业流程。
```
python 3_StoreMapping.py
```
返回结果如下所示，则表示提交成功。
```
{
    "RequestId": "8eaeb01e-94a6-41a1-b40f-95f15417c0b4", 
    "JobId": "job-97smiptb"
}
```

若未提交成功，请检查返回值排查错误，也可以通过 [联系我们](https://intl.cloud.tencent.com/document/product/599/10806)。

### 查看状态
步骤同简单开始中的 [查看状态](https://intl.cloud.tencent.com/document/product/599/10551)。

### 查看结果
1. 登录对象存储控制台，单击左侧导航栏中的**[存储桶列表](https://console.cloud.tencent.com/cos5/bucket)**。
2. 选择已创建的 **Bucket ID**>**文件列表**>**output 文件**。如下图所示：
Batch 会将输出数据从本地目录靠白道远程存储目录中，`3_StoreMapping.py` 的执行结果保存在 `result.txt` 中，`result.txt` 将自动同步到 COS 中。
![](https://main.qcloudimg.com/raw/3f72ff4fd2232fd4a5da62d8aabc11ae.png)
`result.txt` 内容如下所示：
```
45
```

<style>
	.params{margin-bottom:0px !important;}
</style>
