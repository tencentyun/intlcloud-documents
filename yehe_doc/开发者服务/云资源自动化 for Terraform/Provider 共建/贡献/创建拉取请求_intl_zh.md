我们欢迎任何人和团队向腾讯云 Provider 贡献代码，向 Provider 发起拉取请求的流程如下：

## 官方仓库

访问 [官方仓库](https://github.com/tencentcloudstack/terraform-provider-tencentcloud)。

## Fork 代码

您需从主仓库中 Fork 一份代码到子集的仓库，并对 Fork 出来的仓库进行代码变更。 
![](https://qcloudimg.tencent-cloud.cn/image/document/34abff6cc41656a358820d70d7e8f203.png)

## 分支命名约束

分支命名需要约遵循语义化的命名，一般以 `type/scope-content` 的格式，能让他人快速定位您改动的范围和内容，常用的分支前缀如下：
- `fix/*` 修复问题。

- `feat/*` 新增功能。

- `doc/*` 文档变更。

- `style/*` 格式、拼写等不影响逻辑的代码改动。

- `chore/*` 杂项提交，不涉及代码逻辑。


   后缀内容尽可能概括改动模块和内容，如：

- `fix/tke-auth-retry` 表示修复 TKE 模块鉴权重试的问题。

- `feat/new-free-ssl-resource` 表示增加新的 SSL 资源。

- `doc/cvm-field-misspell` 表示修改 CVM 文档某处文字错误。


   避免出现如下命名，如：

- `john-test` 直接以某位开发者的名字命名 。

- `fix/20221027` 无法体现改动了什么范围和内容。

- `fix/bug`以及其他带有不适当内容的名称。


## 验收测试

为了确保您的改动符合预期，涉及到逻辑的变更需要编写并执行验收测试。请参考 [编写测试用例](https://www.tencentcloud.com/document/product/1172/52381)。

## 发起拉取请求

当您的改动完成，请创建一个合并请求到 [主仓库](https://github.com/tencentcloudstack/terraform-provider-tencentcloud) 。图中红框选择主仓库，绿框选择您的仓库。

![](https://qcloudimg.tencent-cloud.cn/image/document/81f8bdba5490b846b3fe92c861acd6db.png)

## 提交 changelog 清单

当拉取请求发起后，您还需要再追加提交一条 `.changelog/<PR号码>.txt` 文件，按格式描述本次拉取请求的类型、模块和改动内容，模板如下：
``` release-note:bug
resource/<module>: something has done
```

具体内容请参考 [提交变更日志](https://www.tencentcloud.com/document/product/1172/52383)。

## 拉取请求检查

拉取请求发起后，Action 会运行一些基本的合并检查。

![](https://qcloudimg.tencent-cloud.cn/image/document/2dbd128c095114f53652db79e3668ca3.png)

如果您的代码需要验收测试，则由代码仓库成员打上 `run-check` 标记，触发执行能覆盖您变更的测试用例。

## 代码合并

当合并检查通过，仓库成员 Review 并确认分支可以合并后，我们会帮您把分支合入主干，后续会根据合入情况，进行版本发布。至此，整个代码贡献流程已走完，您的贡献将会帮到更多的用户！