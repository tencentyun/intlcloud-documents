配置审计支持以下托管规则。如您需求系统支持更多的托管规则，可[提交工单](https://console.intl.cloud.tencent.com/workorder/category)进行申请。
<table>
<thead>
<tr>
<th>云服务</th>
<th>资源类型</th>
<th>托管规则</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan="11">访问管理CAM</td>
<td>访问管理-用户QCS::CAM::User</td>
<td><a href="https://www.tencentcloud.com/document/product/1164/51505">CAM访问管理用户必须开启敏感操作MFA</a></td>
</tr>
<td>访问管理-用户QCS::CAM::User</td>
<td><a href="https://www.tencentcloud.com/document/product/1164/51506">CAM访问管理用户必须开启登陆保护MFA</a></td>
</tr>
<tr>
<td>访问管理-用户组QCS::CAM::Group</td>
<td><a href="https://www.tencentcloud.com/document/product/1164/51507">CAM访问管理没有闲置用户组</a></td>
</tr>
<tr>
<td><ul><li>访问管理-用户QCS::CAM::User </li><li>访问管理-用户组QCS::CAM::Group</li></ul></td>
<td><a href="https://www.tencentcloud.com/document/product/1164/51508">CAM访问管理子帐号必须关联用户组</a></td>
</tr>
<tr>
<td>访问管理-用户QCS::CAM::User</td>
<td><a href="https://www.tencentcloud.com/document/product/1164/51509">CAM访问管理子帐号没有直接授权策略</a></td>
</tr>
<tr>
<td>访问管理-用户QCS::CAM::User</td>
<td><a href="https://www.tencentcloud.com/document/product/1164/51510">CAM访问管理用户，用户组，角色下不存在超级管理员权限</a></td>
</tr>
<tr>
<td><ul><li>访问管理-用户QCS::CAM::User</li>
<li>访问管理-用户组QCS::CAM::Group</li>
<li>访问管理-角色QCS::CAM::Role</li></ul>
</td>
<td><a href="https://www.tencentcloud.com/document/product/1164/51511">CAM访问管理不允许授权指定高风险权限</a></td>
</tr>
<tr>
<td>访问管理-策略QCS::CAM::Policy</td>
<td><a href="https://www.tencentcloud.com/document/product/1164/51512">CAM访问管理不存在闲置的权限策略</a></td>
</tr>
<tr>
<td>访问管理-策略QCS::CAM::Policy</td>
<td><a href="https://www.tencentcloud.com/document/product/1164/51513">CAM访问管理登陆权限检测</a></td>
</tr>
<tr>
<td>访问管理-用户QCS::CAM::User</td>
<td><a href="https://www.tencentcloud.com/document/product/1164/51514">CAM访问管理用户的密钥KEY在指定时间内轮换</a></td>
</tr>
<tr>
<td>访问管理-用户QCS::CAM::User</td>
<td><a href="https://www.tencentcloud.com/document/product/1164/51515">CAM访问管理用户在指定时间内有登录行为</a></td>
</tr>
<tr></tr>
<tr>
</tbody></table>
