本文将为刚入门全站加速网络（ECDN）的用户提供一条学习的路径。

## 1. 熟悉 ECDN 的基础知识

- [ECDN 是怎样工作的？](https://intl.cloud.tencent.com/document/product/570/8645)
- [为什么要选择腾讯云 ECDN？](https://intl.cloud.tencent.com/document/product/570/10358)
- [ECDN 的应用场景有哪些？](https://intl.cloud.tencent.com/document/product/570/38536)
- [ECDN 的常用概念。](https://intl.cloud.tencent.com/document/product/570/38537)



## 2. ECDN 的计费模式

腾讯云 ECDN 的计费模式由 **请求次数计费** 和 **超额流量计费** 组成，即总费用由 **请求次数** 产生的费用和 **流量超出免费额度** 产生的费用两部分组成。详情请参见 [计费说明](https://intl.cloud.tencent.com/document/product/570/37505)。



## 3. 新手入门

#### 3.1 开通服务与选择计费方式

在使用腾讯云 ECDN 之前，您需要注册腾讯云账号并且开通 ECDN 服务。详情请参见 [从零开始配置 ECDN](https://intl.cloud.tencent.com/document/product/570/38299)。

#### 3.2 接入域名

您需为您的加速业务接入加速域名。静态内容通过边缘缓存使用户可就近获取，动态内容通过智能路由优化、协议优化等动态加速技术快速回源获取，实现资源访问加速。详情请参见 [接入域名](https://intl.cloud.tencent.com/document/product/570/10361)。

#### 3.3 配置 CNAME

接入完成后，腾讯云 ECDN 会为您分配对应的 CNAME 地址，您还需要完成 CNAME 的配置，加速服务才能生效。详情请参见 [配置 CNAME](https://intl.cloud.tencent.com/document/product/570/11134)。





## 4. 控制台功能概述

<table>
<thead>
<tr>
<th>如果您想</th>
<th>您可以阅读</th>
</tr>
</thead>
<tbody><tr>
<td>对已经接入的加速域名进行加速服务开启、关闭、删除、修改所属项目等操作。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/10362" target="_blank">域名操作</a></td>
</tr>
<tr>
<td>优化您的 ECDN 加速效果，ECDN 支持多项自定义配置。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/11136" target="_blank">配置概览</a></td>
</tr>
<tr>
<td>了解 ECDN 全站加速支持的高级回源策略。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/35821" target="_blank">高级回源策略</a></td>
</tr>
<tr>
<td>查看控制台功能点与 Action 映射关系。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/35819" target="_blank">控制台权限说明</a></td>
</tr>
<tr>
<td>通过自定义策略语句，实现域名级别的权限分配。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/35820" target="_blank">策略创建</a></td>
</tr>
<tr>
<td>查看请求次数、访问流量和响应时间等指标。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/10368" target="_blank">访问情况统计</a></td>
</tr>
<tr>
<td>使用状态码监控数据查询功能。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/35827" target="_blank">状态码统计</a></td>
</tr>
<tr>
<td>定期清理节点缓存资源，回源站重新拉取最新资源重新缓存。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/35817" target="_blank">缓存刷新</a></td>
</tr>
<tr>
<tr>
<td>对已经接入 ECDN 的域名进行 HTTPS 证书配置。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/10366" target="_blank">证书管理</a></td>
</tr>
<tr>
<td>对您接入域名访问情况的详细日志进行分析。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/570/15258" target="_blank">日志管理</a></td>
</tr>
</tbody></table>



## 5. 新手常见问题

#### 计费类
- [ECDN 超额流量费是如何计算的？](https://intl.cloud.tencent.com/document/product/570/35823)
- [如果账号欠费，对 ECDN 服务有什么影响？](https://intl.cloud.tencent.com/document/product/570/35823)
- [域名服务关闭后（域名下线后），是否还会产生费用？](https://intl.cloud.tencent.com/document/product/570/35823)

#### 访问服务类
- [如何获取客户端访问的加速节点 IP？](https://intl.cloud.tencent.com/document/product/570/35824)
- [为什么获取到的客户端 IP 地址与真实用户 IP 地址不一致？](https://intl.cloud.tencent.com/document/product/570/35824)
- [使用全站加速后，访问出现异常状态码如何解决？](https://intl.cloud.tencent.com/document/product/570/35824)
- [如何快速定位域名访问异常问题？](https://intl.cloud.tencent.com/document/product/570/35824)

#### 域名接入类
- [接入 ECDN 的域名是否必须完成域名备案？](https://intl.cloud.tencent.com/document/product/570/35825)
- [ECDN 是否支持泛域名接入？](https://intl.cloud.tencent.com/document/product/570/35825)
- [加速端口（或访问端口）与回源端口有什么区别？](https://intl.cloud.tencent.com/document/product/570/35825)
- [控制台接入域名失败时如何处理?](https://intl.cloud.tencent.com/document/product/570/35825)

#### 功能概念类
- [全站加速是否支持 HTTPS？](https://intl.cloud.tencent.com/document/product/570/35826)
- [全站加速是否支持 Websocket?](https://intl.cloud.tencent.com/document/product/570/35826)
- [全站加速支持中国境外加速吗？](https://intl.cloud.tencent.com/document/product/570/35826)
- [ECDN 是否支持上传加速？](https://intl.cloud.tencent.com/document/product/570/35826)


## 6. 反馈与建议

使用腾讯云 ECDN 产品和服务中有任何问题或建议，您可以通过以下渠道反馈，将有专人跟进解决您的问题：

- 如果发现产品文档的问题，如链接、内容、API 错误等，您可以单击文档页右侧 【文档反馈】或选中存在问题的内容进行反馈。
- 如果遇到产品相关问题，您可[提交工单](https://console.cloud.tencent.com/workorder/category) 寻求帮助。
