**In order to use the Tencent Cloud File Storage (“CFS”) service (the “Service”), you should read and observe this Cloud File Storage Service Level Agreement (this “Agreement”, or this “SLA”) and the Tencent Cloud Service Agreement. This Agreement contains, among others, the terms and definitions of the Service, level indicators of the Service availability and success rate, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, are in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking “Agree”/ “Next”, or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

### 1.	Terms and Definitions

**1.1	Tencent Cloud File Storage (CFS):** means the network attached storage service provided to you by Tencent Cloud that supports file access protocols such as NFS.  You may write or read data via a file access protocol such as NFS.  **CFS** is scalable on an automatic basis.  For details, please refer to the Service you purchase and the contents of the Service provided by Tencent Cloud.

**1.2	File System Instance: means [to be inserted]. The Service Availability shall be calculated on a single File System Instance basis.**

**1.3	Service Month(s):** means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16.

**1.4	Total Time of a Single File System Instance within a Service Month:** the total number of days of the Service Month for such signal File System Instance × 24 (hours) × 60 (minutes).

**1.5	Single File System Instance Service Downtime within a Service Month:** If (and only if) all your continuous attempts to connect a specific single File System Instance fail within one (1) minute, it shall be deemed that the Service is unavailable within such one (1) minute.  If the continuous attempts that have failed last less than one (1) minute, such time will not be counted into the Service downtime.  The accumulated Service downtime so calculated in minutes of a single File System Instance within a Service Month is the Single File System Instance Service Downtime for such Service Month. 

**1.6	CFS Monthly Service Fee:** CFS Monthly Service Fee means the total service fees under a Tencent Cloud account of a client during one calendar month for a single File System Instance (including without limitation storage capacity, bandwidth or other storage management fees), excluding the portion paid but yet to be consumed and the portion deducted by a coupon or promotional voucher, due to discounted service fee or otherwise deducted.

### 2.	Service Availability/ Service Success Rate

**2.1	Calculation of Service Availability**

The Service Availability of the Tencent Cloud File Storage service will be calculated on a single File System Instance basis as follows:

<<<<<<< HEAD
![](https://main.qcloudimg.com/raw/5a690da01c4ea4380aaf1b3116611dae.png)
=======
<div>
Service Availability = ( <span style="display:inline-block;text-align:center">
<div >Total Time of a Single File System Instance within a Service Month - Single File System Instance Service Downtime within a Service Month </div><hr><div>Total Time of a Single File System Instance within a Service Month</div></span>) * 100% 
</div>
![](https://main.qcloudimg.com/raw/fe5369c3299e4adb36388fcc156b3698.png)
>>>>>>> 9611a1993cf175e4fd580ce5c85c6c220ffb65ce


**2.2	Service Availability/ Standard Indicator**

**The Service Availability of the Service** provided by Tencent Cloud will be no less than 99.9%. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below. 

### 3.	Service Compensation

In respect of this Service, if the Service Availability fails to meet the abovementioned standard, you will be entitled to compensations in accordance with the following terms:

**3.1	Standards of Compensation**

(1) Compensations will be made **in the form of coupon** by Tencent Cloud, and you should follow the rules for using the coupon (including the valid term; for details, please refer to the rules of coupons published on Tencent Cloud’s official website). You cannot redeem such coupon for cash or request to issue an invoice for such coupon. Such coupon can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the coupon to purchase other services of Tencent Cloud, nor should you give the coupon to a third party for consideration or for free.
(2) If the Service Availability for a Service Month fails to meet the standard, the amount of compensation will be calculated for such month independently, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such month** (the Monthly Service Fee referred herein shall exclude the portion deducted by a coupon or promotional voucher, due to discounted service fee or otherwise deducted). 

|Service Availability (Av) for a Service Month	| Value of Compensation Coupon|
|-|-|
|99.9% > Av ≥ 99.0%	|10% of the Monthly Service Fee|
|99.0% > Av ≥ 98.0%	|20% of the Monthly Service Fee|
|98.0% > Av 	|50% of the Monthly Service Fee|

**3.2	Time Limit for Compensation Application**

(1) If the Service Availability for a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the fifth (5th) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail.**

(2) **You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard.** If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

### 4.	Release of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service downtime shall not be counted towards Service unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

**4.1**	any system maintenance with prior notice by Tencent Cloud to you, including system cutover, maintenance, upgrade and failure simulation test;

**4.2**	any failure or configuration adjustment of network or equipment that is not Tencent Cloud facility;

**4.3**	any attack on your application interface or data, or any other misconduct;

**4.4**	any loss or leak of data, pin or password due to your improper maintenance or improper confidentiality measures;

**4.5**	any negligence in authorization or mal-operation by you, or any of your equipment, or third-party software or device; 

**4.6**	any failure of you to abide by documentation or suggestions for using Tencent Cloud products;

**4.7**	any exceeding of the upper limit of the Service capacity corresponding to the version of the Service you purchase, resulting in delay in, or failure of, the delivery of the Service; 

**4.8**	any Service unavailability or failure of the Service to meet the availability standard not attributable to Tencent Cloud.

**4.9**	any other circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately.

### 5.	Miscellaneous
**5.1	The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.**

**5.2**	Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

**5.3**	As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)

