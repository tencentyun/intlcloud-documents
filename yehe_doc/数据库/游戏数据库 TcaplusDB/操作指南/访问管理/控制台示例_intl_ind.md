## Skenario Operasi
Anda dapat memberikan izin kepada pengguna untuk melihat dan menggunakan sumber daya tertentu di Konsol TcaplusDB dengan menggunakan kebijakan CAM. Dokumen ini menjelaskan cara memberikan izin untuk melihat dan menggunakan sumber daya tertentu, sehingga menunjukkan kepada Anda cara menggunakan kebijakan tertentu di konsol.


## Petunjuk
### Kebijakan akses penuh di TcaplusDB
Untuk memberikan izin kepada pengguna untuk membuat dan mengelola instans TcaplusDB, kaitkan kebijakan `QcloudTcaplusDBFullAccess` dengan pengguna.
Kebijakan ini memberikan izin kepada pengguna untuk memanipulasi semua sumber daya di TcaplusDB. Langkah-langkahnya adalah sebagai berikut:
Izinkan kebijakan default `QcloudTcaplusDBFullAccess` dengan pengguna seperti yang diinstruksikan dalam [Manajemen Otorisasi](https://intl.cloud.tencent.com/document/product/598/10602).

### Kebijakan hanya baca di TcaplusDB
Untuk memberikan izin kepada pengguna untuk melihat instans TcaplusDB tetapi tidak membuat, menghapus, atau memodifikasinya, Anda dapat mengaitkan kebijakan `QcloudTcaplusDBReadOnlyAccess` dengan pengguna.
Kebijakan ini memberikan izin kepada pengguna untuk semua operasi di TcaplusDB yang dimulai dengan kata "Describe" atau "Inquiry". Langkah-langkahnya adalah sebagai berikut:
Izinkan kebijakan default `TcaplusDB` dengan pengguna seperti yang diinstruksikan dalam [Manajemen Otorisasi](https://intl.cloud.tencent.com/document/product/598/10602).

### Kebijakan untuk memberikan izin kepada pengguna untuk memanipulasi kluster tertentu
Untuk memberikan izin kepada pengguna untuk memanipulasi kluster TcaplusDB tertentu, Anda dapat mengaitkan kebijakan berikut dengan pengguna. Langkah-langkahnya adalah sebagai berikut:

1. Buat kebijakan kustom seperti yang diinstruksikan dalam [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601).
Kebijakan ini memberikan izin kepada pengguna untuk melakukan semua operasi di kluster TcaplusDB yang ID-nya adalah 19168929215. Konten kebijakan dapat diatur dengan mengacu pada sintaksis kebijakan berikut:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": "qcs::tcaplusdb:ap-shanghai:uin/1231xxx166:cluster/19168929215",
            "effect": "allow"
        }
    ]
}
```
2. Temukan kebijakan yang dibuat dan klik **Associate User/Group** (Kaitkan Pengguna/Grup) di kolom "Operation" (Operasi).
3. Di jendela "Associate User/User Group" (Kaitkan Pengguna/Grup Pengguna) yang muncul, pilih pengguna/grup yang ingin Anda izinkan dan klik **Confirm** (Konfirmasi).


### Kebijakan untuk memberikan izin kepada pengguna untuk memanipulasi semua sumber daya TcaplusDB
Untuk memberikan izin kepada pengguna untuk memanipulasi semua sumber daya TcaplusDB, kaitkan kebijakan berikut dengan pengguna. Langkah-langkahnya adalah sebagai berikut:

1. Buat kebijakan kustom seperti yang diinstruksikan dalam [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601).
Kebijakan ini memberikan izin kepada pengguna untuk memanipulasi semua sumber daya TcaplusDB. Konten kebijakan dapat diatur dengan mengacu pada sintaksis kebijakan berikut:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": "qcs::tcaplusdb:::*",
            "effect": "allow"
        }
    ]
}
```
2. Temukan kebijakan yang dibuat dan klik **Associate User/Group** (Kaitkan Pengguna/Grup) di kolom "Operation" (Operasi).
3. Di jendela "Associate User/User Group" (Kaitkan Pengguna/Grup Pengguna) yang muncul, pilih pengguna/grup yang ingin Anda izinkan dan klik **Confirm** (Konfirmasi).


### Kebijakan untuk menolak semua izin pengguna dari tabel TcaplusDB tertentu
Untuk menolak izin pengguna untuk memanipulasi tabel TcaplusDB tertentu, kaitkan kebijakan berikut dengan pengguna. Langkah-langkahnya adalah sebagai berikut:

1. Buat kebijakan kustom seperti yang diinstruksikan dalam [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601).
Kebijakan ini menolak izin pengguna untuk memanipulasi tabel (ID: tcaplus-c8d1caa4 dan tcaplus-d8d1cbb4). Konten kebijakan dapat diatur dengan mengacu pada sintaksis kebijakan berikut:
```
{
    "version": "2.0",
    "statement": [
        {
            "action": "tcaplusdb:*",
            "resource": [
						"qcs::tcaplusdb::uin/16xxx472:table/tcaplus-c8d1caa4",
						"qcs::tcaplusdb::uin/16xxx472:table/tcaplus-d8d1cbb4",
						],
            "effect": "deny"
        }
    ]
}
```
2. Temukan kebijakan yang dibuat dan klik **Associate User/Group** (Kaitkan Pengguna/Grup) di kolom "Operation" (Operasi).
3. Di jendela "Associate User/User Group" (Kaitkan Pengguna/Grup Pengguna) yang muncul, pilih pengguna/grup yang ingin Anda izinkan dan klik **Confirm** (Konfirmasi).

<span id="CAMCustomPolicy"></span>
### Kebijakan kustom
Jika kebijakan prasetel tidak dapat memenuhi persyaratan, Anda dapat membuat kebijakan kustom sesuai kebutuhan.
Untuk mendapatkan petunjuk mendetail, silakan lihat [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601).
Untuk informasi selengkapnya tentang sintaksis kebijakan CVM, silakan lihat [Sintaksis Kebijakan Otorisasi](https://intl.cloud.tencent.com/document/product/1016/35751).

