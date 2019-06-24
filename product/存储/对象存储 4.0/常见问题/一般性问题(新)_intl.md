### What is the difference between Cloud Object Storage (COS) and Cloud File Storage (CFS)?

[COS](https://intl.cloud.tencent.com/document/product/436) has no limit on data format. You can store files of any format and size in COS, and connect it to the customer's business layer through SDK and tools for real-time storage. It also supports setting custom domain names, and allows you to directly store data such as images or files in COS and access or download them through URL.

[CFS](https://intl.cloud.tencent.com/document/product/582) features a higher price, but secure transfer protocol. It supports creating file systems and can be mounted directly on the server. It is applicable to various memory management systems, and can store data for a range of applications such as websites, online distribution, and archiving. Providing high computing throughput as well as extremely high availability and durability, CFS is also suitable for scenarios demanding high concurrency or shared storage.

### What is "folder" or "directory" in COS?

Folders and directories do not exist in COS. However, considering the usage habits of different users, COS simulates the display mode of "folder" on the console based on the directory structure of traditional file management. For more information ,see [Folders and Directories](https://intl.cloud.tencent.com/document/product/436/13324).

### Does COS have statistics feature?

COS supports basic data statistics and error code statistics. On the **Monitoring List** page in the [COS Console](https://console.cloud.tencent.com/cos5), you can view statistics of basic data and error codes at any time. 

In addition to the COS Console, you can also view the monitoring information of different buckets on the Tencent [Cloud Monitoring](https://console.cloud.tencent.com/monitor/product/COS) page, and configure different alarm policies based on your business needs.

### Does COS support image compression?

COS is a distributed storage service for unstructured data and does not support image compression. For image compression processing, see the [Cloud Infinite](https://intl.cloud.tencent.com/product/ci?idx=1) overview page.

### Does COS support thumbnails?

COS is a distributed storage service for unstructured data and does not support thumbnail feature. For more information on thumbnail feature, see the [Cloud Infinite](https://intl.cloud.tencent.com/product/ci?idx=1) overview page.

### Does COS support transcoding video files?

COS is a distributed storage service for unstructured data and does not support video transcoding.

### Does COS support auto decompression of uploaded files?

COS is a distributed storage service for unstructured data and does not support file decompression.

### What are the specifications and limits of COS?

For more information, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/436/14518).

### Which version of COS should I use, an earlier version or the current version?

The implementation of earlier versions and that of the current version of COS vary greatly. The current version has more features than earlier versions, and earlier versions are not updated with the latest features. **We recommend that you use the current version** for a better experience. If you are using an earlier version, [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1) to activate the current version.

The current version comes with different APIs and SDK APIs than those in earlier versions. JSON APIs are used in earlier versions and XML APIs are used in the current version. JSON APIs have the same underlying architecture as XML APIs. Their data is interoperable and can be cross-used, but they are incompatible and have different domain names.

### How do I monitor the error code information?

You can use [Cloud Monitoring](https://console.cloud.tencent.com/monitor/product/COS) to get different types of HTTP error code messages. For information on how to use cloud monitoring feature and how to obtain relevant data, see [API Documentation](https://intl.cloud.tencent.com/document/product/248/4469).  

### How do I calculate the availability of COS?
COS provides the following example of calculating the availability for your reference:
Tom uses Tencent Cloud COS to run his e-commerce business. Assume that his business consumed a total of 100 CNY in a service month from Nov. 1 to Nov. 30, 2018, during which two unavailable events occurred, as shown below:

<table>
   <tr>
      <th>Unavailable Event No.</th>
      <th>Duration</th>
      <th>5-Minute Record</th>
      <th>HTTP Error Code</th>
      <th>Number of Failed Requests</th>
      <th>Number of Valid Requests</th>
   </tr>
   <tr>
      <td rowspan=3><center>1<center></td >
      <td rowspan=3>15 minutes</td>
      <td>Nov. 15, 2018, 10:00-10:05</td>
      <td>503</td>
      <td>100</td>
      <td>100</td>
   </tr>
   <tr>
      <td>Nov. 15, 2018, 10:05-10:10</td>
      <td>503</td>
      <td>99</td>
      <td>100</td>
   </tr>
   <tr>
      <td>Nov. 15, 2018, 10:10-10:15</td>
      <td>503</td>
      <td>98</td>
      <td>100</td>
   </tr>
   <tr>
      <td rowspan=3><center>2<center></td>
      <td rowspan=3>15 minutes</td>
      <td>Nov. 20, 2018, 16:00-16:05</td>
      <td>501</td>
      <td>150</td>
      <td>150</td>
   </tr>
   <tr>
      <td>Nov. 20, 2018, 16:05-16:10</td>
      <td>501</td>
      <td>148</td>
      <td>150</td>
   </tr>
   <tr>
      <td>Nov. 20, 2018, 16:10-16:15</td>
      <td>501</td>
      <td>140</td>
      <td>150</td>
   </tr>
</table>

In other periods, Tom's requests **were successful and a 200 status code was returned**.

In this case, the overall availability of the service month is as follows:

**1) Calculate the error rate per 5 minutes for the current month**

According to the case details: When Tom's business is normal, the error rate per 5 minutes is 0%.

Unavailable event 1: The duration is from 10:00 to 10:15 on Nov. 15, 2018, and the 5-minute error rates are 100÷100×100%, 99÷100×100%, and 98÷100×100% respectively.

Unavailable event 2: The duration is from 16:00 to 16:15 on Nov. 20, 2018, and the 5-minute error rates are 150÷150×100%, 148÷150×100%, and 140÷150×100% respectively.

**2) Calculate the service availability of the service month**

In this case:

Total duration of the service month: 30 days × 24 hours/day × 60 minutes/hour=43,200 minutes.

Total number of 5 minutes in the service month: 43,200 minutes ÷ 5 minutes=8,640.

Total number of unavailable 5 minutes in the service month: (15+15) minutes ÷ 5 minutes=6.

Sum of the 5-minute error rates in the service month: (100%+99%+98%+100%+98.67%+93.33%)+(8640-6)×0%=589%

The service availability for this month: (1-589%÷8640)×100%=99.93%

**3) Calculate compensation**

In this case, the service availability is 99.93%, which is lower than the availability standard of 99.95% but higher than 99.9%. According to the compensation standard, Tencent Cloud COS should compensate 20% of the total monthly service fee, i.e. 20 CNY. Tom only needs to submit a ticket for compensation within sixty (60) calendar days after the end of the service month, i.e. before Jan. 29, 2019. Tencent Cloud will compensate Tom for the corresponding losses in the form of vouchers.


