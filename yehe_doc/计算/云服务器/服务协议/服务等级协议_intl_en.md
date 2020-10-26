**In order to use the Tencent Cloud Virtual Machine (“CVM”) service (the “Service”), you should read and comply with this Cloud Virtual Machine Service Level Agreement (this “Agreement”, or this “SLA”) and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, among others, the terms and definitions of the Service, level indicators of the Service availability and success rate, compensation plan and release of liabilities. Unless otherwise stipulated, this Agreement does not apply to instances and functions of CVM closed beta testing. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

## 1. Terms and Definitions

#### 1.1 Cloud Virtual Machine (CVM)
CVM means computing capabilities that can be scaled up in the cloud provided to you by Tencent Cloud, which saves you from resource projection and upfront investment required in using traditional servers. For details, please refer to the Service you purchase, and the contents of the Service provided by Tencent Cloud. 

#### 1.2 Single Instance
Single Instance means one (1) CVM instance, i.e., the unit CVM. 

#### 1.3 Total Time of a Single Instance in a Service Month

Total Time of a Single Instance in a Service Month = the total number of days of the Service Month for such Single Instance × 24 (hours) × 60 (minutes).

#### 1.4 Instance Unavailability

When a CVM instance with incoming and outgoing permission rules properly configured fails to communicate with an IP address, neither incoming nor outgoing, via TCP or UDP protocol, and such failure lasts for more than one (1) minute, it will be deemed that the CVM instance is unavailable within such one (1) minute. 

#### 1.5 Single Instance Service Downtime Calculated in Minutes
Single Instance Single Service Downtime Calculated in Minutes = the time Instance Unavailability is fixed – the time Instance Unavailability starts. The Single Instance Single Service Downtime is calculated in minutes. (If the operational failure is fixed within one (1) minute, i.e., the Instance Unavailability lasts for less than one (1) minute, such downtime will not be counted.) A period that is longer than one (1) minute but shorter than two (2) minutes will be counted as two (2) minutes. For example, if the Single Instance Single Service Downtime is one (1) minute and one (1) second, the Single Instance Single Service Downtime Calculated in Minutes would be two (2) minutes. 
The Single Instance Service Downtime Calculated in Minutes is the total of Single Instance Single Service Downtime Calculated in Minutes of such instance in a Service Month.

#### 1.6 Instance Unavailability Across Availability Zones in A Single Region

If the user deploys CVM instances in at least two (2) availability zones in the same region (referred to as “**Across Availability Zones in A Single Region**” herein), when all CVM instances in any availability zone in such region become unavailable and certain CVM instance(s) in other availability zone(s) in such region also becomes unavailable, such unavailability of CVM instance(s) in other availability zone(s) in such region will be deemed as Instance Unavailability Across Availability Zones in A Single Region. For example, if the user deploys CVM instances in both Availability Zone A and Availability Zone B in the same region, when certain CVM instance in Availability Zone A becomes unavailable and all CVM instances in Availability Zone B become unavailable, the unavailability of  instance in Availability Zone A will be deemed as Instance Unavailability Across Availability Zones in A Single Region.


#### 1.7 Service Downtime Across Availability Zones in A Single Region Calculated in Minutes

Single Service Downtime Across Availability Zones in A Single Region Calculated in Minutes = the time Instance Unavailability Across Availability Zones in A Single Region is fixed – the time Instance Unavailability Across Availability Zones in A Single Region starts. The Single Service Downtime Across Availability Zones in A Single Region is calculated in minutes. (If the operational failure is fixed within one (1) minute, i.e., the Instance Unavailability Across Availability Zones in A Single Region lasts for less than one (1) minute, such downtime will not be counted.) A period that is longer than one (1) minute but shorter than two (2) minutes will be counted as two (2) minutes. For example, if the Single Service Downtime Across Availability Zones in A Single Region is one (1) minute and one (1) second, the Single Service Downtime Across Availability Zones in A Single Region would be two (2) minutes.

The Service Downtime Across Availability Zones in A Single Region Calculated in Minutes is the total of Single Service Downtime Across Availability Zones in A Single Region Calculated in Minutes of such instance in a Service Month. 

#### 1.8 Service Month(s)

Service Month(s) means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The availability of the Service will be calculated separately for each Service Month. 

#### 1.9 Monthly Service Fee

Monthly Service Fee means the aggregate service fees paid by you for a Single Instance in one (1) Service Month, excluding the portion paid yet to be consumed, and the portion deducted by a voucher or promotional coupon, due to discounted service fee or otherwise deducted. 

## 2. Service Availability

#### 2.1 Calculation of Service Availability

Tencent Cloud guarantees two levels of Service Availability for a CVM instance, the **Single Instance Service Availability** and the **Service Availability Across Availability Zones in A Single Region**. Both the Single Instance Service Availability and the Service Availability Across Availability Zones in A Single Region are calculated on the basis of **a single instance**.

(1) Single Instance Service Availability:
Single Instance Service Availability = (Total Minutes of a Single Instance in a Service Month - Single Instance Service Downtime Calculated in Minutes) / Total Minutes of a Single Instance in a Service Month × 100%
(2) Service Availability Across Availability Zones in A Single Region:
Service Availability Across Availability Zones in A Single Region = (Total Minutes of a Single Instance in a Service Month - Service Downtime Across Availability Zones in A Single Region Calculated in Minutes of the Single Instance) / Total Minutes of a Single Instance in a Service Month × 100%

#### 2.2 Service Availability

(1) The Single Instance Service Availability of the Service provided by Tencent Cloud will be **no less than 99.975%**. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below. Assuming that a Service Month has thirty (30) days, the total available time of a Single Instance in such month shall be 30 (days) × 24 (hours) × 60 (minutes) × 99.975% = 43189.2 minutes; that is, the Service Downtime of the instance in such month will be 43200 – 43189.2 = 10.8 minutes.

(2) The Service Availability Across Availability Zones in A Single Region of the Service provided by Tencent Cloud will be **no less than 99.995%**. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below. Assuming that a Service Month has thirty (30) days, the total available time of a Single Instance in such month shall be 30 (days) × 24 (hours) × 60 (minutes) × 99.995% = 43197.84 minutes; that is, the Service Downtime Across Availability Zones in A Single Region in such month will be 43200 – 43197.84 = 2.16 minutes.

## 3. Service Compensation

In respect of this Service, if the Service Availability fails to meet the abovementioned standard, you will be entitled to compensations in accordance with the following terms:

#### 3.1 Standards of Compensation

(1) Compensations will be made **in the form of voucher** by Tencent Cloud, and you should follow the rules for using the voucher (including the valid term; for details, please refer to the rules of vouchers published on Tencent Cloud’s official website). You cannot redeem such voucher for cash or request to issue an invoice for such voucher. Such voucher can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the **Single Instance Service Availability** in a Service Month fails to meet the standard, the amount of compensation will be calculated for such month independently, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such month**.

<table>
<thead>
<tr>
<th style="width:60%"><b>Single Instance Service Availability in a Service Month</b></th>
<th style="width:40%"><b>Value of Compensation Voucher</b></th>
</tr>
</thead>
<tbody><tr>
<td>≥ 99%  and < 99.975%</td>
<td>10% of  the Monthly Service Fee</td>
</tr>
<tr>
<td>≥ 95%  and < 99%</td>
<td>25% of  the Monthly Service Fee</td>
</tr>
<tr>
<td><  95% </td>
<td>100%  of the Monthly Service Fee</td>
</tr>
</tbody></table>

(3) If the **Service Availability Across Availability Zones in A Single Region** in a Service Month fails to meet the standard, the amount of compensation will be calculated for such month independently, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such month**.

<table>
<thead>
<tr>
<th style="width:60%"><b>Service Availability Across Availability Zones in A Single Region in a  Service Month</b></th>
<th style="width:40%"><b>Value of Compensation Voucher</b></th>
</tr>
</thead>
<tbody><tr>
<td>≥ 99%  and < 99.995%</td>
<td>10% of  the Monthly Service Fee</td>
</tr>
<tr>
<td>≥ 95%  and < 99% </td>
<td>25% of  the Monthly Service Fee </td>
</tr>
<tr>
<td><  95%  </td>
<td>100%  of the Monthly Service Fee</td>
</tr>
</tbody></table>

(4) If a CVM instance is eligible to compensations according to standards set forth in both Articles 3.1(2) and 3.1(3), whichever is higher shall be applied.

#### 3.2 Time Limit for Compensation Application

(1) If the Single Instance Service Availability or the Service Availability Across Availability Zones in A Single Region in a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail**.

(2) **You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard**. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

## 4. Release of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service downtime shall not be counted towards Service unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**



4.1 any failure or configuration adjustment of any network or equipment that is not Tencent Cloud facility;

4.2 any hacker attack on a user’s application;

4.3 any loss or leak of data, pin or password due to improper maintenance or confidentiality measures of a user;

4.4 any negligence of, or operation authorized by, a user;

4.5 any failure by a user to abide by documentation or suggestions for using Tencent Cloud products, for example, shutting down, restarting, or uninstalling cloud storage of a CVM instance via Tencent Cloud control penal, API, CLI or otherwise;

4.6 any start-up dependence on local disk and data stored herein, which data is removed due to system failure;

4.7 any CVM instance error caused by software installed by a user, any other third-party software or configuration not directly operated by Tencent Cloud;

4.8 any event of force majeure including without limitation natural disasters such as earthquake, flood and plague, social events such as war, riot and government action, technology incidents such as disconnection of telecommunication trunk circuits, hacker attack and network congestion, technological adjustment by telecommunication authorities, and government regulation and control;

4.9 any suspension or termination of servers resulting from any violation by a user of the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), including without limitation the release of a CVM instance open for bidding when the bidding offer of a user is lower than the closing price, and the suspension of service or release of a CVM instance due to a user’s delay in payment;

4.10 any temporary downtime of the Service due to normal maintenance or upgrade of CVM by Tencent Cloud as described in the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248);

4.11 any Service unavailability or failure of the Service to meet the standard due to any reason not attributable to Tencent Cloud;

4.12 any other circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately.

## 5. Miscellaneous

5.1 **The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.**

5.2 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

5.3 As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)

