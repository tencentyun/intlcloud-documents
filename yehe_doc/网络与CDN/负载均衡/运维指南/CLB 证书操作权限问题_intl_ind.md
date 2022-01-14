## Skenario Pengoperasian
Sejak 23 Maret 2020, semua pengoperasian sertifikat CLB telah terhubung dengan Cloud Access Management (CAM) untuk autentikasi.Oleh karena itu, ketika akun subpengguna menjalankan pengoperasian sertifikat CLB, padahal "Anda tidak diotorisasi untuk pengoperasian ini.Silakan hubungi developer Anda."ditampilkan, Anda dapat memberikan izin sertifikat kepada akun subpengguna sesuai petunjuk berikut.

## Prasyarat
Akun yang sudah masuk harus berupa akun root atau akun subpengguna dengan izin CAM (yaitu, berkaitan dengan kebijakan `QcloudCamFullAccess`).
>?
>- Untuk memeriksa apakah akun subpengguna memiliki izin CAM atau tidak, buka [Daftar Pengguna](https://console.cloud.tencent.com/cam) di Konsol CAM, masuk ke halaman detail subpengguna dan periksa apakah kebijakan `QcloudCamFullAccess` telah berkaitan atau belum.
>- Jika kebijakan `QcloudCamFullAccess` sudah terkait, tetapi "Tidak ada izin API (message:GetReceiversOnAllType).Silakan hubungi developer Anda."ditampilkan ketika subpengguna menjalankan pengoperasian sertifikat, silakan diabaikan dan lanjutkan saja.

## Petunjuk
Silakan beri izin sertifikat dengan metode berikut:

### Metode 1.Kaitkan dengan kebijakan khusus
1.Masuk ke [Konsol CAM](https://console.cloud.tencent.com/cam/overview).
2.Di bilah sisi kiri, klik **Policies** (Kebijakan).
3.Klik **Create Custom Policy** (Buat Kebijakan Khusus) dan pilih **Create by Policy Syntax** (Buat berdasarkan Sintaksis Kebijakan) di kotak pop-up.
4.Di halaman "Select Template Policy" (Pilih Kebijakan Templat), pilih **Blank Template** (Templat Kosong) lalu klik **Next** (Selanjutnya).
5.Di halaman "Edit Policy" (Edit Kebijakan), masukkan nama kebijakan dan masukkan konten kebijakan berikut ke dalam kotak input "Edit Policy Content" (Edit Konten Kebijakan):
```
   {
"version":"2.0",
"statement": [
        {
"action": "name/ssl:*",
"resource": "qcs::ssl:::*",
"effect": "allow"
        }
    ]
}  
```
6.Lalu klik **Done** (Selesai) untuk kembali ke halaman daftar "Policy" (Kebijakan).
7.Di bagian atas halaman daftar "Policy" (Kebijakan), pilih **Custom Policy** (Kebijakan Khusus), cari baris kebijakan yang barusan Anda buat dalam daftar, dan klik **Associate User/Group** (Kaitkan Pengguna/Grup) di kolom "Operation" (Pengoperasian).
![](https://main.qcloudimg.com/raw/2a0cf97e6de81cbbc3fcc6af9164bb5a.png)
8.Di kotak pop-up, pilih pengguna yang akan diotorisasi dan klik **OK** (Oke).
![](https://main.qcloudimg.com/raw/2105e8b1ebf79f0d6b1d063aa0bcd158.png)

### Metode 2.Kaitkan kebijakan praatur
1.Masuk ke [Konsol CAM](https://console.cloud.tencent.com/cam/overview).
2.Di bilah sisi kiri, pilih **User** > **User List** (Pengguna > Daftar Pengguna) untuk masuk ke halaman "User List" (Daftar Pengguna).
3.Di baris subpengguna yang akan diotorisasi, klik **Authorize** (Beri Otorisasi) di bilah "Operation" (Pengoperasian).
4.Di kotak pop-up, pilih `QcloudSSLFullAccess` atau `QcloudSSLReadOnlyAccess` dan klik **OK** (Oke).
![](https://main.qcloudimg.com/raw/a18245f729467395f801002f6defcb8d.png)
