## 概要
ここでは、M6ceインスタンスでTencent SGXコンフィデンシャル・コンピューティング環境を構築する方法と、Intel SGXSDKを使用してSGX機能を検証する方法をデモンストレーションします。


##  前提条件
[M6ceインスタンス](https://intl.cloud.tencent.com/document/product/213/11518)が作成され、ログインしていること。
 -インスタンスの作成方法については、[購入画面でインスタンスを作成](https://intl.cloud.tencent.com/document/product/213/4855)をご参照ください。
 -インスタンスのログイン方法については、[標準ログイン方式を使用してLinuxインスタンスにログイン（推奨）](https://intl.cloud.tencent.com/document/product/213/5436)をご参照ください。


<dx-alert infotype="explain" title="">
ここでの手順は、OSがTencentOS Server 3.1(TK4)のインスタンスを使用した例であり、OSのバージョンが異なると手順も異なる場合がありますので、実際の状況に応じて操作してください。
</dx-alert>



## 操作手順
1. 次のコマンドを実行して、kernelバージョンをチェックします。
```
uname -a
```
kernelが5.4.119-19.0008より低いバージョンかどうかを確認します。
 - 「はい」の場合は、次のコマンドを実行して、kernelを更新してください。
```
yum update kernel
```   
 - 「いいえ」の場合は、次の手順に進んでください。
2. 次のコマンドを実行して、SGX runtimeに必要なパッケージをインストールします。
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
SGX AESMサービスのデフォルトのインストールディレクトリは、`/opt/intel/sgx-aesm-service`です。
</dx-alert>
3. 次のコマンドを実行して、Intel SGXSDKをインストールします。
```
yum install sgx-linux-x64-sdk
```
<dx-alert infotype="explain" title="">
Intel SGXSDKのデフォルトのインストールディレクトリは、/`opt/intel/sgxsdk`です。[Intel SGXSDK](https://download.01.org/intel-sgx/sgx-linux/2.13/docs/Intel_SGX_Developer_Reference_Linux_2.13_Open_Source.pdf?spm=a2c4g.11186623.0.0.2f8d31b8PMoC1w&file=Intel_SGX_Developer_Reference_Linux_2.13_Open_Source.pdf)ユーザーマニュアルを参照して、SGXプログラムを開発することができます。
</dx-alert>
4. SGX runtimeとIntel SGXSDKのインストールが完了したら、インスタンスを再起動してください。詳細については、[インスタンスの再起動](https://intl.cloud.tencent.com/document/product/213/4928)をご参照ください。
5. Tencent Cloud SGXリモートアテステーションサービスを構成します。
Tencent Cloud SGXリモートアテステーションサービスは、リージョン化デプロイを採用しています。SGX CVMインスタンスが配置されているリージョンでTencent Cloud SGXリモートアテステーションサービスにアクセスすれば、最高のカスタマーエクスペリエンスを体験できます。Intel SGXSDKをインストールすると、リモートアテステーションサービスのデフォルト構成ファイル`/etc/sgx_default_qcnl.conf`が自動的に生成されます。SGX CVMインスタンスが配置されているリージョンのTencent Cloud SGXリモートアテステーションサービスに適応するように、以下の手順に従ってこのファイルを手動で変更してください。
<dx-alert infotype="explain" title="">
- 現在、北京、上海および広州リージョンのみで、Tencent Cloud SGXリモートアテステーションサービスがサポートされています。
- Intel Ice Lakeは、Intel SGX DCAPベースのリモートアテステーション方式のみをサポートし、Intel EPIDリモートアテステーション方式はサポートしていません。
</dx-alert>
VIMエディタを使用して、`/etc/sgx_default_qcnl.conf`を以下のように変更します。
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.[Region-ID].tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```
`[Region-ID]`をSGX CVMインスタンスが配置されているリージョンのIDに置き換えてください。 例：<br>
 北京リージョンの変更例は次のとおりです。
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.bj.tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```
上海リージョンの変更例は次のとおりです。
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.sh.tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```
広州リージョンの変更例は次のとおりです。
```
# PCCS server address
PCCS_URL=https://sgx-dcap-server-tc.gz.tencent.cn/sgx/certification/v3/
# To accept insecure HTTPS cert, set this option to FALSE
USE_SECURE_CERT=TRUE
```

## SGX機能の検証例

### 例1：Enclaveの起動
Intel SGXSDKは、SGX機能を検証するためのSGXサンプルコードを提供します。デフォルトのディレクトリは、`/opt/intel/sgxsdk/SampleCode`です。この例のコード(SampleEnclave)の効果は、Enclaveを起動して、インストールされたSGXSDKが正常に使用されているか、また、SGX CVMインスタンスの機密メモリリソースが使用可能かどうかを検証することです。
1. 次のコマンドを実行して、Intel SGXSDKに関連する環境変数を設定します。
```
source /opt/intel/sgxsdk/environment
```
2. 次のコマンドを実行して、サンプルコードSampleEnclaveをコンパイルします。
```
cd /opt/intel/sgxsdk/SampleCode/SampleEnclave && make
```
3. 次のコマンドを実行して、コンパイルされた実行可能ファイルを実行します。
```
./app
```
以下のような結果が返されれば、起動に成功しています。
![](https://qcloudimg.tencent-cloud.cn/raw/ae6cf48bfae18e245cb9c22fe85c5c63.png)



### 例2：SGXリモートアテステーション
Intel SGXのcode treeは、SGXリモートアテステーション機能(DCAP)を検証するためのサンプルコードを提供します。この例は、Quoteを発行および検証するためのもので、Quote Generator(QuoteGenerationSample)とQuote Verifier(QuoteVerificationSample)が含まれます。
1. 次のコマンドを実行して、Intel SGXSDKに関連する環境変数を設定します。
```
source /opt/intel/sgxsdk/environment
```
2. 次のコマンドを順に実行してgitをインストールし、Intel SGX DCAP code treeをダウンロードします。
```
cd /root && yum install git
```
```
git clone https://github.com/intel/SGXDataCenterAttestationPrimitives.git
```
3. 次のコマンドを順に実行して、Quote GeneratorのサンプルコードQuoteGenerationSampleをコンパイルして実行します。
    1. QuoteGenerationSampleディレクトリに入ります。 
```
cd /root/SGXDataCenterAttestationPrimitives/SampleCode/QuoteGenerationSample
```
    2. QuoteGenerationSampleをコンパイルします。
```
make
```
    3. QuoteGenerationSampleを実行し、Quoteを発行します。
```
./app
```
4. 次のコマンドを実行して、QuoteVerifierのサンプルコードQuoteVerificationSampleをコンパイルします。
```
cd /root/SGXDataCenterAttestationPrimitives/SampleCode/QuoteVerificationSample && make
```
5. 次のコマンドを実行して、QuoteVerificationSample Enclaveに署名します。
```
sgx_sign sign -key Enclave/Enclave_private_sample.pem -enclave enclave.so -out enclave.signed.so -config Enclave/Enclave.config.xml
```
6. 次のコマンドを実行して、QuoteVerificationSampleを実行し、Quoteを検証します。
```
./app
```
以下のような結果が返されれば、検証に成功しています。
![](https://qcloudimg.tencent-cloud.cn/raw/e32430adce18aa76303d9cd73ac9ff2f.png)
