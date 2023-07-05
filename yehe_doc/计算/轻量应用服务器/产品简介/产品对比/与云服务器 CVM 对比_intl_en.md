Compared with [CVM](https://intl.cloud.tencent.com/document/product/213/495), Lighthouse is easier to use and more suitable for SMEs, developers, cloud computing beginners, and students, as it simplifies CVM's advanced concepts and features. It offers high-bandwidth data transfer plans and integrates basic cloud services into cost-effective bundles. Such bundles contain popular open-source software programs perfect for lightweight use cases with low to medium load and moderate access requests, such as small and mid-sized websites, web applications, blogs, forums, mini games, ecommerce, cloud storage, and image hosting, as well as development, testing, and learning environments in the cloud.

<dx-alert infotype="explain" title="">
- When creating a Lighthouse instance, you cannot specify the CPU model of the underlying physical server; instead, Tencent Cloud will randomly assign a physical CPU model that meets the selected bundle specification.
- At the same specification level, Lighthouse has a CPU and memory performance comparable with that of [CVM](https://intl.cloud.tencent.com/document/product/213/11518).
</dx-alert>



The table below lists Lighthouse's strengths and main differences from CVM:
<table style="width:908px;">
<tr>
<th style="width:95px;height:45px;position:relative;font-weight:700;" valign="top" colspan="2"><div style="position:absolute;width:1px;height: 244px;top:0;left:0;background-color: #d9d9d9;transform: rotate(-76deg);transform-origin:top;"></div><div style="position:relative;left:150px">Product</div>Strength</th>
<th style="font-weight:700;">Lighthouse</th>
<th style="font-weight:700;">CVM</th>
</tr>
<tr>
<th style="font-weight:700;" colspan=2>Target user</th>
<td>SMEs and individual developers</td>
<td>Large enterprises</td>
</tr>
<tr>
<th style="font-weight:700;" colspan=2>Lightweight scenario-oriented</th>
<td>Lightweight use cases:
<ul style="margin:-3px 0px">
<li>Enterprise websites, blogs, forums, news, and product display</li>
<li>General web applications</li>
<li>WeChat mini programs and mini games</li>
<li>Mobile apps, H5 apps, and WeChat Official Account</li>
<li>E-commerce shops, individual websites</li>
<li>Cloud storage and image hosting services</li>
<li>Cloud-based development, testing, and learning environments</li>
</ul>
</td>
<td>Use cases with complex architectures:
<ul style="margin:-3px 0px">
<li>High-concurrency websites</li>
<li>Large games</li>
<li>Complex distributed cluster applications</li>
<li>Video encoding/decoding</li>
<li>Big data analysis</li>
<li>Machine learning and deep learning</li>
</ul>
</td>
</tr>
<tr>
<th style="font-weight:700;" rowspan=2>Favorable pricing</th>
<th style="font-weight:700;">Selling method</th>
<td>Cost-effective bundles (combinations of computing/network/storage resources)</td>
<td>Flexible selection of computing/storage/network resources that are billed independently</td>
</tr>
<tr>
<th style="font-weight:700;">Network billing</th>
<td>High-bandwidth data transfer plan</td>
<td>Fixed bandwidth/traffic usage</td>
</tr>
<tr>
<th style="font-weight:700;" rowspan=5>Simpler use</th>
<th style="font-weight:700;">Console operation</th>
<td>Integrated, independent, and simplified console</td>
<td>For all services, with more details of CVM, VPC, EIP, and security group involved</td>
</tr>
<tr>
<th style="font-weight:700;">Application creation</th>
<td>
<ul style="margin:-3px 0px">
<li>Out-of-the-box and premium official application images, preset with the optimal combination of software stacks required by the application system</li>
<li>Application creation in one minute as well as automatic installation of application software and runtime environment and initialization configuration</li>
</ul>
</td>
<td>Application creation on your own</td>
</tr>
<tr>
<th style="font-weight:700;">Networking</th>
<td>Automatic network resource creation without manual management needed</td>
<td>Network creation, configuration, and management on your own</td>
</tr>
</table>



<dx-alert infotype="explain" title="">
- Compared with CVM, the main limits of Lighthouse at the functional level include the following:
 An instance supports the overall upgrade of the configuration (computing, storage, and network) on a bundle basis but not bundle downgrade. For more information, see [Upgrading Instance Bundle](https://intl.cloud.tencent.com/document/product/1103/41562).
  For the specific use limits of Lighthouse, see [Use Limits](https://intl.cloud.tencent.com/document/product/1103/41265).
- There are certain limits on private network connectivity for Lighthouse. For more information, see [Region and Network Connectivity](https://intl.cloud.tencent.com/document/product/1103/41266).
- Lighthouse [cloud disks](https://intl.cloud.tencent.com/document/product/1103/46567) are independent of CVM [cloud disks](https://intl.cloud.tencent.com/document/product/213/4953), which means Lighthouse cloud disks can only be attached to Lighthouse instances but not CVM instances.
</dx-alert>




For scenarios like high-concurrency websites, video encoding/decoding, large-scale games, and complex distributed cluster applications, it's recommended to use CVM. CVM provides rich instance models, such as Memory Optimized, High I/O, Big Data, Bare Metal, and GPU/FPGA Heterogeneous Computing. For more information, see [CVM Instance Types](https://intl.cloud.tencent.com/document/product/213/11518).
