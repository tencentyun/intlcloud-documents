CI can generate preview images for files of various types to display file content on webpages. This well meets the need to browse files online on different terminals such as PC and app. CI also provides text privacy detection capabilities to effectively recognize sensitive data contained in text like identity card numbers, bank card numbers, and mobile numbers. This fully satisfies various requirements for data availability and privacy protection.



## File Processing Fees

File processing fees are divided into **file-to-image conversion fees**, **file-to-HTML conversion fees**, and **privacy protection fees** as detailed below:

| Billable Item               | Description                                                   | Billing Cycle | Applicable Billing Mode                                         |
| :--------------- | :----------------------------------------------------------- | :------- | :------------- |
| File-to-image conversion fees   | Fees incurred by file-to-image conversion in the file preview service. Such fees are charged by the **number of successfully converted file pages**.  | Monthly | Pay-as-you-go |
| File-to-HTML conversion fees   | Fees incurred by file-to-HTML conversion in the file preview service. Such fees are charged by the **number of successful conversions**.  | Monthly | Pay-as-you-go |
| Privacy protection fees | Fees incurred by detection of privacy data contained in files, such as identity card numbers, license plate numbers, and mobile numbers. Such fees are charged by the **size of successfully detected files**. | Monthly | Pay-as-you-go                             |

## File Processing Pricing

| Billable Item | Price |
| :----------- | :------------- |
| File-to-image conversion | 0.015 USD/1,000 pages |
| File-to-HTML conversion | 0.0014 USD/time |
| Privacy protection | 0.0791 USD/GB |

>？
>
> - The file-to-image conversion feature allows you to perform basic image processing operations on the generated images, such as scaling, cropping, and watermarking, and fees incurred by such operations will be billed as basic image processing fees.
>- Failed file-to-HTML conversions will not be billed. One preview request will be counted as one conversion.
> - Accessing files that are converted to HTML does not generate public network downstream traffic.

## Billing Example

Suppose you upload a batch of files to a bucket and use the file-to-image conversion and file-to-HTML conversion features of CI to process the files.

Usage statistics show that the file processing operation converted 50,000 file pages to images and converted files to HTML 10,000 times.

The following can be concluded:

| Item | Free Tier | Unit Price | Billable Usage | Fees (Unit Price * Billable Usage) |
| :------------- | :------- | :------------- | :------- | :--------------------- |
| File-to-image conversion     | 3,000 pages   | 0.015 USD/1,000 pages | 47,000 pages | 0.015 * 4.7 = 0.0705 USD   |
| File-to-HTML preview | None       | 0.0014 USD/time  | 10,000 times | 0.0014 * 10,000 = 14 USD |
| **Monthly fees**     | -        | -              | -        | **14.0705 USD**          |

>?
>
> - Storage fees are charged by COS.