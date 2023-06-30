
## Differences from CVM

Lighthouse is a new-gen cloud server product oriented to small and medium-sized enterprises (SMEs) and developers. It is generally suitable for supporting low-load lightweight application scenarios with a moderate number of access requests, including small websites, web applications, blogs, forums, and cloud-based development, testing, and learning environments. Lighthouse is easier to use than CVM. It integrates multiple Tencent Cloud services and application service capabilities and simplifies the advanced concepts and features of CVM, allowing you to focus more on business logic and innovation. For more information on their differences, please see the table below:


<table style="width:908px;">
<tr>
<th style ="width:95px;height:45px;position:relative;font-weight:700;" valign="top"><div style="position:absolute;width:1px;height:115px;top:0;left:0;background-color: #d9d9d9;transform:rotate(-60deg);transform-origin:top;"></div>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Product<br>Item</th>
<th style="font-weight:700;">Lighthouse</th>
<th style="font-weight:700;">CVM</th>
</tr>
<tr>
<th style="font-weight:700;">Target users</th>
<td>SMEs and developers</td>
<td>All users</td>
</tr>
<tr>
<th style="font-weight:700;">Entry to cloud capabilities</th>
<td>Integrated, independent, and simplified console</td>
<td>Standard console for all business scenarios</td>
</tr>
<tr>
<th style="font-weight:700;">Package billing</th>
<td>Prepaid package (including computing, network, and storage resources)</td>
<td> Separate billing for different resources (such as computing, network, and storage)</td>
</tr>
<tr>
<th style="font-weight:700;">Network billing</th>
<td>Cost-Effective traffic package</td>
<td>Fixed bandwidth/traffic usage</td>
</tr>
<tr>
<th style="font-weight:700;">Application management</th>
<td>Official application image and application management</td>
<td>Image Marketplace</td>
</tr>
</table>




## Feature Comparison with VPS and Virtual Hosting

Lighthouse is a new-gen cloud server service developed for lightweight use cases and has many advantages over traditional virtual private server (VPS) and virtual hosting services.

>?
>- **VPS**: it uses server virtualization technologies to divide a single physical server into multiple virtual servers, each of which can have an independent IP address. You have complete admin permissions for your VPS servers and can configure them and install software programs on them as needed.
>- **Virtual Hosting**: aka shared web hosting, it allows multiple websites to share the same physical server (or cloud server service, i.e., virtual cloud hosting) at the underlying layer and uses a web server (such as Apache) to sustain these websites. The server has the runtime environments and databases used for website build preinstalled and hosts the database, network bandwidth, and storage resources shared by these websites. You have your own FTP permissions to upload webpage files to your own directory space. You have no permission to log in to the server's backend operating system; instead, you can only use virtual hosting to build websites.


The table below shows the feature comparison:

| Feature | Lighthouse | VPS | Virtual Hosting |
| :-: | :-: | :-: | :-:  |
| Server lifecycle management | ✔ | ✔ | × |
| Server power state management | ✔ | ✔ | × |
| System image | ✔ | ✔ | × |
| Application image | ✔| × | × |
| Quick application deployment (such as corporate website, blog, and forum) | ✔| × | ✔ |
| Application management | ✔| × | × |
| Independent IP | ✔| ✔ | × |
| Firewall | ✔ | ✔ | × |
| Server monitoring | ✔ | ✔ | × |
| Remote server login | ✔| ✔ | × |
| Integration with other Tencent Cloud services | ✔ | × | × |



