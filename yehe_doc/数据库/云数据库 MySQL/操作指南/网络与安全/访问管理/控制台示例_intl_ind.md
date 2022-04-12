
Dokumen ini memberikan contoh tentang cara memberikan izin kepada pengguna untuk melihat dan menggunakan sumber daya tertentu di konsol TencentDB dengan menggunakan kebijakan CAM.

## Kebijakan Akses Penuh untuk TencentDB
Untuk memberikan izin kepada pengguna untuk membuat dan mengelola instans TencentDB, Anda dapat menerapkan kebijakan QcloudCDBFullAccess untuk pengguna.

Login ke [konsol CAM](https://console.cloud.tencent.com/cam/policy), pilih **Policies** (Kebijakan) di bilah sisi kiri, dan cari QcloudCDBFullAccess di sudut kanan atas.
![](https://main.qcloudimg.com/raw/5ec89e71595a5edd3e7f723a19c01a6a.png)
Sintaks kebijakannya sebagai berikut:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cvm:*"
            ],
            "resource": "qcs::cvm:::sg/*",
            "effect": "allow"
        },
        {
            "action": [
                "cos:*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        },
        {
            "action": [
                "kms:CreateKey",
                "kms:GenerateDataKey",
                "kms:Decrypt",
                "kms:ListKey"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
Kebijakan CAM di atas memberikan izin kepada pengguna untuk menggunakan semua sumber daya TencentDB, VPC, grup keamanan, COS, KMS, dan Cloud Monitor.

## Kebijakan Izin Baca Saja untuk TencentDB
Untuk memberikan izin kepada pengguna melihat instans TencentDB tetapi tidak membuat, menghapus, atau memodifikasinya, Anda dapat menerapkan kebijakan QcloudCDBInnerReadOnlyAccess untuk pengguna.

>?Anda disarankan untuk mengonfigurasi kebijakan baca saja untuk TencentDB.

Login ke [konsol CAM](https://console.cloud.tencent.com/cam/policy), pilih **Policies** (Kebijakan) di bilah sisi kiri, klik **Service Type** (Jenis Layanan) di daftar kebijakan dan pilih **TencentDB for MySQL** (TencentDB for MySQL) di daftar drop-down, selanjutnya Anda dapat melihat kebijakan ini di hasil.

Sintaks kebijakannya sebagai berikut:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

## Kebijakan Izin Baca Saja untuk Sumber Daya terkait TencentDB
Untuk memberikan izin kepada pengguna melihat instans TencentDB dan sumber daya terkait (VPC, grup keamanan, COS, dan Cloud Monitor) tetapi tidak membuat, menghapus, atau memodifikasinya, Anda dapat menerapkan kebijakan QcloudCDBReadOnlyAccess untuk pengguna.

Login ke [konsol CAM](https://console.cloud.tencent.com/cam/policy), pilih **Policies** (Kebijakan) di bilah sisi kiri, klik **Service Type** (Jenis Layanan) di daftar kebijakan dan pilih **TencentDB for MySQL** (TencentDB for MySQL) di daftar drop-down, selanjutnya Anda dapat melihat kebijakan ini di hasil.

Sintaks kebijakannya sebagai berikut:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "vpc:Describe*",
                "vpc:Inquiry*",
                "vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cvm:DescribeSecurityGroup*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "cos:List*",
                "cos:Get*",
                "cos:Head*",
                "cos:OptionsObject"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "monitor:*",
            "resource": "*"
        }
    ]
}
```
Sintaks kebijakan CAM di atas memberikan izin pengguna untuk operasi berikut:
- Semua operasi di TencentDB yang dimulai dengan "Describe".
- Semua operasi di VPC yang dimulai dengan "Describe", "Inquiry", atau "Get".
- Semua operasi dalam grup keamanan yang dimulai dengan "DescribeSecurityGroup".
- Semua operasi di COS yang dimulai dengan "List", "Get", dan "Head" serta operasi "OptionsObject".
- Semua operasi di Cloud Monitor.

## Kebijakan untuk Memberikan Izin Pengguna untuk Menggunakan API bukan di Tingkat Sumber Daya
Untuk memberikan izin kepada pengguna agar hanya menggunakan API bukan pada tingkat sumber daya, Anda dapat menerapkan kebijakan QcloudCDBProjectToUser untuk pengguna.
Login ke [konsol CAM](https://console.cloud.tencent.com/cam/policy), pilih **Policies** (Kebijakan) di bilah sisi kiri, klik **Service Type** (Jenis Layanan) di daftar kebijakan dan pilih **TencentDB for MySQL** (TencentDB for MySQL) di daftar drop-down, selanjutnya Anda dapat melihat kebijakan ini di hasil.
Sintaks kebijakannya sebagai berikut:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cdb:BalanceRoGroupLoad",
                "cdb:CancelBatchOperation",
                "cdb:CreateBatchJobFiles",
                "cdb:CreateDBInstance",
                "cdb:CreateDBInstanceHour",
                "cdb:CreateMonitorTemplate",
                "cdb:CreateParamTemplate",
                "cdb:DeleteBatchJobFiles",
                "cdb:DeleteMonitorTemplate",
                "cdb:DeleteParamTemplate",
                "cdb:DescribeBatchJobFileContent",
                "cdb:DescribeBatchJobFiles",
                "cdb:DescribeBatchJobInfo",
                "cdb:DescribeProjectSecurityGroups",
                "cdb:DescribeDefaultParams",
                "cdb:DescribeMonitorTemplate",
                "cdb:DescribeParamTemplateInfo",
                "cdb:DescribeParamTemplates",
                "cdb:DescribeRequestResult",
                "cdb:DescribeRoGroupInfo",
                "cdb:DescribeRoMinScale",
                "cdb:DescribeTasks",
                "cdb:DescribeUploadedFiles",
                "cdb:ModifyMonitorTemplate",
                "cdb:ModifyParamTemplate",
                "cdb:ModifyRoGroupInfo",
                "cdb:ModifyRoGroupVipVport",
                "cdb:StopDBImportJob",
                "cdb:UploadSqlFiles"
            ],
            "effect": "allow",
            "resource": "*"
        }
    ]
}
```

## Kebijakan untuk Memberikan Izin Pengguna untuk Memanipulasi Instans TencentDB Tertentu
Untuk memberikan izin kepada pengguna untuk memanipulasi database tertentu, Anda dapat mengaitkan kebijakan berikut dengan pengguna. Misalnya, kebijakan di bawah ini memungkinkan pengguna untuk memanipulasi instans TencentDB "cdb-xxx" di Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": "qcs::cdb:ap-guangzhou::instanceId/cdb-xxx",
            "effect": "allow"
        }
    ]
}
```

## Kebijakan untuk Memberikan Izin Pengguna untuk Memanipulasi Instans TencentDB dalam Batch
Untuk memberikan izin kepada pengguna memanipulasi instans TencentDB dalam batch, Anda dapat mengaitkan kebijakan berikut dengan pengguna. Misalnya, kebijakan di bawah ini memungkinkan pengguna untuk memanipulasi instans TencentDB "cdb-xxx" dan "cdb-yyy" di Guangzhou dan "cdb-zzz" di Beijing.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": ["qcs::cdb:ap-guangzhou::instanceId/cdb-xxx", "qcs::cdb:ap-guangzhou::instanceId/cdb-yyy", "qcs::cdb:ap-beijing::instanceId/ cdb-zzz"],
            "effect": "allow"
        }
    ]
}
```

## Kebijakan untuk Memberikan Izin Pengguna untuk Memanipulasi Instans TencentDB di Wilayah Tertentu
Untuk memberikan izin kepada pengguna untuk memanipulasi instans TencentDB di wilayah tertentu, Anda dapat mengaitkan kebijakan berikut dengan pengguna. Misalnya, kebijakan di bawah ini memungkinkan pengguna untuk memanipulasi instans TencentDB di Guangzhou.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "cdb:*",
            "resource": "qcs::cdb:ap-guangzhou::*",
            "effect": "allow"
        }
    ]
}
```

### Kebijakan Kustom
Jika kebijakan yang telah ditetapkan tidak dapat memenuhi persyaratan Anda, Anda dapat membuat kebijakan khusus seperti yang ditunjukkan di bawah ini. Jika izin diberikan oleh sumber daya, untuk operasi API TencentDB yang tidak mendukung otorisasi di tingkat sumber daya, Anda masih dapat memberi otorisasi kepada pengguna untuk melakukannya, tetapi Anda harus menentukan `*` sebagai elemen sumber daya dalam pernyataan kebijakan.
     
Sintaks kebijakan kustom adalah sebagai berikut:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "Action"
            ],
            "resource": "Resource",
            "effect": "Effect"
        }
    ]
}
```
- Ganti "Action" (Tindakan) dengan operasi yang diizinkan atau ditolak.
- Ganti "Resource" (Sumber Daya) dengan sumber daya yang ingin Anda izinkan untuk dimanipulasi oleh pengguna.
- Ganti "Effect" (Efek) dengan "Allow" (Izinkan) atau "Deny" (Tolak).
