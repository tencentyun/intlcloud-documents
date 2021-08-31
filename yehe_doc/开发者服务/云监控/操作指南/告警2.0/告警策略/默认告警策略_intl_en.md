## Overview

Currently, the default alarm policy is only supported for: CVM - basic monitoring, TencentDB for MongoDB, TencentDB for MySQL - CVM monitoring, TencentDB for Redis, CKafka - instance, and Elasticsearch Service.

- When you successfully purchase a Tencent Cloud service that supports the default policy for the first time, Cloud Monitor will automatically create the default alarm policy for you. For more information on the metrics/events supported by the default policy or alarm rules, please see the [default policy description](#step1).
- You can also manually create an alarm policy and set it as the default alarm policy. After the default policy is set, newly purchased instances will be automatically associated with the default policy without requiring manual addition.
  ![](https://main.qcloudimg.com/raw/acb5a0ed0f4f44b65a87337d910e17c1.png)

## Default Metric Description

 <span id="step1"></span>

  <table>
  	<tr>
  		<th>Tencent Cloud Service</th>
  		<th>Alarm Type</th>
  		<th>Metric/Event Name</th>
  		<th>Alarm Rule</th>
  	</tr>
  	<tr>
  		<td rowspan="5">CVM</td>
  		<td rowspan="4">Metric alarm</td>
  		<td>CPU utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >95%; the duration is 5 periods</td>
  	</tr>
  	<tr>
  		<td>Memory utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >95%; the duration is 5 periods</td>	
  	</tr>
  	<tr>
  		<td>Disk utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >95%; the duration is 5 periods</td>	
  	</tr>
  	<tr>
  		<td>Public bandwidth utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >95%; the duration is 5 periods</td>	
  	</tr>
  	<tr>
  		<td>Event alarm</td>
  		<td>Read-only disk</td>
  		<td>-</td>
  	</tr>
  	<tr>
  		<td rowspan="3">TencentDB <br>for MySQL - CVM monitoring</td>
  		<td rowspan="2">Metric alarm</td>
  		<td>Disk utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
  	</tr>
  	<tr>
  		<td>CPU utilization</td>
  		<td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
  	</tr>
  	<tr>
  		<td>Event alarm</td>
  		<td>OOM</td>
  		<td>-</td>
  	</tr>
  	    <td rowspan="2">TencentDB for <br>MongoDB</td>
  	    <td rowspan="2">Metric alarm</td>
  	    <td>Disk utilization</td>
  	    <td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
      </tr>
      <tr>
      	<td>Connection utilization</td>
      	<td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
      </tr>
      <tr>
      	<td nowrap="nowrap">TencentDB for Redis: <br>CKV version/community version</td>
      	<td>Metric alarm</td>
      	<td>Capacity utilization</td>
      	<td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
      </tr>
      <tr>
          <td>CKafka: <br>instance</td>
          <td>Metric alarm</td>
      	<td>Disk utilization</td>
      	<td>The measurement period is 1 minute; the threshold is >85%; the duration is 5 periods</td>
      </tr>
      <tr>
      	<td rowspan="4">Elasticsearch Service</td>
      	<td rowspan="4">Metric alarm</td>
      	<td>Average disk utilization</td>
      	<td>The measurement period is 1 minute; the threshold is >80%; the duration is 5 periods</td>
     </tr>
     <tr>
     	    <td>Average CPU utilization</td>
     	    <td>The measurement period is 1 minute; the threshold is >90%; the duration is 5 periods</td>
     </tr>
     <tr>
     	    <td>Average JVM memory utilization</td>
     	    <td>The measurement period is 1 minute; the threshold is >85%; the duration is 5 periods</td>
     </tr>
     <tr>
     	    <td>Cluster health</td>
     	    <td>The measurement period is 1 minute; the threshold is >=1; the duration is 5 periods</td>
     </tr>
  </table>