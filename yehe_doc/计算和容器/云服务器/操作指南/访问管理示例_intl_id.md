## Pengantar

Anda dapat menggunakan kebijakan Cloud Access Management (CAM) untuk mengelola akses pengguna ke sumber daya menggunakan konsol Cloud Virtual Machine (CVM). Dokumen ini menyediakan contoh untuk membantu Anda memahami cara menggunakan kebijakan CAM yang telah ditentukan sebelumnya menggunakan konsol CVM.

## Contoh
### Pembacaan dan penulisan (CVM)
Jika Anda ingin mengizinkan pengguna membuat dan mengelola instans CVM, kaitkan pengguna dengan kebijakan bernama QcloudCVMFullAccess. Kebijakan ini dirancang untuk memberikan izin kepada pengguna untuk mengakses semua sumber daya di CVM, Virtual Private Cloud (VPC), Cloud Load Balancer (CLB), dan Cloud Monitor.
Langkah-langkah detailnya adalah sebagai berikut:
Lihat [Pengelolaan Otorisasi](https://intl.cloud.tencent.com/document/product/598/10602) untuk petunjuk tentang cara memberikan kebijakan prasetel QcloudCVMFullAccess kepada pengguna.

### Hanya baca (CVM)
Jika Anda ingin mengizinkan pengguna untuk hanya membuat kueri, tetapi tidak membuat, menghapus, atau memulai/mematikan instans CVM, kaitkan pengguna dengan kebijakan bernama QcloudCVMInnerReadOnlyAccess. Kebijakan ini dirancang untuk memberikan izin kepada pengguna untuk melakukan semua operasi yang dimulai dengan "Describe" (Jelaskan) dan "Inquiry" (Pertanyaan) di CVM. Langkah-langkah detailnya adalah sebagai berikut:
Lihat [Pengelolaan Otorisasi](https://intl.cloud.tencent.com/document/product/598/10602) untuk petunjuk tentang cara memberikan kebijakan prasetel QcloudCVMInnerReadOnlyAccess kepada pengguna.

### Hanya baca (CVM dan sumber daya terkait)
Jika Anda ingin mengizinkan pengguna untuk hanya membuat kueri, tetapi tidak membuat, menghapus, atau memulai/mematikan instans CVM dan sumber daya terkait (VPC dan CLB), kaitkan pengguna dengan kebijakan bernama QcloudCVMReadOnlyAccess. Kebijakan ini dirancang untuk memberikan izin kepada pengguna untuk melakukan operasi berikut:
- Semua operasi dimulai dengan "Describe" (Jelaskan) dan "Inquiry" (Pertanyaan) di CVM.
- Semua operasi dimulai dengan "Describe" (Jelaskan), "Inquiry" (Pertanyaan), dan "Get" (Dapatkan) di VPC.
- Semua operasi dimulai dengan "Describe" (Jelaskan) di CLB.
- Semua operasi di Monitor.

Langkah-langkah detailnya adalah sebagai berikut:
Lihat [Pengelolaan Otorisasi](https://intl.cloud.tencent.com/document/product/598/10602) untuk petunjuk tentang cara memberikan kebijakan prasetel QcloudCVMReadOnlyAccess kepada pengguna.

### Kebijakan CBS

Jika Anda ingin mengizinkan pengguna untuk melihat, membuat, dan menggunakan disk cloud di konsol CVM, tambahkan operasi berikut ke kebijakan Anda dan kaitkan kebijakan dengan pengguna.
- **CreateCbsStorages:** (CreateCbsStorages:) membuat disk cloud.
- **AttachCbsStorages:** (AttachCbsStorages:) pasang disk cloud yang ditentukan ke CVM yang ditentukan.
- **DetachCbsStorages:** (DetachCbsStorages:) lepaskan disk cloud yang ditentukan.
- **ModifyCbsStorageAttributes:** (ModifyCbsStorageAttributes:) mengubah nama atau ID proyek dari disk cloud yang ditentukan.
- **DescribeCbsStorages:** (DescribeCbsStorages:) menanyakan detail disk cloud.
- **DescribeInstancesCbsNum:** (DescribeInstancesCbsNum:) menanyakan jumlah disk cloud yang dipasang dari CVM dan jumlah maksimum disk cloud yang diizinkan untuk dipasang ke CVM.
- **RenewCbsStorage:** (RenewCbsStorage:) memperbarui disk cloud yang ditentukan.
- **ResizeCbsStorage:** (ResizeCbsStorage:) mengubah ukuran disk cloud yang ditentukan.

Langkah-langkah detailnya adalah sebagai berikut:
1. Lihat [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601) untuk informasi dan buat kebijakan khusus yang memberikan izin untuk melihat informasi disk cloud di konsol CVM dan untuk membuat dan menggunakan disk cloud.
Gunakan berikut ini sebagai referensi sintaksis:
```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "name/cvm:CreateCbsStorages",
                "name/cvm:AttachCbsStorages",
                "name/cvm:DetachCbsStorages",
                "name/cvm:ModifyCbsStorageAttributes",
                "name/cvm:DescribeCbsStorages"
            ],
            "resource": [
                "qcs::cvm::uin/1410643447:*"
            ]
        }
    ]
}
```
2. Temukan kebijakan yang dibuat, dan di kolom “Action” (Tindakan) pada baris tersebut, klik **Associate User/Group** (Kaitkan Pengguna/Grup).
3. Di jendela “Associate User/Group” (Kaitkan Pengguna/Grup), pilih pengguna/grup yang ingin Anda kaitkan, dan klik **OK** (OKE).


### Kebijakan grup keamanan

Untuk mengizinkan pengguna melihat dan menggunakan grup keamanan di konsol CVM, tambahkan operasi berikut ke kebijakan Anda, dan kaitkan kebijakan dengan pengguna.
- **DeleteSecurityGroup:** (DeleteSecurityGroup:) menghapus grup keamanan.
- **ModifySecurityGroupPolicys:** (ModifySecurityGroupPolicys:) mengganti semua kebijakan grup keamanan.
- **ModifySingleSecurityGroupPolicy:** (ModifySingleSecurityGroupPolicy:) mengubah satu kebijakan grup keamanan.
- **CreateSecurityGroupPolicy:** (CreateSecurityGroupPolicy:) membuat kebijakan grup keamanan.
- **DeleteSecurityGroupPolicy:** (DeleteSecurityGroupPolicy:) menghapus kebijakan grup keamanan.
- **ModifySecurityGroupAttributes:** (ModifySecurityGroupAttributes:) mengubah atribut grup keamanan.

Langkah-langkah detailnya adalah sebagai berikut:
1. Lihat [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601) untuk mengetahui informasi dan buat kebijakan khusus yang memberikan izin untuk membuat, menghapus, dan mengubah grup keamanan di konsol CVM.
Gunakan berikut ini sebagai referensi sintaksis:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:ModifySecurityGroupPolicys",
                "name/cvm:ModifySingleSecurityGroupPolicy",
                "name/cvm:CreateSecurityGroupPolicy",
                "name/cvm:DeleteSecurityGroupPolicy"
            ],
            "resource": "*",
            “effect": "allow"
        }
    ]
}
```
2. Temukan kebijakan yang dibuat, dan di kolom “Action” (Tindakan) pada baris tersebut, klik **Associate User/Group** (Kaitkan Pengguna/Grup).
3. Di jendela “Associate User/Group” (Kaitkan Pengguna/Grup), pilih pengguna/grup yang ingin Anda otorisasi, dan klik **OK** (OKE).


### Kebijakan untuk EIP

Jika Anda ingin mengizinkan pengguna untuk melihat dan menggunakan EIP di konsol CVM, tambahkan operasi berikut ke kebijakan Anda, dan kaitkan kebijakan dengan pengguna.
- **AllocateAddresses:** (AllocateAddresses:) menetapkan EIP ke instans VPC atau CVM.
- **AssociateAddress:** (AssociateAddress:) mengaitkan EIP dengan instans atau antarmuka jaringan.
- **DescribeAddresses:** (DescribeAddresses:) melihat EIP di konsol CVM.
- **DisassociateAddress:** (DisassociateAddress:) memisahkan EIP dari instans atau antarmuka jaringan.
- **ModifyAddressAttribute:** (ModifyAddressAttribute) mengubah atribut EIP.
- **ReleaseAddresses:** (ReleaseAddresses:) merilis EIP.

Langkah-langkah detailnya adalah sebagai berikut:
1. Lihat [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601) untuk mengetahui informasi dan buat kebijakan kustom.
Kebijakan ini memungkinkan pengguna untuk melihat EIP dan menetapkannya serta mengaitkannya dengan instans di konsol CVM. Pengguna tidak dapat mengubah atribut EIP, memisahkannya dari instans, atau melepaskan EIP. Gunakan berikut ini sebagai referensi sintaksis:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:DescribeAddresses",
                "name/cvm:AllocateAddresses",
                "name/cvm:AssociateAddress"
            ],
            "resource": "*",
            “effect": "allow"
        }
    ]
}
```
2. Temukan kebijakan yang dibuat, dan di kolom “Action” (Tindakan) pada baris tersebut, klik **Associate User/Group** (Kaitkan Pengguna/Grup).
3. Di jendela “Associate User/Group” (Kaitkan Pengguna/Grup), pilih pengguna/grup yang ingin Anda otorisasi, dan klik **OK** (OKE).

### Kebijakan untuk mengizinkan pengguna melakukan operasi pada CVM tertentu
Jika Anda ingin mengotorisasi pengguna untuk melakukan operasi pada CVM tertentu, kaitkan kebijakan berikut dengan pengguna. Langkah-langkah detailnya adalah sebagai berikut:
1. Lihat [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601) untuk mengetahui informasi dan buat kebijakan kustom.
Kebijakan ini mengizinkan pengguna untuk mengoperasikan instans CVM dengan ID ins-1 di wilayah Guangzhou. Gunakan berikut ini sebagai referensi sintaksis:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cvm:*",
            "resource": "qcs::cvm:ap-guangzhou::instance/ins-1",
            “effect": "allow"
        }
    ]
}
```
2. Temukan kebijakan yang dibuat, dan di kolom “Action” (Tindakan) pada baris tersebut, klik **Associate User/Group** (Kaitkan Pengguna/Grup).
3. Di jendela “Associate User/Group” (Kaitkan Pengguna/Grup), pilih pengguna/grup yang ingin Anda otorisasi, dan klik **OK** (OKE).


### Kebijakan untuk mengizinkan pengguna melakukan operasi pada CVM di wilayah tertentu
Jika Anda ingin mengizinkan pengguna melakukan operasi pada CVM di wilayah tertentu, kaitkan kebijakan berikut dengan pengguna. Langkah-langkah detailnya adalah sebagai berikut:
1. Lihat [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601) untuk mengetahui informasi dan buat kebijakan khusus.
Kebijakan ini mengizinkan pengguna mengoperasikan instans CVM di wilayah Guangzhou. Gunakan berikut ini sebagai referensi sintaksis:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cvm:*",
            "resource": "qcs::cvm:ap-guangzhou::*",
            “effect": "allow"
        }
    ]
}
```
2. Temukan kebijakan yang dibuat, dan di kolom “Action” (Tindakan) pada baris tersebut, klik **Associate User/Group** (Kaitkan Pengguna/Grup).
3. Di jendela “Associate User/Group” (Kaitkan Pengguna/Grup), pilih pengguna/grup yang ingin Anda otorisasi, dan klik **OK** (OKE).


### Memberikan sub-akun semua izin ke instans CVM kecuali pembayaran

Asumsikan bahwa akun CompanyExample, dengan ownerUin12345678, memiliki sub-akun yang disebut Pengembang. Pengembang memerlukan izin pengelolaan penuh (termasuk semua operasi seperti pembuatan dan pengelolaan) untuk instans CVM, kecuali pembayaran, yang berarti Pengembang dapat membuat pesanan tetapi tidak dapat membayarnya.
Anda dapat melakukannya dengan menggunakan salah satu dari dua solusi berikut:
- **Solution A** (Solusi A)
Pemilik akun CompanyExample mengaitkan kebijakan prasetel QcloudCVMFullAccess dengan Pengembang. Untuk informasi selengkapnya, rujuk kepada [Pengelolaan Otorisasi](https://intl.cloud.tencent.com/document/product/598/10602).
- **Solution B** (Solusi B)
 1. Gunakan berikut ini sebagai referensi sintaksis dan buat [kebijakan kustom](#CAMCustomPolicy).
```
 {
    "version": "2.0",
    "statement":[
         {
             "effect": "allow",
             "action": "cvm:*",
             "resource": "*"
         }
    ]
}
```
 2. Kaitkan kebijakan ke sub-akun. Untuk informasi selengkapnya, lihat [Pengelolaan Otorisasi](https://intl.cloud.tencent.com/document/product/598/10602).


### Memberikan sub-akun izin untuk mengelola proyek
Asumsikan bahwa akun perusahaan, CompanyExample, dengan ownerUin 12345678, memiliki sub-akun yang disebut Pengembang. Pemilik CompanyExample ingin mengizinkan Pengembang mengelola proyek, termasuk menetapkan dan menghapus sumber daya, di konsol.
Langkah-langkah detailnya adalah sebagai berikut:
1. Buat kebijakan khusus untuk pengelolaan proyek.
Untuk informasi selengkapnya, lihat [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601).
2. Lihat [Pengelolaan Otorisasi](https://intl.cloud.tencent.com/document/product/598/10602) untuk informasi tentang cara mengaitkan kebijakan kustom dengan sub-akun.
Jika Anda mengalami masalah izin saat mencoba melihat snapshot, citra, dan EIP, kaitkan kebijakan prasetel QcloudCVMAccessForNullProject, QcloudCVMOrderAccess, dan QcloudCVMLaunchToVPC dengan sub-akun. Untuk informasi selengkapnya tentang otorisasi, lihat [Pengelolaan Otorisasi](https://intl.cloud.tencent.com/document/product/598/10602).

<span id="CAMCustomPolicy"></span>
### Kebijakan kustom

Jika kebijakan prasetel tidak dapat memenuhi persyaratan Anda, Anda dapat membuat kebijakan kustom.
Untuk petunjuk mendetail, lihat [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601).
Untuk informasi selengkapnya tentang sintaksis kebijakan CVM, lihat [Sintaksis Kebijakan Otorisasi](https://intl.cloud.tencent.com/document/product/213/10313).

