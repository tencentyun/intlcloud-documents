
超出云函数 SCF 配额限制及解决方案如下表所示：

<table>
<thead>
<tr>
<th>内容</th>
<th>解决方案</th>
</tr>
</thead>
<tbody><tr>
<td>每个地域下命名空间个数达到上限</td>
<td>可通过 <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1">提交工单</a> 提升配额限制。</td>
</tr>
<tr>
<td>命名空间下函数个数达到上限</td>
<td><li>每个地域下可支持多个命名空间，可优先使用其他命名空间函数配额。</li><li>如当前地域下命名空间及函数个数均达到上限，可通过 <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1">提交工单</a> 提升配额限制。</li></td>
</tr>
<tr>
<td>单个函数的触发器个数达到上限</td>
<td><li> 建议将函数业务粒度细化，通过多个函数分别绑定触发器的方式解决单个函数触发器上限问题。</li><li> 如因业务需要无法拆分，可通过 <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1">提交工单</a> 提升配额限制。</li></td>
</tr>
<tr>
<td>每个地域的函数总并发配额达到上限</td>
<td>请在函数【并发配额】页尝试调整【当前地域下总并发配额】。</td>
</tr>
<tr>
<td>函数初始化超时时间超限</td>
<td>可通过 <a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1">提交工单</a> 提升配额限制。</td>
</tr>
</tbody></table>








