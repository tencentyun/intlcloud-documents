安装腾讯云命令行工具 TCCLI 前请确保您的系统已经安装了 Python 环境，详情请参考 [前提条件](https://intl.cloud.tencent.com/document/product/1013/33464)。

## 步骤1：安装 TCCLI	

### 安装 TCCLI
请结合您的实际情况，执行对应命令。
- **未安装 TCCLI**
执行以下命令，通过 pip 可以快速安装 TCCLI，详情请参考 [安装命令行工具](https://intl.cloud.tencent.com/document/product/1013/33464)。
```
$ sudo pip install tccli
```
- **已安装 TCCLI**
执行以下命令，通过 pip 可以快速升级。
```
$ sudo pip install --upgrade tccli
```

### 验证安装  
执行以下命令，检验命令行工具 TCCLI 是否安装成功，以及是否包含 Batch 相关能力。
```
tccli batch help
```
返回结果如下，则成功安装。
```
NAME
        batch
DESCRIPTION
        batch-2017-03-12
USEAGE
        tccli batch <action> [--param...]
OPTIONS
        help
        show the tccli batch help info
        --version
        specify a batch api version
AVAILABLE ACTION
        DescribeComputeEnv
        用于查询计算环境的详细信息
        CreateTaskTemplate
        用于创建任务模板
```

## 步骤2：配置 TCCLI	
1. 登录腾讯云 [API 密钥控制台](https://console.cloud.tencent.com/cam/capi)。
2. 单击**新建密钥**或使用现有密钥，记录 SecretID 及 SecretKey。如下图所示：
![](https://main.qcloudimg.com/raw/0edc3a84752d2ae4524e971156f7e5f3.png)
3. 执行 `tccli configure` 命令，并输入 TCCLI 配置信息，详情请参考 [配置命令行工具](https://intl.cloud.tencent.com/zh/document/product/1013/33465)。
```
$ tccli configure
TencentCloud API secretId[None]:
TencentCloud API secretKey[None]:
region[None]:
output[json]:
```


## 步骤3：准备 COS 目录


### 创建 Bucket 及子文件夹[](id:create)
1. 登录对象存储控制台，选择左侧导航栏中的 **[存储桶列表](https://console.cloud.tencent.com/cos5/bucket)**。
2. 创建一个 Bucket，并且在 Bucket 中创建3个文件夹以便后续使用。如下图所示：
![](https://main.qcloudimg.com/raw/0add1b49c44f4b2740ddc44e3164216b.png)


### 获取 COS 相关访问域名[](id:get)
1. 单击 Bucket 左侧的**基础配置**，可在 Bucket 基础信息中查看访问域名。如下图所示：
![](https://main.qcloudimg.com/raw/cc6a49e7164226efa1cdfe3bcde60a35.png)
2. 获取 COS Bucket 子文件夹访问域名。
<dx-alert infotype="explain" title="">
请结合您的实际情况，获取 COS 相关域名。
</dx-alert>
已获得 COS Bucket 的访问域名为：`https://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com`，可通过 `域名+文件夹` 推算出在 [创建 Bucket 及子文件夹](#create) 中创建的3个文件夹的访问域名。如下所示：

 * `cos://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com/logs/`
 * `cos://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com/input/`
 * `cos://batchdemo-xxxxxxxxx.cos.ap-guangzhou.myqcloud.com/output/`



## 步骤4：下载 Demo 文件
请前往 [Batch Demo](http://batchdemo-1251783334.cosgz.myqcloud.com/demo/BatchDemo.zip) 下载测试文件并解压。

<dx-alert infotype="explain" title="">
Demo 以 Python + Batch 命令行工具的形式提供，Batch 的能力和可配置项较丰富，通过 Python 脚本可以更便捷的操作。
</dx-alert>






## 步骤5：修改 Demo 自定义信息


<dx-alert infotype="notice" title="">
Batch Demo 中需替换自定义信息中的通用部分，请参考以下步骤修改 Demo 中的所有文件。
</dx-alert>


以 `1_SimpleStart.py` 中的自定义信息部分为例：
```
# custom (Change to your info)
imageId = "img-m4q71qnf"
Application = {
    "DeliveryForm": "LOCAL",
    "Command": " python -c \"fib=lambda n:1 if n<=2 else fib(n-1)+fib(n-2); print(fib(20))\" "
}
StdoutRedirectPath = "cos://batchdemo-xxxxxxxxxx.cos.ap-guangzhou.myqcloud.com/logs/"
StderrRedirectPath = "cos://batchdemo-xxxxxxxxxx.cos.ap-guangzhou.myqcloud.com/logs/"
```
需要修改的信息如下表所示：
<table>
	<tr>
	<th>配置项</th>
	<th>描述</th>
	</tr>
	<tr>
	<td>imageId</td>
	<td>
		<ul class="params">
		<li>自定义镜像需要基于此镜像来制作，可参考 <a href="https://intl.cloud.tencent.com/document/product/599/13035">Windows 自定义镜像</a>。</li>
		</ul>
	</td>
	</tr>
	<tr>
	<td>StdoutRedirectPath</td>
	<td rowspan=2>请填写 <a href="#get">获取 COS 相关访问域名</a> 中获取的 logs 文件夹完整访问域名。</td>
	</tr>
	<tr>
	<td>StderrRedirectPath</td>
	</tr>
	<tr>
	<td>Application</td>
	<td>启动命令行，保持默认设置。</td>
	</tr>
</table>


```
cmd = "tccli batch SubmitJob \
    --version 2017-03-12 \
    --Placement '{\"Zone\": \"ap-guangzhou-2\"}' \
    --Job ' %s ' "%(json.dumps(testJob))
```
Demo 中指定在广州二区申请资源，您可以根据 TCCLI 中配置的默认地域，选择相应的可用区并申请资源。
地域和可用区的详细信息请查看 [地域和可用区](https://intl.cloud.tencent.com/document/product/213/6091)。

## 步骤6：测试
请对应文件参考教程，按照下列顺序体验 Batch 的使用方法及计算能力。
1. 1_SimpleStart.py：[简单开始](https://intl.cloud.tencent.com/document/product/599/10551)
2. 2_RemoteCodePkg.py：[执行远程代码包](https://intl.cloud.tencent.com/document/product/599/10552)
3. 3_StoreMapping.py：[远程存储映射](https://intl.cloud.tencent.com/document/product/599/10983)


<style>
	.params{margin-bottom:0px !important;}
</style>


