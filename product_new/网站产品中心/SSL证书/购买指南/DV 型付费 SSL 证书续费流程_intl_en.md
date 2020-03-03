Renewing an SSL certificate is equivalent to applying for a new one in the console, and you need to install and deploy it on the server. The new certificate does not affect the usage of the existing one.
> If you need to modify the certificate information, please apply for a new one.

## Advantages of Renewal

Renewing the existing certificate holds the following advantages over purchasing a new one:

### Simplified renewal procedure

Instead of entering application information again, you only need to confirm the original certificate's application data pulled automatically by the system and proceed with the payment. After making the payment, please upload the confirmation letter and wait for certificate review.

### Extra-prolonged certificate validity after renewal

After renewal, the remaining available time of the original certificate and an extra 1 to 90 days will roll to the validity time of the new certificate for free. You will not experience any loss in certificate validity period due to renewal.   
 
## Certificate Renewal Procedure

### Starting certificate renewal

1. For a paid DV certificate, the fast renewal option will become available 3 months before its expiration date. You can open the fast renewal window by clicking **Fast Renewal** in the "Status" column of the certificate in the certificate list in the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl).    
![](https://main.qcloudimg.com/raw/e879a7c8313de8c4ee48d1157acb2227.png)
2. In the SSL certificate renewal prompt window that pops up, confirm the information and click **Renew Now** to enter the renewal page. 

### Confirming renewal information and making payment

1. When renewing a certificate, you do not need to enter the certificate information again. A new certificate will be generated after the renewal, so you need to configure a CSR file for the new certificate.
   - You can automatically generate a CSR file through the system (**this option is recommended, and the CSR and private key can be generated**).
   - You can also upload a CSR file (**no private key can be generated with this option**).
2. After confirming the information, select the renewal period and click **Pay** to enter the payment process as shown below:
![](https://main.qcloudimg.com/raw/41e0203685862dd22800625594feaa88.png)
3. Confirm the certificate information and click **Purchase** for payment.   

### Completing domain name identity verification

1. After purchasing a certificate successfully, you can find a new certificate generated with the status of **To be verified** in the certificate list in the SSL Certificate Service Console. Then, you can click **Details** to enter the certificate details page.   
2. The DNS verification value will be generated in the certificate details. You need to add that DNS record and wait for scan and verification by the CA. The certificate will be issued immediately after approval as shown below:
 ![](https://main.qcloudimg.com/raw/beb1b5ae08553a832cabe9c0cb881cc5.png)
