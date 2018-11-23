Renewing an SSL certificate is equivalent to applying for a new certificate in the console, so you need to install and deploy the new certificate to the server. The new certificate does not affect the use of the existing certificate.
> **Note:**
> If you need to modify the certificate information, please apply for a new one.

## Advantages of Renewal
Renewing the existing certificate shows the following advantages over purchasing a new one:    
### Simplified renewal procedure
Instead of entering the application information again, you only need to confirm the original certificate's application data pulled automatically by the system to enter the payment process. After the payment is completed, upload the confirmation letter for certificate review.   
### Extra-prolonged certificate validity after renewal
After renewal, the unused time of the original certificate and a complimentary period of 1 to 90 days will be added to the validity of the new certificate. You will not suffer certificate validity loss.   

## Certificate Renewal Procedure
### 1. Enter the certificate renewal entry
(1) The quick renewal channel is opened for a DV paid certificate 3 months before its expiration. You can go to the certificate list in the SSL certificate console, click **Quick Renewal** in the status column of the corresponding certificate, and then the quick renewal window pops up.    
![](https://mc.qcloudimg.com/static/img/f1a8c5f4245cde0334dbf2e0770960d8/image.png)
(2) In the SSL certificate renewal prompt page, confirm the information and click **Go to Renewal** to enter the renewal page. 

### 2. Confirm the renewal information and make the payment
(1) When renewing a certificate, you do not need to enter the certificate information again. A new certificate will be generated after the renewal, so you need to configure a CSR file for the new certificate. The system can automatically generate a CSR file, or you can upload a CSR file.
(2) After confirming the information, you can select the renewal period and click **Quick Pay** to enter the payment process.
![](https://mc.qcloudimg.com/static/img/7c949a9725f458b8d6b84ddc6975e566/image.png)
(3) Confirm the certificate information and click **Purchase** for payment.   

### 3. Upload the confirmation letter for review
(1) After purchasing a certificate successfully, you can find a new certificate generated in the certificate list of the SSL Certificates Service console, with the status of **To be verified**. Then you can click **Details** to go to the certificate details page.   
  
(2) A resolution verification value is generated in the certificate details, and you need to add this DNS resolution record. After that, wait for the CA to scan for verification. The certificate will be issued immediately after the verification is passed.   
 ![](https://mc.qcloudimg.com/static/img/dbf0dd813451ecffa1ca71de8089c2c5/image.png)

