**[Copyright Statement]**

© 2013-2020 Tencent Cloud All rights reserved. The copyright of this documentation is exclusively owned by Tencent Cloud. Without the prior written permission of Tencent Cloud, no entity shall copy, modify, plagiarize, or distribute all or part of this documentation in any form. 

**[Trademark Statement]**

“Tencent Cloud” and all other trademarks related to Tencent Cloud services are owned by Tencent Cloud Computing (Beijing) Co., Ltd. and its affiliates. Trademarks of third-party entities involved in this documentation are legally owned by the right holders thereof. 

**Service Statement**

This documentation is intended to introduce an overview of all or part of Tencent Cloud products and services to customers for the time being. Content of some products and services may be subject to changes. The type and standard of service of Tencent Cloud products and services you purchased shall be stipulated in the commercial agreements between you and Tencent Cloud. Unless otherwise agreed by both parties, Tencent Cloud does not make any express or implicit guarantees or warranties with regard to the content of this documentation. 

 

​                                                   **Face Recognition Service Level Agreement**

**In order to use the Tencent Cloud Face Recognition Service (hereinafter referred to as the “Service”), you shall read and comply with this Tencent Cloud Face Recognition Service Level Agreement (this “Agreement”, or this “SLA”) and the Tencent Cloud Service Agreement. This Agreement contains, among others, the terms and definitions of the Service, level indicators of the Service Availability or the Service Success Rate, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention. **

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

**1.    Terms and Definitions**

1.1  **Tencent Cloud Face Recognition Service**: the Tencent Cloud Face Recognition Service provided by Tencent Cloud is a technical method to identify a user by comparing his/her face in the selfie (or selfie video) with that in the ID photo. The Service mainly implements AI technologies such as liveness detection and facial recognition.

1.2  **Service Period**: a Service Period is one calendar month. The Service Availability is calculated on the basis of one Service Period, which is one calendar month. Any period shorter than one calendar month will not be counted as a Service Period and no Service Availability will be calculated for such period.

1.3  **Failed Request**: the Tencent Cloud Face Recognition Service deems any request with an error code of “InternalError” and any request that fails to reach the server end of the Face Recognition Service due to the malfunction of the Tencent Cloud Face Recognition Service as a Failed Request, excluding any of the following requests:

(1) any request failed by the Face Recognition Service due to requests in excess of the QPS (Query Per Second) of the Face Recognition Service (error code: InternalError) which results from the adoption of inappropriate access modes.

(2) any error request or unavailability of the Service due to reasonable upgrades, modifications, or suspensions initiated by the Face Recognition Service.

(3) any request failed by the Face Recognition Service (error code: InternalError) due to hacker attacks on your application.

1.4  **Valid Request:** any request received by the server end of the Tencent Cloud Face Recognition Service will be deemed as a Valid Request, **excluding any of the following requests**:

(1) any request that is sent without subscription to or authorization of the Service, that fails the authentication, and that is sent with overdue fees or with incorrect keys.

(2) any request sent by your application suffering attacks by hackers.

**Error Rate Per 5 Minutes****: Error Rate Per 5 Minutes = (Count of Failed Requests per 5 minutes / Count of all requests per 5 minutes) \* 100%**

1.5  **Monthly Service Fee****:** The total of service fees you paid for the Face Recognition Service within a calendar month. If you have paid service fees for multiple months in a lump sum, the Monthly Service Fee will be calculated by dividing the service fees by the number of the months you paid for.

**2.    Service Availability**

The Tencent Cloud Face Recognition Service promises a Service Availability of **99.9%**. You are entitled to the compensation as set forth in Section 3 of this Agreement if the Service Availability fails to meet the Service Availability promised above.

**2.1  Calculation of the Service Availability**

The Service Availability of the Tencent Cloud Face Recognition Service is calculated on the basis of Service Periods. The average of the Error Rate Per 5 Minutes is calculated by dividing the sum of Error Rate Per 5 Minutes within a Service Period by the total number of 5-minute periods in that Service Period, from which the Service Availability is then derived, i.e., Service Availability = ( 1 – The sum of Error Rate Per 5 Minutes in a Service Period / The total number of 5-minute periods in that Service Period ) * 100%.

*Note: the total number of 5-minute periods in a Service Period = 12\*24\*number of days in that Service Period*

**2.2  The Scope of Release of Liability**

If the Service is unavailable due to any of the following circumstances, such unavailability of the Service will be excluded from the scope of compensation:

(1) ordinary system maintenances and upgrades;

(2) maintenance or malfunction of any external object on which the Service relies;

(3) where the Service is unavailable due to reasons attributable to you or any third party, or due to *force majeure*;

(4) any circumstance where the Service is unavailable or failed to meet the Service Availability standard due to any reason not attributable to Tencent Cloud;

(5) any other circumstance where Tencent Cloud will be exempted or released from its liabilities for compensation or otherwise according to relevant laws, regulations, agreements or rules, or any relevant rules or guidelines published by Tencent Cloud separately.

**3.    Compensation Plan**

In respect of the Service, if the Service Availability is lower than 99.9%, you will be entitled to compensations in accordance with the following terms:

**3.1  Standards of Compensation**

(1) Compensations will be made in the form of **voucher (and not cash)** by Tencent Cloud. Such voucher can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability in a Service Month fails to meet the abovementioned standard, the amount of compensation shall be calculated for such Service Month independently, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such Service Month** (the Monthly Service Fee referred to herein shall exclude the portion deducted by a voucher or promotional coupon, due to discounted service fee or otherwise deducted).

>  Note:
>
>  the Service Month in this Agreement means every calendar month within the term of the Service purchased by you. For example, if you purchase the Service for a term of two months starting from March 17, the first Service Month will be from March 17 to March 31, the second will be from April 1 to April 30, and the third will be from May 1 to May 16.*

| **Service   Availability in a Service Month** | **Value of   Compensational Voucher** |
| --------------------------------------------- | ------------------------------------- |
| Less than   99.9% but is or higher than 95%   | 10% of the   Monthly Service Fee      |
| Less than 95%   but is or higher than 90%     | 25% of the   Monthly Service Fee      |
| Less than 90%                                 | 100% of the   Monthly Service Fee     |

 

**3.2  Time Limit for Compensation Application**

1、If the Service Availability in a Service Month fails to meet the Service Availability standard, you may **apply for compensation only through the support ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud shall prevail**.

**2、You shall apply for compensation no later than the sixtieth (60th) calendar day following the end of the applicable Service Month in which the Service Availability fails to meet the abovementioned standard.** If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

**4.    Requirements of Legal Compliance**

**When you use the Tencent Cloud Face Recognition Service, you shall ensure that the following conditions are met before you submit the subject’s information to Tencent Cloud for ID verification:**

4.1  The subject’s information is obtained with legitimate and valid methods or means.

4.2  You shall include in relevant agreements of services provided by you to the public the following terms or similar terms: “The user authorizes Company XX (i.e., “you” in this Agreement), unless otherwise provided by laws and regulations, to provide the information provided by the user to Company XX and the information generated by using Company XX’s services (including the information provided and generated before the signing of this authorization provision), etc., to Company xx and the partners with whom Company XX cooperates or to whom Company XX  entrusts (including the necessary service providers of such partners) due to the necessity of services, so as to provide services and recommend products to customers, carry out market surveys and data analysis of the information and so forth. Company XX promises to, and will require its partners (including their necessary service providers) to, keep the abovementioned information strictly confidential and take measures to protect the information security.” In addition, you shall keep the authorization agreement signed by you and your users on file on Tencent Cloud for future reference. You shall inform the information subject of the legal implications of such authorization.

4.3  The authorization of the information subject shall cover the identification activities by Tencent Cloud and the legitimate and reasonable scope of use of the subject’s information by Tencent Cloud.

4.4  Otherwise, Tencent Cloud has the right to terminate the Service, and you shall be liable for compensating all losses incurred by Tencent arising therefrom.

**5.    The Reviewability of the Service**

In accordance with existing laws and regulations, Tencent Cloud may provide relevant information, including the operation logs of key components, maintenance personnel’s operation records, customers’ operation records and other information for the needs of cooperating with supervisions, or security investigations and evidence collection of regulatory agencies of the government, provided that procedures are obeyed and formalities are complete.



**6.    The Accuracy of Measurement of Services**

Fees of Tencent Cloud services are expressly displayed both in the customer management center and on the order page. Customers can select specific types of services on their own and purchase such services at the specified prices.

**7.    Miscellaneous**

Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. 