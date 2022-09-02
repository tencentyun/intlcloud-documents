本文将为您介绍安全评分细则。

## 安全评分
安全评分满分100，底分20。依据安全事件类型、安全事件数量、事件威胁等级进行扣分，以最终分数来划分安全等级。
![](https://qcloudimg.tencent-cloud.cn/raw/9d1a5ef6e265669833b7d570693ab180.png)
### 扣分规则
<table>
<thead>
<tr>
<th>等级</th>
<th>安全事件（按事件数计算）</th>
<th>扣分/个</th>
<th>叠加最大扣分</th>
</tr>
</thead>
<tbody><tr>
<td>严重</td>
<td>木马文件、暴破成功、恶意请求</td>
<td>-40分</td>
<td>-50分</td>
</tr>
<tr>
<td>高危</td>
<td>严重漏洞、高危漏洞、严重基线、高危基线、异常登录（高危）、本地提权、反弹Shell</td>
<td>-10分</td>
<td>-20分</td>
</tr>
<tr>
<td>中危</td>
<td>中危漏洞、中危基线</td>
<td>-3分</td>
<td>-10分</td>
</tr>
<tr>
<td>低危</td>
<td>低危漏洞、低危基线</td>
<td>-2分</td>
<td>-5分</td>
</tr>
<tr>
<td>其他</td>
<td>基础版防护、未安装主机安全客户端</td>
<td>-1分</td>
<td>-5分</td>
</tr>
</tbody></table>

### 安全等级
<table>
<thead>
<tr>
<th>等级</th>
<th>体检评分</th>
<th>字体颜色</th>
<th>状态说明</th>
</tr>
</thead>
<tbody><tr>
<td>优</td>
<td>90分 - 100分</td>
<td>绿色</td>
<td>资产安全状态较好，需继续保持，定期巡检。</td>
</tr>
<tr>
<td>中危</td>
<td>60分 - 89分</td>
<td>橙色</td>
<td>资产存在较多安全风险，建议您及时处理安全事件。</td>
</tr>
<tr>
<td>高危</td>
<td>20分 - 59分</td>
<td>红色</td>
<td>资产存在严重安全风险，请您尽快处理安全事件。</td>
</tr>
</tbody></table>
