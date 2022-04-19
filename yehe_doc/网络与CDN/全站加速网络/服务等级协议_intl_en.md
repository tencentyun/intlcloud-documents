**In order to use the Tencent Cloud Enterprise Content Delivery Network Service (the “Service”), you shall read and comply with this Tencent Cloud Enterprise Content Delivery Network Service Level Agreement (this “Agreement”, or this “SLA”) and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, among others, the terms and definitions of the Service, Service Availability and Service Uptime Metrics, compensation plan and disclaimer of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or disclaiming certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties. For the purposes of these Terms of Service, “Tencent Cloud” refers to the applicable Tencent contracting entity as set forth in the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248).**

## 1. Terms and Definitions

### 1.1 Tencent Cloud Enterprise Content Delivery Network Service
Refers to the Tencent Cloud Enterprise Content Delivery Network, through which Tencent Cloud will publish your static content to massive accelerated nodes in countries around the world, so that users of your website can get the content they need nearby. The Service can allocate dynamic content, schedule the optimal return-to-source paths, ensure fast return speed and improve user access experience. The specific content of the Service is subject to the service you have purchased and the service provided by Tencent Cloud.

### 1.2 Service Month(s)
Service Month(s) refers to the calendar month(s) within the term of the Service you use after you start the Service. For example, if you start the Service on March 17, the first Service Month will be from March 17 to March 31, and each calendar month thereafter (e.g., the second from April 1 to April 30, the third from May 1 to May 31) will be a Service Month. The Service Availability will be calculated separately for each Service Month.

### 1.3 Service Region(s)
The Service Regions of the Tencent Cloud Enterprise Content Delivery Network Service are divided into service regions within China and outside of China with different service pricing. The Tencent Cloud will bill you separately for the inbound and outbound Service you have activated.

### 1.4 Monthly Service Fee
The Monthly Service Fee will be calculated for each Service Month by calculating actual consumption based on the actual billing method of the Service Region activated by you, and calculating the monthly service fee you should pay in the Service Region based on the pricing of the Service Region.

### 1.5 Daily Service Fee
The Daily Service Fee will be calculated for each service day by calculating actual consumption based on the actual billing method of the Service Region activated by you, and calculating the daily service fee you should pay in the Service Region based on the pricing of the Service Region.

### 1.6 Aggregate Monthly Service Fee
The Aggregate Monthly Service Fee will be calculated for each Service Month by adding up the Monthly Service Fee of each Service Region you use.

### 1.7 Monthly Service Fee for a Single Accelerated Domain
The Monthly Service Fee for a Single Accelerated Domain will be calculated for each Service Month by allocating the regional Monthly Service Fee pro rata to the actual consumption of the single accelerated domain, which actual consumption shall be calculated based on the Service Regions activated by you.

### 1.8 Daily Service Fee for a Single Accelerated Domain
The Daily Service Fee for a Single Accelerated Domain will be calculated for each service day by allocating the regional Daily Service Fee pro rata to the actual consumption of the single accelerated domain, which actual consumption shall be calculated based on the Service Regions activated by you.

### 1.9 Aggregate Monthly Service Fee for a Single Accelerated Domain
The Aggregate Monthly Service Fee for a Single Accelerated Domain will be calculated for each Service Month by adding up the Monthly Service Fee for a Single Accelerated Domain of each Service Region you use.

### 1.10 Unit Time
For measuring the Service, each 5 minutes will be deemed as one measurement unit, resulting in 288 measurement points each day. The measurement point of 00:00:00 represents the time slot from 00:00:00 to 00:04:59, and the rest can be deduced by analogy.

### 1.11 Error Rate within Unit Time
Error Rate within Unit Time means the percentage of the number of failed requests returned within one Unit Time in relation to a single accelerated domain due to any reason attributable to Tencent Cloud out of the total number of requests within such Unit Time, in which failed requests refer to requests with return status code 5xx or connection timeout. Error Rate within Unit Time = the number of failed requests within one Unit Time / the total number of requests within such Unit Time. The Error Rate within Unit Time will be calculated independently based on the number of accelerated domains metrics involved in the Service purchased by you.

### 1.12 Service Downtime within Service Month(s) Calculated in Minutes
The Error Rate within Unit Time for a single accelerated domain greater than 0.05% is considered an abnormality for the Unit Time. If two consecutive Unit Times are abnormal, the 10 minutes is counted as unavailable unit time, and less than two consecutive Unit Times is not counted as Service Downtime. The unavailable unit time in each Service Month is added up to get the Service Downtime within Service Month(s) Calculated in Minutes.

### 1.13 Monthly Service Fee for Domains of which the Service Availability Fails to Meet the Standard
The Monthly Service Fee for Domains of which the Service Availability Fails to Meet the Standard will be calculated for each Service Month by allocating the Aggregate Monthly Service Fee pro rata to the actual consumption of each single accelerated domain, which actual consumption for the Service Region’s all domains of which the Service Availability fails to meet the standard shall be calculated based on the actual billing method.

### 1.14 Total Number of Minutes within Service Month(s)
Total Number of Minutes within Service Month(s) = the total number of days of the Service Month(s) × 24 (hours) × 60 (minutes).


## 2. Service Availability / Service Uptime Metrics

### 2.1 Calculation of Service Availability / Service Uptime Metrics
**Service Availability = 1 - (Service Downtime within a Service Month Calculated in Minutes / Total Time of the Service within a Service Month Calculated in Minutes) × 100%**

**Service Availability = 1 - (Service Downtime within a Service Day Calculated in Minutes / Total Time of the Service within a Service Day Calculated in Minutes) × 100%**

The Service Availability will be calculated independently for each accelerated domain involved in the Service you use.

### 2.2 Service Availability / Service Metrics
**The Service Availability for each accelerated domain involved in the Service provided by Tencent Cloud should not be less than 99.9%.** If the Service fails to meet the Standard (except under circumstances for disclaimer of liabilities), you may claim compensation in accordance with Article 3 of this Agreement.

## 3. Compensation Plan
In respect of the Service, if the Service Availability fails to meet the standard, you will be entitled to compensations in accordance with the following terms:

### 3.1 Standards of Compensation

(1) Compensations will be made **in the form of voucher** by Tencent Cloud, and you should use the voucher by abiding the voucher usage rules (including usage period, etc., subject to the voucher usage rules published on Tencent Cloud official website). Such voucher cannot be converted into cash, and no invoice will be issued with respect thereof. The voucher may only be used to purchase the Service by using your Tencent Cloud account, and you cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) Enterprise Content Delivery Network provides services to multiple domains simultaneously, and compensations will be made only to the domains of which the global Service Availability fails to meet the standard within a Service Month. The amount of compensation will be calculated for each such Service Month independently, and **the aggregate amount shall be no more than the Aggregate Monthly Service Fee for Domains of which the Service Availability Fails to Meet the Standard** (the Monthly Service Fee referred to herein shall exclude the portion deducted by vouchers, coupons, service fee reduction or exemption, etc.).

(3) For the domain of which the Service Availability fails to meet the standard, the Monthly Service Fee for Domains of which the Service Availability Fails to Meet the Standard may be calculated and compensation may be made according to the following list:

<table>
<thead>
<tr>
<th>Service Availability in a Service Month</th>
<th>Value of Compensational Voucher</th>
</tr>
</thead>
<tbody>
<tr>
<td>Less than 99.9% but is or higher than 99.0%.</td>
<td>10% of the aggregate Monthly Service Fee for Domains of which the Service Availability Fails to Meet the Standard.</td>
</tr>
<tr>
<td>Less than 99.0%</td>
<td>25% of the aggregate Monthly Service Fee for Domains of which the Service Availability Fails to Meet the Standard.</td>
</tr>
</tbody></table>

### 3.2 Time Limit for Compensation Application

(1) If the Service Availability in a Service Month fails to meet the Service Availability standard, you may **apply for compensation only through the support ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud shall prevail**.

(2) **You shall apply for compensation no later than the sixtieth (60th) calendar day following the end of the applicable Service Month in which the Service Availability fails to meet the abovementioned standard.** If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

## 4. Disclaimer of Liabilities
**If the Service is unavailable due to any of the following reasons, the corresponding Service Downtime shall not be counted towards Service Unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

4.1 any request error due to the malfunction of the Customer's origin server;

4.2 any error due to a ban on or block of a domain name for any non-compliant content of the Customer or otherwise;

4.3 any change to configuration of an origin server or DNS of an accelerated domain by the Customer without prior notice to the Tencent Cloud, resulting in the failure of a Tencent Cloud node server to access the Customer 's origin server;

4.4 any loss or leak of data, passcode or password due to improper maintenance or improper confidentiality measures of the Customer;

4.5 any upgrade of the operation system by the Customer on its own;

4.6 any hacker attack on the Customer 's website;

4.7 any impromptu increase of traffic of the Customer (increasing by 30% or more of the billed bandwidth in the preceding month) without at least three (3) business days prior written notice to Tencent Cloud;

4.8 any system maintenance with prior notice by Tencent Cloud to the Customer, including system cutover, maintenance, upgrade and malfunction simulation test;

4.9 any malfunction or configuration adjustment of network or equipment that is not Tencent Cloud facility;

4.10 any event of force majeure or accident;

4.11 any other reasons not attributable to Tencent Cloud.

## 5. Miscellaneous

**5.1 The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total Service Fees you have paid for the relevant Service which is not performed. **

5.2 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

5.3 As an ancillary agreement to the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement is of the same legal effect as the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In respect of any matter not agreed herein, you shall comply with relevant terms under the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In case of any conflict or discrepancy between this Agreement and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement prevails to the extent of such conflict or discrepancy. 



