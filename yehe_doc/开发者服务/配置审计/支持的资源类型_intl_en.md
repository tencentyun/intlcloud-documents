
Config supports the following Tencent Cloud resource types. If you want more resource types to be supported, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.

<table>
<thead>
<tr>
<th>Tencent Cloud Service</th>
<th>Resource Type</th>
<th>Relationship</th>
<th>Associated Resource Type</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="5">CVM</td>
<td  rowspan="4">CVM - InstanceQCS::CVM::Instance</td>
<td>is associated with</td>
<td>VPC - Security group QCS::VPC::SecurityGroup</td>
</tr>
<tr><td>attaches</td>
<td>CVM - CBS QCS::CBS::Disk</td>
</tr>
<tr><td>is contained in</td>
<td>VPC - VPC QCS::VPC::Vpc</td>
</tr>
<tr><td>is contained in</td>
<td>VPC - Subnet QCS::VPC::Subnet</td>
</tr>
<tr><td>CVM - CBSQCS::CBS::Disk</td>
<td>attaches</td>
<td>CVM - Instance QCS::CVM::Instance</td>
</tr>
<tr>
<td rowspan="8">CAM</td>
<td  rowspan="2">CAM - UserQCS::CAM::User</td>
<td>attaches</td>
<td>CAM - User group QCS::CAM::Group</td>
</tr>
<tr><td>attaches</td>
<td>CAM - Policy QCS::CAM::Policy</td>
</tr>
<tr><td  rowspan="2">CAM - User groupQCS::CAM::Group</td>
<td>contains</td>
<td>CAM - User QCS::CAM::User</td>
</tr>
<tr><td>attaches</td>
<td>CAM - Policy QCS::CAM::Policy</td>
</tr>
<tr><td>CAM - RoleQCS::CAM::Role</td>
<td>attaches</td>
<td>CAM - Policy QCS::CAM::Policy</td>
</tr>
<tr><td  rowspan="3">CAM - PolicyQCS::CAM::Policy</td>
<td>attaches</td>
<td>CAM - User QCS::CAM::User</td>
</tr>
<tr><td>attaches</td>
<td>CAM - User group QCS::CAM::Group</td>
</tr>
<tr><td>attaches</td>
<td>CAM - Role QCS::CAM::Role</td>
</tr>
<tr>
<td rowspan="4">VPC</td>
<td rowspan="2">VPC - VPC QCS::VPC::Vpc</td>
<td>  contains</td>
<td>CVM - Instance QCS::CVM::Instance</td>
</tr>
<tr><td>contains</td>
<td>VPC - Subnet QCS::VPC::Subnet</td>
</tr>
<tr><td>VPC - Security group QCS::VPC::SecurityGroup</td>
<td> is associated with</td>
<td>CVM - Instance QCS::CVM::Instance</td>
</tr>
<tr><td>VPC - Subnet QCS::VPC::Subnet</td>
<td> is contained in</td>
<td>VPC - VPC QCS::VPC::Vpc</td>
</tr>
<tr>
<td>COS</td>
<td>COS - BucketQCS::COS::Bucket</td>
<td>N/A</td>
<td>N/A</td>
</tr>
<tr>
</table>