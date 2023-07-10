CI integrates various powerful features of Tencent Cloud AI for data stored in COS, such as image tagging, smart face cropping, QR code recognition, speech recognition, beauty filter, and face filter. These value-added services are widely used in ecommerce and video websites as well as social media and photo apps to facilitate image content management.



## Content Recognition Fees

Content recognition fees are divided into **QR code recognition fees**, **image tagging fees**, **image quality assessment fees**, **face recognition fees**, **FaceID fees**, **vehicle recognition fees**, **OCR fees**, and **speech recognition fees** as detailed below:

| Billable Item               | Description                                                   | Billing Cycle | Applicable Billing Mode                                         |
| ----------------------- | ------------------------------------------------------------ | -------- | ---------------------------------------------------------- |
| QR code recognition fees | Fees incurred by recognizing QR codes in images. Such fees are charged by the **number of recognitions**. | Monthly | Pay-as-you-go <br />Resource Pack: Content recognition resource pack |
| Image tagging fees | Fees incurred by tagging images (displayed as content recognition fees in bills). Such fees are charged by the **number of recognitions**. | Monthly | Pay-as-you-go <br />Resource Pack: Content recognition resource pack |
| Image quality assessment fees | Fees incurred by assessing the quality of images. Such fees are charged by the **number of assessments**. | Monthly | Pay-as-you-go |
| Face recognition fees | Fees incurred by recognizing faces in images, including face detection and face filter (beauty filter, gender swap, age change, face cut-out, etc.). Such fees are charged by the **number of recognitions**. | Monthly | Pay-as-you-go <br />Resource pack: Face filter resource pack (deductible only for the face filter service) |
| FaceID fees | Fees incurred by verifying the identity of faces in images. Such fees are charged by the **number of successful API calls**. | Monthly | Pay-as-you-go |
| Vehicle recognition fees | Fees incurred by recognizing vehicles in images, including license plate number recognition and vehicle recognition. Such fees are charged by the **number of recognitions**. | Monthly | Pay-as-you-go |
| OCR fees | Fees incurred by performing OCR on images, including ID card recognition and general character recognition (print recognition, print recognition (high-precision), print recognition (lite), print recognition (high-speed), and handwriting recognition). Such fees are charged by the **number of recognitions**. | Monthly | Pay-as-you-go |
| Speech recognition fees | Fees incurred by recognizing speeches in recording files and returning the recognized text. Such fees are charged by the **duration of recognition**. | Monthly | Pay-as-you-go |



## Content Recognition Pricing

### QR code recognition fees

| Billable Item | Price |
| :--------- | :------- |
| QR code recognition | 1 USD/1,000 times |



### Image tagging fees

| Images Recognized per Month (N) | Price |
| :------------------- | :---------- |
| N ≤ 3 million | 1.50 USD/1,000 times |
| 3 million < N ≤ 15 million | 1.35 USD/1,000 times |
| 15 million < N ≤ 30 million | 1.30 USD/1,000 times |
| N > 30 million | 1.10 USD/1,000 times |

> !Content recognition adopts a scoring mechanism, with a score between 0 and 100 returned for each image.



### Image quality assessment fees

| Images Assessed per Month | Price |
| :--------------------- | :--------- |
| 0 < assessments ≤ 1 million | 3 USD/1,000 times |
| 1 million < assessments ≤ 3 million | 2.5 USD/1,000 times |
| 3 million < assessments ≤ 15 million | 2 USD/1,000 times |
| Assessments > 15 million | 1.5 USD/1,000 times |



### Face recognition fees

**Face detection**

| Images Detected per Month | Price |
| :--------------------- | :--------- |
| 0 < detections ≤ 3 million | 0.5 USD/1,000 times |
| 3 million < detections ≤ 15 million | 0.4 USD/1,000 times |
| Detections > 15 million | 0.3 USD/1,000 times |

**Face filter**

| Calls per Month | Price |
| :-------------------- | :-------- |
| 0 < calls ≤ 10,000 | 10 USD/1,000 times |
| 10,000 < calls ≤ 100,000 | 9 USD/1,000 times |
| 100,000 < calls ≤ 1 million | 8 USD/1,000 times |
| Calls > 1 million | 7 USD/1,000 times |



### FaceID fees

| Calls per Month | Price |
| :----------------- | :-------- |
| 0 < calls ≤ 1000 | 1 USD/time |
| 1,000 < calls ≤ 10,000 | 0.85 USD/time |
| 10,000 < calls ≤ 100,000 | 0.75 USD/time |
| Calls > 100,000 | 0.68 USD/time |



### Vehicle recognition fees

| Images Recognized per Month | Price |
| :--------------------- | :--------- |
| 0 < recognitions ≤ 1 million     | 3 USD/1,000 times   |
| 1 million < recognitions ≤ 3 million | 2.5 USD/1,000 times   |
| 3 million < recognitions ≤ 15 million | 2 USD/1,000 times   |
| Recognitions > 15 million | 1.5 USD/1,000 times   |



### Image OCR fees

**OCR** prices vary by recognition type as shown below:

| Recognition Type | 0 < Calls ≤ 10,000 | 10,000 < Calls ≤ 100,000 | Calls > 100,000 |
| :------------- | :--------------- | :------------------ | :-------- |
| Print recognition | 0.15 USD/time | 0.10 USD/time | 0.06 USD/time |
| High-precision print recognition | 0.50 USD/time | 0.35 USD/time | 0.20 USD/time |
| Simplified print recognition | 0.08 USD/time | 0.05 USD/time | 0.03 USD/time |
| High-speed print recognition | 0.50 USD/time | 0.35 USD/time | 0.20 USD/time |
| Handwriting recognition | 0.15 USD/time | 0.10 USD/time | 0.06 USD/time |

**ID card recognition**

| Images Recognized per Month | Price |
| :----------------- | :-------- |
| 0 < recognitions ≤ 10,000 | 0.15 USD/time |
| 10,000 < recognitions ≤ 100,000 | 0.1 USD/time |
| Recognitions > 100,000 | 0.06 USD/time |



### Speech recognition fees

| Monthly Usage (N) | Price |
| :----------------------- | :---------- |
| N ≤ 120,000 hours | 1.75 USD/hour |
| 120,000 hours < N ≤ 300,000 hours | 1.4 USD/hour |
| N > 300,000 hours | 0.95 USD/hour |



## Billing Example

Suppose you upload a batch of images to a bucket, use CI's **content recognition** feature, and enable the CDN acceleration service.

Usage statistics show that QR code recognition, face filter, and ID card recognition are used 30,000, 50,000, and 50,000 times respectively, and 100 GB CDN origin-pull traffic is generated in this month. You also purchase a 100,000-time face filter resource pack valid for 12 months in the Chinese mainland in this month.

The following can be concluded:

| Item | Free Tier | Unit Price | Resource Pack | Billable Usage | Fees (Unit Price * Billable Usage) |
| --------------- | -------- | -------- | -------------------- | ------- | ------------------- |
| QR code recognition fees | None | 1 USD/1,000 times | None | 30,000 times | 30 USD |
| Face filter fees | None | 9 USD/1,000 times | 100,000-time face filter resource pack | 0 times | 0 USD |
| ID card recognition fees | None | 0.1 USD/time | None | 50,000 times | 5,000 USD |
| CDN origin-pull traffic fees | 10 GB | 0.15 USD/GB | None | 100 GB | 15 USD |
| **Monthly fees**      | -        |       -   |          -            |       -  | **5045 USD**          |

>?
> - The deduction order of CI billable items is resource pack > pay-as-you-go. Face filters can be deducted from face filter resource packs and don't incur pay-as-you-go fees.
> - ID card recognition adopts tiered pricing. When the number of recognitions is above 10,000 times, the unit price is 0.1 USD/time.
