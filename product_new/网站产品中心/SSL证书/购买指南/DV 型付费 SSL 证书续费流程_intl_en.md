Renewing an SSL certificate is equivalent to applying for a new certificate in the console, so you need to install and deploy the new certificate to the server. The new certificate does not affect the normal use of the existing one.
>  If you need to modify the certificate information, please apply for a new one.

## Advantages of Renewal

Renewing the existing certificate shows the following advantages over purchasing a new one:

### Simplified renewal procedure

Instead of entering the application information again, you only need to confirm the original certificate's application data pulled automatically by the system to enter the payment process. After making the payment, please upload the confirmation letter and wait for certificate review.

### Extra-prolonged certificate validity after renewal

After renewal, the unused time of the original certificate and a complimentary period of 1 to 90 days will be added to the validity of the new certificate. You will not suffer any loss in terms of certificate validity period due to renewal.   

## Certificate Renewal Procedure

### Enter the certificate renewal entry

(1) For a paid DV certificate, the fast renewal option will become available 3 months before its expiration date. You can open the fast renewal window by clicking **Fast Renewal** in the "Status" column of the certificate in the certificate list in the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl).    
![](https://main.qcloudimg.com/raw/f978dc2826bf8e1dae216528de4354a9.jpg)
(2) In the SSL certificate renewal prompt page, confirm the information and click **Go to Renewal** to enter the renewal page. 

### Confirm the renewal information and make the payment

(1) For certificate renewal, you do not need to enter the information again. As a new certificate will be generated after the renewal, you need to set the CSR file for the new certificate. You can automatically generate a CSR file through the system or upload a CSR file on your own.
(2) After confirming the information, you can select the renewal period and click **Quick Pay** to enter the payment process.
![](https://main.qcloudimg.com/raw/887f113d125e44b00fc949cafcb577c1.jpg)
(3) Confirm the certificate information and click **Purchase** for payment.   

### Complete domain name authentication

(1) After purchasing a certificate successfully, you can find a new certificate generated in the certificate list of the SSL Certificate Service Console, with the status of **To be verified**. Then you can click **Details** to go to the certificate details page.   
(2) The DNS verification value will be generated in the certificate details. You need to add that DNS record and wait for scan and verification by the CA. The certificate will be issued immediately after approval.   
 ![](https://main.qcloudimg.com/raw/89de6fa1a8d2a52855df62f2dc810fbe.jpg)
