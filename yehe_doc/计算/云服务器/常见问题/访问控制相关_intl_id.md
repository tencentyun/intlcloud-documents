### Bagaimana cara membuat kebijakan kustom?

Jika kebijakan prasetel tidak dapat memenuhi persyaratan Anda, Anda dapat membuat kebijakan kustom.
Sintaks kebijakan kustom sebagai berikut:

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
- Ganti "Resource" (Sumber Daya) dengan sumber daya yang ingin diotorisasi untuk dioperasikan oleh pengguna.
- Ganti "Effect" (Eefek) dengan Izinkan atau Tolak.

### Bagaimana cara mengonfigurasi kebijakan baca saja untuk CVM?

Jika Anda ingin mengizinkan pengguna untuk mengkueri instans CVM, tetapi tidak membuat, menghapus, dan memulai/menghentikan instans, Anda dapat menerapkan kebijakan bernama QcloudCVMInnerReadOnlyAccess.

Login ke konsol CAM dan cari **CVM** di halaman [Kebijakan](https://console.cloud.tencent.com/cam/policy) untuk menemukan kebijakan dengan cepat.

Sintaks kebijakannya sebagai berikut:

```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:Describe*",
                "name/cvm:Inquiry*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```

Kebijakan di atas dirancang untuk **grant users the permissions to perform the following operations** (memberikan izin kepada pengguna untuk melakukan operasi berikut):

- Semua operasi dimulai dengan "Describe" (Jelaskan) di CVM.
- Semua operasi dimulai dengan "Inquiry" (Pertanyaan) di CVM.

### Bagaimana cara mengonfigurasi kebijakan baca saja untuk sumber daya CVM?

Jika Anda ingin mengizinkan pengguna untuk mengkueri instans CVM dan sumber daya yang relevan (VPC, CLB), tetapi tidak membuat, menghapus, dan memulai/menghentikan instans, Anda dapat menerapkan kebijakan bernama QcloudCVMReadOnlyAccess.

Login ke konsol CAM dan cari **CVM** di halaman [Kebijakan](https://console.cloud.tencent.com/cam/policy) untuk menemukan kebijakan dengan cepat.

Sintaks kebijakannya sebagai berikut:

```
 {
    "version": "2.0",
    "statement": [
        {
            "action": [
                "name/cvm:Describe*",
                "name/cvm:Inquiry*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/vpc:Describe*",
                "name/vpc:Inquiry*",
                "name/vpc:Get*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "action": [
                "name/clb:Describe*"
            ],
            "resource": "*",
            "effect": "allow"
        },
        {
            "effect": "allow",
            "action": "name/monitor:*",
            "resource": "*"
        }
    ]
}
```

Kebijakan di atas dirancang untuk **grant users the permissions to perform the following operations** (memberikan izin kepada pengguna untuk melakukan operasi berikut):

- Semua operasi dimulai dengan "Describe" (Jelaskan) dan "Inquiry" (Pertanyaan) di CVM.
- Semua operasi dimulai dengan "Describe" (Jelaskan), "Inquiry" (Pertanyaan), dan "Get" (Dapatkan) di VPC.
- Semua operasi dimulai dengan "Describe" (Jelaskan) di CLB.
- Semua operasi di Monitor.

