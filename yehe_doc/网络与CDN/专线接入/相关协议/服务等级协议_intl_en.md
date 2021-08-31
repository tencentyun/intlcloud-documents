
**In order to use the Tencent Cloud Direct Connect Service (hereinafter referred to as the “Service”), you shall read and comply with this Tencent Cloud Direct Connect Service Level Agreement (this “Agreement”, or this “SLA”) and the  [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, among others, the terms and definitions of the Service, level indi-cators of the Service Availability or the Service Success Rate, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your ma-terial rights and interests, are in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely un-derstood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

## 1.	Terms and Definitions

#### 1.1 Direct Connect (DC)
Refers to a solution provided by Tencent Cloud to connect your enterprise data center with Ten-cent Cloud, through which you may establish a private connection service that is completely iso-lated from the public network. The specific content of the services shall be subject to the Service you purchase, and the contents actually provided by Tencent Cloud.

#### 1.2 Standard Architecture of the Tencent Cloud Direct Connect
Refers to the technical requirements of the standard access architecture of Direct Connect prod-ucts provided by Tencent Cloud, i.e., in order to use the Tencent Cloud Direct Connect, the user needs to use at least two dedicated physical connections through physically separated paths that connect to Tencent Cloud’s access points at different geographical locations.

#### 1.3 Single Direct Connect Instance
Refers to an instance of the Direct Connect through one single physical connection. A Single Direct Connect Instance may contain multiple Dedicated Tunnels and Direct Connect Gateways. Service Availability Rate shall be calculated separately for each Single Direct Connect Instance.

#### 1.4 Service Unavailability

#### 1.4.1 Calculation of Packet Loss Rate
The Packet Loss Rate shall be calculated by sending packets under the ICMP protocol between the connecting IP addresses on Tencent Cloud’s end and the user’s end, and assuming that 60 PING packets are sent in each 60-second period.

#### 1.4.2 Service Unavailability Minutes
The Service is deemed to be unavailable in a Unit Time (each minute is a Unit Time) if, due to reasons attributable to Tencent Cloud, all of your attempts to communicate through a Single Direct Connect Instance failed in such Unit Time, i.e., the Packet Loss Rate of the Single Direct Connect Instance is 100% according to the monitoring data of the Ten-cent Cloud). An instance of Service Unavailability will be counted towards the Service Unavail-ability Minutes only if it lasts for 1 minute or longer; any instance of Service Unavailability short-er than 1 minute will not be counted towards the Service Unavailability Minutes.

#### 1.5 Service Unavailability Time
The Service Unavailability Time within a Service Month is the total of all Service Unavailability Minutes of a Direct Connect Instance in that Service Month.

#### 1.6 Service Month
Service Month refers to each calendar month covered by service period of the Service you pur-chase. For example, if you purchase the Service for a period of three months with the Service commencement date on March 17, the Service period shall include four Service Months, i.e., the first Service Month is from March 17 to March 31, the second Service Month is from April 1 to April 30, the third Service Month is from May 1 to May 31, and the fourth Service Month is from June 1 to June 16.

#### 1.7 Monthly Service Fee
The total Service Fee for a Single Direct Connect Instance in one Service Month shall exclude the portion of Service that you have purchased but not yet use. The Monthly Service Fee shall exclude the amount that is deductible under any vouchers and coupons and the amount oth-erwise reduced or exempted.

## 2. Service Availability/ Service Success Rate

#### 2.1 Calculation of Service Availability/Service Success Rate
The Service Availability of the Direct Connection Service is calculated separately for each Single Direct Connect Instance with the following formula:

Service Availability = {(Total number of minutes in a Service Month – Service Unavailability Minutes in the Service Month)/Total number of minutes of the Service Month} × 100%.
For example: There are 30 days in the Service Month of April 2019, therefore, the total number of minutes in that Service Month is 30 days × 24 hours × 60 minutes = 43200 minutes; assuming the total Service Unavailability Minutes in that month is 15 minutes,  the Service Availability Rate = (((43200 - 15) / 43200) × 100% ≈ 99.97%.

#### 2.2 Service Availability/Service Indicators Standard
The Service Availability Rate of this Service provided by Tencent Cloud should not be less than 99.95%. If the Service fails to meet the Standard (except under circumstances for release of lia-bilities), you may claim compensation in accordance with Article 3 of this Agreement.

## 3. Compensation Plan
In respect of the Service, if the Service Availability is lower than the above Standard, you will be entitled to compensations in accordance with the following terms:

#### 3.1 Standards of Compensation
(1) Compensations will be made in the form of voucher by Tencent Cloud. And you should use the voucher by abiding the voucher usage rules published by Tencent Cloud (including usage pe-riod, etc., subject to the voucher rules published on Tencent Cloud official website). Such vouch-er cannot be converted into cash and no invoice will be issued with respect thereof and the voucher may only be used to purchase the Service by using your Tencent Cloud account. You cannot use the voucher to purchase other Services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability in a Service Month fails to meet the abovementioned standard, the amount of compensation shall be calculated for such Service Month independently, and **the ag-gregate amount shall be no more than the applicable Monthly Service Fee paid by you for such Service Month** (the Monthly Service Fee referred to herein shall exclude the portion de-ducted by a voucher or promotional coupon, and the portion otherwise deducted or exempted).

<table>
<thead>
<tr>
<th style="width:60%"><b>Service Availability in a Service Month</b></th>
<th style="width:40%"><b>Value of Compensational Voucher</b></th>
</tr>
</thead>
<tbody><tr>
<td>Less than 99.95% but is or higher than 99%</td>
<td>10% of the Monthly Service Fee</td>
</tr>
<tr>
<td>Less than 99% but is or higher than 95%</td>
<td>25% of the Monthly Service Fee</td>
</tr>
<tr> 	
<td>Less than 95%</td>
<td>100% of the Monthly Service Fee</td>
</tr>
</tbody></table>	

#### 3.2 Time Limit for Compensation Application
(1) If the Service Availability in a Service Month fails to meet the Service Availability standard, you may **apply for compensation only through the support ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud shall prevail.**

(2) **You shall apply for compensation no later than the sixtieth (60th) calendar day following the end of the applicable Service Month in which the Service Availability fails to meet the abovementioned standard.** If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

## 4. Release of Liability

**If the Service Unavailability is due to the following reasons, the time when the Service is un-available shall not be calculated into Service Unavailability Minutes and Tencent Cloud shall not undertake any liabilities with respect thereof, including compensation liabilities:**

- any system maintenance of Tencent Cloud for which a prior notice has been given to client, including any system cutting over, maintenance, upgrade and simulated failure drill;
- any failure or configuration adjustment of network or equipment that are not owned by Tencent Cloud;
- any circumstance where the client’s application or data information suffers a hacker attack;
- any improper configuration of the client’s network device or route;
- any loss or disclosure of data, password and security code because the client fails to proper-ly keep or fails to take proper confidentiality measures with respect to the same;
- any upgrade of the operating system independently carried out by the client;
- any activities of the client’s application or installation operation;
- any negligence of the client or act authorized by client;
- any force majeure or accidents.
- any circumstance where the client fails to configure the system according to the Standard Architecture for Tencent Cloud Direct Connect provided by Tencent Cloud.
- any circumstance where the Service is unavailable or falls short of the Standards due to rea-sons that are not attributable to Tencent Cloud; or
- other circumstances where Tencent Cloud may be exempted from liabilities as set forth in the relevant laws and regulations, the relevant agreements, or the relevant rules and instruc-tions separately issued by Tencent Cloud.

## 5. Miscellaneous

5.1 **The Parties hereby acknowledge that if you suffer any losses in the process of use of the Service due to the breach of contract by Tencent Cloud, Tencent Cloud's total liabilities for compensation with respect to your loss shall not exceed the aggregate amount of the Service Fee you have paid for the corresponding Service.**

5.2 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agree-ment terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

5.3 As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy.
