**To use the Tencent Cloud Weiling service (hereinafter referred to as the "Service"), you must read and comply with the Service Level Agreement for Tencent Cloud Weiling (hereinafter referred to as this "Agreement" or "SLA") and the Tencent Cloud Service Agreement. This Agreement contains the terms associated with the Service and their definitions, metrics for service availability and service success rate level, compensation, and disclaimer. Please be sure to carefully read and fully understand the provisions hereof. The limitation of liability and disclaimer clauses or other clauses which relate to your major rights and interests may be highlighted in bold or underlined for emphasis. 
Unless you have fully read and completely understand and accept all of the provisions hereof, do not purchase the Service. By clicking "Agree" or "Next", purchasing or using the Service, or accepting this Agreement otherwise expressly or implicitly, you acknowledge that you have read this Agreement and agree to be bound by it, and this Agreement will enter into force between you and Tencent Cloud (each a "Party" and collectively the "Parties") and become a legal instrument that is binding upon the Parties. **

## 1. Terms and Definitions
1.1 **Tencent Cloud Weiling**: Tencent Cloud Weiling provided by Tencent Cloud is an IoT building operating system well adapted to smart building scenarios. It provides connection, management, and digital operations services for various resources in buildings, such as hardware devices, applications, and services.
1.2 **Service cycle**: a service cycle is a natural month. The service availability is determined on a service cycle basis. The service cycle is calculated monthly, and any period of less than one natural month will not be counted as a service cycle, nor the service availability will be determined for that period. 
1.3 **Failed request**: Tencent Cloud Weiling regards requests that return an error code of "internal error" and normal user requests that fail to arrive at its server due to any failure in it as failed requests. However, failed requests shall not include the following types of request: (1) requests that are made failed by Tencent Cloud Weiling due to excess of its QPS (queries per second) caused by the use of inappropriate access modes; (2) failed requests or service unavailability caused by reasonable upgrades, changes, or shutdowns initiated by Tencent Cloud Weiling; (3) requests made failed by Tencent Cloud Weiling due to hacker attacks against your applications; and (4) requests not successfully sent to your devices by Tencent Cloud Weiling or not successfully reported to it by your devices due to ISP network failures.
1.4 **Valid requests**: all requests received by the Tencent Cloud Weiling server are regarded as valid requests, **excluding the following types of request**: (1) requests that are initiated to the service before it is activated and authorized, fail to be authenticated, or are initiated with an incorrect key; (2) requests initiated by your applications after they are attacked by hackers; (3) requests to platform server APIs that are throttled due to excessive call frequency or return an error due to network disconnections; (4) requests that are throttled due to excessive device reporting frequency (the limit is 1 QPS per device); (5) requests sent to your devices by the platform that are throttled (the limit is 1 QPS per device); and (6) requests that are discarded due to noncompliance with the data format requirements of Tencent Cloud Weiling.
**5-minute error rate: (number of failed requests per 5 minutes/total number of requests per 5 minutes) * 100% **
1.5 **Monthly service fees**: it refers to the total service fees paid for Tencent Cloud Weiling by you in a natural month. If you pay service fees for multiple months at a time, the monthly service fees will be calculated by apportioning the total service fees among the number of months purchased. 


## 2. Service Availability 
Tencent Cloud Weiling guarantees a 99% service availability. If such guarantee is not honored, you may get compensation as specified in Article 3 of this Agreement. 
**2.1 Calculation method for service availability **
The service availability of Tencent Cloud Weiling is determined on a service cycle basis. It is calculated from the average 5-minute error rate, which is calculated by dividing the sum of 5-minute error rates in a service cycle by the total number of 5-minute periods in the service cycle, i.e., service availability = (1 - sum of 5-minute error rates in a service cycle/total number of 5-minute periods in the service cycle) * 100%.
>!
>Total number of 5-minute periods in a service cycle = 12 * 24 * number of days in the service cycle.
>

**2.2 Exclusions from compensation **
Any service unavailability caused by the following shall not be entitled to compensation:
(1) Any system maintenance performed by Tencent Cloud with prior notice to you, including cutover, repair, upgrade, and failure emergency response drill;
(2) The maintenance of or failure in any external objects that the Service depends on;
(3) Any causes attributable to you or a third party or force majeure; 
(4) Any failures in your own networks, systems, software, or devices;
(5) Any loss or leakage of your data or passwords due to any breaches of security by you;
(6) Hacking of your devices or applications;
(7) Any failure to follow the user guide or usage recommendations for Tencent Cloud Weiling by you;
(8) Your negligence or any operations authorized by you;
(9) Any controls implemented by regulatory authorities such as the MIIT and communications administration bureaus or ISPs;
(10) Any failures or configuration adjustments in any networks or devices other than Tencent Cloud networks and devices;
(11) Force majeure or accidents;
(12) The unavailability of the Service or the failure of the Service to reach the specified standard caused by any other reasons not attributable to Tencent Cloud.
(13) Any circumstances in which Tencent Cloud shall not be liable under applicable laws, regulations, agreements, or rules, or applicable terms of service, rules, or instructions that are issued by Tencent Cloud separately.


## 3. Compensation 
 If the service availability of the Service is lower than 99%, you may get compensation as specified below: 
**3.1 Compensation standard **
(1) Tencent Cloud will compensate you by** issuing vouchers (non-cash)**, which may only be used by you for purchasing the Service rather than other Tencent Cloud services and may not be transferred or gifted to any third parties.
(2) If the Service fails to reach the service availability standard in a certain service month, you will be compensated as calculated for such service month, **and the aggregate liability of Tencent Cloud to you shall not exceed the service fees paid by you for the Service for such service month** (the monthly service fees herein shall not include non-cash deductions made to the service fees through vouchers or coupons). 

>!
>For the purposes of this Agreement, a service month shall refer to each natural month included in the term for which you purchase the Service. For example, if you purchase the Service for two months, and the Service is activated on March 17, then the 1st service month will refer to the period from March 17 to March 31, the 2nd from April 1 to April 30, and the 3rd from May 1 to May 16. 
>

<table>
<thead>
<tr>
<th><b>Service Availability for Service Month</b></th>
<th><b>Amount of Voucher Issued as Compensation</b></th>
</tr>
</thead>
<tbody>
<tr>
<td>Lower than 99% but equal to or higher than 95% </td>
<td>10% of the monthly service fees.</td>
</tr>
<tr>
<td>Lower than 95% but equal to or higher than 90%</td>
<td>25% of the monthly service fees</td>
</tr>
<tr>
<td>Below 90%</td>
<td>100% of the monthly service fees </td>
</tr>
</tbody></table>
**3.2 Time limit for submitting a compensation claim **
3.2.1. If the Service fails to reach the service availability standard in a certain service month, you may submit a claim for compensation **only by contacting your Tencent Cloud rep by email** after the fifth (5) business day of the month following such service month. Tencent Cloud will review your claim for compensation. In case of any dispute over the calculation of the service availability for a certain service month, **the Parties agree that the records on the backend of Tencent Cloud shall apply.**
3.2.2. **You shall submit any claim for compensation no later than sixty (60) natural days after the end of the service month in which the Service fails to reach the service availability standard.** If you fail to submit a claim for compensation within such period, or if you submit a claim for compensation after such period, or if you submit a claim for compensation not pursuant to this Agreement, you will be deemed to have waived your claim for compensation and your other claims against Tencent Cloud, and Tencent Cloud shall have the right not to accept your claim for compensation or compensate you.  


## 4. Legality Requirements 
**If you use Tencent Cloud Weiling, before you submit the information of the entity that needs to be verified by Tencent Cloud, you must warrant the following:**
4.1 Such information has been legally obtained;
4.2 You shall have included the following or similar provision in the relevant service agreement provided to the public: "The User authorizes XX (i.e. "you" in this Agreement) to offer the information provided to XX by the User and the information generated from the use of the services provided by XX (including the information provided or generated before the signing of this authorization provision) to XX and its partners which are necessary for the provision of its services (including the service providers necessary for its partners) in order to provide services, recommend products, and conduct market research and information and data analysis for users. XX undertakes to maintain and request its partners (including their necessary service providers) to maintain strict confidence of such information and take measures to protect the information security.", have submitted the authorization agreement entered into by and between you and users to Tencent Cloud for the record, and have informed the entity of the legal consequences of such authorization.
4.3 The entity's authorization can meet Tencent Cloud's needs for identification and legal and reasonable use of its information.
4.4 Otherwise, Tencent Cloud may terminate the Service, and you shall compensate Tencent Cloud for all the losses thus incurred. 

## 5. Service Auditability 
Tencent Cloud may provide relevant information, including the execution logs of key components and the operation records of OPS personnel and customers, as necessary to assist regulatory authorities with regulation, evidence collection, or investigation under the existing system of laws and regulations and after completing all the necessary formalities.
## 6. Service Measurement Accuracy 
The fees for Tencent Cloud services are clearly indicated in the business contract and on the order page. You can select the specific service types and purchase them at the indicated price.
## 7. Miscellaneous 
Tencent Cloud shall have the right to amend the provisions of this Agreement in due course or as necessary, and you can check the latest version of this Agreement on Tencent Cloud's official website.
If you do not agree to such amendments, you shall have the right to stop using the Service. By continuing to use the Service, you acknowledge that you agree to the amended Agreement.
This Agreement shall constitute a supplementary agreement to and have the same legal force and effect as the Tencent Cloud Service Agreement. Any issues not covered by this Agreement shall be governed by the Tencent Cloud Service Agreement. In case of any conflict or inconsistency between the provisions hereof and those of the Tencent Cloud Service Agreement, this Agreement shall prevail, but only to the extent of such conflict or inconsistency.



