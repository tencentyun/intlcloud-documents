**In order to use the Tencent Cloud Web Application Firewall ("WAF") service (the "Service"), you should read and observe this Web Application Firewall Service Level Agreement (this "Agreement", or this "SLA") and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, *among others*, the terms and definitions of the Service, Service availability and Service uptime metrics, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, may be in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking "Agree"/ "Next", or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

## 1. Terms and Definitions

 1.1  **Web Application Firewall (WAF)**: means the web security and prevention service provided by Tencent Cloud to you ("client") by means of Web Application Firewall, including without limitation visualized analysis of service security of websites and applications and website security services such as OWASP TOP 10 protection and business BOT protection. For details, please refer to the Service you purchase and the contents of the Service provided by Tencent Cloud.
    
 1.2  **Service Month(s)**: means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The availability of the Service will be calculated independently for each Service Month.
    
 1.3 **Service Unavailability**: mainly include:
     (1) failure of any Service request to reach a Service server due to any reason attributable to WAF per se.
     (2) return of "4xx" or "5xx" status codes by a Service server due to any reason attributable to WAF per se.

 1.4  **Service Downtime within a Service Month Calculated in Minutes**: Service Downtime Calculated in Minutes = the time when the Service Unavailability is fixed -- the time when the Service Unavailability starts. Such downtime will be calculated in minutes, and when the downtime, or a portion thereof, is less than sixty (60) seconds, it will be rounded up to one (1) minute. For example, if the actual downtime is one (1) minute and one (1) second, the Service Downtime Calculated in Minutes would be two (2) minutes. However, when the Service Unavailability is fixed within one (1) minute, which means that the actual downtime of the Service is less than one (1) minute, such downtime will not be counted in the Service downtime defined herein.
    
 1.5 **Total Time within a Service Month Calculated in Minutes**: equals to the total number of days of the Service Month × 24 (hours) × 60 (minutes).

## 2. Service Availability / Service Uptime Metrics
### 2.1 Calculation of Service Availability

**Service Availability = (1 -- Service Downtime within a Service Month Calculated in Minutes / Total Time within a Service Month Calculated in Minutes) × 100%**

### 2.2  Service Availability Standard

**The Service Availability of the Service provided by Tencent Cloud will be** **no less than 99.95%**. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below.

*Assuming that a Service Month has thirty (30) days, the total available time in such month would be 30 (days) × 24 (hours) × 60 (minutes) × 99.95% = 43178.4 minutes; that is, the Service downtime of the instance in such month will be 43200 -- 43178.4 = 21.6 minutes.*

## 3. Service Compensation

In respect of this Service, if the Service Availability fails to meet the abovementioned standard, you will be entitled to compensations in accordance with the following terms:

### 3.1 Standards of Compensation

(1) Compensations will be made **in the form of voucher** by Tencent Cloud, and you should follow the rules for using the voucher (including the valid term; for details, please refer to the rules of vouchers published on Tencent Cloud's official website). You cannot redeem such voucher for cash or request to issue an invoice for such voucher. Such voucher can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability for a Service Month fails to meet the standard, the amount of compensation will be calculated for such month independently, and **the aggregate amount shall be no more than the applicable monthly service fee paid by you for such month** (the monthly service fee referred to herein shall exclude the portion deducted by a voucher or promotional credits, due to discounted service fee or otherwise deducted).

|**Service Availability (Av) for a Service Month** |  **Value of Compensation Voucher**|
|--------------------------------------------------- |-----------------------------------|
|99.95% > Av ≥ 99%	|10% of the monthly service fee|
|99% > Av ≥ 95%|	25% of the monthly service fee|
|95% > Av	|100% of the monthly service fee|


### 3.2 Time Limit for Compensation Application

(1) If the Service Availability for a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the fifth (5^th^) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail**.

(2) **You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard**. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

## 4. Release of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service downtime shall not be counted towards Service Unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

4.1	any Service Unavailability due to any act of you or your end users, which poses a security threat to the Service provided by Tencent Cloud, or is fraudulent or illegal.
4.2	any Service Unavailability due to any device, software or technology of you or any third party (not directly controlled by Tencent Cloud).
4.3	any Service Unavailability due to your failure to use the products in accordance with the configuration required by Tencent Cloud.
4.4	any Service Unavailability due to your non-payment or delay in payment.
4.5	any Service Unavailability due to a severe malfunction of a network operator.
4.6	any Service Unavailability due to various source server problems on your business end, such as fully-occupied bandwidth, IP exposure, machine room malfunction, and chain network jitter of the source server.
4.7	any Service Unavailability due to traffic attacks that exceed the specification of the WAF you purchased.
4.8	any temporary downtime of the Service due to normal maintenance or upgrade of WAF by Tencent Cloud as described in the Tencent Cloud Service Agreement.
4.9	any Service Unavailability due to any event of force majeure.
4.10 any Service Unavailability or failure of the Service to meet the availability standard due to any reason not attributable to Tencent Cloud.
4.11 any other circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately.

## 5. Miscellaneous

5.1	**The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.**
5.2	Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.
5.3	As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)

