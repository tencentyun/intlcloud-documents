## 功能简介
清除缓存，即清除节点中已缓存的资源。清除后，用户访问资源时，将回源获取最新的资源进行响应。
>!清除缓存后，因节点上无该资源的缓存，只能回源获取，短时间内会增加回源请求量，减弱加速效果。如果清除的缓存资源较多，产生较多回源请求，源站会有一定压力。

## 适用场景
#### 发布新资源
业务源站更新了资源，需清除节点上已缓存的旧资源，避免用户仍请求到旧资源。清空全网缓存后，用户可请求到最新的资源。

#### 清理违规资源
如果业务站点上存在违规资源，需要及时整改并清理。由于节点上可能仍缓存着这些违规资源，需要清除节点上已缓存的违规资源。

## 操作步骤
1. 登录 [边缘安全加速平台控制台](https://console.cloud.tencent.com/edgeone)，在左侧菜单栏中，单击**站点加速** > **缓存配置**。
2. 在缓存配置页面，选择所需站点，单击清除缓存模块的**清除缓存**。
![](https://qcloudimg.tencent-cloud.cn/raw/4488d444245ae27e789b8e62e1d56e37.png)
3. 在清除缓存弹窗中，输入对应的资源内容，单击**确认清除**。
<table>
<thead>
<tr>
<th width="15%">支持类型</th>
<th width="85%">详情</th>
</tr>
</thead>
<tbody><tr>
<td>URL</td>
<td>匹配 Url(s) 的节点缓存资源，例如 <code>https://www.example.com/path/foo.jpg</code>。</td>
</tr>
<tr>
<td>前缀</td>
<td>匹配前缀路径的节点缓存资源，例如 <code>https://www.example.com/path</code>。</td>
</tr>
<tr>
<td>Hostname</td>
<td>匹配 Hostname(s) 的节点缓存资源，例如 <code>www.example.com</code>。<br>注意：不支持提交 <code>http://*.test.com/</code> 格式的 URL，即域名中不能包含<code>*</code>，需要写明对应的子域名。</td>
</tr>
<tr>
<td>Cache-Tag</td>
<td>匹配 HTTP 应答包中 <code>Cache-Tag</code> 响应头的标签值（tags）清除缓存，例如 <code>Cache-Tag: tag1,tag2,tag3</code>。<ul><li>仅适用企业版套餐。</li><li> EdgeOne 支持识别源站响应头 <code>Cache-Tag</code>，请添加 tag(s) 至此头部：<ul><li>头部大小最大为 6KB。</li><li> 多个 tag 用“,”分隔，单个 tag 不超过128字符，tag 个数上限为1,000。</li><li>tag 忽略大小写，即 Tag1 和 tag1 会识别为相同的 tag。</li></td>
</tr>
<tr>
<td>全部缓存</td>
<td>站点在节点的全部缓存资源。<br>注意：若当前站点（example.com）下接入了泛域名，例如 <code>*.foo.example.com</code>，则该泛域名无法生效，需单独提交其各个具体子域名的清除缓存任务。</td>
</tr>
</tbody></table>

4. 单击**查看历史**，可查看指定时间段和清除类型的历史记录。
![](https://staticintl.cloudcachetci.com/yehe/backend-news/fIQc461_QQ20221116-121021.png)

## 注意事项
### 内容规范
请您先关注确认提交的内容是否符合规范：
- 请避免提交已关闭/被锁定/未接入当前账号的站点内容。
- 若您选择了上传文件的提交方式，需确保文件格式为 txt，大小不超过10M。
- 若内容含有非 ASCII 字符集的字符，请打开 URL Encode 开关，编码转换。
 - 编码规则遵循 RFC3986。
 - 空格无论出现在何处均编码转换为`%20`。
 - 若有编码转换，仅清除编码转换后匹配的资源。

### 提交限额
- 不同计费套餐有不同限额，详见 [计费概述](https://www.tencentcloud.com/document/product/1145/48705)。
- 若您选择了上传文件的提交方式，无单次限额，会直接在单日限额中扣除提交的个数。
