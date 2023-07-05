### Bagaimana cara membuat kebijakan kustom?

Jika kebijakan prasetel tidak memenuhi persyaratan, Anda dapat membuat kebijakan kustom.
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

- Tindakan: ganti ini dengan operasi yang diizinkan atau ditolak.
- Sumber daya: ganti ini dengan sumber daya yang ingin diotorisasi.
- Efek: ganti ini dengan "Allow" (Izinkan) atau "Deny" (Tolak).

### Bagaimana cara mengonfigurasi kebijakan baca saja untuk CVM?

Untuk mengizinkan pengguna mengkueri instans CVM tetapi tidak membuat, menghapus, memulai, atau menghentikan instans, aktifkan kebijakan QcloudCVMInnerReadOnlyAccess.

Untuk melakukannya, login ke Konsol CAM. Di halaman [Kebijakan](https://console.cloud.tencent.com/cam/policy), cari **CVM** untuk menemukan kebijakan.

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

Kebijakan sebelumnya **grants users the permissions to perform the following operations** (memberi izin kepada pengguna untuk melakukan operasi berikut):

- Semua operasi dimulai dengan "Describe" (Jelaskan) di CVM.
- Semua operasi dimulai dengan "Inquiry" (Pertanyaan) di CVM.

### Bagaimana cara mengonfigurasi kebijakan baca saja untuk sumber daya terkait CVM?

Untuk mengizinkan pengguna mengkueri instans CVM dan sumber daya yang relevan (instans VPC dan CLB) tetapi tidak membuat, menghapus, memulai, atau menghentikan instans dan sumber daya yang relevan, aktifkan kebijakan QcloudCVMReadOnlyAccess.

Untuk melakukannya, login ke Konsol CAM. Di halaman [Kebijakan](https://console.cloud.tencent.com/cam/policy), cari **CVM** untuk menemukan kebijakan.

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

Kebijakan sebelumnya **grants users the permissions to perform the following operations** (memberi izin kepada pengguna untuk melakukan operasi berikut):

- Semua operasi dimulai dengan "Describe" (Jelaskan) dan "Inquiry" (Pertanyaan) di CVM.
- Semua operasi dimulai dengan "Describe" (Jelaskan), "Inquiry" (Pertanyaan), dan "Get" (Dapatkan) di VPC.
- Semua operasi dimulai dengan "Describe" (Jelaskan) di CLB.
- Semua operasi di monitor.

