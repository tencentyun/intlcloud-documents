
腾讯云云函数提供多种方式创建函数，本文向您介绍如何通过控制台和命令行工具创建函数。

## 使用控制台创建函数

1. 登录 [Serverless 控制台](https://console.cloud.tencent.com/scf)，单击左侧导航栏的**函数服务**。
2. 在函数服务页面上方选择期望创建函数的地域和命名空间，并单击**新建**，进入函数创建流程。如下图所示： 
![](https://staticintl.cloudcachetci.com/yehe/backend-news/wnBG038_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219142236.png)
3. 在“新建函数”页面，您可以根据实际需求选择创建函数的方式。
  - **模板创建**：通过填写必选的函数名称，使用函数模板中的配置来完成函数的创建。
  - **从头开始**：通过填写必填的函数名称、运行环境来完成函数的创建。
  - **使用容器镜像**：基于容器镜像来创建函数。详情见 [使用镜像部署函数](https://intl.cloud.tencent.com/document/product/583/41077)。
4. 配置函数基础信息。
<dx-tabs>
::: 模板创建
1. 在“模糊搜索”中添加标签查询模板。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/8X3I157_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219142541.png)
2. 选择模板后，单击**下一步**。
3. 填写函数基础信息。
	- **函数名称**：函数名称默认填充，可根据需要自行修改。
	- **地域**：地域默认填充，可根据需要自行修改。
	- **时区**：云函数内默认使用 UTC 时间，您可以通过配置环境变量 TZ 修改。在您选择时区后，将自动添加对应时区的 TZ 环境变量。
:::
::: 从头开始
填写函数基础信息。
- **函数类型**：支持选择**事件函数**和**Web 函数**。
  - 事件函数：接收云 API、多种触发器的 JSON 格式事件触发函数执行。详情见 [事件函数概述](https://intl.cloud.tencent.com/document/product/583/9210)。
  - Web 函数：直接接收 HTTP 请求触发函数执行，适用于 Web 服务场景。详情见 [Web 函数概述](https://intl.cloud.tencent.com/document/product/583/40688)。
- **函数名称**：函数名称默认填充，可根据需要自行修改。
- **地域**：地域默认填充，可根据需要自行修改。
- **运行环境**：运行环境默认填充，可根据需要自行修改。
- **时区**：云函数内默认使用 UTC 时间，您可以通过配置环境变量 TZ 修改。在您选择时区后，将自动添加对应时区的 TZ 环境变量。
:::
::: 使用容器镜像
填写函数基础信息。
- **函数类型**：支持选择**事件函数**和**Web 函数**。
  - 事件函数：接收云 API、多种触发器的 JSON 格式事件触发函数执行。详情见 [事件函数概述](https://intl.cloud.tencent.com/document/product/583/9210)。
  - Web 函数：直接接收 HTTP 请求触发函数执行，适用于 Web 服务场景。详情见 [Web 函数概述](https://intl.cloud.tencent.com/document/product/583/40688)。
- **函数名称**：函数名称默认填充，可根据需要自行修改。
- **地域**：选择函数部署的地域，请务必于镜像仓库处于同一地域。
- **时区**：云函数内默认使用 UTC 时间，您可以通过配置环境变量 TZ 修改。在您选择时区后，将自动添加对应时区的 TZ 环境变量。
:::
</dx-tabs>
5. 配置函数代码。
<dx-tabs>
::: 模板创建
运行环境、执行方法默认填充。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/USNv964_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219143734.png)
:::
::: 从头开始
选择函数代码提交方法和执行方法。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/HzWL458_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219144056.png)
- **提交方法**：支持在线编辑、本地上传zip包、本地上传文件夹、通过 cos 上传 zip 包。
  - 针对脚本类语言：可直接使用函数代码编辑器。
  - 针对非脚本类语言：通过 zip 包上传、通过对象存储 COS 上传的方式提交函数代码进行编辑。
- **执行方法**：执行方法表明了调用云函数时需要从哪个文件中的哪个函数开始执行。详情见 [函数执行方法](https://intl.cloud.tencent.com/document/product/583/19805)。
:::
::: 使用容器镜像
填写镜像相关内容。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/bykn557_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219145120.png)
- **镜像**：请选择当前地域镜像仓库已经构建好的镜像。
- **ENTRYPOINT**：容器的启动命令。该参数为可选参数，如果不填写，则默认使用 Dockerfile 中的 Entrypoint。输入规范，填写可运行的指令，例如 `python`。
- **CMD**：容器的启动参数。该参数为可选参数，如果不填写，则默认使用 Dockerfile 中的 CMD。输入规范，以“空格”作为参数的分割标识，例如 `-u app.py`。
- **镜像加速**：默认不开启。开启加速后，云函数将较大程度减少拉取镜像的耗时。开启过程需要 30 秒以上时间，请耐心等待。
:::
</dx-tabs>
6. 在日志配置中，选择是否开启日志投递。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/QNye895_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219145400.png)
日志投递默认不开启。启用时，可将函数运行日志实时投递到指定位置。详情见 [日志投递配置](https://intl.cloud.tencent.com/document/product/583/39778)。
<dx-alert infotype="notice" title="">
镜像部署函数和 Web 函数暂不支持日志格式选择。
</dx-alert>
7. 在高级配置中，您可以根据实际需求对函数进行环境配置、权限配置、层配置、网络配置等，详情见 [函数相关配置](https://intl.cloud.tencent.com/document/product/583/19805)。
8. 在触发器配置中，选择是否创建触发器。如果您选择“自定义创建”，详情见 [触发器概述](https://intl.cloud.tencent.com/document/product/583/9705)。
9. 单击**完成**。您可以在 [函数服务](https://console.cloud.tencent.com/scf/list) 中查看已创建的函数。



## 使用命令行工具创建函数 

您可根据实际需求，选择更多方式创建函数：
- 使用 Serverless Cloud Framework 命令行工具，可参考 [使用 CLI 创建函数](https://intl.cloud.tencent.com/document/product/583/32743)。

