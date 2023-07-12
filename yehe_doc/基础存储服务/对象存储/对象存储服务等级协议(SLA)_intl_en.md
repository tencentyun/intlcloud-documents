**In order to use the Tencent Cloud Object Storage (“COS”) service (the “Service”), you should read and observe this Cloud Object Storage Service Level Agreement (this “Agreement”, or this “SLA”) and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248).  This Agreement contains, among others, the terms and definitions of the Service, level indicators of the Service availability and success rate, compensation plan and release of liabilities.  Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof.  By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement.  This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

**1. Terms and Definitions**

**Cloud Object Storage (COS)**: Object storage means a storage service that enables a user to store massive amounts of data using a Web interface.  A user may upload, download and manage data via the HTTP REST API of the COS.  COS supports automatic expansion, and the payment for the Service may be made in advance or in arrears.

**Service Month(s)**: Service Month(s) means the calendar month(s) within the term of the Service purchased by you.  For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16).  The availability of the Service will be calculated independently for each Service Month. 

**Error Rate Per Five Minutes**: Error Rate Per Five Minutes means the rate of the number of Failed Requests returned by COS within five (5) minutes to the total number of user requests within such five (5) minutes, calculated as follows:

![](https://main.qcloudimg.com/raw/f5c5f21ae418dc8a8b19699e804fa390.png)

**Failed Request**:  Failed Request means a request with a server internal error code (including “Internal Error” (500 error) and “Service Unavailable” (503 error)) returned by COS, excluding any traffic restriction request due to the triggering of frequency control and any Failed Request due to the upgrade, alteration or shutdown of COS.  User request means a request sent by a user and received by a COS server, excluding that sent by a user whose identity has not been authenticated, whose authentication fails, or for whom the Service is suspended or terminated due to unpaid overdue payment.  Any request received by a COS server in a hacker attack, or any request asynchronously executed on back end with the configuration of cross-regional replication or life cycle rules, will not be deemed an effective or a Failed Request.

**COS Service Monthly Fee**: COS Service Monthly Fee means the fee for storing capacity, flow, request, data retrieval and other storage management fee incurred under a certain Tencent Cloud account of a user within a calendar month for using the COS Service.

**2. Service Availability**

2.1  Calculation of Service Availability

The Service Availability of the COS is calculated by the category of storage as follows: 

![](https://main.qcloudimg.com/raw/13d7bdb9c49b0e8440f8c1c246500887.png)

2.2  Standards of Service Availability

You may upload, download and manage data via the API, SDK, control penal or user tools provided by the COS.  In respect of different categories of storage, Tencent Cloud guarantees that **the Service Availability of the standard storage service will be no less than 99.95%**, and **the Service Availability of the low frequency storage will be no less than 99.9%**.  If the Service Availability fails to meet aforementioned standard in a Service Month (other than circumstances set forth in the Release of Liabilities Section below), you may submit a support ticket to make an application to Tencent Cloud in accordance with Section 3 below.

**3. Service Compensation**

In respect of this Service, if the Service Availability of the standard storage service is lower than 99.95%, or the Service Availability of the low frequency storage is lower than 99.9%, compensations will be made as follows:

**3.1  Standards of Compensation**

1)  Compensations will be made **in the form of coupon** by Tencent Cloud, and you should follow the rules for using the coupon (including the valid term; for details, please refer to the rules of coupons published on Tencent Cloud’s official website).  You cannot redeem such coupon for cash or request to issue an invoice for such coupon.  Such coupon can only be used to purchase the Service by using your Tencent Cloud account.  You cannot use the coupon to purchase other services of Tencent Cloud, nor should you give the coupon to a third party for consideration or for free.

2)  If the Service Availability in a Service Month fails to meet the standard, the amount of compensation shall be calculated for such month independently, and **the aggregate amount will be no more than the applicable COS Service Monthly Fee paid by you for such month** (for the purpose of this provision, COS Service Monthly Fee shall exclude the portion deducted by a coupon or promotional voucher, due to discounted service fee or otherwise deducted). 

<table>
   <tr>
      <th>Storage Category</th>
      <th>Service Availability in a Service Month</th>
      <th>Value of Compensation Coupon</th>
   </tr>
   <tr>
      <td rowspan=2>Standard Storage</td>
      <td>≥ 99% and < 99.95%</td>
      <td>20% of the COS Service Monthly Fee</td>
   </tr>
   <tr>
      <td>< 99%</td>
      <td>50% of the COS Service Monthly Fee</td>
   </tr>
   <tr>
      <td rowspan=2>Low Frequency Storage</td>
      <td>≥ 98% and < 99.9%</td>
      <td>20% of the COS Service Monthly Fee</td>
   </tr>
   <tr>
      <td>< 98%</td>
      <td>50% of the COS Service Monthly Fee</td>
   </tr>
</table>

**3.2  Time Limit for Compensation Application**

1)  If the Service Availability in a Service Month fails to meet the aforementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month.  Tencent Cloud will verify and ascertain your application upon receipt of such application.  If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail**.

2)  You should apply for such compensation no later than sixty (60) calendar days following the expiry of the Service Month in which the Service Availability fails to meet the standard.  If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

**4. Release of Liabilities**

**If the Service is unavailable due to any of the following reasons, the corresponding Service unavailable time shall not be counted towards Service unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

**4.1  any system maintenance or unavailability with at least seven (7) days prior notice from Tencent Cloud to users.**

**4.2  any failure due to any network, equipment or configuration that is not Tencent Cloud facility.**

**4.3  any failure of the application interface or data of a user due to attack or other misconducts.**

**4.4  any failure due to negligence in authorization or mal-operation by a user, or due to any equipment of user, or third-party software or device.**

**4.5  any failure due to any force majeure event or accident.**

**4.6  any Service unavailability or failure to meet Service Availability standard due to any reason not attributable to Tencent Cloud.**

**4.7  any other circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately.**

**5. Miscellaneous**

**5.1  The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.**

5.2  Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course.  You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud.  If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

5.3  As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement.  In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement.  In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)

> **Note:**
> If you have questions about the calculation of availability, see [the COS availability calculation example](https://intl.cloud.tencent.com/document/product/436/6282#how-do-i-calculate-the-availability-of-cos.3F ).



