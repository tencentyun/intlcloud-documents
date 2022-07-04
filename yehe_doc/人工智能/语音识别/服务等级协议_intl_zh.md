**In order to use the Tencent Cloud Speech Recognition Public Cloud Service (the “Service”), you shall read and comply with this Tencent Cloud Speech Recognition Public Cloud Service Level Agreement (this “Agreement”, or this “SLA”) and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, among others, the terms and definitions of the Service, Service Availability or success rate, compensation plan and disclaimer of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or disclaiming certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties. For the purposes of these Terms of Service, “Tencent Cloud” refers to the applicable Tencent entity as set forth in the Tencent Cloud Service Agreement.**

## 1. Terms and Definitions

### 1.1 Speech Recognition Public Cloud Service
Refers to the public cloud speech recognition interface call service provided by Tencent Cloud, including audio file recognition, one-sentence recognition and real-time speech recognition, etc., subject to the specific services you use. You can use the Service to achieve the conversion from speech to text.

### 1.2 Service Month(s)
Service Month(s) refers to the full calendar month(s) within the term of the Service you use. For example, if you start the Service on March 17, there will be four (4) Service Months as of June 16 (the first Service Month from March 1 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 30). The Service Availability will be calculated separately for each Service Month.

### 1.3 Unavailable Minutes within a Service Month
A minute will be counted towards the Unavailable Minutes within a Service Month only if all your continuous requests to the Service through the API or SDK return with internal errors within that minute. If none of or only a part of your requests to the Service through the API or SDK within a minute return with internal errors, the Service will be deemed to be fully available in that minute and that minute shall not be counted towards the Unavailable Minutes within a Service Month. If you make no requests to the Service in a minute, that minute shall not be counted towards he Unavailable Minutes. The sum of the unavailable minutes of the Service within a Service Month shall be the Unavailable Minutes within a Service Month.

### 1.4 Internal Error
The Internal Error means the abnormal return of API or SDK due to the malfunction of the Tencent Cloud Speech Recognition Service. The Internal Error can be determined by the error return code of the Service and be identified by the Internal Error return code, negative error return code or 500 return code in the error return code of the Service. Any request return error of API or SDK caused by the users’ problems such as a network failure, user request parameter error (for example, an illegal request parameter or an invalid URL) or a format error of an audio input shall not be deemed as an Internal Error.

### 1.5 Total Number of Minutes within a Service Month
Total Number of Minutes within a Service Month = the total number of days of the Service Month × 24 (hours) × 60 (minutes).

## 2. Service Availability

### 2.1 Calculation of the Service Success Rate
Service Availability = (1 – Unavailable Minutes within a Service Month / Total Number of Minutes within a Service Month) × 100%

### 2.2 Service Indicator Standard
The Service Availability of the Service provided by Tencent Cloud should not be less than **99.9%**. If the Service fails to meet the Standard (except under circumstances for disclaimer of liabilities), you may claim compensation in accordance with Article 3 of this Agreement.

## 3. Compensation Plan

In respect of the Service, if the Service Availability fails to meet the Standard, you will be entitled to compensations in accordance with the following terms:

### 3.1 Standards of Compensation

(1) Compensations will be made **in the form of voucher (not cash)** by Tencent Cloud, and you should use the voucher by abiding the voucher usage rules (including usage period, etc., subject to the voucher usage rules published on Tencent Cloud official website). Such voucher cannot be converted into cash, and no invoice will be issued with respect thereof. The voucher may only be used to purchase the Service by using your Tencent Cloud account, and you cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability in a Service Month fails to meet the service availability standard, the amount of compensation shall be calculated for such Service Month separately, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such Service Month** (the Monthly Service Fee referred to herein shall exclude the portion deducted by vouchers, coupons, service fee reduction or exemption, etc.).

|Service Availability in a Service Month|	Value of Compensational Voucher|
|---------|---------|
|Less than 99.9% but is or higher than 99%|	10% of the Monthly Service Fee|
|Less than 99% but is or higher than 95%|	20% of the Monthly Service Fee|
|Less than 95%|	50% of the Monthly Service Fee|

### 3.2 Time Limit for Compensation Application

(1) If the Service Availability in a Service Month fails to meet the Service Availability standard, you may **apply for compensation only through the support ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud shall prevail.**

(2) **You shall apply for compensation no later than the sixtieth (60th) calendar day following the end of the applicable Service Month in which the Service Availability fails to meet the abovementioned standard**. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

### 3.3 Application Materials for Compensation

If you believe that the Service fails to meet the Service Availability Standard, you may apply for compensation within the period of time as stipulated under this SLA, and you should at least provide the following information together with your compensation application:

(1) the AppID and UIN used by the Service;

(2) the specific time period of the service unavailability, down to the minute.

## 4. Disclaimer of Liabilities
**If the Service is unavailable due to any of the following reasons, the corresponding Service Downtime shall not be counted towards Service Unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

**4.1** any system maintenance with prior notice by Tencent Cloud, including system cutover, maintenance, upgrade and malfunction simulation test;

**4.2** any failure or configuration adjustment of any network or equipment that is not a Tencent Cloud facility;

**4.3** any attack on your application interface or data, or any other misconduct;

**4.4** any loss or leak of data, passcode or password due to your improper maintenance or improper confidentiality measures;

**4.5** any negligence in authorization or incorrect operation by you, or any of your own equipment, or third-party software or device;

**4.6** any failure of you to abide by documentation or suggestions for using Tencent Cloud products;

**4.7** any use exceeding the Service capacity limit indicated for the current version of the Service;

**4.8** any unavailability of the Service or failure to meet the Service Availability standard due to any reason not attributable to Tencent Cloud; 

**4.9** any other circumstances in which Tencent Cloud will be exempted or released from its liabilities for compensation or otherwise according to relevant laws, regulations, agreements or rules, or any relevant rules or guidelines published by Tencent Cloud separately;

**4.10** you understand and agree that the Service provided by Tencent Cloud is provided based on the current technology and conditions. Due to the limitation of current technology and conditions, or changes of relevant information, data, etc. provided by you or other circumstances that are not Tencent Cloud's fault, or beyond Tencent Cloud's control or reasonable foreseeability, Tencent Cloud cannot guarantee that the Services it provides are flawless and that the identification results are completely accurate. In this case, it will not be regarded as a breach of contract by Tencent Cloud, and Tencent Cloud can be exempted from liability, while both parties should work together in good faith to solve the problem;

**4.11** you shall ensure the legitimacy of the voice source you submit for speech recognition. If your voice audio comes from a third party, you shall ensure that you have obtained the appropriate permission of the third party to use the voice audio, otherwise, you shall be solely responsible for the liabilities arising therefrom.

## 5. Miscellaneous

**5.1 The parties hereto acknowledge and agree that, for any losses incurred by you for the use of the Service due to any breach by Tencent Cloud, the total aggregate liability of Tencent Cloud for damages shall not exceed the total fees you have paid to Tencent Cloud for the Service in the 12 months immediately preceding the date that event giving rise to the liability first occurred.**

**5.2** Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted this Agreement as amended.

**5.3** As an ancillary agreement to the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement is of the same legal effect as the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In respect of any matter not agreed herein, you shall comply with relevant terms under the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). In case of any conflict or discrepancy between this Agreement and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248), this Agreement prevails to the extent of such conflict or discrepancy.
