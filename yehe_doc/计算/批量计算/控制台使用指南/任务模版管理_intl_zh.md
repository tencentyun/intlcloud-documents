## 创建任务模板
任务模板的相关说明，请参考 [名词解释](https://intl.cloud.tencent.com/document/product/599/10396) 中的“任务模板”。您可以通过 [批量计算控制台](https://console.cloud.tencent.com/batch/task) 创建任务模板，具体步骤如下。
1. 登录[ 批量计算控制台](https://console.cloud.tencent.com/batch/task) 。如果您尚未开通批量计算服务，请参照批量计算控制台主页相关提示开通。
2. 选择左侧导航栏中的**任务模板**，并在页面上方选择目标地域。
3. 单击**新建**，进入“新建任务模板”页面，参考以下信息进行创建。如下图所示：
![](https://main.qcloudimg.com/raw/1791e9f754b7529c487dc0f10eb4bb98.png)
主要参数信息如下：
 - **计算环境类型**：
	 - **已有计算环境**：可选择已有计算环境。
	 - **自动计算环境**：即无须预先创建固定的计算环境。作业提交后，自动创建 CVM 实例并运行任务，任务完成后自动销毁实例。
   - 	 **资源配置**：可单击**云主机详细配置**进一步选择，详情请参见 [云服务器产品文档](https://intl.cloud.tencent.com/document/product/213) 。
   - **资源数量**：决定并行执行任务的资源数，详情请参见 [名词解释](https://intl.cloud.tencent.com/document/product/599/10396)  中“任务实例”。
   - **镜像**：详情请参考 [名词解释](https://intl.cloud.tencent.com/document/product/599/10396) “镜像”。
4. 单击**下一步**，设置程序配置信息。如下图所示：
![](https://main.qcloudimg.com/raw/423bf1b3ac0639169d9ba4ece661732f.png)
   - **执行方式**：当选择 “Package” 时，需要填写“程序包地址”。“程序包地址”存放在 [对象存储](https://intl.cloud.tencent.com/document/product/436) 中。
   - **程序包地址/ Stdout 日志/ Stderr 日志**：需满足固定的格式，请参考 [COS、CFS路径填写](https://intl.cloud.tencent.com/document/product/599/13996)。
5. 单击**下一步**，配置存储映射。如下图所示：
![](https://main.qcloudimg.com/raw/dfcff0f1f896906316fd9227b105d54e.png)
   - **输入路径映射**：对于 Linux 系统，支持 [对象存储](https://intl.cloud.tencent.com/document/product/436) 和 [文件存储](https://intl.cloud.tencent.com/document/product/582)。对于 Windows 系统，支持 [文件存储](https://intl.cloud.tencent.com/document/product/582) 。对象存储和文件存储的格式要求，请参考 [COS、CFS路径填写](https://intl.cloud.tencent.com/document/product/599/13996) 。同时，针对不同的操作系统，请注意本地路径的格式区别。
   - **输出路径映射**：支持 [对象存储](https://intl.cloud.tencent.com/document/product/436)，对象存储格式请参考 [COS、CFS路径填写](https://intl.cloud.tencent.com/document/product/599/13996)。
6. 单击**下一步**，任务模板 JSON 文件确认无误后，单击**保存**即可完成任务模板创建。
![](https://main.qcloudimg.com/raw/3aadaf52ef74160eb1cd7e92b401e4e6.png)

## 删除任务模板
当您不再需要使用某个任务模板时，可在“任务模板”列表页面进行删除。如下图所示：
![](https://main.qcloudimg.com/raw/cfcdac39a8b7abb42c4d442e3bf948ed.png)

## 修改任务模板
当您需要编辑已有的任务模板时，可在“任务模板”列表页面单击任务模板 ID，进入任务模板配置页逐项编辑。如下图所示：
![](https://main.qcloudimg.com/raw/bb50e54947c48a241faca8f2fb369fcc.png)
