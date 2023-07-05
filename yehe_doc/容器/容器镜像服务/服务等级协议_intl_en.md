**Tencent Container Registry Enterprise Edition Service Level Agreement**

This Tencent Container Registry Enterprise Edition Service Level Agreement shall be effective on December 7, 2020.

**In order to use the Tencent Container Registry Enterprise Edition (the “Service”), you shall read and comply with this Tencent Container Registry Enterprise Edition Service Level Agreement (this “Agreement”, or this “SLA”) and the** [**Tencent Cloud Service Agreement**](https://intl.cloud.tencent.com/document/product/301/9248)**. This Agreement contains, among others, the terms and definitions of the Service, level indicators of the Service Availability or success rate, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

## 1. Terms and Definitions



#### 1.1 Tencent Container Registry (TCR)



Refers to the cloud hosting and distribution service for container images and other cloud-native products provided to you (or the “**Client**”) by Tencent Cloud through the Tencent Cloud Platform, which includes a free Personal Edition and a paid Enterprise Edition. 

#### 1.2 Tencent Container Registry Enterprise Edition (TCR EE)



Refers to the enterprise-level cloud hosting and distribution service for container images and other cloud-native products provided to you (or the “**Client**”) by Tencent Cloud through the Tencent Cloud Platform, which supports the storage and distribution of Docker images and Helm Chart and security scan of images, and provides enterprise clients with granular access management and network access control. The service offers a paid tier; the user can purchase dedicated Registry Instances from the product console and enjoy the guarantees of this SLA. In this documentation, the Tencent Container Registry or TCR shall by default mean the Enterprise Edition thereof. 

#### 1.3 Single Instance



A Container Registry Instance with the unit count of 1.

#### 1.4 Total Minutes of a Single Instance in a Service Month



Calculated by the formula: The total number of days in a Service Month for a Single Instance × 24 (hours) × 60 (minutes).

#### 1.5 Instance Unavailable Minutes



A TCR EE Instance is deemed as unavailable in a minute if, within such minute, the client side attempts to access the given TCR EE Instance but is continuously returned with internal errors or fails to upload or pull images. The Instance Unavailable Minutes are the total number of minutes in which a TCR EE Instance is unavailable in a Service Period.

#### 1.6 Service Month(s)



Service Month(s) means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months, with the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16. The Service Availability will be calculated separately for each Service Month.

#### 1.7 The Most Relevant Cloud Product



The use of the Tencent Container Registry feature through this Service involves the use of Tencent Cloud’s Cloud Object Storage (COS) product. The Most Relevant Cloud Product refers to the policy that if the malfunction of operation is attributable to a TCR component, the compensation shall be limited to the fees of the directly impacted product and exclude the fees of indirectly impacted products. The applicable circumstances include but not limited to: (1) If the COS interface as the backend of TCR malfunctions, the compensation shall be limited to the fees of the object storage service and exclude the fees of the TCR.

## 2. Service Availability



#### 2.1 Calculation of Service Availability



The Service Availability shall be calculated on the basis of a Single Instance and with the following formula: Service Availability = (Total number of minutes in a Service Period – Unavailable Minutes of the Service) / Total number of minutes in a Service Period × 100%.

#### 2.2 Service Availability Standard



The Service Availability of the Service provided by Tencent Cloud will be no less than **99.9%**. You are entitled to the compensation as set forth in Section 3 of this Agreement if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided in the Release of Liabilities provisions.

## 3. Compensation Plan



In respect of the Service (Tencent Container Registry Enterprise Edition), if the Service Availability is less than **99.9%**, you are entitled to compensations in accordance with the following terms:

#### 3.1 Standards of Compensation



(1) Compensations will be made in the form of **voucher** by Tencent Cloud, and you should follow the rules for using the voucher (including the valid term; for details, please refer to the rules of vouchers published on Tencent Cloud’s official website). You cannot redeem such voucher for cash or request to issue an invoice for such voucher. Such voucher can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability in a Service Month fails to meet the abovementioned standard, the amount of compensation shall be calculated for such Service Month independently, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such Service Month** (the Monthly Service Fee referred to herein shall exclude the non-cash fee deducted by a voucher, a promotional coupon, or otherwise).



| Service Availability in a   Service Month (Av) | Value   of Compensational Voucher |
| ---------------------------------------------- | --------------------------------- |
| 99.9% > Av ≥ 90%                               | 10% of the Monthly Service Fee    |
| 90% > Av                                       | 25% of the Monthly Service Fee    |



#### 3.2 Time Limit for Compensation Application



(1) If the Service Availability in a Service Month fails to meet the abovementioned Service Availability standard, **you may apply for compensation only through the support ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. **If there is any dispute over the calculation of the Service Availability for a Service Month,** **both parties agree that the back-end record of Tencent Cloud shall prevail.**

(2) **You shall apply for compensation no later than the sixtieth (60th) calendar day following the end of the applicable Service Month in which the Service Availability fails to meet the abovementioned standard.** If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

#### 3.3 Application Materials for Compensation

If you believe that the Service fails to meet the standards of the Service Availability or the service response period, you may apply for compensation within the period of time as stipulated under this Agreement. For the convenience of verifying the circumstance, you shall at least provide the following information together with your compensation application:

(1) The date, start time, end time of the failure and a simple description of the failure.

(2) The screenshot or screencast of the failure or the system log.

(3) Other relevant information such as the account, device information (such as the models of the device hardware, the operation system, and the browser), the software configurations, and debugging information.

## 4. Release of Liabilities



**If the Service is unavailable due to any of the following reasons, the corresponding duration of Service unavailability shall not be considered when calculating the Service unavailability period, shall not be eligible for compensation by Tencent Cloud, and Tencent Cloud shall not be held liable to you:**

4.1 any failure or configuration adjustment of any network or equipment that is not a Tencent Cloud facility;

4.2 any hacker attack on a user’s application;

4.3 any loss or leak of data, pin or password due to improper maintenance or confidentiality measures of a user;

4.4 any negligence of, or operation authorized by, a user;

4.5 any failure by a user to abide by the documentation or suggestions for using Tencent Cloud products; for example, any unavailability resulting from the user’s operation to delete a TCR instance via the console, the API, CLI or other methods of control or the deletion or destroy of data of the COS Bucket backend storage with which a TCR instance is associated.

4.6 any event of force majeure including but not limited to natural disasters such as earthquake, flood and pandemic, social events such as war, riot and government action, technology incidents such as disconnection of telecommunication trunk circuits, hacker attack and network congestion, technological adjustment by telecommunication authorities, and government regulation and control;

4.7 any suspension or termination of service resulting from any violation by a user of the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), including but not limited to the suspension of service or release of a TCR instance due to a user’s delay in payment;

4.8 any temporary downtime of the Service due to normal maintenance or upgrade of TCR by Tencent Cloud as described in the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248);

4.9 any Service unavailability or failure of the Service to meet the standard due to any reason not attributable to Tencent Cloud;

4.10 any other circumstances in which Tencent Cloud will be exempted or released from its liabilities for compensation or otherwise according to relevant laws, regulations, agreements or rules, or any relevant rules or guidelines published by Tencent Cloud separately.

## 5. Miscellaneous



5.1 **The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total Service Fees you have paid for the relevant Service which is not performed.**

5.2 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

5.3 As an ancillary agreement to the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement is of the same legal effect as the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In respect of any matter not agreed herein, you shall comply with relevant terms under the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In case of any conflict or discrepancy between this Agreement and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)
