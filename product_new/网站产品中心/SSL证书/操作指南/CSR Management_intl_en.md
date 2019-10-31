## Use cases

CSR is short for Certificate Signing Request. To obtain an SSL certificate, you need to first generate a CSR file and submit it to the certificate authority (CA). A CSR file contains a public key and a distinguished name and is usually generated from a web server. A pair of public and private keys for encryption and decryption will be created at the same time. This document describes how to generate and manage CSR files.

## Prerequisites

You have logged in to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl/csr)

## Directions

### Generate a CSR

1. Select **SSL Certificate Service** > **CSR Management** and click **Create CSR**.

  ![](https://main.qcloudimg.com/raw/3a2958a6e96ade184b47f0a68a689ede.png)

2. Enter the relevant information, as shown below:

   ![](https://main.qcloudimg.com/raw/aef3a40c847fcc792fe2b631160d70e7.png)

Main parameters:

- Domain name: Enter the domain name/wildcard domain name to be bound to the certificate.

- Organization Name: The legally registered name of your organization. The complete English name must be entered for DV certificates. For OV and EV certificates, please enter the complete English or Chinese name as shown on the business license.

- Organizational Unit: This field is used to differentiate departments within an organization, such as "Engineering Department " or "Human Resources".

- Email (E): Your email address, which is optional.

- State/Province (S): The state or province where your organization is located.

- City/Locality (L): The city or locality where your organization is registered or located.

- Country/Region (C): The code of the country/region where your organization is legally registered, in the format of two letters as defined by the International Organization for Standardization (ISO). 

- Key Algorithm: Optional. Value range: RSA, ECDSA.

- Key Strength: Optional. Value range: 2048, 4096

- Private Key Password: Password for the private key, which is optional.

  

3. Click **Generate**. The following prompt will pop up when the CSR has been successfully created.

  ![](https://main.qcloudimg.com/raw/fbb31bf7f27dd43fabdf068a83626eb0.png)


4. Click **Confirm** to view the **CSR File** and **Key File**.

  ![](https://main.qcloudimg.com/raw/736f32c5a82054eacfd38a8f4ade1630.png)

### Manage a CSR

You can view, delete, or perform other operations on a CSR in [CSR Management](https://console.cloud.tencent.com/ssl/csr)

1. Click **Details** to view the CSR information.

  ![](https://main.qcloudimg.com/raw/c610af2047986324ad253b3a4aa74341.png)

  ![](https://main.qcloudimg.com/raw/8acf71eadbbc1e193a1564e0ef88e4c9.png)

2. Select a CSR and click **Delete** to delete it.

  ![](https://main.qcloudimg.com/raw/9b0abe34bc84aa00733cadda5b20b5e7.png)

3. Add remarks to a CSR to distinguish the CSRs used for different projects.

  ![](https://main.qcloudimg.com/raw/2469175d5285e8cfbb1dd2a11751b9ba.png)

  
