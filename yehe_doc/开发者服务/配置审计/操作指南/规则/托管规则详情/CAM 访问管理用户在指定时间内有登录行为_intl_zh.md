﻿**规则含义：**检查 CAM 访问管理用户在指定时间内是否有登录行为
**合规检测逻辑：**帐号访问管理中，用户在指定时间内若有登录行为，则符合规则
**规则标识符：**`cam-user-logged-in`
**风险等级：**中
**适用的资源类型：**`QCS::CAM::User`
**规则触发类型：**周期执行，24小时
**关键词：**用户，登录
**规则入参：**

<table>
<thead>
<tr>
<th>参数名称</th>
<th>默认值</th>
<th>关系</th>
</tr>
</thead>
<tbody>
<tr>
<td >days</td>
<td>90</td>
<td>小于等于</td>
</tr>
</table>


