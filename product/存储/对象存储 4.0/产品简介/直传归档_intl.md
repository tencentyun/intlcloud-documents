Currently, there are two archive storage modes: Cloud Archive Storage (CAS) and archive storage in Cloud Object Storage (COS) through lifecycle transition. We will unify those two modes in the future by removing the former and retaining the latter. In addition, we have implemented direct upload archiving in COS, i.e., directly uploading objects to COS in the archive storage class.

You can use the console, API, SDK, or COSCMD tool for direct upload archiving in COS.

- Upload via the console
After selecting the object to be uploaded through **Upload a File** in the [COS Console](https://console.cloud.tencent.com/cos5), select the storage class as **Archive Storage** in the "Set Object Properties" tab.
![](https://main.qcloudimg.com/raw/a4988d35919e07340aa8bc46d42dd32a.png)
 
- Upload via API
Direct upload archiving can be implemented by setting x-cos-storage-class to ARCHIVE in the PUT Object, POST Object, or Initiate Multipart Upload APIs.
>The Append Object API does not support direct upload archiving.

- Upload via SDK
Currently, all SDKs of COS support direct upload archiving by setting the StorageClass parameter to ARCHIVE during file upload.

- Upload via COSCMD
The COSCMD tool supports direct upload archiving by adding the header field x-cos-storage-class and setting it to ARCHIVE during file upload.

#### Archive Storage Restoration and Download
Downloading the archive storage is different from the standard and standard infrequent access storage. You need to restore it first before you can download it. The restoration can be performed in the following three ways:
- Expedited mode: Files below 256 MB can be read in 1 to 5 minutes.
- Standard mode: Restoration can be completed generally in 3 to 5 hours.
- Batch mode: Data can be retrieved generally in 5 to 12 hours with the lowest cost.

In addition, the console, API, SDK, and COSCMD tool all support archive storage restoration and download.

#### Current Constraints for Direct Upload Archiving
- If you want to download an archive storage object, you need to restore it first.
- If you want to replicate an archive storage object, you need to restore it first.
- Archive storage objects cannot be replicated across regions.
- Archive storage objects cannot be converted to standard or standard infrequent access storage.
