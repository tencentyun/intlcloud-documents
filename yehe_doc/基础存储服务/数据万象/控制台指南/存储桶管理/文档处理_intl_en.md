## Overview

CI provides **privacy protection** and **file preview** features for document files.



## File Preview

The file preview feature allows generating **images** from multiple types of files for preview. It addresses the display problems of file content on webpages and enables easy **online file preview** on PC, app, and other terminals. It is widely suitable for diverse business scenarios, such as online education, enterprise OA, and website transcoding. Currently, this feature supports **real-time preview during download** and **async file preview job creation**.

>?
>- Currently supported input file types include:
>  Presentation files: PPTX, PPT, POT, POTX, PPS, PPSX, DPS, DPT, PPTM, POTM, PPSM.
>  Text files: DOC, DOT, WPS, WPT, DOCX, DOTX, DOCM, DOTM.
>  Spreadsheet files: XLS, XLT, ET, ETT, XLSX, XLTX, CSV, XLSB, XLSM, XLTM, ETS.
>  Other files: PDF, LRC, C, CPP, H, ASM, S, JAVA, ASP, BAT, BAS, PRG, CMD, RTF, TXT, LOG, XML, HTM, HTML.
>- The input file size cannot exceed 200 MB.
>- The number of pages in the input file cannot exceed 5,000.

### Directions

The **File Preview** page in the console provides file preview operations, such as enabling/disabling the file preview feature, creating file preview jobs, enabling/disabling file preview queues, and setting the callback.

#### Activating service

1. Log in to the [CI console](https://console.cloud.tencent.com/ci/) and click **Bucket Management** to enter the bucket management page.
2. On the **Bucket Management** page, click the target bucket to enter the bucket details page.
3. Click **File Processing** on the left and select the **File Preview** configuration item.
4. Click **Edit** to enable file preview and click **Save**.
5. After the feature is enabled, you can use the corresponding file preview API to preview files during downloading as instructed in [Sync Request API](https://intl.cloud.tencent.com/document/product/1045/47929). You can also create file preview jobs asynchronously as instructed in [Submitting File Transcoding Job](https://intl.cloud.tencent.com/document/product/1045/47932).



#### Creating job

1. Click **Create Job** in the job management module and enter job parameters as follows:
 - File Path: The file path must start with "/" and use "/" to separate folders, such as `/doc/example.dox`.
 - Preview Setting: Select to preview whole document or specified page. A job supports up to 5,000 pages. If more pages are input, only the first 5,000 pages can be converted.
 - Queue: After you activate the file preview service, the system will enable the `queue-doc-process-1` queue for you by default. You can manually disable it in the queue module. If you need more queues, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
 - Output Bucket: Select a bucket for which the file preview feature has been enabled in the current region.
 - Output Image Format: Currently, JPG and PNG formats are supported for output images.
 - Output Path: It is optional. If it is not set, it will be the same as the input file path.
 - Output File Name: The file preview feature converts each page of the original file into an image. Therefore, you need to add a placeholder (`${Number}` or `${Page}`) to the output filename to number the output images. The output numbers are the same as the file page numbers. For example, if you want to preview a file with three pages and set the output filename to `output${Number}.jpg`, then three images `output1.jpg`, `output2.jpg`, `output3.jpg` will be output.

2. Click **Confirm**.

#### Managing job

You can filter and view file preview jobs in the job management module by time, job ID, and job status. You can also click **View** in the **Operation** column to view more job information in addition to that displayed on the page.



#### Setting queue

After you activate the file preview service, the system will enable the `queue-doc-process-1` queue for you by default. You can pause it in the **Operation** column in the queue module.



#### Setting callback

1. Click **Queue** to enter the **Queue** page.
2. Click **Configure Callback Rule** in the **Operation** column to enter the callback settings page.
3. Click **Edit** to enable callback, enter a callback URL, and click **Confirm**. Then, after a file preview job is completed, its execution result will be sent to the callback URL for you to perform subsequent operations.
>! The callback URL can be used only if the HTTP 200 status code is returned by default. It will take effect in five minutes after configuration.
>


>?
> - File preview is a paid feature. For billing details, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1045/33431).



## Privacy Protection

CI's privacy protection feature can filter various types of private data in files to effectively prevent information leakage, such as ID number, taxpayer identification number, business registration number, military ID number, email address, license plate number, and mobile number. Currently, it can only scan data automatically during upload.

>?Currently, the privacy protection feature is supported for the following types of files:
>
>- Microsoft Office files: DOC, DOCX, PPT, PPTX, XLS, XLSX, RTF
>- WPS files: WPS, DPS, ET
>- PDF files: PDF
>- Plain text files: TXT, XML, SLK
>- Web files: HTML, MSG
>- Email files: EML, PST

### Directions

1. Log in to the [CI console](https://console.cloud.tencent.com/ci/bucket) and click **Bucket Management** to enter the bucket management page.
2. On the **Bucket Management** page, click the target bucket to enter the bucket details page.
3. Click **File Processing** on the left and select the **Privacy Protection** configuration item.
4. Click **Edit** to enable this feature and configure it as follows:
    - File Type: You can select multiple file types for which privacy protection will be automatically triggered.
    - Moderation Type: You can select multiple types of sensitive data to be filtered.
    - Callback: After callback is enabled, you can enter a callback URL to receive the filtering results of privacy protection. Note that the callback URL can be used only if the HTTP 200 status code is returned by default. It will take effect in five minutes after configuration.

5. After enabling privacy protection, you can view the **private data details** below by time, violation type, sensitivity level, or moderation type.


>?Violation types include violation of GDPR, cybersecurity classified protection compliance, and the Cybersecurity Law of China. Files will be classified into high, medium, and low sensitivity levels based on the moderation results.
>
