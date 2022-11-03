
This document describes the default limits on the number of Pods in different VPC-CNI network modes.

## Limits on the Number of Pods with Shared ENI

The number of Pods with shared ENI is limited by the number of ENIs that can be bound to a node and the number of IPs that can be bound on a single ENI. By default, **the maximum number of Pod IPs on a single node with multiple ENIs = the maximum number of secondary ENIs that can be bound * the number of secondary IPs that can be bound on a single ENI**, and **the maximum number of Pod IPs on a single node with a single ENI = the number of secondary IPs that can be bound on a single ENI**. See the table below for details.
<table style="width:600px;">
<tr>
	<th style="width:30%">CPU Cores</th><th>1</th><th>2-6</th><th>8-10</th><th>>=12</th>
</tr>
<tr>
	<td>The maximum number of secondary ENIs that can be bound</td><td>1</td><td>3</td><td>5</td><td>7</td>
</tr>
<tr>
	<td>The number of secondary IPs that can be bound on a single ENI</td><td>5</td><td>9</td><td>19</td><td>29</td>
</tr>
<tr>
	<td>The maximum number of Pod IP addresses on a single node (with multiple ENIs)</td><td>5</td><td>27</td><td>95</td><td>203</td>
</tr>
<tr>
	<td>The maximum number of Pod IP addresses on a single node (with a single ENI)</td><td>5</td><td>9</td><td>19</td><td>29</td>
</tr>
</table>

>! Multi-ENI component versions are supported (v3.3 or later in non-static IP address mode, and v3.4 or later in static IP address mode).

The number of ENIs that can be bound to each model and the number of IPs that can be bound on a single ENI is slightly different. For details, see [Use Limits](https://intl.cloud.tencent.com/document/product/576/18527).

## Limits on the Number of Pods with Exclusive ENIs

The number of Pods with exclusive ENIs is only limited by the number of ENIs that can be bound to the node. It only supports some models such as S5, SA2, IT5 and SA3. See the table below for details.
<table style="width:600px;">
<tr>
<th style ="width:95px;height:45px;position:relative;font-weight:700;" valign="top"><div style="position:absolute;width:1px;height:115px;top:0;left:0;background-color: #d9d9d9;transform:rotate(-60deg);transform-origin:top;"></div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;CPU Cores<br>Model</th><th>1</th><th>2</th><th>4</th><th>>=8</th><th>>=128</th>
</tr>
<tr>
	<td>S5</td><td>4</td><td>9</td><td>19</td><td>39</td><td>23</td>
</tr>
<tr>
	<td>SA2</td><td>4</td><td>9</td><td>19</td><td>39</td><td>23</td>
</tr>
<tr>
	<td>IT5</td><td>4</td><td>9</td><td>19</td><td>39</td><td>23</td>
</tr>
<tr>
	<td>SA3</td><td>4</td><td>9</td><td>15</td><td>15</td><td>15</td>
</tr>
</table>


