**规则含义：**检查 CAM 访问管理是否授权指定高风险权限
**合规检测逻辑：**帐号访问管理下的用户，用户组，角色，若没有授权指定的高风险权限，则符合规则
**规则标识符：**`cam-user-risky-policy-bound`
**风险等级：**低
**适用的资源类型：**`QCS::CAM::User`，`QCS::CAM::Group`，`QCS::CAM::Role`
**规则触发类型：**周期执行，24小时
**关键词：**用户，用户组，角色,策略
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
<td >policies</td>
<td>AdministratorAcces</td>
<td>包含</td>
</tr>
</table>
