**In order to use the Tencent Cloud Text to Speech Public Cloud Service (the “Service”), you shall read and comply with this Text to Speech Public Cloud Service Level Agreement (this “Agreement”) and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, among others, the terms and definitions of the Service, Service Availability, compensation plan and disclaimer of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or disclaiming certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties. For the purposes of these Terms of Service, “Tencent Cloud” refers to the applicable Tencent entity as set forth in the Tencent Cloud Service Agreement.**

## 1. Terms and Definitions

### 1.1 Text to Speech Public Cloud Service
Refers to the public cloud text to speech interface call service provided by Tencent Cloud. You can use the Service to achieve the conversion from text to speech. The specific content of the Service is subject to the service you use.

### 1.2 Service Month(s)
Service Month(s) refers to the calendar month(s) within the term of the Service you use. For example, if you start the Service on March 17, there will be four (4) Service Months as of June 16 (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 30). The Service Availability will be calculated separately for each Service Month.

### 1.3 Unavailable Minutes within a Service Month
A minute will be counted towards the Unavailable Minutes within a Service Month only if all your continuous requests to the Service through the API or SDK return with internal errors within that minute. If none of or only a part of your requests to the Service through the API or SDK within a minute return with internal errors, the Service will be deemed to be fully available in that minute and that minute shall not be counted towards the Unavailable Minutes within a Service Month. If you make no requests to the Service in a minute, that minute shall not be counted towards the Unavailable Minutes. The sum of the unavailable minutes of the Service within a Service Month shall be the Unavailable Minutes within a Service Month.

### 1.4 Internal Error
The Internal Error means the abnormal return of API or SDK due to the malfunction of the Service. The Internal Error can be determined by the error return code of the Service and be identified by the Internal Error return code or 500 return code in the error return code of the Service. Any request return error of API or SDK caused by the problems not attributable to Tencent Cloud, such as a network failure, user request parameter error (for example, an illegal request parameter or an invalid URL) or a format error of an audio input shall not be deemed as an Internal Error.

### 1.5 Total Number of Minutes within a Service Month
Total Number of Minutes within a Service Month = the total number of days of the Service Month × 24 (hours) × 60 (minutes).

## 2. Service Availability

### 2.1 Calculation of Service Availability
**Service Availability = (1 – Unavailable Minutes within a Service Month / Total Number of Minutes within a Service Month) × 100%**

### 2.2 Service Availability Standard
The Service Availability of the Service should not be less than 99.9%. If the Service fails to meet the Standard (except under circumstances for disclaimer of liabilities), you may claim compensation in accordance with Article 3 (Compensation Plan) of this Agreement.

## 3. Compensation Plan

In respect of the Service, if the Service Availability fails to meet the Standard, you will be entitled to compensations in accordance with the following terms:

|Service Availability in a Service Month|	Value of Compensational Voucher|
|---------|---------|
|Less than 99.9% but is or higher than 99%|	10% of the Monthly Service Fee|
|Less than 99% but is or higher than 95%|	20% of the Monthly Service Fee|
|Less than 95%|	50% of the Monthly Service Fee|

### 3.1 Standards of Compensation

(1) **Compensations will be made in the form of voucher (not cash) by Tencent Cloud, and you should use the voucher by abiding the voucher usage rules** (including usage period, etc., subject to the voucher usage rules published on Tencent Cloud official website). **Such voucher cannot be converted into cash, and no invoice will be issued with respect thereof. The voucher may only be used to purchase the Service by using your Tencent Cloud account, and you cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.**

(2) If the Service Availability in a Service Month fails to meet the service availability standard, the amount of compensation shall be calculated for such Service Month separately, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such Service Month** (the Monthly Service Fee referred to herein shall exclude the portion deducted by vouchers, coupons, service fee reduction or exemption, etc.).

### 3.2 Time Limit for Compensation Application

(1) **If the Service Availability in a Service Month fails to meet the Service Availability standard, you may apply for compensation only through the support ticket system under your relevant account after the fifth (5th) business day of the month immediately following such Service Month**. Tencent Cloud will verify and ascertain your application upon receipt of such application. **If there is any dispute over the calculation of the Service Availability for a Service Month, both parties agree that the back-end record of Tencent Cloud shall prevail.**

(2) **You shall apply for compensation no later than the sixtieth (60th) calendar day following the end of the applicable Service Month in which the Service Availability fails to meet the abovementioned standard.** If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

### 3.3 Application Materials for Compensation

If you believe that the Service fails to meet the Service Availability Standard, you may apply for compensation within the period of time as stipulated under this Agreement, and you should at least provide the following information together with your compensation application:

(1) the AppID and UIN used by the Service;

(2) the specific time period of the service unavailability, down to the minute.

## 4. Disclaimer of Liabilities

**4.1 If the Service is unavailable due to any of the following reasons, the corresponding Service Downtime shall not be counted towards Service Unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

(1) any system maintenance with prior notice by Tencent Cloud, including system cutover, maintenance, upgrade and malfunction simulation test;

(2) any failure or configuration adjustment of any network or equipment that is not a Tencent Cloud facility;

(3) any attack on your application interface or data, or any other misconduct;

(4) any loss or leak of data, passcode or password due to your improper maintenance or improper confidentiality measures;

(5) any negligence in authorization or incorrect operation by you, or any of your own equipment, or third-party software or device;

(6) any failure of you to abide by documentation or suggestions for using Tencent Cloud products;

(7) any use exceeding the Service capacity limit indicated for the current version of the Service;

(8) any unavailability of the Service or failure to meet the Service Availability standard due to any reason not attributable to Tencent Cloud; 

(9) any other circumstances in which Tencent Cloud will be exempted or released from its liabilities for compensation or otherwise according to relevant laws, regulations, agreements or rules, or any relevant rules or guidelines published by Tencent Cloud separately.

## 5. Warranties and Covenants

**5.1 You undertake that you are the end-user of the Services. If you are an agent procuring the Service for a third party, you shall confirm that you have had the full authority of the end-user to accept and agree to all the terms of this Agreement.**

**5.2 You undertake that the specific business data identified by the Service (including, without limitation, the voice data submitted by you using the voice replication and the voice customization service, and the contents submitted by you using the text to speech service) have been obtained by you through legal means and fully authorized by the information owner to use such business data, and undertake that you will not infringe upon the intellectual property rights and other legitimate rights and interests of any third party. Tencent Cloud reminds you to prudently review the legitimacy of the data source and content. You undertake not to use the Service to engage in any acts in violation of laws and regulations or public order and good morals, or to provide assistance for the above acts.**

**5.3 You undertake that any outputs or results (including, without limitation, AI synthesized audio files) obtained as a result of your use of the Service shall be used for your personal use only and shall be marked as AI-generated works in the course of your use, and shall not be disclosed, provided, forwarded or transmitted to any third party by yourself or through others in any manner or medium.**

**5.4 If you violate your undertakings, you shall be solely liable for all consequences and liabilities caused thereby and Tencent Cloud shall have the right to take immediate measures, including but not limited to deleting your relevant information and data, suspending or terminating the provision of the Service, restricting or prohibiting your use of some or all functions, freezing or deactivating the account until deregistration, or unilaterally terminating or rescinding this Agreement without any liabilities. If Tencent Cloud suffers any loss or is subject to any penalty as a result thereof, you shall fully indemnify all losses.**

## 6. Miscellaneous
**6.1 The parties hereto acknowledge and agree that, for any losses incurred by you for the use the Service due to any breach by Tencent Cloud, the total aggregate liability of Tencent Cloud shall under no circumstance exceed the total Service Fees you have paid for the relevant Service which is not performed. If you have used the Service for more than 12 months, the total aggregate liability of Tencent Cloud for damages shall not exceed the total fees you have paid to Tencent Cloud for the Service in the 12 months immediately preceding the date that event giving rise to the liability first occurred. ** 

**6.2 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted this Agreement as amended.**

**6.3** As an ancillary agreement to the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement is of the same legal effect as the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In respect of any matter not agreed herein, you shall comply with relevant terms under the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In case of any conflict or discrepancy between this Agreement and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement prevails to the extent of such conflict or discrepancy.