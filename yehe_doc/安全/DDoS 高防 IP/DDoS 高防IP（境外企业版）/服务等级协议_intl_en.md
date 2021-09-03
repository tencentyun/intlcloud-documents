**To use Tencent Cloud Anti-DDoS service (hereinafter referred to as the "Service"), you must read and comply with the Service Level Agreement for Anti-DDoS (hereinafter referred to as this "Agreement" or the "SLA") and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/12905). This Agreement contains the terms associated with the Service and their definitions, metrics for service availability and service success rate level, compensation, and disclaimer. Please be sure to carefully read and fully understand the provisions hereof. The limitation of liability and disclaimer clauses or other clauses which relate to your major rights and interests may be highlighted in bold or underlined for emphasis.**

**Unless you have fully read and completely understand and accept all of the provisions hereof, do not purchase the Service. By clicking "Agree" or "Next", purchasing or using the Service, or accepting this Agreement otherwise expressly or impliedly, you acknowledge that you have read this Agreement and agree to be bound by it, and this Agreement will enter into force between you and Tencent Cloud (each a "Party" and collectively the "Parties") and become a legal instrument that is binding upon the Parties.**

## 1. Terms and Definitions
#### 1.1 Tencent Cloud Anti-DDoS service
This shall refer to the DDoS protection service provided by Tencent Cloud for the Anti-DDoS Pro and Anti-DDoS Advanced instances purchased by you, subject to the services purchased by you and the services provided by Tencent Cloud.

#### 1.2 Service Unavailability
This shall refer to incidents where the packet loss rate caused by the DDoS protection service system itself is higher than 20% or the TCP connection success rate is lower than 30%. This is not applicable to the availability of the entire linkage (for example, the bandwidth of your real server is used up, or the data center of your real server fails).

#### 1.3 Duration of Service Unavailability
This shall refer to the total number of minutes in a service month for which Anti-DDoS is not available. Anti-DDoS treats each minute as a sampling point; therefore, the total number of minutes of service unavailability in a service month is equal to the total number of sampling points where the Anti-DDoS service is unavailable in the said month.

#### 1.4 Service Month
A service month shall refer to each natural month included in the term for which you purchase the Service. If you purchase the Service for three months, and the Service is activated on March 17, there will be a total of four (4) service months, where the 1st service month will refer to the period from March 17 to March 31, the 2nd from April 1 to April 30, the 3rd from May 1 to May 31, and the 4th from June 1 to June 16. Service availability shall be calculated on a per service month basis.

## 2. Service Availability/Service Success Rate
#### 2.1 Calculation Method for Service Availability/Service Success Rate
Service availability = ((Total number of minutes in a service month - number of minutes of service unavailability in a service month)/total number of minutes in a service month) * 100%

#### 2.2 Service Availability/Service Metric Standard
The availability of the Service provided by Tencent Cloud shall not be lower than 99.9%, and you may be entitled to compensation in accordance with Article 3 of this Agreement for any failure to reach such availability standard (except as otherwise specified in the Disclaimer clause).

## 3. Compensation
If the service availability of the Service is lower than the standard, you shall have the right to be compensated as specified below:
#### 3.1 Compensation Standard
1. Tencent Cloud will compensate you by **issuing vouchers**, and you shall comply with the rules governing the use of vouchers (such as validity period, as specified in the rules applicable to vouchers published on Tencent Cloud's official website). Vouchers cannot be redeemed or invoiced for and may only be used by you for purchasing the Service rather than other Tencent Cloud services through your Tencent Cloud account. You shall not transfer or gift vouchers to any third parties.
2. If the Service fails to reach the service availability standard in a certain service month, **you will be compensated as calculated for such service month, and the aggregate liability of Tencent Cloud to you shall not exceed the service fees paid by you for the Service for such service month** (the monthly service fees herein shall not include deductions made to the service fees through vouchers, coupons, or discounts).

| Service Availability for Service Month | Amount of Voucher Issued as Compensation | 
|---------|---------|
| Lower than 99.9% but equal to or higher than 99% | 10% of the monthly service fees | 
| Lower than 99% but equal to or higher than 95% | 25% of the monthly service fees | 
| Lower than 95% | 100% of the monthly service fees |	

#### 3.2 Time limit for submitting a compensation claim
(1) If the Service fails to reach the service availability standard in a certain service month, you **may submit a claim for compensation only through the ticket system under your account** after the fifth (5) business day of the month following such service month. Tencent Cloud will review your claim for compensation. In case of any dispute over the calculation of the service availability for a certain service month, **the Parties agree that the records on the backend of Tencent Cloud shall apply**.
(2) **You shall submit any claim for compensation no later than sixty (60) natural days after the end of the service month in which the Service fails to reach the service availability standard.** If you fail to submit a claim for compensation within such period, or if you submit a claim for compensation after such period, or if you submit a claim for compensation not pursuant to this Agreement, you will be deemed to have waived your claim for compensation and your other claims against Tencent Cloud, and Tencent Cloud shall have the right not to accept your claim for compensation or compensate you.

#### 3.3 Supporting Documents for Compensation Claims
If you believe the Service fails to reach the service availability standard, you may submit a claim for compensation within the time limit specified in this Service Level Agreement, provided that such claim for compensation is submitted with at least the following information:
(1) A detailed written description of the incident.
(2) The specific date, time, duration, and other particulars of service unavailability, cleansing time, or the proportion of normal traffic.
(3) If your claim for compensation is based on an unusual normal traffic proportion, you shall provide a packet capture file that covers at least one hour and can obviously evidence the presence and amount of exceptional traffic.
(4) Other information reasonably requested by Tencent Cloud.

## 4. Disclaimer
**TENCENT CLOUD SHALL NOT BE LIABLE TO YOU FOR ANY SERVICE UNAVAILABILITY RESULTING FROM ANY OF THE FOLLOWING, AND THE DURATION OF SERVICE UNAVAILABILITY SHALL NOT BE INCLUDED IN THE CALCULATION OF SERVICE UNAVAILABILITY OR THE COMPENSATION BY TENCENT CLOUD:**
4.1 The unavailability of the Service or the failure of the Service to reach the specified standard caused as a result of you or your end user posing a threat to the security of, or engaging in any fraud or illegal activity in connection with, the Service provided by Tencent Cloud;
4.2 The unavailability of the Service or the failure of the Service to reach the specified standard caused by you or any third-party (not directly controlled by Tencent Cloud) device, software, or technology;
4.3 The unavailability of the Service or the failure of the Service to reach the specified standard caused as a result of any failure by you to use the Service as configured by Tencent Cloud;
4.4 The unavailability of the Service or the failure of the Service to reach the specified standard caused as a result of your violation of any of the Tencent Cloud terms of service;
4.5 The unavailability of the Service or the failure of the Service to reach the specified standard caused due to any non-payment or any delay in payment by you;
4.6 The unavailability of the Service or the failure of the Service to reach the specified standard caused due to a serious failure involving the ISP;
4.7 The unavailability of the Service or the failure of the Service to reach the specified standard caused by your non-compliant or illegal use of the Tencent Cloud Service;
4.8 The unavailability of the Service or the failure of the Service to reach the specified standard caused by any real server issues arising on the backend of the Anti-DDoS Service (such as any exhaustion of the bandwidth of the real server, any exposure of the real server's IP, any failure in the real server's data center, or any network jitter on the linkage of the real server);
4.9 The unavailability of the Service or the failure of the Service to reach the specified standard caused by the maintenance or upgrading of the network, hardware, or Service (Tencent Cloud will give you commercially reasonable notice of any scheduled maintenance);
4.10 The unavailability of the Service or the failure of the Service to reach the specified standard caused by force majeure events;
4.11 The unavailability of the Service or the failure of the Service to reach the specified standard caused by your IP being blackholed by attacks not covered by the specification of the Anti-DDoS Service you purchased;
4.12 The unavailability of the Service or the failure of the Service to reach the specified standard caused by any other reasons not attributable to Tencent Cloud;
4.13 Any circumstances in which Tencent Cloud shall not be liable under applicable laws, regulations, agreements, or rules, or applicable rules or instructions that are issued by Tencent Cloud separately.

## 5. Miscellaneous
5.1 **THE PARTIES HEREBY CONFIRM AND ACKNOWLEDGE THAT UNDER NO CIRCUMSTANCES SHALL THE AGGREGATE LIABILITY OF TENCENT CLOUD FOR ANY LOSSES INCURRED BY YOU AS A RESULT OF ANY BREACH OF THIS AGREEMENT BY TENCENT CLOUD DURING YOUR USE OF THE SERVICE EXCEED THE TOTAL AMOUNT OF SERVICE FEES PAID BY YOU FOR THE SERVICE.**
5.2 Tencent Cloud shall have the right to amend the provisions of this Agreement in due course or as necessary, and you can check the latest version of this Agreement on Tencent Cloud's official website. If you do not agree to such amendments, you shall have the right to stop using the Service. By continuing to use the Service, you acknowledge that you agree to the amended Agreement.
5.3 This Agreement shall constitute a supplementary agreement to and have the same legal force and effect as the Tencent Cloud Service Agreement. Any issues not covered by this Agreement shall be governed by the Tencent Cloud Service Agreement. In case of any conflict or inconsistency between the provisions hereof and those of the Tencent Cloud Service Agreement, this Agreement shall prevail, but only to the extent of such conflict or inconsistency.
