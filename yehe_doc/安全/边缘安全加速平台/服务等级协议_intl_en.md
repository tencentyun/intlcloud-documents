In order to use the Tencent Cloud EdgeOne Service (the “Service”), you shall read and comply with this Tencent Cloud EdgeOne Service Level Agreement (this “Agreement”, or this “SLA”) and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, among others, the terms and definitions of the Service, Service Availability and Service Uptime Metrics, compensation plan and disclaimer of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or disclaiming certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.

Please do not purchase or use the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties. For the purposes of these Terms of Service, “Tencent Cloud” refers to the applicable Tencent entity as set forth in the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248).

**1. Terms and Definitions**

**1.1 Tencent Cloud EdgeOne**

Tencent Cloud EdgeOne Service refers to the acceleration and security services for the content and network services based on the edge computing nodes of Tencent Cloud. The SLA described herein applies to the data and request services of a single product (instance) only.

**1.2 Service Month(s)**

Service Month(s) refers to the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The Service Availability will be calculated separately for each Service Month.

**1.3 Service Region(s)**

The Service Region(s) in which the Tencent Cloud EdgeOne Service is available shall be subject to the information on the Tencent Cloud official website.

**1.4 Monthly Service Fee**

The Monthly Service Fee refers to the accumulated service fee for the services you use within a Service Month.

**1.5 Time Unit**

The usage statistics of the Service takes 5 minutes as a time unit, resulting in 288 measurement points each day. The measurement point of 00:00:00 represents the time slot from 00:00:00 to 00:04:59, and the rest can be deduced by analogy.

**1.6 Service Downtime within Service Month(s) Calculated in Minutes** 

Any Time Unit of the Service shall be considered as abnormal if the error rate within such Time Unit in the following situations (error rate within one Time Unit = the number of failed requests within such Time Unit / the total number of requests within such Time Unit) is more than 0.1%: 

(1) The business request of a zone proxy fails to reach the business server due to reasons solely attributable to the Tencent Cloud EdgeOne;

(2) The business server of a zone proxy returns 4xx and 5xx status codes due to reasons solely attributable to the Tencent Cloud EdgeOne;

(3) The packet loss rate by the Layer 4 proxy is higher than 20% or the success rate of TCP connections is lower than 30% due to reasons solely attributable to the Tencent Cloud EdgeOne.

The Service Availability is only applicable to the Tencent Cloud EdgeOne Service and does not apply to abnormalities caused by related services other than the Service (including, without limitation, full bandwidth or server room failure of the Customer's source station). If two consecutive Time Units are deemed to be abnormal, the 10 minutes is counted as unavailable unit time; and the abnormal time less than two consecutive Time Units is not counted as Service Downtime. The unavailable unit time in each Service Month is added up to get the Service Downtime within Service Month(s) Calculated in Minutes.

**1.7 Total Number of Minutes within Service Month(s)**

Total Number of Minutes within Service Month(s) = the total number of days of the Service Month(s) × 24 (hours) × 60 (minutes).

**2. Service Availability**

**2.1 Calculation of Service Availability**

Service Availability = ((Total Time of the Service within a Service Month Calculated in Minutes - Service Downtime within a Service Month Calculated in Minutes) / Total Time of the Service within a Service Month Calculated in Minutes) × 100%. The Service Availability will be calculated separately for each security and acceleration zone (instances) involved in the Service you use.

**2.2 Service Availability Standard**

The Service Availability for the Service shall be no less than 99.9% (“Service Availability Standard”). If the Service fails to meet the Service Availability Standard (except under circumstances as set forth in the Disclaimer of Liabilities), you may claim compensation in accordance with Article 3 of this Agreement.

**3. Compensation Plan**

In respect of the Service, if the Service Availability for a single instance of the Service fails to meet the Service Availability Standard, you will be entitled to compensations in accordance with the following terms:

**3.1 Standards of Compensation**

(1) Compensations will be made **in the form of voucher** by Tencent Cloud, and you should use the voucher by abiding the voucher usage rules (including usage period, etc., subject to the voucher usage rules published on Tencent Cloud official website). Such voucher cannot be converted into cash, and no invoice will be issued with respect thereof. The voucher may only be used to purchase the Service by using your Tencent Cloud account, and you cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability Standard is not met for any Service Month, the amount of compensation will be calculated for each such Service Month independently, and **the aggregate amount shall be no more than the aggregate Monthly Service Fee for the Service Month in which the Service Availability fails to meet the Service Availability Standard** (the Monthly Service Fee referred to herein shall be the cash amount you have actually paid, excluding the portion deducted by vouchers, coupons, service fee reduction or exemption, etc.). Standards of Compensation are as follows.

| **Service Availability in a Service Month** | **Value of Compensational Voucher** |
| ------------------------------------------------- | ----------------------------------------- |
| Less than 99.9% but is or higher than 99.0%       | 10% of the Monthly Service Fee            |
| Less than 99.0% but is or higher than 95.0%       | 25% of the Monthly Service Fee            |
| Less than 95.0%                                   | 50% of the Monthly Service Fee            |

**3.2 Time Limit for Compensation Application**

(1) If the Service Availability in a Service Month fails to meet the Service Availability standard, you may **apply for compensation only through the Tencent Cloud ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud shall prevail**.

(2) **You shall apply for compensation no later than the sixtieth (60th) calendar day following the end of the applicable Service Month in which the Service Availability fails to meet the abovementioned standard.** If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

**4. Disclaimer of Liabilities**

**If the Service is unavailable due to any of the following reasons, the corresponding Service Downtime shall not be counted towards Service Unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

- Any service unavailability due to the act of You or your end users, which poses a security threat to the Service provided by Tencent Cloud, or is fraudulent or illegal;

- Any service unavailability due to the device, software or technology of You or any third party (not directly controlled by Tencent Cloud);

- Any service unavailability due to your failure to use the products in accordance with the specification required by Tencent Cloud;

- Any service unavailability due to your non-payment or delay in payment;

- Any service unavailability due to a severe malfunction of a network operator;

- Any request error due to the malfunction of the Customer's source station;

- Any error due to a ban on or block of a domain name for any non-compliant content of the Customer or otherwise;

- Any change to configuration of an source station or DNS of an accelerated domain by the Customer without prior notice to the Tencent Cloud, resulting in the failure of a Tencent Cloud node server to access the Customer 's source station;

- Any loss or leak of data, passcode or password due to improper maintenance or improper confidentiality measures of the Customer;

- Any upgrade of the operation system by the Customer on its own;

- Any impromptu increase of traffic of the Customer (increasing by 30% or more of the billed bandwidth in the preceding month) without at least three (3) business days prior written notice to Tencent Cloud;

- Any service unavailability due to various source station issues at your business end (e.g., source station bandwidth running full, source station IP exposure, source station server room failure, source station link network jitter, etc.);

- Any system maintenance with prior notice by Tencent Cloud to the Customer, including system cutover, maintenance, upgrade and malfunction simulation test; or any service unavailability due to the maintenance or upgrade of any network, hardware or service (Tencent Cloud will notify you in advance of the schedule of maintenance in accordance with reasonable business principles);

- Any temporary service interruption arising from routine maintenance and upgrade to the Service by Tencent Cloud as described in the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248);

- Any service unavailability due to any event of force majeure;

- Any service unavailability due to any reason not attributable to Tencent Cloud;

- Any other circumstances in which Tencent Cloud will be exempted or released from its liabilities for compensation or otherwise according to relevant laws, regulations, agreements or rules, or any relevant rules or guidelines published by Tencent Cloud separately.

**5. Miscellaneous**

**The parties hereto acknowledge and agree that, for any losses incurred by you for the use of the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total Service Fees you have paid for the relevant Service which fails to meet the Service Availability Standard.If you have used the Service for more than 12 months, the maximum liability of Tencent Cloud for damages shall not exceed the fees you have paid to Tencent Cloud for the Service in the 12 months immediately preceding the date that event giving rise to the liability first occurred (for the avoidance of doubt, the fees refer to the cash that you have actually paid for your use of the Service, excluding vouchers and fees prepaid but not actually consumed).**

Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the Tencent Cloud official website. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted this Agreement as amended.

As an ancillary agreement to the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement is of the same legal effect as the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In respect of any matter not agreed herein, you shall comply with relevant terms under the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In case of any conflict or discrepancy between this Agreement and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement prevails to the extent of such conflict or discrepancy. 

The Service purchased by you shall be used only for your own business. If you operate without any applicable license or provide the Service to a third party by means of resale, sublease or otherwise, you shall be solely responsible for the liabilities arising therefrom. If Tencent Cloud suffers from any losses as a result thereof, you shall indemnify and hold Tencent Cloud harmless from such losses arising therefrom. (End)