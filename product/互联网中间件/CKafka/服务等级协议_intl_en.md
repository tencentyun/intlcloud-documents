**The Cloud KAFKA Service Level Agreement (New Version) will be available on the official website of Tencent Cloud for the public to comment for thirty (30) days, and will take effect as of August 23, 2019 (Please note that the Cloud Kafka Service Level Agreement (Old Version) is also available on the official website of Tencent Cloud until August 23, 2019). Any service availability issue in relation to the CKafka service on or before August 23, 2019 is governed by the Cloud KAFKA Service Level Agreement (Old Version), while the service availability issue as from August 24, 2019 shall be subject to the Cloud KAFKA Service Level Agreement (New Version).**

**In order to use the Tencent Cloud Kafka ("CKafka") service (the "Service"), you should read and observe this Cloud Kafka Service Level Agreement (this "Agreement") and the [Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, *among others*, the terms and definitions of the Service, Service availability and Service uptime metrics, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, may be in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase or use the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking "Agree"/ "Next", or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

## 1.  Terms and Definitions

1.1  **Cloud** **Kafka (CKafka)**: means a distributed, high-throughput, highly scalable messaging system that is compatible with open-source Apache Kafka API (version 0.9 and version 0.10). Based on the publish/subscribe model, CKafka enables async interaction between the message producer and consumer by decoupling the messages and thereby eliminating wait time. CKafka supports data compression and offline and real-time data processing, making it ideal for collection of compressed logs and aggregation of monitoring data.

1.2  **Single Instance**: means one (1) CKafka instance. The Service Availability will be calculated on a Single Instance basis.

1.3 **Total Time of a Single Instance within a Service Month**: equals to the total number of days of the Service Month × 24 (hours) × 60 (minutes).

1.4 **Instance Unavailability**: When a CKafka instance with incoming and outgoing permission rules properly configured fails to communicate with an IP address, neither incoming nor outgoing, and such failure lasts for more than five (5) minutes, it will be deemed that the CKafka instance is unavailable within such five (5) minutes.

1.5 **Single Instance Service Downtime Calculated in Minutes**: Single Instance Service Downtime Calculated in Minutes = the time when the Instance Unavailability is fixed -- the time when the Instance Unavailability starts. Service downtime means the time period starting from the malfunction to the recovery to normal use, including the time period for maintenance. It will not be counted in the Service downtime unless and until the malfunction of the Service lasts for at least five (5) minutes; when the Instance Unavailability is fixed within five (5) minutes, which means that the actual downtime of the Service is less than five (5) minutes, such downtime will not be counted in the Service downtime defined herein.

1.6 **Service Month(s)**: means the calendar month(s) within the term of the Service purchased by you. For example, if you purchase the Service for a term of three months starting from March 17, there will be four (4) Service Months (the first Service Month from March 17 to March 31, the second from April 1 to April 30, the third from May 1 to May 31, and the fourth from June 1 to June 16). The availability of the Service will be calculated independently for each Service Month.

1.7 **Monthly Service Fee**: means the aggregate service fees paid by you in cash for a Single CKafka Instance within one (1) Service Month, excluding the portion paid yet to be consumed, and the portion deducted by a voucher or promotional credits, due to discounted service fee or otherwise deducted.

## 2.  Service Availability

### 2.1 Calculation of Service Availability

Service Availability = (total time of a Single Instance within a Service Month calculated in minutes - Single Instance Service Downtime Calculated in Minutes) / total time of a Single Instance within a Service Month calculated in minutes × 100%

### 2.2 Service Availability Standard

**The Service Availability of the Service provided by Tencent Cloud will be** **no less than 99.95%**. You are entitled to the compensation as set forth in Section 3 (*Service Compensation*) below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below.

Assuming that the Total Time of a Single Instance within a Service Month is 30 × 24 × 60 × 99.95% = 43178.4 minutes, the Service downtime of the instance in such month will be 43200 -- 43178.4 = 21.6 minutes.

>?
> - The standard above applies only to the availability of the components of the Service per se; for the service availability of the other relevant Tencent Cloud services, such as COS, EMR and Oceanus, please refer to their respective service level agreement.
> - None of the additional functionality provided by the Service, including without limitation storing messages via COS, is covered by Service Availability guarantee herein.
> - The data in the Service is delivered asynchronously, which means, *among others*, that the Service cannot guarantee 100% storage of the data under the circumstance of multiple server malfunction, and therefore, in order to ensure the security of the data, you should make replicas of your instances and be responsible for backing up your data.

## 3. Service Compensation

In respect of this Service, if the Service Availability fails to meet the abovementioned standard, you will be entitled to compensations in accordance with the following terms:

### 3.1 Standards of Compensation

(1) Compensations will be made **in the form of voucher** by Tencent Cloud, and you should follow the rules for using the voucher (including the valid term; for details, please refer to the rules of vouchers published on Tencent Cloud's official website). You cannot redeem such voucher for cash or request to issue an invoice for such voucher. Such voucher can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability for a Service Month fails to meet the standard, the amount of compensation will be calculated for such month independently, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such month** (the Monthly Service Fee referred to herein shall exclude the portion deducted by a voucher or promotional credits, due to discounted service fee or otherwise deducted).

|**Service Availability (Av) for a Service Month**  | **Value of Compensation Voucher**|
|--------------------------------------------------- |-----------------------------------|
|99.95% > Av ≥ 99%	|10% of the Monthly Service Fee|
|99% > Av ≥ 95%|	25% of the Monthly Service Fee|
|95% > Av	|100% of the Monthly Service Fee|


### 3.2 Time Limit for Compensation Application

(1) If the Service Availability for a Service Month fails to meet the abovementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the fifth (5<sup>th</sup>) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail**.

(2) **You should apply for such compensation no later than sixty (60) calendar days following the expiry of the applicable Service Month in which the Service Availability fails to meet the standard**. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

## 4. Release of Liabilities

**If the Service is unavailable due to any of the following reasons, the corresponding Service downtime shall not be counted towards Service unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**
4.1	any failure of the Service to meet the availability standard due to reaching or exceeding the limit of the scale of the single business instance purchased by you.
4.2	any Service unavailability or failure of the Service to meet the availability standard due to any reason not attributable to Tencent Cloud.
4.3	any circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any terms of service, rules or guidelines published by Tencent Cloud separately.
4.4	any system maintenance with prior notice by Tencent Cloud to you, including system cutover, maintenance, upgrade and malfunction simulation test.
4.5	any defects of data flow or management flow resulting from open source community.
4.6	any attack on your application endpoint or data, or any other mal-operation.
4.7	any failure of you to abide by user guide or suggestions for using Tencent Cloud products.


## 5. Miscellaneous

5.1	**You understand that Tencent Cloud cannot warrant that the Service is error free; however Tencent Cloud will endeavor to continuously improve the quality and level of its services. As such, you hereby agree that Tencent will not be deemed to have breached this Agreement in case of any error of the Service, as long as such error is unavoidable in the context of the then existing technologies in the industry. You agree to cooperate with Tencent to resolve aforementioned error.**
5.2	**The parties hereto acknowledge and agree that, for any losses incurred by you during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.**
5.3	Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.
5.4	As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)

