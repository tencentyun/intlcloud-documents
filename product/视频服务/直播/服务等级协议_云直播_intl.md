**In order to use the Tencent Cloud Cloud Streaming Services ("CSS") service (the "Service"), you should read and observe this Cloud Streaming Services Service Level Agreement (this "Agreement", or this "SLA") and the** **[Tencent Cloud Service Agreement](https://intl.cloud.tencent.com/document/product/301/9248). This Agreement contains, *among others*, the terms and definitions of the Service, level indicators of the Service availability and success rate, compensation plan and release of liabilities. Please carefully read and fully understand each and every provision hereof, and the provisions restricting or releasing certain liabilities, or otherwise related to your material rights and interests, may be in bold font or underlined or otherwise brought to your special attention.**

**Please do not purchase the Service unless and until you have fully read, and completely understood and accepted all the terms hereof. By clicking "Agree"/ "Next", or by purchasing or using the Service, or by otherwise accepting this Agreement, whether express or implied, you are deemed to have read, and agreed to be bound by, this Agreement. This Agreement shall then have legal effect on both you and Tencent Cloud, constituting a binding legal document on both parties.**

##  **1. Terms and Definitions**

1.1  **Cloud Streaming Services (CSS) Service**: is the low-latency, high-concurrency, stable and smooth audio and video broadcasting service provided by Tencent Cloud. CSS supports functions including but not limited to real-time transcoding, intelligent porn detection, screenshot and recording, and is subject to the Service you purchase and contents of the Service provided by Tencent Cloud.

1.2  **Service Period/Month**: A calendar month is counted as a Service Period. When the period concerned is less than one full calendar month, the period from the day on which a user starts to use the Service to the very last day of such month will be counted as one Service Period. For example, if one starts to use the Service on March 19, the first Service Period will be from March 19 to March 31. The availability of the Service is calculated independently for each Service Period.

1.3  **Unit of Time**: For measuring the Service, each 5 minutes will be deemed as one measurement unit, resulting in 288 measurement points each day. The measurement point of 00:00:00 represents the time slot from 00:00:00 to 00:04:59, and the rest can be deduced by analogy.

1.4  **Failure Rate of Video Playing within each Unit of Time**: the proportion of the number of failed requests of the Service due to reasons attributable to Tencent Cloud within one Unit of Time out of the total number of valid requests within such Unit of Time, i.e., Failure Rate of Video Playing within each Unit of Time = number of failed requests for video loading within one Unit of Time / total number of valid requests within such Unit of Time × 100%. A failed request refers to a valid quest with the return of a 5XX error code or a user request failure due to the unavailability of any Tencent Cloud Cloud Streaming Services node. A valid request refers to a request received by the server of the Cloud Streaming Services. However, any failure of video playing due to expiration of any anti-leech protection adopted by a user with anti-leech authentication enabled, or block of a domain name caused by any illegal or prohibited live broadcasting content or otherwise, or any anomaly on the push end, will not be deemed a valid request. If the total number of your valid requests within one Unit of Time is less than 250, service availability will not be counted for such Unit of Time. One IP will be deemed as one user, and all repeated failed requests of one IP within the measurement time period will be deemed as one failed request.

1.5  **Service Downtime within a Service Period Calculated in Minutes**: If the Failure Rate of Video Playing within each Unit of Time of the Cloud Streaming Services service is more than 0.4%, it shall be deemed that the Service is unavailable within such Unit of Time. If such situation lasts for ten (10) minutes or more, such time period shall be counted into the Service downtime. If such situation that lasts less than ten (10) minutes, it will not be counted into the Service downtime. The accumulative total of Service downtime within a Service Period is the Service Downtime within a Service Period Calculated in Minutes.

1.6  **Monthly Service Fee for a Service Month**: the service fees for CSS under a Tencent Cloud account of a client during one Service Month (including data charges by data volume or by bandwidth, and charges for transcoding, recording, screenshot, porn detection and other value-added services). 

1.7  **Total Time within a Service Month Calculated in Minutes**: the total number of days within such Service Month × 24 (hours) × 60 (minutes).

##   **2. Service Availability**

###  **2.1 Calculation of Service Availability**

Service Availability = (1 - Service Downtime within a Service Period Calculated in Minutes / Total Time within a Service Period Calculated in Minutes) × 100%

### **2.2 Service Standard Indicator**

**The Service Availability of the Service** provided by Tencent Cloud will be **no less than 99.9%**. You are entitled to the compensation as set forth in Section 3 below if the Service Availability fails to meet the aforementioned standard, other than in any circumstance as provided for in the release of liabilities provisions below.

##  **3. Service Compensation**

In respect of this Service, if the Service Availability fails to meet the aforementioned standard, you will be entitled to compensations in accordance with the following terms:

### **3.1 Standards of Compensation**

(1) Compensations will be made **in the form of CSS voucher** by Tencent Cloud, and you should follow the rules for using the voucher (including the valid term; for details, please refer to the rules of vouchers published on Tencent Cloud's official website). You cannot redeem such voucher for cash or request to issue an invoice for such voucher. Such voucher can only be used to purchase the Service by using your Tencent Cloud account. You cannot use the voucher to purchase other services of Tencent Cloud, nor should you give the voucher to a third party for consideration or for free.

(2) If the Service Availability of a Service Month fails to meet the standard, the amount of compensation will be calculated for such month independently, and **the aggregate amount shall be no more than the applicable Monthly Service Fee paid by you for such month** (the Monthly Service Fee referred herein shall exclude the portion deducted by a voucher or promotional credits, due to discounted service fee or otherwise deducted).

|Service Availability of a Service Month  | Value of Compensation Voucher|
|-| -|
|≥ 95% and < 99.9%    |  5% of the Monthly Service Fee|
|< 95%  |10% of the Monthly Service Fee|

###  **3.2 Time Limit for Compensation Application**

(1) If the Service Availability of a Service Month fails to meet the aforementioned Service Availability standard, you may apply for compensation **through (and only through) the support ticket system under your relevant account** after the fifth (5^th^) business day of the month immediately following such Service Month. Tencent Cloud will verify and ascertain your application upon receipt of such application. If there is any dispute over the calculation of the Service Availability for a Service Month, **both parties agree that the back-end record of Tencent Cloud will prevail**.

(2) **You should apply for such compensation no later than sixty (60) calendar days following the expiration of the applicable Service Month in which the Service Availability fails to meet the standard**. If you fail to make any application within such period, or make the application after such period, or make the application by any means other than that agreed herein, it shall be deemed that you have voluntarily waived your right to apply for such compensation and any other rights you may have against Tencent Cloud, in which case Tencent Cloud has the right to reject your application for compensation and not to make any compensation to you.

##  **4. Release of Liabilities**

**If the Service is unavailable due to any of the following reasons, the corresponding Service downtime shall not be counted towards Service unavailability period, and is not eligible for compensation by Tencent Cloud, and Tencent Cloud will not be held liable to you:**

4.1 any error due to the block of a domain name due to any illegal or prohibited content of a client or otherwise.

4.2 any loss or leak of data, pin or password due to improper maintenance or improper confidentiality measures of a client.

4.3 any hacker attack on a client's website.

4.4 any impact on the availability of the Service due to impromptu increase of traffic of a client (impromptu increase by 200% of daily peak of which the bandwidth is greater than 200Gbps) unless the client has provided a three-business day prior written notice to Tencent Cloud and subscribed a CSS escort service.

4.5  any system maintenance with prior notice by Tencent Cloud to a client, including system cutover, maintenance, upgrade and failure simulation test.

4.6 any failure or configuration adjustment of network or equipment that is not Tencent Cloud facility.

4.7 any failure of video playing due to expiration of any anti-leech protection adopted by a client with anti-leech authentication enabled.

4.8  any failure of video playing due to block of a domain name caused by any illegal or prohibited content of a client or otherwise.

4.9  any failure of video playing due to anomaly on the push end.

4.10  any force majeure event or accident.

4.11  any other reason not attributable to Tencent Cloud.

4.12  any Service unavailability or failure of the Service to meet the availability standard above not attributable to Tencent Cloud.

4.13  any other circumstances in which Tencent Cloud will be exempted or released from its liabilities (for compensation or otherwise) according to relevant laws, regulations, agreements or rules, or any rules or guidelines published by Tencent Cloud separately.


##  **5. Miscellaneous**

5.1  The parties hereto acknowledge and agree that, for your losses during the course of using the Service due to any breach by Tencent Cloud, the aggregate compensation amount payable by Tencent Cloud shall under no circumstance exceed the total service fees you have paid for the relevant Service which is not performed.

5.2 **Cloud Streaming Services offer the verification methods, such as using IP, Referer or Authentication Key (“Verification Methods”) to verify the legitimacy of the service access request, which you may choose to use at your sole discretion, but the Verification Methods may be circumvented by counterfeit information, and you shall not solely rely on the Verification Methods for your content protection. Tencent Cloud disclaims liability for any loss of the piracy caused by circumvention of the Verification Methods. It is strongly recommended that you remotely verify the legitimacy of Cloud Streaming Services request if you have higher requirements for the content security.**

5.3 Tencent Cloud has the right to amend the terms of this Agreement as appropriate or necessary in light of changes in due course. You may review the most updated version of relevant Agreement terms on the official website of Tencent Cloud. If you disagree with such revisions made by Tencent Cloud to this Agreement, you have the right to cease using the Service; by continuing to use the Service, you shall be deemed to have accepted the Agreement as amended.

5.4  As an ancillary agreement to the Tencent Cloud Service Agreement, this Agreement is of the same legal effect as the Tencent Cloud Service Agreement. In respect of any matter not agreed herein, you shall comply with relevant terms under the Tencent Cloud Service Agreement. In case of any conflict or discrepancy between this Agreement and the Tencent Cloud Service Agreement, this Agreement prevails to the extent of such conflict or discrepancy. (End of Document)
