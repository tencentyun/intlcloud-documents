CI can generate preview images for files of various types to display file content on webpages. This well meets the need to browse files online on different terminals such as PC and app. CI also provides text privacy detection capabilities to effectively recognize sensitive data contained in text like identity card numbers, bank card numbers, and mobile numbers. This fully satisfies various requirements for data availability and privacy protection.



## File Processing Fees

File processing fees are divided into **file-to-image conversion fees**, **file-to-HTML conversion fees**, and **privacy protection fees** as detailed below:

| Billable Item               | Description                                                   | Billing Cycle | Applicable Billing Mode                                         |
| ---------------- | ------------------------------------------------------------ | -------- | ------------------------------------ |
| File-to-image conversion fees   | Fees incurred by file-to-image conversion in the file preview service. Such fees are charged by the **number of successfully converted file pages**.  | Monthly | Pay-as-you-go<br />Resource pack: File preview resource pack |
| File-to-HTML conversion fees   | Fees incurred by file-to-HTML conversion in the file preview service. Such fees are charged by the **number of successful conversions**.  | Monthly | Pay-as-you-go<br />Resource pack: File preview resource pack |
| Privacy protection fees | Fees incurred by detection of privacy data contained in files, such as identity card numbers, license plate numbers, and mobile numbers. Such fees are charged by the **size of successfully detected files**. | Monthly | Pay-as-you-go                             |



## File Processing Pricing

| Billable Item | Price |
| ------------ | ---------- |
| File-to-image conversion | 0.1 USD/1,000 pages |
| File-to-HTML conversion | 0.01 USD/time |
| Privacy protection | 0.5 USD/GB |

>?
> - The file-to-image conversion feature allows you to perform basic image processing operations on the generated images, such as scaling, cropping, and watermarking, and fees incurred by such operations will be billed as basic image processing fees.
>- Failed file-to-HTML conversions will not be billed, and a preview request will be counted as one conversion.
> - Accessing files that are converted to HTML does not generate public network downstream traffic.



## Billing Example

Suppose you upload a batch of files to a bucket and use the file-to-image conversion and file-to-HTML conversion features of CI to process the files.

Usage statistics show that the file processing operation converted 50,000 file pages to images and converted files to HTML 10,000 times. You purchased a 100,000-time file preview resource pack valid for 12 months in the Chinese mainland last month.

The following can be concluded:

| Item | Free Tier | Unit Price | Resource Pack | Billable Usage | Fees (Unit Price * Billable Usage) |
| ---------- | -------- | ---------- | -------------------- | ------- | ------------------- |
| File-to-image conversion | 3,000 pages | 0.1 USD/1,000 pages | 100,000-time file preview resource pack | 0 pages | 0 USD |
| File-to-HTML conversion | None | 0.01 USD/time | 100,000-time file preview resource pack | 47,000 times | 470 USD |
| **Monthly fees** | -        |          -  |           -           |    -     | **470 USD**           |

>?
> - A CI file preview resource pack is used to deduct preview pages of images converted from files and HTML previews of such images at the ratio of 1:1 and 100:1, respectively. For example, 10,000 preview pages will be deducted from the resource pack for 10,000 preview pages of images converted from files, while one million preview pages will be deducted for 10,000 HTML previews of such images.
> - The deduction order of CI billable items is resource pack > pay-as-you-go. File-to-image conversions can be deducted from image compression resource packs and don't incur pay-as-you-go fees.
> - Storage fees are charged by COS.
