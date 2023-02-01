通过控制台或 Serverless Cloud Framework 命令行均可以完成函数查询。

## 通过控制台查看函数
1. 登录 [Serverless 控制台](https://console.cloud.tencent.com/scf)，选择左侧导航栏中的**函数服务**。
2. 在“函数服务”页面上方选择期望查看函数所在的地域及命名空间。通过函数列表，可查看指定地域及命名空间内的全部函数。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/Azbs372_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219114446.png)
3. 函数列表中包括了函数名、监控、函数类型、运行环境、日志配置、创建时间等，您可根据自身需求自定义列表字段。单击函数列表右侧![](https://qcloudimg.tencent-cloud.cn/raw/0cb8ff5c087a438c195cd954e321754f.png)。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/EB2D161_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219114927.png)
在弹窗中勾选您想显示的列表详细信息，单击**确定**。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/7ach916_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219115035.png)
3. 单击函数名称，可进入该函数的详情页面。如下图所示：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/b2xD508_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20221219115137.png)
函数详情页面包含以下内容：
	- **函数管理**：可查看并管理函数配置、[函数代码](https://intl.cloud.tencent.com/document/product/583/39008)、[函数层](https://intl.cloud.tencent.com/document/product/583/37039)。
	- **版本管理**：可通过发布版本固定函数代码及配置内容。详情见 [函数版本](https://intl.cloud.tencent.com/document/product/583/35953)。 
	- **别名管理**：使用别名可以调用已绑定的函数。 
	- **触发管理**：展示函数已配置触发器，并可以通过此页面创建触发器。详情见 [触发器管理](https://intl.cloud.tencent.com/document/product/583/31441)。 
	- **监控信息**：显示函数运行监控信息。详情见 [函数监控](https://intl.cloud.tencent.com/document/product/583/32739)。
	- **日志查询**：查看函数运行日志，并可以根据一定条件过滤查询日志。详情见 [日志信息](https://intl.cloud.tencent.com/document/product/583/32740)。
	- **并发配额**：展示函数的并发额度，可以通过此页面设定函数最大独占配额和预置并发。详情见 [并发管理](https://intl.cloud.tencent.com/document/product/583/37040)。
	- **部署日志**：查看云函数部署日志信息。


## 通过 Serverless Cloud Framework 命令行获取部署信息
>?在使 Serverless Cloud Framework 工具之前，请参考 [安装 Serverless Cloud Framework](https://intl.cloud.tencent.com/document/product/583/36263) 完成安装。
>
您可通过 Serverless Cloud Framework，执行 `scf info` 命令查看部署信息。

