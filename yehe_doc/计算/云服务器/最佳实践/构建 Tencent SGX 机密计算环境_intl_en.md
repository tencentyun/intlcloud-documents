## Overview
This document describes how to build a Tencent SGX confidential computing environment in an M6ce instance and use the Intel SGX SDK to verify SGX features.


## Prerequisites
You have created and logged in to an [M6ce instance](https://intl.cloud.tencent.com/document/product/213/11518).
 - For detailed directions on how to create an instance, see [Creating Instances via CVM Purchase Page](https://intl.cloud.tencent.com/document/product/213/4855).
 - For detailed directions on how to log in to an instance, see [Logging in to Linux Instance Using Standard Login Method](https://intl.cloud.tencent.com/document/product/213/5436).


<dx-alert infotype="explain" title="">
This document uses an instance on the TencentOS Server 3.1 (TK4) as an example. 
</dx-alert>



## Directions
1. Run the following command to check the kernel version.
```
uname -a
```
Check whether the kernel version is earlier than 5.4.119-19.0008.
 - If yes, run the following command to update the kernel:
```
yum update kernel
```   
 - If no, proceed to the next step.
2. Run the following command to install the software packages required by the SGX runtime:
```
yum install \
    libsgx-ae-le libsgx-ae-pce libsgx-ae-qe3 libsgx-ae-qve \
    libsgx-aesm-ecdsa-plugin libsgx-aesm-launch-plugin libsgx-aesm-pce-plugin libsgx-aesm-quote-ex-plugin \
    libsgx-dcap-default-qpl libsgx-dcap-default-qpl-devel libsgx-dcap-ql libsgx-dcap-ql-devel \
    libsgx-dcap-quote-verify libsgx-dcap-quote-verify-devel libsgx-enclave-common libsgx-enclave-common-devel libsgx-epid-devel \
    libsgx-launch libsgx-launch-devel libsgx-pce-logic libsgx-qe3-logic libsgx-quote-ex libsgx-quote-ex-devel \
    libsgx-ra-network libsgx-ra-uefi libsgx-uae-service libsgx-urts sgx-ra-service \
sgx-aesm-service
``` <dx-alert infotype="explain" title="">
The default installation directory of the SGX AESM service is `/opt/intel/sgx-aesm-service`.
</dx-alert>
3. Run the following command to install the Intel SGX SDK:
```
yum install sgx-linux-x64-sdk
```
<dx-alert infotype="explain" title="">
The default installation directory of the Intel SGX SDK is `/opt/intel/sgxsdk`. You can develop an SGX program as instructed in [Intel® Software Guard Extensions (Intel® SGX) SDK for Linux OS Developer Reference](https://download.01.org/intel-sgx/sgx-linux/2.13/docs/Intel_SGX_Developer_Reference_Linux_2.13_Open_Source.pdf?spm=a2c4g.11186623.0.0.2f8d31b8PMoC1w&file=Intel_SGX_Developer_Reference_Linux_2.13_Open_Source.pdf).
</dx-alert>

4. After installing the SGX runtime and Intel SGX SDK, restart the instance as instructed in [Restarting Instances](https://intl.cloud.tencent.com/document/product/213/4928) .

5. Configure the Tencent Cloud SGX remote attestation service.
The Tencent Cloud SGX remote attestation service is deployed at the regional level. You can access the service in the region where your SGX CVM instance resides to get the optimal experience. After you install the Intel SGX SDK, the default configuration file `/etc/sgx_default_qcnl.conf` of the service will be generated automatically. Manually modify the file in the following steps to adapt to the service in the region of your SGX CVM instance.
<dx-alert infotype="explain" title="">
- Currently, the SGX remote attestation service is available only in the Beijing, Shanghai, and Guangzhou regions.
- Intel Ice Lake supports only the remote attestation method based on Intel SGX DCAP rather than Intel EPID.
</dx-alert>

Use the Vim editor to modify `/etc/sgx_default_qcnl.conf` as follows:
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.[Region-ID].tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```
Replace `[Region-ID]` with the ID of the region where your SGX CVM instance resides; for example: <br>
 Sample configuration for the Beijing region:
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.bj.tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```
Sample configuration for the Shanghai region:
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.sh.tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```
Sample configuration for the Guangzhou region:
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.gz.tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```

## Examples of SGX Feature Verification

### Example 1. Start an enclave
The Intel SGX SDK provides sample SGX code for verifying SGX features in the default directory of `/opt/intel/sgxsdk/SampleCode`. The effect of this sample code (`SampleEnclave`) is to start an enclave to check whether the installed SGX SDK works normally and whether the confidential memory resource of your SGX CVM instance is available.
1. Run the following command to set the relevant environment variables of the Intel SGX SDK:
```
source /opt/intel/sgxsdk/environment
```
2. Run the following command to compile the sample code `SampleEnclave`:
```
cd /opt/intel/sgxsdk/SampleCode/SampleEnclave && make
```
3. Run the following command to run the complied executable file:
```
./app
```
If a result in the following figure is returned, the enclave is started.
![](https://qcloudimg.tencent-cloud.cn/raw/ae6cf48bfae18e245cb9c22fe85c5c63.png)



### Example 2. Perform remote SGX verification
The code tree of Intel SGX provides sample code to verify the SGX remote attestation feature, i.e., DCAP. This example is to generate and verify a quote and involves the quote generator (`QuoteGenerationSample`) and verifier (`QuoteVerificationSample`).
1. Run the following command to set the relevant environment variables of the Intel SGX SDK:
```
source /opt/intel/sgxsdk/environment
```
2. Run the following commands in sequence to install Git and download the Intel SGX DCAP code tree:
```
cd /root && yum install git
```
```
git clone https://github.com/intel/SGXDataCenterAttestationPrimitives.git
```
3. Run the following commands in sequence to compile and run the sample code of the quote generator `QuoteGenerationSample`:
    1. Enter the `QuoteGenerationSample` directory: 
```
cd /root/SGXDataCenterAttestationPrimitives/SampleCode/QuoteGenerationSample
```
    2. Compile `QuoteGenerationSample`:
```
make
```
    3. Run `QuoteGenerationSample` to generate a quote:
```
./app
```
4. Run the following command to compile the sample code of the quote verifier `QuoteVerificationSample`:
```
cd /root/SGXDataCenterAttestationPrimitives/SampleCode/QuoteVerificationSample && make
```
5. Run the following command to sign the `QuoteVerificationSample` enclave:
```
sgx_sign sign -key Enclave/Enclave_private_sample.pem -enclave enclave.so -out enclave.signed.so -config Enclave/Enclave.config.xml
```
6. Run the following command to run `QuoteVerificationSample ` to verify the quote:
```
./app
```
If a result in the following figure is returned, the verification succeeds.
![](https://qcloudimg.tencent-cloud.cn/raw/e32430adce18aa76303d9cd73ac9ff2f.png)
