## Tencent Cloud Cloud Connect Network Service Level Agreement

**In order to use the Tencent Cloud Cloud Connect Network (“CCN”) service (the “Service”), you should read and observe this Tencent Cloud Cloud Connect Network Service Level Agreement (this “Agreement”, or this “SLA”) and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, among others, the terms and definitions of the Service, Service availability and Service uptime metrics, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, may be in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

### 1. Terms and Definitions

1.1 **Cloud Connect Network (CCN)**

The Cloud Connect Network (CCN) Service refers to multi-point interconnection services provided by Tencent Cloud connecting cloud VPC, VPC and local data centers. You may access the entire network resources through a single point connect by adding VPC and direct gateway instance to CCN, thus easily establishing a simple, intelligent, secure and flexible hybrid cloud and worldwide Internet. For details, please refer to the Service you purchase and the Service provided by Tencent Cloud. 

1.2 **Service Unavailability**

If, due to any reason attributable to Tencent Cloud, all your attempts to establish communication between two regions or in a single region through designated CCN within one (1) minute fail (i.e., within one (1) minute and between such two regions or in such single region, the packet loss rate of the communications through the CCN of all instances associated with the CCN is 100%, the details of which is subject to the monitoring data of Tencent Cloud), it should be deemed that the CCN service between such two regions or in such single region within such one (1) minute is unavailable. 

1.3 **Service Downtime**

Service Downtime within a Service Month between two regions or in a single region refers to the accumulated duration of Service Unavailability calculated in minutes between such two regions or in such single region within such month.

1.4 **Service Month(s)**

Service Month(s) refer to the calendar month(s) in which you use the Service after you subscribe to the Service. For example, if you subscribe to the Service on March 17, the first Service Month is from March 17 to March 31, and each of the subsequent Service Months is a calendar month, i.e., the second Service Month from April 1 to April 30, the third from May 1 to May 31, etc. The Service Availability will be calculated separately for each Service Month.

1.5 **Monthly Service Fee**

The monthly service fees paid by you within one (1) Service Month for a CCN instance between two regions or in a single region.

### 2. Service Availability

2.1 **Calculation of Service Availability**

The Service Availability is calculated on an instance basis between designated regions or in a single region as follows: Service Availability = [ (total time calculated in minutes within a Service period - Service Downtime calculated in minutes / total time of a Service period calculated in minutes] × 100%

2.2 **Standard of Service Availability**

The Service has **three Service levels, namely, Platinum, Gold and Silver**, and the standard of Service Availability for each tier is set forth in the chart below. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below. 



| Service Level (QOS) | Service Availability |
| ------------------- | -------------------- |
| Platinum            | 99.99%               |
| Gold                | 99.95%               |
| Silver              | 99.50%               |



>?
>- For Services within the same city, the Service level is default to Gold and cannot be changed.
>- For Services across cities, you may select among the three Service levels, i.e., Platinum, Gold, and Silver, when you create a CCN instance.

### 3. Service Compensation

In respect of this Service, if the Service Availability fails to meet the abovementioned standard, you will be entitled to compensations in accordance with the following terms:

3.1 **Standards of Compensation**

(1) Compensations will be made **in the form of voucher** by Tencent Cloud, and you should follow the rules for using the voucher (including the valid term; for details, please refer to the rules of vouchers published on Tencent Cloud’s official website). You cannot redeem such voucher for cash or request to issue an invoice for such voucher. Such voucher can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability for a Service Month of a CCN instance between two regions or in a single region fails to meet the Standard, the amount of compensation will be calculated for such month independently, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such month of the CCN instance between such two regions or in such single region** (the Monthly Service Fee referred to herein shall exclude the fee deducted by a voucher or promotional coupon, Service fee discounted or waived, or fees otherwise deductible). 

<table>
<thead>
<tr>
<th>Service Level</th>
<th>Service Availability of a Service Month</th>
<th>Amount of Compensational Voucher</th>
</tr>
</thead>
<tbody><tr>
<td rowspan="3">Platinum</td>
<td>99.99% ＞ Service Availability ≥ 99.95%</td>
<td>15% of the Monthly Service Fee</td>
</tr>
<tr>
<td>99.95% ＞ Service Availability ≥ 99.50 %</td>
<td>30% of the Monthly Service Fee</td>
</tr>
<tr>
<td>99.50% ＞ Service Availability</td>
<td>100% of the Monthly Service Fee</td>
</tr>
<tr>
<td rowspan="3">Gold</td>
<td>99.95% ＞ Service Availability ≥ 99.50%</td>
<td>15% of the Monthly Service Fee</td>
</tr>
<tr>
<td>99.50% ＞ Service Availability ≥ 99.00%</td>
<td>30% of the Monthly Service Fee</td>
</tr>
<tr>
<td>99.00% > Service Availability</td>
<td>100% of the Monthly Service Fee</td>
</tr>
<tr>
<td rowspan="3">Silver</td>
<td>99.50% ＞ Service Availability ≥ 99.00%</td>
<td>15% of the Monthly Service Fee</td>
</tr>
<tr>
<td>99.00% ＞ Service Availability ≥ 95.00%</td>
<td>30% of the Monthly Service Fee</td>
</tr>
<tr>
<td>95.00% > Service Availability</td>
<td>100% of the Monthly Service Fee</td>
</tr>
</tbody></table>



>!The Monthly Service Fee in the above table refers to the relevant Monthly Service Fee charged for the relevant CCN instance between two regions or in a single region, and shall exclude any fee charged in the following circumstances:
>- any Monthly Service Fee charged for any other CCN instance that meets the Service Availability Standard in a single region or between regions;
>- any Monthly Service Fee charged for such CCN instance between other regions or in another region where the Service Availability Standard is met. For example, if a CCN instance fails to meet the Service Availability Standard between Shanghai and Beijing in May, but meets the Service Availability Standard between Shanghai and Guangzhou, the amount of voucher to be compensated shall be the fees charged for that CCN instance between Shanghai and Beijing in May × the applicable ratio of compensations.

 

3.2 **Time Limit for Compensation Application**

(1) If the Service Availability for a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail**.

(2) **You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard**. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

### 4. Release of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service Downtime shall not be counted towards Service Unavailability, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

4.1    any system maintenance with prior notice by Tencent Cloud to a client, including system cutover, maintenance, upgrade and failure simulation test.

4.2    any malfunction or configuration adjustment of network or equipment that is not Tencent Cloud facility.

4.3    any hacker attack targeting the application or data information, or any exception of a backend service, of a client.

4.4    any improper network configuration of a client, including but not limited to the configurations of routing, ACL, security groups, and bandwidth throttling.

4.5    any failure of an instance associated with the CCN (e.g., a private line gateway, VPC, VPN and etc.) to meet its service availability standard, resulting in the failure to meet the Service Availability Standard of the CCN.

4.6    any circumstance where only one availability zone is involved during a party’s communications through the CCN, e.g., where all private lines are connected to the same access point or all cloud-based services are deployed to the same availability zone.

4.7    any loss or leak of any data, pin or password due to improper maintenance or improper confidentiality measures of a client.

4.8    any application or installation operation of the client’s, or any upgrade of the operation system by a client on its own.

4.9    any negligence of a client or any operation authorized by a client.

4.10  any failure of the client to follow the product documentations or suggestions of use.

4.11  any force majeure event or accident. 

4.12  any Service Unavailability or failure of the Service to meet the availability standards due to any reason not attributable to Tencent Cloud.

4.13  any other circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately.

### 5. Miscellaneous

**5.1 The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate amount of compensation payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.**

**5.2 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.**

5.3 As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)

 
