# Service Level Agreement

**In order to use the TI Platform TIONE (the “Service”), you shall read and comply with this TI Platform TIONE Service Level Agreement (this “Agreement”, or this “SLA”) and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, among others, the terms and definitions of the Service, level indicators of the Service availability and success rate, compensation plan and disclaimer of liabilities. Unless otherwise stipulated, this Agreement does not apply to functions of the Service’s closed beta testing. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.
Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.
**

## 1. Terms and Definitions

#### 1.1 Service Month(s)

Service Month(s) refers to the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The Service Availability will be calculated separately for each Service Month.

#### 1.2 Total Time of a Service Month Calculated in Minutes

Total Time of a Service Month Calculated in Minutes = The number of days of the Service Month × 24 (hours) × 60 (minutes).

#### 1.3 Service Downtime Calculated in Minutes within a Service Month

Refers to the service downtime that lasts longer than 5 minutes due to the platform anomalies. Intermittent service unavailability of less than 5 minutes cannot be counted towards the Service Downtime of the Service Month.

#### 1.4 Scope of Services Unavailability

Refers to the circumstances where the platform interface is accessible due to the platform anomalies as confirmed by the logs of the TIONE platform.

#### 1.5 Service Area Applicable to the Service

Refers to all area covered by the Service.

## 2. Service Availability

#### 2.1 Calculation of Service Availability

Service Availability = 1 - (Service Downtime Calculated in Minutes within a Service Month / Total Time of a Service Month Calculated in Minutes) × 100% 

#### 2.2 Standards of Service Availability

The Service Availability of the Service provided by Tencent Cloud will be no less than 99.9%. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the disclaimer of liabilities provisions below.

## 3. Compensation Plan

#### 3.1 Scope of Compensation

Tencent Cloud TI Platform TIONE provides compensation for affected product features including without limitation the following:

（1）Data loss or data access anomalies due to the Tencent Cloud TI Platform TIONE services.
（2）Training task anomalies due to model training components of Tencent Cloud TI Platform TIONE.
（3）Anomalies of service publishing function and service access function due to online service components of Tencent Cloud TI Platform TIONE.

> ？
> The following features are beyond the scope of compensation for Standards of Service Availability of the Service.
> - Effect caused open-source software Kubernetes, Docker, operating system kernel, TensorFlow, Pytorchand and other open-source portions.
> - Effect caused by relevant Tencent Cloud products per se, e.g., failure for online service publishing and access due to CLB interface anomaly, anomaly for the platform to create resources because the quota has been reached or the resources are sold out.
> - Data, tasks and service anomalies due the user's failure to use the platform reasonably in accordance with its operating rules.

#### 3.2 Standards of Compensation

The Service Availability for each TI Service is calculated separately and the compensation amount is calculated according to the criteria in the table below. The compensation shall be limited to vouchers used to purchase the TI products and the total amount of compensation shall not exceed the monthly service fee paid by the user for the TI Service during the month in which the Service Availability is not reached (excluding the offset with vouchers).

| Service Availability in a Service Month    | Value of Compensational Voucher|
| :-------------------------- | :--------------------- |
| Less than 99.90% but is or higher than 95.00% | 10% of the Monthly Service Fee     |
| Less than 95.00%               | 30% of the Monthly Service Fee     |


#### 3.3 Time Limit for Compensation Application

（1）If the Service Availability for a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation through (and only through) the support ticket system under your relevant account after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, both parties agree that the back-end record of Tencent Cloud will prevail.
（2）You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you. 


## 4. Disclaimer of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service Downtime shall not be counted towards service unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**
4.1 Any system maintenance with prior notice by Tencent Cloud to you, including system cutover, maintenance, upgrade and failure simulation test;
4.2 Any failure or configuration adjustment of network or equipment that is not Tencent Cloud facility;
4.3 Any attack on your application interface or data, or any other misconduct;
4.4 Any loss or leak of data, pin or password due to your improper maintenance or improper confidentiality measures;
4.5 Any negligence in authorization or mal-operation by you, or any of your equipment, or third-party software or device;
4.6 Any failure of you to abide by documentation or suggestions for using Tencent Cloud products;
4.7 Any Service unavailability or failure of the Service to meet the availability standard not attributable to Tencent Cloud;
4.8 Any other circumstances in which Tencent Cloud will be exempted or disclaimed from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately.


**Before using the Tencent Cloud TI Platform TIONE, you should read carefully the relevant service description, technical specification and operation guide, etc. in official documentation of Tencent Cloud, and fully understand the relevant content and potential consequences. You understand and agree that, your use of the Tencent Cloud TI Platform TIONE is based on your sole independent and prudent judgement, and you shall be responsible for your own judgement or actions, including without limitation:**

(1) You should decide on your own the compatibility between the model training, inference and other related services, and the frame mirror and hardware computing power you choose;
(2) The TI Platform TIONE Service does not guarantee the availability of operating system and kernel defects caused by the community;
(3) You shall be responsible for your own operations (e.g., resource limitation configuration, container image configuration, code writing and business logic setting);
(4) If you use other paid Tencent Cloud products while using the Service, you shall pay for such products in accordance with the corresponding pricing arrangement and observe corresponding service terms;
(5) The Service is only responsible for the availability of its own service module of the machine learning platform, including training tasks, notebook and service publishing, etc. For other Tencent Cloud products such as TKE, CLB, CBS and API Gateway, please refer to relevant service level agreements. You shall be solely responsible for correctness and usability of custom parts (e.g. inference code, training code, training data, model files, etc.).

## 5. Miscellaneous

5.1 The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total Service Fees you have paid for the relevant Service which is not performed.

5.2 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary with notice in light of changes in due course. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

5.3 As an ancillary agreement to the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement is of the same legal effect as the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In respect of any matter not agreed herein, you shall comply with relevant terms under the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In case of any conflict or discrepancy between this Agreement and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)






