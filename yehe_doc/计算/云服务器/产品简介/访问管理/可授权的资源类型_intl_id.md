Izin tingkat sumber daya mengacu pada kemampuan untuk menentukan sumber daya mana yang diizinkan untuk dioperasikan pengguna. Cloud Virtual Machine (CVM) memiliki dukungan parsial untuk izin tingkat sumber daya. Ini berarti bahwa untuk CVM tertentu, Anda dapat mengontrol kapan pengguna diizinkan untuk mengoperasikannya, dan sumber daya spesifik apa yang boleh digunakan oleh pengguna. Misalnya, Anda [mengizinkan pengguna untuk melakukan operasi pada CVM tertentu di Guangzhou](https://intl.cloud.tencent.com/document/product/213/10312).
Jenis sumber daya yang dapat diotorisasi di Cloud Access Management (CAM) adalah sebagai berikut:

| Jenis Sumber Daya | Metode Deskripsi Sumber Daya dalam Kebijakan Otorisasi |
| :-------- | -------------- |
| [Instans CVM](#CVMCorrelation) |  ` qcs::cvm:$region::instance/* `|
| [Kunci CVM](#KeyCorrelation) |   `qcs::cvm:$region::keypair/*`  |
| [Citra CVM](#ImageCorrelation) |   `qcs::cvm:$region:$account:image/*` |

[Instans CVM](#CVMCorelation), [Kunci CVM](#KeyCorelation) dan [Citra CVM](#ImageCorelation) memperkenalkan operasi CVM API yang saat ini mendukung izin tingkat sumber daya, serta sumber daya dan kunci kondisi yang didukung oleh operasi CVM API ini. **Saat mengonfigurasi jalur sumber daya,** Anda perlu mengubah parameter variabel seperti `$ region`, ` $ account` menjadi informasi parameter aktual Anda. Anda juga dapat menggunakan karakter pengganti \* di jalur. Untuk informasi selengkapnya, lihat [Contoh Operasi](https://intl.cloud.tencent.com/document/product/213/10312).
> Operasi CVM API yang tidak tercantum dalam tabel tidak mendukung izin tingkat sumber daya. Anda masih dapat mengotorisasi pengguna untuk melakukan operasi ini, tetapi Anda harus menetapkan \* sebagai elemen sumber daya dalam pernyataan kebijakan.
>

<span id="CVMCorrelation"></span>
#### Instans CVM

| Operasi API | Jalur Sumber Daya | Kunci Kondisi |
| :-------- | :--------| :------ |
|DescribeInstanceInternetBandwidthConfigs	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstanceInternetChargeType	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ModifyInstancesAttribute](https://intl.cloud.tencent.com/document/product/213/33246)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`  | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ModifyInstancesProject](https://intl.cloud.tencent.com/document/product/213/33245)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|ModifyInstancesRenewFlag	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[RebootInstances](https://intl.cloud.tencent.com/document/product/213/33243)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|RenewInstances	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstance](https://intl.cloud.tencent.com/document/product/213/33242)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs::cvm:$region:$account:systemdisk/*` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesInternetMaxBandwidth](https://intl.cloud.tencent.com/document/product/213/33241)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesPassword](https://intl.cloud.tencent.com/document/product/213/33240)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResetInstancesType](https://intl.cloud.tencent.com/document/product/213/33239)	|  `qcs::cvm:$region:$account:instance/* `<br>`qcs::cvm:$region:$account:instance/$instanceId`| cvm:region<br>cvm:zone<br>cvm:instance_type|
|[ResizeInstanceDisks](https://intl.cloud.tencent.com/document/product/213/33238)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[RunInstances](https://intl.cloud.tencent.com/document/product/213/33237)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`<br>`qcs::cvm:$region:$account:sg/*`<br>`qcs::cvm:$region:$account:sg/$sgId`<br>`qcs::vpc:$region:$account:subnet/* `<br>`qcs::vpc:$region:$account:subnet/$subnetId`<br>`qcs::cvm:$region:$account:systemdisk/*`<br>`qcs::cvm:$region:$account:datadisk/*`<br>`qcs::vpc:$region:$account:vpc/* `<br>`qcs::vpc:$region:$account:vpc/$vpcId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[StartInstances](https://intl.cloud.tencent.com/document/product/213/33236)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[StopInstances](https://intl.cloud.tencent.com/document/product/213/33235)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|
|[TerminateInstances](https://intl.cloud.tencent.com/document/product/213/33234)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId` | cvm:region<br>cvm:zone<br>cvm:instance_type|


<span id="KeyCorrelation"></span>
#### Kunci CVM

| Operasi API | Jalur Sumber Daya | Kunci Kondisi |
| :-------- | :--------| :------ |
|[AssociateInstancesKeyPairs](https://intl.cloud.tencent.com/document/product/213/33232)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId`  | -|
|[CreateKeyPair](https://intl.cloud.tencent.com/document/product/213/33231)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|[DeleteKeyPairs](https://intl.cloud.tencent.com/document/product/213/33230)	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|[DescribeKeyPairs](https://intl.cloud.tencent.com/document/product/213/33229)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|DescribeKeyPairsAttribute	|  `qcs::cvm:$region:$account:keypair/*`<br>` qcs::cvm:$region:$account:keypair/$keyId` | -|
| [DisassociateInstancesKeyPairs](https://intl.cloud.tencent.com/document/product/213/33228)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br>`qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|
|[ImportKeyPair](https://intl.cloud.tencent.com/document/product/213/33227)	|  `qcs::cvm:$region:$account:keypair/*` | -|
|[ModifyKeyPairAttribute](https://intl.cloud.tencent.com/document/product/213/33226)	|  `qcs::cvm:$region:$account:keypair/*`<br>`qcs::cvm:$region:$account:keypair/$keyId` | -|

<span id="ImageCorrelation"></span>
#### Citra CVM

| Operasi API | Jalur Sumber Daya | Kunci Kondisi |
| :-------- | :--------| :------ |
| [CreateImage](https://intl.cloud.tencent.com/document/product/213/33276)	|  `qcs::cvm:$region:$account:instance/*`<br>`qcs::cvm:$region:$account:instance/$instanceId`<br> `qcs::cvm:$region:$account:image/*` | cvm:region |
| [DeleteImages](https://intl.cloud.tencent.com/document/product/213/33275)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
|[DescribeImages](https://intl.cloud.tencent.com/document/product/213/33272)| `qcs::cvm:$region:$account:image/*`|cvm:region|
| DescribeImagesAttribute|  `qcs::cvm:$region:$account:image/*`<br>` qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [DescribeImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33273)	|  `qcs::cvm:$region:$account:image/*` | cvm:region |
| [ModifyImageAttribute](https://intl.cloud.tencent.com/document/product/213/33269)|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [ModifyImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33268)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |
| [SyncImages](https://intl.cloud.tencent.com/document/product/213/33267)	|  `qcs::cvm:$region:$account:image/*`<br>`qcs::cvm:$region:$account:image/$imageId` | cvm:region |







