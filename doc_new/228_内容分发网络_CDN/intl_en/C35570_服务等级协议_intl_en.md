>**The Content Delivery Network Service Level Agreement (New Version) is currently available to the public for comments and will take effect as of Sep 1, 2019. Any service availability issue in relation to the Content Delivery Network on or before Aug 31, 2019 is governed by the Content Delivery Network Service Level Agreement (Old Version), while the service availability issue as from Sep 1, 2019 shall be subject to the Content Delivery Network  Service Level Agreement (New Version).**

**In order to use the Tencent Cloud Content Delivery Network ("CDN") service (the "Service"), you should read and observe this Content Delivery Network Service Level Agreement (this "Agreement", or this "SLA") and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, among others, the terms and definitions of the Service, Service availability and Service uptime metrics, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, may be in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking "Agree"/ "Next", or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

## 1.  Terms and Definitions

**Content Delivery Network (CDN)**: means the network architecture provided by Tencent Cloud that delivers contents on clients' websites to a huge number of cache nodes worldwide, which enables end users to get access to contents from the closest node, thus improving user experience.

**Service Month(s)**: means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, the first Service Month will be from March 17 to March 31, and each calendar month thereafter (e.g., from April 1 to April 30) will be a Service Month. The availability of the Service will be calculated independently for each Service Month. **Regional Monthly Service Fee for a Single Accelerated Domain**: will be calculated for each Service Month by allocating the regional monthly service fee pro rata to the actual consumption of the single accelerated domain, which actual consumption shall be calculated based on the regions activated by you.

**Aggregate Monthly Service Fee for a Single Accelerated Domain**: means the sum of the monthly service fee of such accelerated domain in all Service regions within a Service Month.
**Unit Time**: For measuring the Service, each 5 minutes will be deemed as one measurement unit, resulting in 288 measurement points each day. The measurement point of 00:00:00 represents the time slot from 00:00:00 to 00:04:59, and the rest can be deduced by analogy.

**Error Rate within Unit Time**: means the percentage of the number of failed requests returned within one Unit Time in relation to a single accelerated domain due to any reason attributable to Tencent Cloud out of the total number of requests within such Unit Time, in which failed requests refer to requests with return status code 5xx or connection timeout. Error Rate within Unit Time = the number of failed requests within one Unit Time / the total number of requests within such Unit Time. The Error Rate within Unit Time will be calculated independently based on the number of accelerated domains metrics involved in the Service purchased by you.

**Service Downtime within a Service Month Calculated in Minutes**: When the Error Rate within Unit Time of a single accelerated domain is over 0.05%, it will be deemed that anomaly occurs within such Unit Time; when such anomaly occurs twice in a row, such two Unit Time (i.e. ten minutes) will be counted into Service downtime. Unless such anomaly occurs at least twice in a row, no single Unit Time with anomaly occurring will be counted into Service downtime. Service Downtime within a Service Month Calculated in Minutes will be the sum of such Unit Time counted into Service downtime within the Service Month.

**Total Time of a Service Month Calculated in Minutes**: the number of days of such Service Month × 24 (hour) × 60 (minute).

## 2.  Service Availability / Service Uptime Metrics

2.1  **Calculation of Service Availability / Service Metrics**

Service Availability = 1 -- (Service Downtime within a Service Month Calculated in Minutes / Total Time of the Service within a Service Month Calculated in Minutes) × 100%

The Service Availability will be calculated independently for each accelerated domain involved in the Service you use.

2.2  **Standard of Service Availability / Service Metrics**

**The Service Availability for each accelerated domain involved in the Service will be** **no less than 99.9%**. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below.

## 3.  Service Compensation

In respect of this Service, if the Service Availability fails to meet the abovementioned standard, you will be entitled to compensations in accordance with the following terms:

3.1  **Standards of Compensation**

(1) Compensations will be made **in the form of voucher** by Tencent Cloud, and you should follow the rules for using the voucher (including the valid term; for details, please refer to the rules of vouchers published on Tencent Cloud's official website). You cannot redeem such voucher for cash or request to issue an invoice for such voucher. Such voucher can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) CDN provides services to multiple domains simultaneously, and compensations will be made only to the domains of which the global Service Availability fails to meet the standard within a Service Month. The amount of compensation will be calculated for each such month independently, and **the aggregate amount shall be no more than the aggregate monthly service fee for domains of which the Service Availability fails to meet the standard** (such monthly service fee shall exclude the portion deducted by a voucher or promotional credit or due to discounted service fee or otherwise deducted).

|**Service Availability (Av) for a Service Month**|   **Value of Compensation Voucher**|
|-|-|
|99.9% \> Av ≥ 99.0% |                                10% of the aggregate monthly service fee for domains of which the Service Availability fails to meet the standard|
|99.0% \> Av ≥ 95.0%|                                 25% of the aggregate monthly service fee for domains of which the Service Availability fails to meet the standard|
|95.0% \> Av |                                        50% of the aggregate monthly service fee for domains of which the Service Availability fails to meet the standard|

3.2  **Time Limit for Compensation Application**

(1) If the Service Availability for a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the fifth (5^th^) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail**.

(2) **You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard**. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

## 4.  Release of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service downtime shall not be counted towards Service unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

4.1  any request error due to the malfunction of the client's origin server;

4.2  any error due to a ban on or block of a domain name for any non-compliant content of a client or otherwise;

4.3  any change to configuration of a origin server or DNS of an accelerated domain by a client without prior notice to Tencent Cloud, resulting in the failure of a Tencent Cloud node server to access the client's origin server;

4.4  any loss or leak of data, passcode or password due to improper maintenance or improper confidentiality measures of a client;

4.5  any upgrade of the operation system by a client on its own;

4.6  any hacker attack on a client's website;

4.7  any impromptu increase of traffic of a client (increasing by 30% or more of the billed bandwidth in the preceding month) without at least three (3) business days prior written notice to Tencent Cloud;

4.8  any system maintenance with prior notice by Tencent Cloud to a client, including system cutover, maintenance, upgrade and malfunction simulation test;

4.9  any malfunction or configuration adjustment of network or equipment that is not Tencent Cloud facility;

4.10  any event of force majeure or accident;

4.11  any other reason not attributable to Tencent Cloud.

## 5.  Miscellaneous

5.1  The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.

5.2  Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

5.3  As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)
