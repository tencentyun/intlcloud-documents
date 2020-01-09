**Media Processing Service Level Agreement**

**In order to use the Tencent Cloud Media Processing Service (the “MPS” or “Service”), you should read and observe this Media Processing Service Level Agreement (this “Agreement”, or this “SLA”) and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, among others, the terms and definitions of the Service, Service availability and Service uptime metrics, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, may be in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

## 1. Terms and Definitions

**1.1   Tencent Cloud Media Processing Service:** means the audio and video transcoding, content identification and video moderation service provided by Tencent Cloud. For details, please refer to the Service you purchase and the contents of the Service provided by Tencent Cloud. 

**1.2     Error Rate** = (the number of “5xx” errors within unit time + the number of requests made by a user in a regular way that fail to reach the MPS server due to Service malfunction within unit time) / the number of all requests made by a user within unit time.

5xx: HTTP status code indicating server errors.

 **1.3    Service Unavailability:**  If the Error Rate of the Service is higher than 0.5% (exclusive) within one unit time (each five (5) minutes as one calculation time unit), it shall be deemed that the Service is unavailable within such unit time; when such situation lasts for ten (10) minutes or more, such time shall be counted into the Service Downtime, while any such situation that lasts less than ten (10) minutes will not be counted into the Service Downtime.  The Service Downtime is calculated based on the Error Rate on the server end.

For example, assuming that the number of total requests for MPS made by user A within five (5) minutes is 10,000, during which period there’s no Service malfunction and the number of “5xx” errors returned is 100, then the Error Rate would be calculated as follows: (100 + 0)/10000 = 1%, *i.e.*, higher than 0.5%, and such five (5) minutes will be counted towards the Service Downtime.

**1.4    Service Downtime:** means the aggregate time of Service Unavailability calculated in minutes within a Service Month.

**1.5    Service Month(s):** means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The availability of the Service will be calculated independently for each Service Month.

**1.6    Significant Impromptu Increase of Business Scale:** The Service is not subject to any transcoding limitation, and is scalable on a dynamic basis to meet your actual business needs; *provided, however*, that you should notify Tencent Cloud at least three (3) business days in advance in writing in case of any significant impromptu increase of business scale, otherwise the availability of the Service may be affected. Tencent Cloud does not make any guarantee to the availability of the Service in case of any significant impromptu increase of business scale that you fail to so notify Tencent Cloud, nor will Tencent Cloud be liable for any impact on the availability of the Service thereof. 

**Impromptu Increase Metrics**:

- transcoding: the output of transcoding expected to increase by more than 100,000 minutes/day.

- video moderation: the volume of video moderation expected to increase by more than 40,000 minutes/day.

- content identification: the volume of content identification expected to increase by more than 40,000 minutes/day.

## 2. Service Availability/ Service Uptime Metrics

#### 2.1     **Calculation of Service Availability**

Service Availability = (1 - Service Downtime / total time within a Service Month) × 100%

#### 2.2     **Standard of Service Availability/ Service Metrics**

**The Service Availability of the Service provided by Tencent Cloud will be no less than 99.70%**. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below. 

##  3. Service Compensation

In respect of this Service, if the Service Availability fails to meet the abovementioned standard, you will be entitled to compensations in accordance with the following terms:

#### 3.1     **Standards of Compensation**

  (1) Compensations will be made **in the form of voucher** by Tencent Cloud, and you should follow the rules for using the voucher (including the valid term; for details, please refer to the rules of vouchers published on Tencent Cloud’s official website). You cannot redeem such voucher for cash or request to issue an invoice for such voucher. Such voucher can only be used to purchase the Service (Tencent Cloud Media Processing Service) by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

  (2) If the Service Availability for a Service Month fails to meet the standard, the amount of compensation will be calculated for such month independently, and **the aggregate amount shall be no more than the applicable monthly service fee paid by you for such month** (the monthly Service fee referred to herein shall exclude the fee deducted by a voucher or promotional coupon, Service fee discounted or waived, or fees otherwise deductible). 

| **Service   Availability** **(Av)** **for a Service Month** | **Value   of Compensation Voucher**                     |
| ----------------------------------------------------------- | ------------------------------------------------------- |
| 99.70% > Av ≥ 99%                                           | 10% of the monthly service fee for the applicable month |
| 99% > Av ≥ 95%                                              | 25% of the monthly service fee for the applicable month |
| 95% > Av                                                    | 50% of the monthly service fee for the applicable month |

 

#### 3.2     **Time Limit for Compensation Application**

  (1) If the Service Availability for a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the third (3rd) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail**.

  (2) **You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard**. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

#### 3.3     **Application Materials for Compensation**

If you believe that the Service fails to meet the Service Availability standards specified hereunder, you may submit the compensation application within the period set forth under this SLA. Your compensation application shall be submitted along with at least the following documents:

  (1)   the appid of the account for which the Service is unavailable.

  (2)     the duration of the Service Unavailability and other relevant evidence thereof.

##  4. Release of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service downtime shall not be counted towards Service Unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

4.1 any system maintenance with prior notice by Tencent Cloud to you, including system cutover, maintenance, upgrade and malfunction simulation test;

4.2 any malfunction or configuration adjustment of any network or equipment that is not Tencent Cloud facility;

4.3 any attack on any of your application endpoints or data, or any other mal-operation;

4.4 any loss or leak of data, passcode or password due to your improper maintenance or improper confidentiality measures;

4.5 any negligence in authorization or mal-operation by you, or any of your equipment, or third-party software or device;

4.6 any failure of you to abide by user guide or suggestions for using Tencent Cloud products;

4.7 any malfunction due to block of a domain name caused by your illegal or prohibited content or otherwise;

4.8 any decline in the availability of the Service due to your impromptu increase of traffic without prior written notice to Tencent Cloud;

4.9 any Service Unavailability or failure of the Service to meet the availability standard due to any reason not attributable to Tencent Cloud;

4.10 any other circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately;

4.11 Tencent Cloud provides you with the Service only, and shall under no circumstance be liable for any violation of any law, regulation or government policy, or any infringement upon any right or interest of any third party, by any video provided by you.

##  5. Miscellaneous

**5.1  The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.**

5.2  Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course, and will announce such amendment via a notice on its website, an email notice or a text message notice. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended, and no additional consent is required from you therefor.

**5.3  As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy.**

5.4  This Agreement is executed in Nanshan District, Shenzhen, Guangdong Province, the People’s Republic of China (“**China**”). The formation, effectiveness, performance, interpretation and dispute resolution of this Agreement shall be governed by law of the China (for the purpose of this Agreement only, excluding China’s Hong Kong, Macau and Taiwan), without regard to the conflict of law.

5.5  In case of any dispute or claim between you and Tencent Cloud in connection with this Agreement, it shall first be resolved through friendly negotiation.  If such dispute or claim cannot be settled amicably, you agree to submit such dispute or claim to a people’s court with competent jurisdiction in the place where this Agreement is executed (*i.e.*, Nanshan District, Shenzhen, Guangdong Province). (End of Document).