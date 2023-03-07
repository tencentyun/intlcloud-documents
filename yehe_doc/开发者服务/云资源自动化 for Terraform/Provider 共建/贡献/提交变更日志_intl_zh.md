开源项目始终保持用户友好、可读的 CHANGELOG.md，可以让用户快速判断出一个版本是否会对他们产生任何影响，并评估升级的风险。

按照规范，当您发起 PR 时，要求有个`.txt`变更文件来描述您这次更改的内容。之后我们会通过 [go-changelog](https://github.com/hashicorp/go-changelog) 工具，解析`.changelog`目录中的 txt 文件，生成 CHANGELOG.md。CHANGELOG.md 的更新规则如下：

## 变更日志格式

### 命名

当前 PR 的涉及的 changelog 日志，应该提交在`.changelog`目录下，名称为`{PR-NUMBER}.txt`。例如，PR 的 Number 是1326，则应该有一个名为`.changelog/1326.txt`的变更日志。

![](https://qcloudimg.tencent-cloud.cn/image/document/75448838bcf79eade86de13a4b21b585.png)

### 格式

`changelog.txt`格式如下，其中`{HEADER}`为对应 changelog 类别，`{ENTRY}` 为对应 changelog 的详细内容。
```
   release-note:{HEADER}
{ENTRY}
```

如果一个拉取请求应该包含多个变更日志条目，那么可以将多个块添加到同一个变更日志文件中。例如：

```
   release-note:bug
resource/tencentcloud_teo_zone: change tag description from zoneName to zoneId.

   release-note:enhancement
resource/tencentcloud_redis_instance: support update `security_groups`.
```


## 变更日志规则分类

CHANGELOG 旨在显示对特定版本的代码库影响操作员的更改。如果对代码的每一次更改或提交都会导致一个条目，那么 CHANGELOG 对操作员的用处就会降低。以下列表是需要做出决定以决定更改是否应具有条目的一般准则和示例。

### 新资源

一个新的资源，它的变更日志应该只包含资源的名称，并使用release-note:new-resource标题。

```
   release-note:new-resource
tencentcloud_postgresql_instance
```


### 新数据源

一个新的数据源，它的变更应该只包含数据源的名称，并使用release-note:new-data-source标题。

```
   release-note:new-data-source
tencentcloud_sqlserver_zone_config
```

### 问题修复

一个新的问题修复，它的变更应该使用release-note:bug标题，并有一个前缀指示它对应的资源或数据源，一个冒号，然后是一个简短的摘要。

> 如果是Provider级别的修复，使用provider前缀
> 

```
   release-note:bug
resource/tencentcloud_cdn_domain: Fix `https_config` inconsistency after apply
```


### 功能增强

一个新的功能增强，它的变更应该使用release-note:enhancement标题，并有一个前缀指示它对应的资源或数据源，一个冒号，然后是一个简短的摘要。

> 如果是Provider级别的功能增强，使用provider前缀
> 

```
   release-note:enhancement
resource/tencentcloud_cdn_domain: Support follow redirect and authentication
```



### 功能弃用

一个功能弃用，它的变更应该使用release-note:deprecation标题，并有一个前缀指示它对应的资源或数据源，一个冒号，然后是一个简短的摘要。

>?
> 如果是 Provider 级别的功能弃用，需要使用 provider 前缀。
> 

``` 
   release-note:deprecation
resource/tencentcloud_kubernetes_cluster: The `as_enabled` attribute is being deprecated.
```


## 不需要提交变更日志的情况
- 资源和提供者文档更新

- 测试更新

- 代码重构

