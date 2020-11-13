**Secrets Manager Service Level Agreement**

**In order to use the Tencent Cloud Secrets Manager Service (the “Service”), you shall read and comply with this Secrets Manager Service Level Agreement (this “Agreement”, or this “SLA”) and the** [**Tencent Cloud Service Agreement**](https://intl.cloud.tencent.com/document/product/301/9248)**. This Agreement contains, among others, the terms and definitions of the Service, level indicators of the Service Availability or success rate, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

**1. Terms and Definitions**

**1.1 Failed Request**

Refers to a request returned with an “InternalError” error code after such request is sent by you during the use of the Service (excluding circumstances covered by provisions of release of liabilities).

**1.2 Valid Request**

A request received by the server end of the Secrets Manager is deemed as a Valid Request (excluding circumstances covered by provisions of release of liabilities).

**1.3 Error Rate Per 5 Minutes**

The Error Rate Per 5 Minutes is calculated on the basis of consecutive 5-minute periods. Error Rate Per 5 Minutes = Failed Requests per 5 minutes / Total Valid Requests per 5 minutes x 100%

**1.4 Total Number of 5-Minute Periods in A Service Period**

The Total Number of 5-Minute Periods in A Service Period = 12 * 24 * Number of Days in that Service Period.

**1.5 Service Month(s)** 

Service Month(s) means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The Service Availability will be calculated separately for each Service Month.

**2. Service Availability/Service Success Rate**

**2.1 Calculation of Service Availability/Service Success Rate**

Service Availability = (1 – The Sum of Error Rate Per 5 Minutes in a Service Month / Total Number of 5-Minute Periods in a Service Month) × 100%

**2.2 Service Availability/Service Indicator Standard**

The Service Availability of the Service provided by Tencent Cloud will be no less than 99.90%. The customer is entitled to the compensation as set forth in Section 3 of this Agreement if the Service Availability of the Secret Manager Service fails to meet the aforementioned standard, other than in any circumstance as provided in the Release of Liabilities provisions.

**2.3 Examples**

(1) Presume that the user accesses the Service and sends a total number of 1,000,000 requests in a 5-minute period, during which there is no node failure, and there are 1,000 responses with an “InternalError” error code, then the Error Rate = (1,000 + 0) / 1,000,000 = 0.1%.

(2) Total Number of 5-Minute Periods in A Service Period = 12 × 24 × 30 = 8640 (periods).

(3) If the Service Availability calculated with the aforementioned formula is less than 99.90%, the Service of that month under the SLA is deemed as failed to meet the Standard.

**3. Compensation Plan**

In respect of the Service, if the Service Availability is less than 99.90%, you will be entitled to compensations in accordance with the following terms:

**3.1 Standards of Compensation**

(1) Compensations will be made **in the form of voucher (and not cash)** by Tencent Cloud. Such voucher can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability in a Service Month fails to meet the abovementioned standard, the amount of compensation shall be calculated for such Service Month independently, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such Service Month** (the Monthly Service Fee referred to herein shall exclude the non-cash fee deducted by a voucher, a promotional coupon, or otherwise).

| Service Availability in a Service Month      | Value of Compensational Voucher   |
| -------------------------------------------- | --------------------------------- |
| Less than 99.90% but is or higher than 99%| 10% of the Monthly Service Fee|
| Less than 99% but is or higher than 95%   | 25% of the Monthly Service Fee |
| Less than 95%                             | 100% of the Monthly Service Fee|

**3.2 Time Limit for Compensation Application**

(1) If the Service Availability in a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation only through the support ticket system under your relevant account after the fifth (5th) business day of the month immediately following such Service Month. **Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month,** **both parties agree that the back-end record of Tencent Cloud shall prevail.**

(2) You shall apply for compensation no later than the sixtieth (60th) calendar day following the end of the applicable Service Month in which the Service Availability fails to meet the abovementioned standard. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, **it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.**

**3.3 Application Materials for Compensation**

If you believe that the Service fails to meet the Service Availability standard, you may apply for compensation within the period of time as stipulated under this SLA, and you should at least provide the following information together with your compensation application:

(1) a detailed description of the incident, which shall include the specified date, time, and duration when the Service was unavailable and other details on the Service unavailability.

(2) other information Tencent Cloud reasonably requires you to provide.

**4. Release of Liabilities**

**If the Service is unavailable due to any of the following reasons, the corresponding duration of Service unavailability shall not be considered when calculating the Service unavailability period, shall not be eligible for compensation by Tencent Cloud, and Tencent Cloud shall not be held liable to you:**

4.1 any system maintenance with prior notice by Tencent Cloud, e.g., system cutover, maintenance, upgrade, malfunction simulation test, and other planned downtime;

4.2 any failure or configuration adjustment of any network or equipment that is not a Tencent Cloud facility;

4.3 any unavailability caused by a third-party other than Tencent Cloud, e.g., any availability caused by an attack by hackers or the negligence of a third-party supplier of yours;

4.4 any loss or leak of data, passcode or password due to your improper maintenance or improper confidentiality measures;

4.5 any incorrect operation resulted from your negligence or operation you have authorized;

4.6 any failure of you to abide by documentation or instructions for using Tencent Cloud products;

4.7 any request sent by the user who has not subscribed to the Service or has overdue service fees;

4.8 any force majeure;

4.9 any unavailability of the Service or failure to meet the Service Availability standard due to any reason not attributable to Tencent Cloud;

4.10 any other circumstances in which Tencent Cloud will be exempted or released from its liabilities for compensation or otherwise according to relevant laws, regulations, agreements or rules, or any relevant rules or guidelines published by Tencent Cloud separately.

**5. Miscellaneous**

**5.1** **The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total Service Fees you have paid for the relevant Service which is not performed.**

5.2 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

5.3 As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)

 