本文将为刚入门内容分发网络（CDN）的用户提供一条学习的路径。

## 1. 熟悉 CDN 的基础知识

- [CDN 是怎么工作的？](https://intl.cloud.tencent.com/document/product/228/2939)
- [我为什么选择腾讯云 CDN？](https://intl.cloud.tencent.com/document/product/228/2941)
- [CDN 的各个应用场景介绍。](https://intl.cloud.tencent.com/document/product/228/32980)
- [使用腾讯云 CDN 有哪些限制？](https://intl.cloud.tencent.com/document/product/228/32981)
- [CDN 的常用概念。](https://intl.cloud.tencent.com/document/product/228/36183)



## 2. CDN 的计费模式

腾讯云 CDN 的计费模式分为**带宽计费**和**流量计费**。您需要全面了解 CDN 的计费模式，有利于您选择最优的计费方案。详情请参见 [计费说明](https://intl.cloud.tencent.com/document/product/228/2949)。






## 3. 新手入门

#### 3.1 开通服务与选择计费方式

在使用腾讯云 CDN 之前，您需要注册腾讯云账号并且开通 CDN 服务。详情请参见 [从零开始配置 CDN](https://intl.cloud.tencent.com/document/product/228/32978)。

#### 3.2 接入域名

您需为您的加速业务接入加速域名。CDN 通过加速域名把源站资源缓存到 CDN 加速节点，用户可就近获取所需资源，实现资源访问加速。详情请参见 [接入域名](https://intl.cloud.tencent.com/document/product/228/5734)。

#### 3.3 配置 CNAME

接入完成后，腾讯云 CDN 会为您分配对应的 CNAME 地址，您还需要完成 CNAME 的配置，CDN 服务才能生效。详情请参见 [配置 CNAME](https://intl.cloud.tencent.com/document/product/228/3121)。

>? 您也可以参见以下最佳实践进行操作，快速上手腾讯云 CDN，加速您的域名。
>- [腾讯云 CDN 加速云服务器 CVM 的实例。](https://intl.cloud.tencent.com/document/product/228/34035)
>- [腾讯云 CDN 加速对象存储 COS 的实例。](https://intl.cloud.tencent.com/document/product/228/34036)




## 4. 控制台界面

以下为 CDN 控制台总览页面：
![](https://main.qcloudimg.com/raw/95fff730b132974403698b512260f3fb.png)




## 5. 控制台功能概述

<table>
<thead>
<tr>
<th>如果您想</th>
<th>您可以阅读</th>
</tr>
</thead>
<tbody><tr>
<td>对已经接入的加速域名进行查看、启动或关闭操作。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/5736" target="_blank">域名操作</a></td>
</tr>
<tr>
<td>筛选列表查看，或根据标签、项目等进行云资源管理。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32913" target="_blank">域名检索</a></td>
</tr>
<tr>
<td>优化您的 CDN 加速效果，CDN 支持多项自定义配置。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6288" target="_blank">配置概览</a></td>
</tr>
<tr>
<td>查看控制台功能点与 Action 映射关系。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35229" target="_blank">控制台权限说明</a></td>
</tr>
<tr>
<td>通过自定义策略语句，实现域名级别的权限分配。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35228" target="_blank">策略创建</a></td>
</tr>
<tr>
<td>针对项目级别的授权操作进行细化。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35743" target="_blank">项目级权限说明</a></td>
</tr>
<tr>
<td>根据实时监控数据来分析运行情况。</td>
<td>实时监控</a></td>
</tr>
<tr>
<td>分析您的用户来源和用户分布及使用情况。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/32923" target="_blank">数据分析</a></td>
</tr>
<tr>
<td>定期清理节点缓存资源，回源站重新拉取最新资源重新缓存。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6299" target="_blank">缓存刷新</a></td>
</tr>
<tr>
<td>将指定资源提前加载至加速节点。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/39000" target="_blank">缓存预热</a></td>
</tr>
<tr>
<td>下载访问日志，按自身需要进行热门资源分析、活跃用户分析等。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6316" target="_blank">日志下载</a></td>
</tr>
<tr>
<td>对您的日志数据快速检索与分析。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/35380" target="_blank">实时日志</a></td>
</tr>
<tr>
<td>查看全网实时状态概览及详情。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6311" target="_blank">全网状态监控</a></td>
</tr>
<tr>
<td>以报表形式多维度展示您的业务状态，帮助您进行业务状态分析。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6312" target="_blank">运营报表</a></td>
</tr>
<tr>
<td>在 CDN 控制台查看中国境内流量包的使用情况。</td>
<td>流量包管理</a></td>
</tr>
<tr>
<td>验证指定的 IP 是否为腾讯云 CDN 节点。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/10747" target="_blank">IP 归属查询</a></td>
</tr>
<tr>
<td>诊断某访问异常的 URL，快速定位问题。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/228/6304" target="_blank">自助诊断工具</a></td>
</tr>
<tr>
<td>进行 DDoS、CC、WAF 全方位防护及攻击监控。</td>
<td>安全加速</a></td>
</tr>
<tr>
<td>使用腾讯云 CDN 进行海量图片分发。</td>
<td>图片优化</a></td>
</tr>
</tbody></table>


## 6. 新手常见问题
#### 计费相关问题
- [怎么查询 CDN 账单？](https://intl.cloud.tencent.com/document/product/228/31479)
- [买了 CDN 中国境内流量包不想用了，是否能退货？](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDN 是否支持按照请求数计费？](https://intl.cloud.tencent.com/document/product/228/31479)
- [源站使用的是 COS，CDN 回源至 COS 产生的流量收费吗？](https://intl.cloud.tencent.com/document/product/228/31479)
- [关闭 CDN（CDN 服务下线后），是否还会有流量，是否会产生费用？](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDN 是否支持变更计费方式？](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDN 中国境内流量包使用管理](https://intl.cloud.tencent.com/document/product/228/31479)
- [CDN 计费是不是只是计算下行流量？](https://intl.cloud.tencent.com/document/product/228/31479)

#### 域名接入问题

- [CDN 是否支持泛域名接入？](https://intl.cloud.tencent.com/document/product/228/31476)
- [域名已在工信部进行过备案了，为何添加 CDN 加速域名提示域名未备案？](https://intl.cloud.tencent.com/document/product/228/31476)
- [CDN 配置大概需要多久？](https://intl.cloud.tencent.com/document/product/228/31476)
- [源站 IP 可以配置多个吗？](https://intl.cloud.tencent.com/document/product/228/31476)
- [如何判断 CDN 是否生效？](https://intl.cloud.tencent.com/document/product/228/31476)
- [域名只能关闭，不能删除是什么原因？](https://intl.cloud.tencent.com/document/product/228/31476)
- [如何关闭加速服务？](https://intl.cloud.tencent.com/document/product/228/31476)
- [如何删除加速域名？](https://intl.cloud.tencent.com/document/product/228/31476)
- [加速域名 / 源站支持配置端口吗？](https://intl.cloud.tencent.com/document/product/228/31476)
- [CDN 文件无法下载](https://intl.cloud.tencent.com/document/product/228/31476)



## 7. 反馈与建议
使用腾讯云 CDN 产品和服务中有任何问题或建议，您可以通过以下渠道反馈，将有专人跟进解决您的问题：
- 如果发现产品文档的问题，如链接、内容、API 错误等，您可以单击文档页右侧 【文档反馈】或选中存在问题的内容进行反馈。
- 如果遇到产品相关问题，您可[提交工单](https://console.cloud.tencent.com/workorder/category) 寻求帮助。

