Lighthouse is a new-gen cloud server product oriented to small and medium-sized enterprises (SMEs) and developers. It features light OPS and out-of-the-box usage, making it generally suitable for supporting low-load lightweight application scenarios with a moderate number of access requests, including small websites, web applications, blogs, forums, and cloud-based development, testing, and learning environments.

Lighthouse is easier to use than [CVM](https://intl.cloud.tencent.com/document/product/213/495). It simplifies the advanced concepts and features of CVM and integrates multiple Tencent Cloud services at one stop, enabling you to deploy, configure, and manage applications more conveniently and efficiently and offering you the best way to get started with Tencent Cloud.
>?
> - When creating a Lighthouse instance, you cannot specify the CPU model of the underlying physical server; instead, Tencent Cloud will randomly assign a physical CPU model that meets the selected package specification.
> - At the same specification level, Lighthouse has a CPU and memory performance comparable with that of [CVM](https://intl.cloud.tencent.com/document/product/213/11518).
>

The table below lists Lighthouse's strengths and main differences from CVM:
<table style="width:908px;">
<tr>
<th style="width:95px;height:45px;position:relative;font-weight:700;" valign="top" colspan="2"><div style="position:absolute;width:1px;height: 244px;top:0;left:0;background-color: #d9d9d9;transform: rotate(-76deg);transform-origin:top;"></div><div style="position:relative;left:150px">Product</div>Strength</th>
<th style="font-weight:700;">Lighthouse</th>
<th style="font-weight:700;">CVM</th>
</tr>
<tr>
<th style="font-weight:700;" colspan=2>More targeted user group</th>
<td>SMEs, developers, and cloud computing beginners</td>
<td>All cloud users</td>
</tr>
<tr>
<th style="font-weight:700;" colspan=2>More lightweight business scenarios</th>
<td>Lightweight low-load application scenarios with a moderate number of access requests:
<ul style="margin:-3px 0px">
<li>Corporate websites, personal websites, blogs, forums, ecommerce websites, and web application services</li>
<li>Personal cloud storage and image hosting services</li>
<li>WeChat Mini Program and Mini Game backend services</li>
<li>Cloud-Based development, testing, and learning environments</li>
</ul>
</td>
<td>All business scenarios</td>
</tr>
<tr>
<th style="font-weight:700;" rowspan=2>More favorable billing modes</th>
<th style="font-weight:700;">Selling method</th>
<td>Cost-Effective packages (combinations of computing/network/storage resources)</td>
<td>Flexible selection of computing/storage/network resources that are billed independently</td>
</tr>
<tr>
<th style="font-weight:700;">Network billing</th>
<td>High-Bandwidth traffic package</td>
<td>Fixed bandwidth/traffic usage</td>
</tr>
<tr>
<th style="font-weight:700;" rowspan=5>Simplified feature design</th>
<th style="font-weight:700;">Entry to cloud capabilities</th>
<td>Integrated, independent, and simplified console</td>
<td>Console for all business scenarios</td>
</tr>
<tr>
<th style="font-weight:700;">Application deployment</th>
<td>You can use it out of the box, which is preinstalled with the optimal combination of software stacks required by the corresponding application system, and the application and runtime environment installation and initial configuration are automatically completed</td>
<td>You usually need to deploy an application after creating an instance or use the Image Marketplace</td>
</tr>
<tr>
<th style="font-weight:700;">Image</th>
<td>Selected dedicated high-quality application images</td>
<td>Public image, custom image, shared image, and Image Marketplace</td>
</tr>
<tr>
<th style="font-weight:700;">Network</th>
<td>Network resources are automatically created, with no need to manually manage VPCs, subnets, public IPs, etc.</td>
<td>You need to create, configure, and manage networks by yourself</td>
</tr>
</table>

>?
>- Compared with CVM, the main limits of Lighthouse at the functional level include the following:
>  - After an instance is created, its public IP cannot be changed.
>  - Currently, cloud disks cannot be mounted as instance data disks.
>  - An instance supports the overall upgrade of the configuration (computing, storage, and network) on a package basis but not package downgrade. For more information, please see [Upgrading Instance Package](https://intl.cloud.tencent.com/document/product/1103/41407).
>  - Currently, it doesn't support generating ICP filing authorization codes.
>     For the specific use limits of Lighthouse, please see [Use Limits](https://intl.cloud.tencent.com/document/product/1103/41265).
>- There are certain limits on private network connectivity for Lighthouse. For more information, please see [Region and Network Connectivity](https://intl.cloud.tencent.com/document/product/1103/41266).
>


If you want to use more instance types, such as Memory Optimized, High I/O, Big Data, Bare Metal, and GPU/FPGA Heterogeneous Computing, to support your business scenarios such as high-concurrency websites, video encoding/decoding, large games, and complex distributed cluster applications, please use CVM. For more information, please see [Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).
