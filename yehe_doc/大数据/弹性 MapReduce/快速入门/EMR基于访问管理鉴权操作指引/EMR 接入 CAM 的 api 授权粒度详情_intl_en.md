## List of APIs supporting resource-level authorization
EMR supports resource-level authorization. You can grant a specified sub-account the API permission of a specified resource.

>!A permission error may occur when new APIs are subsequently added. In case of such permission error, you can add the missing API permission in the policy based on the error message.

APIs supporting resource-level authorization include:
<table>
<thead>
<tr>
<th width="25%">API</th>
<th width="30%">Description</th>
<th width="45%">Resource Type/Six-Segment Example of Resource</th>
</tr>
</thead>
<tbody>
<tr>
<td >DescribeKeyTabFile</td>
<td >Exports keytab file (user management)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeShowUserManagerTab</td>
<td >Specifies whether to show the user management tab (user management)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeResourceSchedule</td>
<td >Gets data from the YARN resource scheduling page</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeCamUserList</td>
<td >Queries CAM user list</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeClusterServiceInfo</td>
<td >Queries service information</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeUserManagerUserList</td>
<td >Queries user list (user management)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyUserManagerPwd</td>
<td >Changes user password (user management)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyResourcePools</td>
<td >Refreshes dynamic resource pool</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DeleteUserManagerUserList</td>
<td >Deletes user (user management)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyResourceScheduler</td>
<td >Modifies the YARN resource scheduler (the change will take effect after you click **Apply**)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyResourceScheduleSwitch</td>
<td >After this switch is turned on, the configuration file of resource scheduling needs to be synced to the resource scheduler first before the resource scheduler page can be viewed and operations can be performed on the page</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >AddUserManagerUserList</td>
<td >Adds user (user management)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyUserManagerInfo</td>
<td >Modifies user information (user management)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyResourceScheduleConfig</td>
<td >Modifies the resource configuration of YARN resource scheduling</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyResourceScheduleConfigForRollback</td>
<td >Cancels saving the resource configuration of YARN resource scheduling</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >InquirePriceRefundEmr</td>
<td >Queries the refund amount of terminated node</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifySecurityGroup</td>
<td >Modifies cluster security group</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeInstanceRenewNodes</td>
<td >Queries renewed nodes of EMR cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >InquirePriceRenewEmr</td>
<td >Queries cluster price for renewal</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeInstancesList</td>
<td >Queries the list of EMR cluster instances</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyFlowStatus</td>
<td >Changes workflow status</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyMasterIp</td>
<td >Updates EMR cluster IP</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >CheckFlowCanBeCancelled</td>
<td >Checks whether the workflow can be canceled</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeModifySpec</td>
<td >Queries target specification</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >AddShellScriptTask</td>
<td >Generates cluster script task</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeShellScriptTaskList</td>
<td >Queries the list of cluster script tasks</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeShellScriptNodes</td>
<td >Queries the list of nodes in a single cluster script task</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeNodeList</td>
<td >Views node information</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeNodeList</td>
<td >Views node information</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeShellScriptNodeDetails</td>
<td >Queries the detailed execution result of cluster script task on a single node</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DeleteShellScriptList</td>
<td >Deletes the records of cluster script tasks</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeMasterIp</td>
<td >Gets EMR cluster instance IP</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeEKSInstances</td>
<td >Queries the API information of TKE cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >AddServiceConfFile</td>
<td >Adds custom configuration file</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DeleteServiceConfFile</td>
<td >Deletes custom configuration file</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyBootScript</td>
<td >Modifies bootstrap script</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeInstanceAlias</td>
<td >Gets alias</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeBootScript</td>
<td >Gets bootstrap script</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeSubJobFlowStatus</td>
<td >Describes EMR subtask workflow</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ListConfLogs</td>
<td >Gets configuration delivery logs</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >GenerateScaleoutGoodsDetail</td>
<td >Generates scale-out order</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >GenerateRenewGoodsDetail</td>
<td >Generates renewal order</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >GenerateModifyGoodsDetail</td>
<td >Generates configuration adjustment order</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyAutoScaleGlobalConf</td>
<td >Updates the global configuration of auto scaling</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeFlowStatusDetail</td>
<td >Queries EMR task execution details</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeFileIps</td>
<td >Queries the list of IPs of the specified configuration file</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeExportConfsList</td>
<td >Queries the list of exportable configuration files</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeFlowStatus</td>
<td >Queries the EMR instance workflow status</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeFlowNum</td>
<td >Queries the number of workflows in EMR cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeClusterNodes</td>
<td >Queries the hardware node information of EMR cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ClearMetadata</td>
<td >Clears the metadata information of EMR cluster and terminates cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeAutoScaleGlobalConf</td>
<td >Gets the global configuration of auto scaling</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeAutoScaleSpecs</td>
<td >Gets auto scaling specification</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyAutoScaleSpecs</td>
<td >Modifies auto scaling specification</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >AddMetricScaleStrategy</td>
<td >Adds metric load-based scaling rule</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DeleteAutoScaleSpec</td>
<td >Deletes auto scaling specification</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeAutoScaleRecords</td>
<td >Gets auto scaling history</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DeleteAutoScaleStrategy</td>
<td >Deletes auto scaling rule</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyStrategyPriority</td>
<td >Changes rule priority</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeAutoScaleMetaRange</td>
<td >Gets auto scaling metadata</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeAutoScaleStrategies</td>
<td >Gets auto scaling rules</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyAutoScaleStrategy</td>
<td >Modifies auto scaling rule</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >AddAutoScaleSpec</td>
<td >Adds auto scaling specification</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >TerminateAutoScaleNodes</td>
<td >Terminates all automatically scaled nodes</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeCbsEncrypt</td>
<td >Describes CBS encryption</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyConfigGroup</td>
<td >Modifies configuration group</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DeleteConfigGroup</td>
<td >Deletes configuration group</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >AddConfigGroup</td>
<td >Adds configuration group</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeConfigGroup</td>
<td >Describes configuration group</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >SynchronizeGroupConfCheck</td>
<td >Syncs configuration check</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >UnbindInstanceAndNodesTags</td>
<td >Unbinds cluster from labels</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeNodeResourceConfigFast</td>
<td >Quickly gets node specification configuration</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >InstallCos</td>
<td >Enables COS upon installation</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeScaleoutableService</td>
<td >Describes services that can be scaled out</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeNodeResourceConfig</td>
<td >Gets node specification configuration</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DeleteNodeResourceConfig</td>
<td >Deletes node specification configuration</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >AddNodeResourceConfig</td>
<td >Adds node specification configuration</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >SetNodeResourceConfigDefault</td>
<td >Sets the default attributes of node specification configuration</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeHbaseTableMetricDataOverview</td>
<td >Gets HBase table-level monitoring data overview</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeInstanceNode</td>
<td >Pulls node resources from the Tag console</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >UpdateWebproxyPassword</td>
<td >Updates the password of proxy component</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >TerminateTasks</td>
<td >Terminates task nodes</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >TerminateNodes</td>
<td >Terminates nodes</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >TerminateInstance</td>
<td >Terminates EMR instance</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >StopService</td>
<td >Stops component service</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >StopMonitor</td>
<td >Stops component monitoring</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >StartService</td>
<td >Starts component service</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >StartMonitor</td>
<td >Starts component monitoring</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ScaleOutRouter</td>
<td >Adds router nodes</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeDestroyInfo</td>
<td >Queries the termination information of EMR cluster or node</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ScaleOutInstance</td>
<td >Scales out instance</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >RollBackConf</td>
<td >Rolls back configuration</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >RestartService</td>
<td >Restarts component service</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyServiceParams</td>
<td >Modifies service component parameters</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyResource</td>
<td >Adjusts instance configuration</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >AssignInstancesProject</td>
<td >Assigns EMR cluster to specified project</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyOptionalSpecStatus</td>
<td >Changes the status of optional specification</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyOptionalSpec</td>
<td >Modifies optional specification</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeSelectedOptionalSpec</td>
<td >Queries selected optional specification</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyInstanceBasic</td>
<td >Renames cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >InstallSoftware</td>
<td >Installs component</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >InquiryPriceAddRouter</td>
<td >Queries the price of router adding</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >InquiryPriceRenewInstance</td>
<td >Queries the price for renewal</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >InquiryPriceUpdateInstance</td>
<td >Queries the price for configuration adjustment</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >InquiryPriceScaleOutInstance</td>
<td >Queries the price for scale-out</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribleClusterNodes</td>
<td >Queries the hardware node information of EMR cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeServiceNodeInfos</td>
<td >Queries the service process information of EMR cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeServiceGroups</td>
<td >Queries the service group information of EMR cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeServiceConfs</td>
<td >Queries all configuration information of the EMR cluster service</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeScaleoutGoodsDetail</td>
<td >Queries scale-out order</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeRouterGoodsDetail</td>
<td >Queries router node order</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeRenewGoodsDetail</td>
<td >Queries renewal order</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeOptionalSpec</td>
<td >Queries the optional specifications of EMR instance node</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeModifyGoodsDetail</td>
<td >Queries configuration adjustment order</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeMetricsDimension</td>
<td >Queries the dimension values of monitoring at different levels</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeMetricMeta</td>
<td >Queries the monitoring metadata of EMR cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeInstanceOplog</td>
<td >Queries the operation log of EMR instance</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeExecCustomScript</td>
<td >Queries the information of custom script</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeInstanceAlerts</td>
<td >Queries the alarm information of EMR cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeInstances</td>
<td >Queries the information of EMR instances</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeInstallSoftwareInfo</td>
<td >Queries the information of components installed and uninstalled for EMR cluster</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeExportConfs</td>
<td >Queries export configuration</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td >CheckDiskInfo</td>
<td >Checks whether the disk metadata in the console is updated</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td >SyncDiskInfo</td>
<td >Updates disk metadata in console</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td >DescribeServiceConfsNew</td>
<td >Gets the configuration information of component (configuration management page)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td >DescribeConfFileList</td>
<td >Gets the list of configuration files (configuration management page)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td >DescribeServiceConfCategories</td>
<td > Gets the configuration type of component (configuration management page)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td >DescribeServiceConfDiff</td>
<td > Compares configurations (configuration management page)</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td >DescribeConfigGroupList</td>
<td > Queries the configuration group information of node type</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeHbaseStatus</td>
<td > Displays the information of `DescribeHbaseStatus`</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >ModifyHbaseRit</td>
<td >	Fixes HBase RIT issue</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >TerminateSparkApp</td>
<td >	Terminates Spark job</td>
<td >emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr><tr>
<td >DescribeAccessKey</td>
<td >	Gets the `AccessKey` of cluster</td>
<td >	emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeAttachableDisks</td>
<td>Queries the cloud disks that can be mounted to the node</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>InquirePriceRenewDisks</td>
<td>Queries the price for cloud disk renewal</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>AttachDisks</td>
<td>Mounts cloud disk</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeNodeDataDisks</td>
<td>Queries the data disk information of node</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>InquirePriceResizeDisks</td>
<td>Queries the price for cloud disk expansion</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ResizeDataDisks</td>
<td>Expands cloud disk</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ModifyAutoRenewFlag</td>
<td>Automatic Renewal</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ScaleOutCluster</td>
<td>Adds cluster nodes</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>StartStopServiceOrMonitor</td>
<td>Starts or stops monitoring or service</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeClusterClients</td>
<td>Views the client information on the page</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeDelayedServiceConfig</td>
<td>Gets expired configuration (configuration management page)</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeFailedServiceConfig</td>
<td>Gets failed configuration (configuration management page)</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeServiceConfDimensionDiff</td>
<td>Compares the configurations at different levels (configuration management page)</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ModifyEmrManagerAgent</td>
<td>Updates EMR Manager Agent</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ModifyServiceConfDiff</td>
<td>Overwrites different configuration (configuration management)</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ModifyYarnLabelState</td>
<td>Delivers an instruction to add, delete, or bind a label</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeYarnScheduleHistory</td>
<td>Views the YARN resource scheduling history</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeYarnDeployMessage</td>
<td>Gets the prompt message</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ModifyYarnDeploy</td>
<td>Applies deployment</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeParentLabels</td>
<td>Gets the list of labels of the parent queue</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeYarnLastestLabels</td>
<td>Gets the latest label information</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ModifyYarnLabels</td>
<td>Syncs YARN node labels</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ModifyYarnQueue</td>
<td>Modifies the resource pool in resource scheduling</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ModifyOldLabelConfig</td>
<td>Cancels saving the edited content in YARN label management</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeNodeLabelWebUrl</td>
<td>Gets the web URL of YARN node labels</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeNodeManagerHosts</td>
<td>Gets the list of NodeManager IPs</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ModifyGlobalScaleConf</td>
<td>Modifies the scaling configuration of cluster, including whether to enable scaling and the scaling type</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeGlobalScaleConf</td>
<td>Gets the scaling configuration of cluster, including whether to enable scaling and the scaling type</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>ModifyManagedScaleGlobalConf</td>
<td>Updates the global configuration of managed scaling</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeManagedScaleGlobalConf</td>
<td>Gets the global configuration of managed scaling</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeServiceComponentInfos</td>
<td>Describes the role information of container cluster</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DescribeRssClusterList</td>
<td>Gets the RSS clusters in the same EKS cluster as the current Spark cluster</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>CreateSparkLinkRss</td>
<td>Associates RSS cluster with Spark cluster</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
<tr>
<td>DeleteSparkLinkRss</td>
<td>Disassociates RSS cluster from Spark cluster</td>
<td>emr-instance|qcs::emr:${region}:uin/${uin}:emr-instance/$emrInstanceId</td>
</tr>
</tbody>
</table>


## List of APIs supporting API-level authorization
<table>
<thead>
<tr>
<th width="50%">API</th>
<th width="50%">Description</th>
</tr>
</thead>
<tbody>
<tr>
<td >RunJobFlow</td>
<td >Creates and runs job</td>
</tr><tr>
<td >DescribeJobFlow</td>
<td >Queries running jobs</td>
</tr><tr>
<td >DescribeK8sResourcePrice</td>
<td >Queries the price of K8s resource</td>
</tr><tr>
<td >DescribePodSpecs</td>
<td >Describes Pod specification</td>
</tr><tr>
<td >GenerateCreateGoodsDetail</td>
<td >Generates cluster creation order</td>
</tr><tr>
<td >DescribeLogSearchFileNames</td>
<td >Gets the list of log search files</td>
</tr><tr>
<td >DescribeInstanceServiceRoleNames</td>
<td >Gets service role names</td>
</tr><tr>
<td >DescribeCompareMetricsList</td>
<td >Gets the list of comparison metrics</td>
</tr><tr>
<td >DescribeHeatMapMetricList</td>
<td >Returns the list of metrics in the aggregated cluster server dimension</td>
</tr><tr>
<td >DescribeHBaseRegionList</td>
<td >Gets the list of HBase regions</td>
</tr><tr>
<td >DescribeClusterOverview</td>
<td >Queries cluster overview</td>
</tr><tr>
<td >DescribeEMRNodeOverview</td>
<td >Queries the deployment status of various processes on node</td>
</tr><tr>
<td >DescribeNodeHardwareInfo</td>
<td >Queries the basic configuration of the host</td>
</tr><tr>
<td >DescribeTopNMeta</td>
<td >Gets the top N metadata information items</td>
</tr><tr>
<td >DescribeMetricDataAutoGranularity</td>
<td >Gets monitoring data and automatically sets time granularity</td>
</tr><tr>
<td >DescribeLogSearchTabs</td>
<td >Gets log search tabs</td>
</tr><tr>
<td >DescribeEMRHostOverview</td>
<td >Queries the process status on the host details page</td>
</tr><tr>
<td >DescribeLogSearchRecords</td>
<td >Gets log search content</td>
</tr><tr>
<td >DescribeTopNByProcess</td>
<td >Gets the top N processes</td>
</tr><tr>
<td >DescribeDiskInfo</td>
<td >Returns specific disk information</td>
</tr><tr>
<td >DescribeTopNByHost</td>
<td >Queries the top N hosts on the overview page</td>
</tr><tr>
<td >DescribeHeatMapDistribution</td>
<td >Returns the heat map data of cluster</td>
</tr><tr>
<td >DescribeInstanceServiceRoleTable</td>
<td >Gets the data of service role table</td>
</tr><tr>
<td >DescribeNodeAlias</td>
<td >Gets the alias of EMR node</td>
</tr><tr>
<td >DescribeInstanceNodes</td>
<td >Gets the host information of cluster</td>
</tr><tr>
<td >DescribeKeyPairs</td>
<td >Queries the information of key pairs</td>
</tr><tr>
<td >DescribeHbaseTableMetricData</td>
<td >Queries HBase table-level monitoring data</td>
</tr><tr>
<td >DescribeKeyPairs</td>
<td >Queries the information of key pairs</td>
</tr><tr>
<td >DescribeEmrMetaDB</td>
<td >Gets the unified metadatabase information of Hive</td>
</tr><tr>
<td >ModifyEmrRole</td>
<td >Updates the information of EMR role</td>
</tr><tr>
<td >DescribeDisasterRecoverGroup</td>
<td >Gets the information of spread placement group</td>
</tr><tr>
<td >DescribeTags</td>
<td >Pulls all labels of cluster</td>
</tr><tr>
<td >InquiryPriceCreateInstance</td>
<td >Queries the price of created instance</td>
</tr><tr>
<td >DescribleAccountBalance</td>
<td >Queries account balance</td>
</tr><tr>
<td >DescribeSecurityGroup</td>
<td >Gets the information of EMR security group</td>
</tr><tr>
<td >DescribeCvmSpec</td>
<td >Queries CVM instance specification</td>
</tr><tr>
<td >DescribeCdbPrice</td>
<td >Queries the price of TencentDB instance</td>
</tr><tr>
<td >CreateInstance</td>
<td >Creates EMR instance</td>
</tr><tr>
<td >GetMetricDataForMcController</td>
<td >Gets the monitoring information on the details page in the console</td>
</tr><tr>
<td >DescribeVpcList</td>
<td >Queries the list of VPCs</td>
</tr><tr>
<td >DescribeSceneProductInfo</td>
<td >Gets the cluster use case, type, product, and component information from the purchase page</td>
</tr><tr>
<td >DescribeRegionAndZoneSaleInfo</td>
<td >Gets the region and AZ information from the console and the purchase page</td>
</tr><tr>
<td >DescribeCgwProjects</td>
<td >Gets the list of CGW projects</td>
</tr><tr>
<td >DescribeServiceUpgradeVersion</td>
<td >View the service minor version that can be upgraded</td>
</tr><tr>
<td >ModifyServiceVersion</td>
<td >Upgrades service minor version</td>
</tr><tr>
<td >DescribeServiceRoleInstanceConstraints</td>
<td >Gets the constraint information of role instances removed from the service</td>
</tr><tr>
<td >CheckSupportServiceRoleInstance</td>
<td >Checks whether a role instance can be added to the service</td>
</tr><tr>
<td >DescribeServiceRoleNames</td>
<td >Gets the drop-down list of role names (or role types) of the service</td>
</tr><tr>
<td >DescribeServiceRoleInstanceDeployableNodes</td>
<td >Queries the list of nodes where the service role can be deployed</td>
</tr><tr>
<td >DescribeServiceDeletableRoleInstances</td>
<td >Queries the list of role instances that can be deleted from the service</td>
</tr><tr>
<td >DeleteServiceRoleInstance</td>
<td >Removes role instance</td>
</tr><tr>
<td >AddServiceRoleInstance</td>
<td >Adds role instance</td>
</tr>
<tr>
<td >ModifyResourcesTags</td>
<td >Forcibly modifies label</td>
</tr><tr>
<td >CreateCluster</td>
<td >Creates cluster</td>
</tr>
</tbody>
</table>

For more information on resource-level and API-level authorization, see [Authorization Granularity Scheme](https://intl.cloud.tencent.com/document/product/1026/44862).
