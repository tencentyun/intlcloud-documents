**In order to use the Tencent Cloud Data Subscription Service (the “Service”), you shall read and comply with this Tencent Cloud Data Subscription Service Level Agreement (this “Agreement”, or this “SLA”) and the** [**Tencent Cloud Service Agreement**](https://intl.cloud.tencent.com/document/product/301/9248)**. This Agreement contains, among others, the terms and definitions of the Service, Service Availability or success rate, compensation plan and disclaimer of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or disclaiming certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties. For the purposes of these Terms of Service, “Tencent Cloud” refers to the applicable Tencent entity as set forth in the Tencent Cloud Service Agreement.**

## 1. Terms and Definitions

#### 1.1 Data Subscription Service

Refers to the unified incremental data subscription services provided by Tencent Cloud to you with Tencent Cloud database as the core through the data subscription service in the Data Transmission Service products, including the data subscription service, data subscription SDK, etc. The specific content of the Service is subject to the service you have purchased and the service provided by Tencent Cloud. You can subscribe to the incremental data of Tencent Cloud database through the Service and consume it in the real time to achieve the application of incremental data by downstream systems.

#### 1.2 Service Month(s)

Refers to the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 7, there will be four (4) Service Months (the first Service Month from March 7 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 6). The Service Availability will be calculated separately for each Service Month.

#### 1.3 Service Downtime Calculated in Minutes within a Service Month

If you continuously fail to consume all information through the Data Subscription SDK of the Service and the failure state lasts for more than 5 minutes, the minutes in the failure state will be counted as Service Downtime Calculated in Minutes within a Service Month (less than 1 minute will be counted as 1 minute). For example, if the failure status lasts for 6 minutes and 01 seconds, Service Downtime Calculated in Minutes is calculated as 7 minutes. The sum of Service Downtime Calculated in Minutes in a Service Month is Service Downtime Calculated in Minutes within a Service Month.

#### 1.4 Total Number of Minutes within a Service Month

Total Number of Minutes within a Service Month = the total number of days of the Service Month × 24 (hours) × 60 (minutes).

#### 1.5 Monthly Service Fee

Refers to the total service fee you pay for a single Data Subscription Service in a Service Month, excluding the amount you have purchased but not yet consumed. If you pay for several Service Months at once, the Monthly Service Fee will be apportioned based on the number of Service Months purchased.


## 2. Service Availability

#### 2.1 Calculation of Service Availability

Service Availability shall be calculated on the basis of a single instance as follows:

Service Availability = (1 - Service Downtime Calculated in Minutes within a Service Month of a single instance / Total Number of Minutes within a Service Month of a single instance) × 100% 

The single instance refers to a data subscription instance created through the Tencent Cloud Data Subscription console.

#### 2.2 Service Availability Standard

The Service Availability of the Service provided by Tencent Cloud shall be no less than 99.95% (“Service Availability Standard”). **If the Service fails to meet the Service Availability Standard (except under circumstances as set forth in the Disclaimer of Liabilities), you may claim compensation in accordance with Article 3 of this Agreement.**

## 3. Compensation Plan

In respect of the Service, if the Service Availability fails to meet the Service Availability Standard, you will be entitled to compensations in accordance with the following terms:

#### 3.1 Standards of Compensation

(1) Compensations will be made **in the form of voucher** by Tencent Cloud, and you should use the voucher by abiding the voucher usage rules (including usage period, etc., subject to the voucher usage rules published on Tencent Cloud official website). Such voucher cannot be converted into cash, and no invoice will be issued with respect thereof. The voucher may only be used to purchase the Service by using your Tencent Cloud account, and you cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability in a Service Month fails to meet the Service Availability Standard, the amount of compensation shall be calculated for such Service Month separately, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such Service Month** (the Monthly Service Fee referred to herein shall exclude the portion deducted by vouchers, coupons, service fee reduction or exemption, etc.).

| **Service Availability in a Service   Month** | **Value of Compensational Voucher** |
| --------------------------------------------- | ----------------------------------- |
| Less than 99.95% but is or higher than 99%    | 10% of the Monthly Service Fee      |
| Less than 99% but is or higher than  95%      | 25% of the Monthly Service Fee      |
| Less than 95%                                 | 50% of the Monthly Service Fee      |

#### 3.2 Time Limit for Compensation Application

(1) If the Service Availability in a Service Month fails to meet the Service Availability Standard, you may **apply for compensation only through the Tencent Cloud ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud shall prevail**.

(2) **You shall apply for compensation no later than the sixtieth (60th) calendar day following the end of the applicable Service Month in which the Service Availability fails to meet the Service Availability Standard.** If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

#### 4. Disclaimer of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service Downtime shall not be counted towards Service Unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you****:**

4.1 any system maintenance with prior notice by Tencent Cloud, including system cutover, maintenance, upgrade and malfunction simulation test;

4.2 any failure or configuration adjustment of any network or equipment that is not attributable to Tencent Cloud;

4.3 any attack on your application interface or data, or any other misconduct;

4.4 any loss or leak of data, passcode or password due to your improper maintenance and improper confidentiality measures;

4.5 any negligence in authorization or mal-operation by you, or any of your equipment, or third-party software or device;

4.6 any failure of you to abide by documentation or suggestions for using Tencent Cloud products;

4.7 any delayed or dropped pushes due to usage exceeding the service capability limit of the current paid version;

4.8 any unavailability of the Service or failure to meet the Service Availability Standard due to any reason not attributable to Tencent Cloud; 

4.9 any other circumstances in which Tencent Cloud will be exempted or released from its liabilities for compensation or otherwise according to relevant laws, regulations, agreements or rules, or any relevant rules or guidelines published by Tencent Cloud separately.

#### 5. Miscellaneous

**5.1 The parties hereto acknowledge and agree that, for any losses incurred by you for the use of the Service due to any breach by Tencent Cloud, the aggregate liability of Tencent Cloud shall under no circumstance exceed the total Service Fees you have paid for the relevant Service which fails to meet the Service Availability Standard. If you have used the Service for more than 12 months, the total aggregate liability of Tencent Cloud shall not exceed the total Service Fees you have paid to Tencent Cloud for the Service which fails to meet the Service Availability Standard in the 12 months immediately preceding the date that event giving rise to the liability first occurred.** 

5.2 Tencent Cloud shall be entitled to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the Tencent Cloud website. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted this Agreement as amended.

5.3 As an ancillary agreement to the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement is of the same legal effect as the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In respect of any matter not agreed herein, you shall comply with relevant terms under the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In case of any conflict or discrepancy between this Agreement and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement prevails to the extent of such conflict or discrepancy. (End)