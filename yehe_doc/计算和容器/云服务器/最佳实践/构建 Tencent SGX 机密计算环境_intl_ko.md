## 작업 시나리오
본문은 M6ce 인스턴스에서 Tencent SGX 보안 컴퓨팅 환경을 구축하는 방법을 소개하고, intel SGXSDK를 사용하여 SGX 기능을 인증하는 방법을 안내합니다.


## 전제 조건
[M6ce 인스턴스](https://intl.cloud.tencent.com/document/product/213/11518)를 생성 및 로그인 완료해야 합니다.
 - 인스턴스 생성 방법은 [구매 페이지를 통한 인스턴스 생성](https://intl.cloud.tencent.com/document/product/213/4855)을 참고하십시오.
 - 인스턴스에 로그인하는 방법은 [Linux 인스턴스에 로그인](https://intl.cloud.tencent.com/document/product/213/5436)을 참고하십시오.


<dx-alert infotype="explain" title="">
본문은 TencentOS Server 3.1(TK4) 운영 체제의 인스턴스를 예시로 사용합니다. 운영 체제 버전에 따라 과정이 다르므로 실제 상황에 맞게 작업하십시오.
</dx-alert>



## 작업 단계
1. 다음 명령어를 실행하여 kernel 버전을 확인합니다.
```
uname -a
```
kernel 버전이 5.4.119-19.0008보다 낮은지 확인합니다.
 - 낮다면 다음 명령어를 실행하여 kernel을 업데이트합니다.
```
yum update kernel
```   
 - 낮지 않다면 다음 단계를 진행합니다.
2. 다음 명령어를 실행하여 SGX runtime에 필요한 소프트웨어 패키지를 설치합니다.
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
SGX AESM 서비스의 기본 설치 디렉터리는 `/opt/intel/sgx-aesm-service`입니다.
</dx-alert>
3. 다음 명령어를 실행하여 intel SGXSDK를 설치합니다.
```
yum install sgx-linux-x64-sdk
```
<dx-alert infotype="explain" title="">
Intel SGXSDK의 기본 설치 디렉터리는 /`opt/intel/sgxsdk`입니다. [intel SGXSDK](https://download.01.org/intel-sgx/sgx-linux/2.13/docs/Intel_SGX_Developer_Reference_Linux_2.13_Open_Source.pdf?spm=a2c4g.11186623.0.0.2f8d31b8PMoC1w&file=Intel_SGX_Developer_Reference_Linux_2.13_Open_Source.pdf) 사용자 매뉴얼을 참고하여 SGX 프로그램을 개발할 수 있습니다.
</dx-alert>
4. SGX runtime 및 intel SGXSDK가 설치된 후 인스턴스를 재시작합니다. 자세한 내용은 [인스턴스 재시작](https://intl.cloud.tencent.com/document/product/213/4928)을 참고하십시오.
5. Tencent Cloud SGX 원격 증명 서비스를 설정합니다.
Tencent Cloud SGX 원격 증명 서비스는 리전별 배치가 적용됩니다. SGX CVM인스턴스가 위치한 리전에서 Tencent Cloud SGX 원격 증명 서비스에 접속하여 최상의 경험을 얻을 수 있습니다. intel SGXSDK를 설치한 후 원격 증명 서비스의 기본 구성 파일 `/etc/sgx_default_qcnl.conf`가 자동으로 생성됩니다. SGX CVM 인스턴스가 위치한 리전의 Tencent Cloud SGX 원격 증명 서비스에 맞게 파일을 수동으로 수정하려면 아래 단계를 따르십시오.
<dx-alert infotype="explain" title="">
- 현재 베이징, 상하이, 광저우 리전만 Tencent Cloud SGX 원격 증명 서비스를 지원합니다.
- Intel Ice Lake는 Intel EPID 원격 증명 방식이 아닌 Intel SGX DCAP 기반 원격 증명 방식만 지원합니다.
</dx-alert>
VIM 편집기를 사용하여 `/etc/sgx_default_qcnl.conf`를 다음 내용으로 수정합니다.
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.[Region-ID].tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```
`[Region-ID]`를 SGX CVM 인스턴스가 위치한 리전의 ID로 바꾸십시오. 예시: <br>
 베이징 리전 수정 예시는 다음과 같습니다.
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.bj.tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```
상하이 리전 수정 예시는 다음과 같습니다.
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.sh.tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```
광저우 리전 수정 예시는 다음과 같습니다.
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.gz.tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```

## SGX 기능 인증 예시

### 예시1: Enclave 실행
Intel SGXSDK는 SGX 기능을 인증하기 위한 SGX 샘플 코드를 제공합니다. 기본 디렉터리는 `/opt/intel/sgxsdk/SampleCode`입니다. 이 예시에서 코드(SampleEnclave)의 효과는 설치된 SGXSDK의 정상 사용 여부와 SGX CVM 인스턴스의 보안 메모리 리소스 사용 가능 여부를 확인하기 위해 Enclave를 실행하는 것입니다.
1. 다음 명령어를 실행하여 intel SGXSDK와 관련된 환경 변수를 설정합니다.
```
source /opt/intel/sgxsdk/environment
```
2. 다음 명령어를 실행하여 샘플 코드 SampleEnclave를 컴파일합니다.
```
cd /opt/intel/sgxsdk/SampleCode/SampleEnclave && make
```
3. 다음 명령어를 실행하여 컴파일된 실행 파일을 실행합니다.
```
./app
```
아래 이미지와 같은 결과가 반환되면 실행이 완료된 것입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ae6cf48bfae18e245cb9c22fe85c5c63.png)



### 예시2: SGX 원격 증명
Intel sgx의 code tree는 SGX 원격 증명 기능(DCAP)을 인증하기 위한 샘플 코드를 제공합니다. 이 예시는 Quote 생성 및 인증을 위한 것으로, Quote 생성(QuoteGenerationSample) 및 Quote 인증(QuoteVerificationSample)을 포함합니다.
1. 다음 명령어를 실행하여 intel SGXSDK 관련 환경 변수를 설정합니다.
```
source /opt/intel/sgxsdk/environment
```
2. 다음 명령어를 순서대로 실행하여 git을 설치하고 intel sgx DCAP code tree를 다운로드합니다.
```
cd /root && yum install git
```
```
git clone https://github.com/intel/SGXDataCenterAttestationPrimitives.git
```
3. 다음 명령어를 순서대로 실행하여 Quote 생성의 QuoteGenerationSample 샘플 코드를 컴파일하고 실행합니다.
    1. QuoteGenerationSample 디렉터리를 입력합니다. 
```
cd /root/SGXDataCenterAttestationPrimitives/SampleCode/QuoteGenerationSample
```
    2. QuoteGenerationSample을 컴파일합니다.
```
make
```
    3. QuoteGenerationSample을 실행하고 Quote를 생성합니다.
```
./app
```
4. 다음 명령어를 실행하여 Quote 인증의 QuoteVerificationSample 샘플 코드를 컴파일합니다.
```
cd /root/SGXDataCenterAttestationPrimitives/SampleCode/QuoteVerificationSample && make
```
5. 다음 명령어를 실행하여 QuoteVerificationSample Enclave에 서명을 진행합니다.
```
sgx_sign sign -key Enclave/Enclave_private_sample.pem -enclave enclave.so -out enclave.signed.so -config Enclave/Enclave.config.xml
```
6. 다음 명령어를 통해 QuoteVerificationSample을 실행하여 Quote를 확인합니다.
```
./app
```
아래 이미지와 같은 결과가 반환되면 인증이 완료된 것입니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e32430adce18aa76303d9cd73ac9ff2f.png)
