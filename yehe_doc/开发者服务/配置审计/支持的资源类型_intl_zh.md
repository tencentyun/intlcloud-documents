
配置审计支持以下云服务的资源类型。如您需求系统支持更多的资源类型，可[提交工单](https://console.intl.cloud.tencent.com/workorder/category)进行申请。

<table>
<thead>
<tr>
<th>云服务</th>
<th>资源类型</th>
<th>关系类型</th>
<th>关联资源类型</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="5">云服务器CVM</td>
<td  rowspan="4">云服务器-实例<br/>QCS::CVM::Instance</td>
<td>关联 <br/>is related to</td>
<td>私有网络-安全组 <br/>QCS::VPC::SecurityGroup</td>
</tr>
<tr><td>挂载 <br/>attachs</td>
<td>云服务器-云硬盘 <br/>QCS::CBS::Disk</td>
</tr>
<tr><td>被包含 <br/>is contained in</td>
<td>私有网络-私有网络 <br/>QCS::VPC::Vpc</td>
</tr>
<tr><td>被包含 <br/>is contained in</td>
<td>私有网络-子网 <br/>QCS::VPC::Subnet</td>
</tr>
<tr><td>云服务器-云硬盘<br/>QCS::CBS::Disk</td>
<td>挂载 <br/>attachs</td>
<td>云服务器-实例 <br/>QCS::CVM::Instance</td>
</tr>
<tr>
<td rowspan="8">访问管理CAM</td>
<td  rowspan="2">访问管理-用户<br/>QCS::CAM::User</td>
<td>绑定  <br/>attachs</td>
<td>访问管理-用户组 <br/>QCS::CAM::Group</td>
</tr>
<tr><td>绑定  <br/>attachs</td>
<td>访问管理-策略 <br/>QCS::CAM::Policy</td>
</tr>
<tr><td  rowspan="2">访问管理-用户组<br/>QCS::CAM::Group</td>
<td>包含   <br/>contains</td>
<td>访问管理-用户 <br/>QCS::CAM::User</td>
</tr>
<tr><td>绑定  <br/>attachs</td>
<td>访问管理-策略 <br/>QCS::CAM::Policy</td>
</tr>
<tr><td>访问管理-角色<br/>QCS::CAM::Role</td>
<td>绑定  <br/>attachs</td>
<td>访问管理-策略 <br/>QCS::CAM::Policy</td>
</tr>
<tr><td  rowspan="3">访问管理-策略<br/>QCS::CAM::Policy</td>
<td>绑定  <br/>attachs</td>
<td>访问管理-用户 <br/>QCS::CAM::User</td>
</tr>
<tr><td>绑定  <br/>attachs</td>
<td>访问管理-用户组 <br/>QCS::CAM::Group</td>
</tr>
<tr><td>绑定  <br/>attachs</td>
<td>访问管理-角色 <br/>QCS::CAM::Role</td>
</tr>
<tr>
<td rowspan="4">私有网络VPC</td>
<td rowspan="2">私有网络-私有网络<br/>QCS::VPC::Vpc</td>
<td>包含 <br/>contains</td>
<td>云服务器-实例 <br/>QCS::CVM::Instance</td>
</tr>
<tr><td>包含 <br/>contains</td>
<td>私有网络-子网 <br/>QCS::VPC::Subnet</td>
</tr>
<tr><td>私有网络-安全组<br/>QCS::VPC::SecurityGroup</td>
<td>关联 <br/>is related to</td>
<td>云服务器-实例 <br/>QCS::CVM::Instance</td>
</tr>
<tr><td>私有网络-子网<br/>QCS::VPC::Subnet</td>
<td>被包含 <br/>is contained in</td>
<td>私有网络-私有网络 <br/>QCS::VPC::Vpc</td>
</tr>
<tr>
<td>对象存储COS</td>
<td>对象存储-存储桶<br/>QCS::COS::Bucket</td>
<td>NA</td>
<td>NA</td>
</tr>
<tr>
</table>
