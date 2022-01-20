## 2021年05月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody>
<tr>
<td>自助诊断工具上线</td>
<td>自助诊断工具是腾讯云对象存储为用户提供的 Web 工具，可用于错误请求的自助诊断排查。</td>
<td> 2021-05-27</td>
<td>自助诊断工具 </a>
</tr>
<tr>
<td>CDN 日志备份上线</td>
<td>CDN 日志备份是腾讯云对象存储 COS 基于 云函数 SCF 为用户提供的将 CDN 日志转存至 COS 的功能，可以协助用户将 CDN 日志进行转存以便于进行访问行为分析、服务质量监控等。</td>
<td> 2021-05-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/40485">CDN 日志备份</a>
</tr>
<tr>
<td>TDMQ 消息备份上线</td>
<td>TDMQ 消息备份是腾讯云对象存储 COS 基于云函数 SCF 为用户提供的 TDMQ 消息转存至 COS 的功能，可以协助用户将 TDMQ 消息进行转存以便于对数据进行分析与下载等操作。</td>
<td> 2021-05-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/40541">TDMQ 消息备份</a>
</tr>
</tbody></table>


## 2021年04月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody>
<tr>
<td>日志清洗上线</td>
<td>日志清洗是对象存储 COS 基于云函数 SCF 为用户提供的日志文件处理解决方案。当用户开启日志管理服务或自行上传日志文件时，将自动触发对象存储为您预配置的云函数，通过函数中您预先指定的 SQL 检索语句，自动将文件中的日志信息进行过滤清洗。</td>
<td> 2021-04-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/39925">日志清洗</a>
</tr>
<tr>
<td>Ckafka 消息备份上线</td>
<td>Ckafka 消息备份是对象存储 COS 基于云函数 SCF 为用户提供的 Ckafka 消息转存至 COS 的功能，可以协助用户将 Ckafka 消息进行转存以便于对数据进行分析与下载等操作。</td>
<td> 2021-04-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/39926">Ckafka 消息备份</a>
</tr>
</tbody></table>



## 2021年02月


<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody>
<tr>
<td>云数据库备份上线</td>
<td>云数据库备份是对象存储 COS 基于云函数 SCF 为用户提供的数据库备份功能，可以协助用户将腾讯云数据库上的备份文件转存至对象存储进行持久化的保存，以防止数据丢失或损坏。</td>
<td>2021-02-02</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/41112">设置云数据库备份</a>
</tr>
</tbody></table>




## 2021年01月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody>
<tr>
<td>图片处理功能已全部支持公有云地域</td>
<td>图片处理功能新增支持海外公有云地域，目前图片处理功能已全部支持 COS 所有公有云地域。</td>
<td> 2021-01-20</td>
<td><ul  style="margin: 0;">
<li><a href="https://intl.cloud.tencent.com/document/product/436/35280">图片处理概述</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/436/6224">地域和访问域名</a></li>
</ul>
</tr>
</tbody></table>

## 2020年12月
<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody>
<tr>
<td>上线回源容灾功能</td>
<td>用户配置 COS 回源源站时，支持配置备份源站。针对回源失败的场景，能够保证当回源地址失效时，迅速切换至备用回源地址，保障业务连续不中断。</td>
<td> 2020-12-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31508">设置回源</a>
</tr>
<tr>
<td>上线同步回源功能</td>
<td>开启同步回源后，COS 将从源站直接拉取数据并实时返回给请求端，不再返回重定向的3XX 状态码。</td>
<td> 2020-12-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31508">设置回源</a>
</tr>
<tr>
<td>COS 批量处理功能优化升级</td>
<td>1. 批量复制时支持自定义复制、添加、修改对象标签及元数据。<br>2. 优化后端处理逻辑，按文件量级动态分配处理资源，处理效率提升50%。</td>
<td> 2020-12-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32958">批量处理概述</a>
</tr>
</tbody></table>

## 2020年11月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody>
<tr>
<td>COSDistcp 工具发布 </td>
<td>COSDistcp 是一款基于 MapReduce 的分布式文件拷贝工具，主要用于 HDFS 和 COS 之间的数据拷贝。</td>
<td> 2020-11-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/38863">COSDistcp 工具</a>
</tr>
<tr>
<td>上线存储网关功能</td>
<td>存储网关是腾讯云提供的混合云存储服务。您可以选择为存储桶配置存储网关，配置完成后，COS 中的存储桶可以以网络文件夹的形式挂载至您任意一台 CVM 服务器上作为存储设备进行使用。</td>
<td> 2020-11-21</td>
<td>-
</tr>
<tr>
<td>上线智能分层存储</td>
<td>智能分层存储类型为数据提供了冷热分层机制，能够根据用户数据的访问模式，自动地转换数据的冷热层级，从而降低用户数据的存储成本。</td>
<td> 2020-11-12</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/38305">智能分层存储简介</a>
</tr>
</tbody></table>

## 2020年09月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody>
<tr>
<td>生命周期功能迭代和存储桶概览页上线</td>
<td>1. 生命周期功能支持将历史版本文件沉降为其他存储类型；<br>2. COS 控制台支持对单个存储桶进行全局概览，包括查看用量、存储桶基本信息、功能和告警配置情况等。</td>
<td> 2020-09-28</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/14605">设置生命周期</a>
<br><a href="https://intl.cloud.tencent.com/document/product/436/38493">存储桶概览</a></td>
</tr>
<tr>
<td>上线深度归档存储</td>
<td>深度归档存储（Deep Archive）是对象存储 COS 提供的可让海量数据长期归档的存储服务。深度归档存储提供了磁带存储级别的存储单价，为用户数据长期存储提供了低成本方案。</td>
<td> 2020-09-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/38304">深度归档存储简介</a></td>
</tr>
</tbody></table>

## 2020年08月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody>
<tr>
<td>回源功能和生命周期功能迭代</td>
<td>1. 支持设置触发回源规则后跳转的具体路径，同时支持设置多个回源规则；<br>2. 生命周期规则的应用范围支持指定对象标签。</td>
<td> 2020-08-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31508">设置回源</a>
<br><a href="https://intl.cloud.tencent.com/document/product/436/14605">设置生命周期</a></td>
</tr>
</tbody></table>



## 2020年07月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody>
<tr>
<td>上线 CDN 缓存刷新功能</td>
<td>CDN 缓存刷新是腾讯云对象存储 COS 基于云函数服务 SCF 为用户提供的数据刷新功能，可以协助用户自动刷新 CDN 边缘节点上的缓存数据。</td>
<td> 2020-07-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/37273">设置 CDN 缓存刷新</a>
</tr>
</tbody></table>


## 2020年03月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>上线对象标签和文件解压缩功能<br>以及控制台改版优化</td>
<td>1. 控制台概览页全新改版，联动云监控告警配置、提供产品发布动态以及关联产品展示位；
<br>2. 提供文件解压缩能力；
<br>3. 提供对象标签功能，通过标签分组管理存储在 COS 上的对象；
<br>4. 存储桶列表支持排序、地域筛选、导出列表。</td>
<td >2020-03-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/35665">对象标签概述</a>
<br><a href="https://intl.cloud.tencent.com/document/product/436/35663">文件解压缩</a>
<br><a href="https://intl.cloud.tencent.com/document/product/436/16871">计费概述</a>
</td>
</tr>
<tr>
<td>上线图片处理功能</td>
<td>腾讯云对象存储 COS 集成了数据万象（Cloud Infinite，CI）专业的一体化媒体解决方案，涵盖图片处理、审核、识别等功能。您可以通过 COS 的上传和处理接口来进行媒体数据的处理操作。</td>
<td >2020-03-13</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/35280">图片处理概述</a></td>
</tr>
<tr>
<td>上线全球加速功能</td>
<td>腾讯云对象存储 COS 的全球加速功能，可帮助全球各地用户快速访问您的存储桶，提升您的业务访问成功率，进一步保障您的业务稳定和提升您的业务体验。</td>
<td >2020-03-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/33409">全球加速概述</a></td>
</tr>
</tbody></table>



## 2019年12月


<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>南京地域上线</td>
<td>对象存储上线南京地域（ap-nanjing）。</td>
<td nowrap="nowrap">2019-12-19</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/6224">地域和访问域名</a></td>
</tr>
<tr>
<td>存储桶加密功能上线</td>
<td>通过设置存储桶加密，可对新上传至存储桶的所有对象默认以指定的服务端加密方式进行加密。</td>
<td nowrap="nowrap">2019-12-16</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/33457">存储桶加密概述</a></td>
</tr>
</tbody></table>



## 2019年10月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>批量处理功能上线</td>
<td>批量处理功能可以让您对存储桶内指定的对象列表执行指定的操作。</td>
<td nowrap="nowrap">2019-10-22</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32958">批量处理概述</a></td>
</tr>
<tr>
<td>检索功能上线</td>
<td>COS 检索功能通过结构化查询语句（SQL）筛选存储在 COS 上的对象，以便检索对象并获取用户所需的数据。</td>
<td nowrap="nowrap">2019-10-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32472">Select 概述</a></td>
</tr>
</tbody></table>


## 2019年08月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>日志管理功能上线</td>
<td>日志管理功能够记录对于指定源存储桶的详细访问信息，并将这些信息以日志文件的形式保存在指定的存储桶中，以实现对存储桶更好的管理。</td>
<td nowrap="nowrap">2019-08-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/16920">日志管理概述</a></td>
</tbody></table>


## 2019年06月
<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>版本控制功能上线</td>
<td>版本控制用于实现在相同存储桶中存放同一对象的多个版本。</td>
<td nowrap="nowrap">2019-06-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/19883">版本控制概述</a></td>
</tr>
<tr>
<td>跨地域复制功能上线</td>
<td>通过配置跨地域复制规则，可以在不同存储区域的存储桶中自动、异步地复制增量对象。</td>
<td nowrap="nowrap">2019-06-20</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/19237">跨地域复制概述</a></td>
</tr>
<tr>
<td>支持自定义源站域名</td>
<td>用户可以将已备案的自定义域名，绑定至当前存储桶，通过自定义域名访问桶内对象。</td>
<td nowrap="nowrap">2019-06-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/18424">域名管理概述</a></td>
</tr>
<tr>
<td>清单功能上线</td>
<td>清单是一种帮助用户管理存储桶中对象的功能，可以有计划地取代对象存储同步 List API 操作。</td>
<td nowrap="nowrap">2019-06-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/30622">清单功能概述</a></td>
</tr>
</tbody></table>



## 2019年05月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>存储桶标签上线</td>
<td>存储桶标签是管理存储桶的一个标识，便于用户对存储桶进行分组管理。</td>
<td nowrap="nowrap">2019-05-10</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/31509">存储桶标签概述</a></td>
</tr>
</tbody></table>


## 2019年04月
<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>直传归档功能上线</td>
<td>在 COS 中直接上传存储类型为归档存储的对象。</td>
<td nowrap="nowrap">2019-04-26</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/30933">直传归档</a></td>
</tr>
</tbody></table>


## 2018年11月

<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>海外地域取消默认域名强制弹出下载</td>
<td>对象存储在海外地域允许直接使用腾讯云提供的访问域名，在浏览器中直接打开可识别的对象，不再需要绑定自定义域名。</td>
<td nowrap="nowrap">2018-11</td>
<td>—</td>
</tr>
</tr>
</thead>
<tbody><tr>
<td>优化请求速率的性能</td>
<td>对象存储全面支持超高频率发起访问请求，满足大数据计算等高频访问的场景。</td>
<td nowrap="nowrap">2018-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/13653">请求速率与性能优化</a></td>
</tr>
</tbody></table>

## 2018年10月
<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>通过 Policy 和 ACL 管理访问权限</td>
<td>对象存储全新上线有关支持 Policy 和 ACL 的方式管理权限的功能。授予访问权限，指的是用户可以决定什么人、在何种条件下、对哪些资源、执行具体操作的控制能力组合，满足在您在规划团队和资源等多个维度的权限管理需求。</td>
<td nowrap="nowrap">2018-10</td>
<td>—</td>
</tr>
</tbody></table>



## 2018年08月
<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>日本东京地域上线</td>
<td>对象存储上线日本东京（ap-tokyo）地域。</td>
<td nowrap="nowrap">2018-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/6224">地域和访问域名</a></td>
</tr>
<tr>
<td>新版控制台灰度上线</td>
<td>
支持更多新的地域
新版控制台使用全新接口，支持更多的地域。
新增功能
新版控制台支持生命周期等功能。
<br>注意：
<br>1. 官网功能、案例等文档将按照新版控制台界面同步更新。
<br>2. 后续推出的新功能将只会在新版控制台上发布，旧版控制台不再继续发布新功能。</td>
<td nowrap="nowrap">2018-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/11365">控制台概述</a></td>
</tr>
</tbody></table>


## 2018年06月
<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>发布 Hadoop COS 插件，支持大数据场景</td>
<td>正式发布 Hadoop COS 插件包，可以直接导入到 Hadoop 环境中，通过修改配置文件 core-site.xml 后，可使用 cosn:// 协议直接访问对象存储中的数据。</td>
<td nowrap="nowrap">2018-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/6884">Hadoop 工具</a></td>
</tr>
<tr>
<td>私有存储桶可绑定 CDN 访问功能</td>
<td>
对象存储支持通过 CDN 访问功能了。除了公有存储桶外，您还可以在私有存储桶上绑定 CDN 访问，同时开启 CDN 安全鉴权功能后，保障您的数据在 CDN 边缘缓存也受到保护，同时享受遍布全球的 CDN 加速能力。</td>
<td nowrap="nowrap">2018-06</td>
<td>—</td>
</tr>
</tbody></table>




## 2018年05月
<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>泰国曼谷、俄罗斯莫斯科地域上线</td>
<td>对象存储在全球多个新地域上线，包含泰国曼谷（ap-bangkok）和俄罗斯莫斯科（eu-moscow）地域。</td>
<td nowrap="nowrap">2018-05</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/6224">地域和访问域名</a></td>
</tr>
</tbody></table>



## 2018年04月
<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>可使用 PATH 方式创建请求</td>
<td>在支持虚拟托管域名的同时，支持了域名路径方式访问对象存储。对于地域根节点 cos.[region].myqcloud.com 发出请求，将可返回当前地域的存储桶和对象信息，兼容 AWS S3 的访问方式和 AWS Authentication V4 签名。配置对应的密钥和节点后，您可直接使用 S3 的各类代码和工具访问腾讯云 COS。</td>
<td nowrap="nowrap">2018-04</td>
<td>—</td>
</tr>
<tr>
<td>美国硅谷、弗吉尼亚（阿什本）、韩国首尔和印度孟买地域上线</td>
<td>对象存储在全球多个新地域上线，包含美国硅谷（na-siliconvalley）、弗吉尼亚（阿什本 na-ashburn）、韩国首尔（ap-seoul）和印度孟买（ap-mumbai）地域。</td>
<td nowrap="nowrap">2018-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/6224">地域和访问域名</a></td>
</tr>
</tbody></table>


## 2017年12月
<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>对象存储流量日结上线</td>
<td>为了让用户及时了解流量使用情况及费用情况，对象存储流量计费由月结变更为日结，其他计费项保持月结不变</td>
<td nowrap="nowrap">2017-12-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/33776">计费项</a></td>
</tbody></table>


## 2017年09月
<table>
<thead>
<tr>
<th width="20%">动态名称</th>
<th width="50%">动态描述</th>
<th width="15%">发布时间</th>
<th width="15%">相关文档</th>
</tr>
</thead>
<tbody><tr>
<td>对象存储发布全球多地域设施</td>
<td>对象存储新增成都、中国香港、新加坡、多伦多、法兰克福地域的存储服务，为全球用户提供就近存储和接入的能力，并调整降低了中国大陆地域的外网流量价格。</td>
<td nowrap="nowrap">2017-09</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/6224">地域和访问域名</a></td>
</tbody></table>
