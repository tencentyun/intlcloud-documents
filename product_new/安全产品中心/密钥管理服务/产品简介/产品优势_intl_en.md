## Security and Compliance
KMS leverages the FIPS-140-2 certified hardware security module (HSM) to generate and protect keys. The security and quality control practices adopted by KMS are accredited by multiple compliance schemes. The creation, management, and other operations of your master keys are performed in the compliant HSM, and no one (including Tencent Cloud) will be able to obtain your plaintext master keys.

## High Availability
At the service architecture level, the reliability of KMS is guaranteed through a single-region multi-data center deployment. The HSM used in the underlying system is also deployed in a clustered manner across data centers with cold backup enabled to ensure high availability of the service. At the access level, KMS can be accessed through TencentCloud API 3.0 deployed in different regions with both unified and region-specific access domain names provided to ensure high accessibility.

## Centralized Key Management
KMS can be called and integrated through APIs, SDKs, and connected Tencent Cloud products to centrally manage the key policies of your business applications in and outside Tencent Cloud.

## Low Cost
Pay-as-you-go KMS can be deployed quickly at the click of a button. Tencent Cloud covers all backend maintenance, eliminating your need to purchase any dedicated hardware encryption devices.
