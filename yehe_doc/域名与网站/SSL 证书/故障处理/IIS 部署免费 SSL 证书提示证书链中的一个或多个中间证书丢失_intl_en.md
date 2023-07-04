## Symptom

"One or more intermediate certificates in the certificate chain are missing. To resolve this issue, make sure that all of the intermediate certificates are installed" is prompted when a free SSL certificate is deployed on the IIS web server.


## Possible Causes

Intermediate certificates are missing.

## Solutions

### Step 1. View the encryption algorithm of the certificate

Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/certoverview) and view the encryption algorithm type of your certificate.

### Step 2. Download the intermediate certificate file

Download the intermediate certificate file to your CVM instance based on the encryption algorithm type of your certificate.
- RSA encryption algorithm: Download [here](https://upload-dianshi-1255598498.file.myqcloud.com/TrustAsia%20RSA%20DV%20TLS%20CA%20G2-02085dd70442134c6abdefd92f9d40ce16e5774c.crt).

- ECC encryption algorithm: Download [here](https://upload-dianshi-1255598498.file.myqcloud.com/TrustAsia%20ECC%20DV%20TLS%20CA%20G2-677875f5af3a5f066dc7d0fbb9400745e97d1a53.crt).


### Step 3. Install the intermediate certificate
1. On the target server, double-click the intermediate certificate file and click **Install Certificate** in the pop-up window.

2. In the certificate import wizard, set **Store Location** to **Local Machine** and click **Next**.

3. In **Certificate Store**, select **Place all certificates in the following store** > **Intermediate Certification Authorities** and click **Next**.

4. Check the location to install the certificate and click **Finish**.

5. If "The import was successful." is displayed, the operation is successful. Then, try deploying your SSL certificate again.
