GPU Cloud Computing is a rapid, stable and flexible computing service based on GPU, and is applicable to deep learning training/reasoning, graphic/image processing and scientific computing. It is managed easily in the same way as with standard CVM. With its powerful computing capability of processing mass data in a rapid manner, GPU Cloud Computing can effectively relieve the user's computing pressure, improving the efficiency and competitiveness of business processing.

## Why GPU Cloud Computing?
Comparison between GPU Cloud Computing and Self-built GPU Cloud Computing:
<table class="npf-comparsion-table">
	<colgroup>
		<col class="col2" style="width: 6%;" />
		<col class="col3" style="width: 54%;" />
		<col class="col4" style="width: 40%;" />
	</colgroup>
	<thead>
		<tr>
			<th>
			<div>Advantages</div>
			</th>
			<th class="stress-item">
			<div class="gradient ">Tencent Cloud GPU Instance</div>
			</th>
			<th>
			<div>Custumer GPU-based Servers</div>
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>
			<div><span class="unit-text">Elastic</span></div>
			</td>
			<td class="stress-item">
			<div>
			
<ul class="text-list">
	<li>In just a few minutes, you can easily obtain one or more high-performance computing instances. </li>
	<li>It can be customized flexibly as needed, and upgraded to an instance specification with higher performance and larger capacity with just one click, to achieve rapid, smooth expansion, and satisfy the requirement for fast business development.</li>
<ul>
			</div>
			</td>
			<td>
			<div><span class="unit-text">Fixed configuration makes it hard to satisfy the ever-changing requirements.</span></div>
			</td>
		</tr>
		<tr>
			<td>
			<div><span class="unit-text">High-performance</span></div>
			</td>
			<td class="stress-item">
			<div>
			
<ul class="text-list">
	<li>It supports GPU pass-through to make the best use of GPU performance. </li>
	<li>Peak computing capacity for single machine: 125.6T Flops for single-precision floating point computing and 62.4T Flops for double-precision floating point computing.</li>
<ul>
			</div>
			</td>
			<td>
			<div>
			<ul class="text-list">
	<li>Users have to perform disaster recovery manually, depending on the robustness of hardware. </li>
	<li>Single point of failure may occur on physical server. Data security is uncontrollable. </li>
<ul>
			</div>
			</td>
		</tr>
		<tr>
			<td>
			<div><span class="unit-text">Ease of Use</span></div>
			</td>
			<td class="stress-item">
			<div>
			<ul class="text-list">
	<li>Seamless connection with CVM, CLB and many other Tencent Cloud products. Private network traffic is free of charge. </li>
	<li>Designed for ease of use, it is managed in the same way as with CVM, without the need to use jump server for login. </li>
	<li>It provides clear guides on installation and deployment of GPU driver to make it easier for users to get started with it. </li>
<ul>
			</div>
			</td>
			<td>
			<div>
						<ul class="text-list">
	<li>Users must purchase installation management service to achieve automatic hardware expansion and driver installation. </li>
	<li>Jump server is required for login with complicated operation procedures. </li>
<ul>
			</div>
			</td>
		</tr>
		<tr>
			<td>
			<div><span class="unit-text">Secure</span></div>
			</td>
			<td class="stress-item">
			<div>
						<ul class="text-list">
	<li>Resources are completely isolated among different users to ensure the data security.</li>
	<li>Complete security groups and network ACL settings allow you to control and securely filter the inbound and outbound network traffic to or from instances and subnets. </li>
	<li>It can be seamlessly connected to Cloud Security, and has the basic protection and high defense services of Cloud Security equivalent to that of CVM. </li>
<ul>
			</div>
			</td>
			<td>
			<div>
			<ul class="unit-text">
			<li>Resources are shared among different users, and data is not isolated. </li>
			<li>Additional security protection services must be purchased. </li>
			<ul>
			</div>
			</td>
		</tr>
		<tr>
			<td>
			<div><span class="unit-text">Low-cost</span></div>
			</td>
			<td class="stress-item stress-last-item">
			<div>
<ul class="unit-text">
			<li>It supports the prepaid billing method. You can purchase physical servers without the need to make a huge one-off investment. </li>
			<li>Hardware is updated with the mainstream GPU, eliminating the need to replace the hardware after each update. </li>
			<li>With low server OPS cost, you can effectively reduce investment in infrastructure construction without the need to purchase and prepare hardware resources in advance.</li>
			<ul>
			</div>
			</td>
			<td>
			<div>
			<ul class="unit-text">
			<li>The cost for the server OPS is high. </li>
			<li>Due to high power consumption of devices, hardware modification is required. </li>
			<li>Higher IT OPS cost is required to guarantee the stability of service. </li>
			<ul>
			</div>
			</td>
		</tr>
	</tbody>
</table>


Comparison between GPU Instance and CPU Instance
![](//mc.qcloudimg.com/static/img/ac3ea7314a71758f5c7caef08ec63692/image.jpg)

<table class="table" contenteditable="true">
	<thead>
		<tr>
			<th>Dimension</th>
			<th>GPU</th>
			<th>CPU</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>Kernels</td>
			<td>Thousands of accelerated kernels (dual ENI, M40, and up to 6,144 accelerated kernels)</td>
			<td>Dozens of kernels</td>
		</tr>
		<tr>
			<td>Product features</td>
			<td>1. Numerous efficient arithmetic logic units (ALU) support parallel processing<br />
			2. Massively parallel throughput can be achieved using multiple threads<br />
			3. Simple logic control</td>
			<td>1. Complex logic control unit<br />
			2. Powerful ALUs<br />
			3. Simple logic control</td>
		</tr>
		<tr>
			<td>Use Cases</td>
			<td>Compute-intensive applications that support parallel processing</td>
			<td>Applications with logic control and serial arithmetic</td>
		</tr>
	</tbody>
</table>



