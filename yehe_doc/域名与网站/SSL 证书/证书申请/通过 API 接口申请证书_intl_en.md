## Overview

This document describes how to use SSL Certificate Service APIs to apply for a paid SSL certificate.

## Prerequisites

You have signed up for a Tencent Cloud account. 

## Applying for a Certificate via APIs

The process for applying for a certificate via APIs varies by certificate brand and type. Select the certificate brand and type as needed.


### Applying for a paid DV certificate via APIs

Call the corresponding SSL Certificate Service APIs as shown below. The CA will review the information and contact you for manual review.
After the certificate is issued, download it via the `DownloadCertificate` API as shown below:
![](https://main.qcloudimg.com/raw/3e66184ff219d6c9031a0ab468f5707a.png)

### Applying for a GeoTrust, SecureSite, TrustAsia, or GlobalSign OV/EV certificate via APIs

Call the corresponding SSL Certificate Service APIs as shown below. The CA will review the confirmation letter and contact you for domain validation. For detailed directions, see [DNS Validation](https://intl.cloud.tencent.com/document/product/1007/45895) or [File Validation](https://intl.cloud.tencent.com/document/product/1007/43542).
After the certificate is issued, download it via the `DownloadCertificate` API as shown below:
![](https://main.qcloudimg.com/raw/61d621dcdc7f5430a6809f29c6383aec.png)

### Applying for a paid WoTrus OV/EV certificate via APIs

Call the corresponding SSL Certificate Service APIs as shown below. The CA will review the information and contact you for manual review.
After the certificate is issued, download it via the `DownloadCertificate` API as shown below:
![](https://main.qcloudimg.com/raw/c484b304196d476495c3c62856011bcf.png)
