## Ikhtisar
Anda dapat mengonfigurasi domain pengirim di konsol SES. Dokumen ini menjelaskan cara membuat domain pengirim.

## Prasyarat
- Anda harus memiliki izin admin di domain pengirim.
- Jika domain Anda dihosting dengan Tencent Cloud, login ke [konsol DNSPod](https://console.cloud.tencent.com/cns) untuk konfigurasi. Jika domain Anda dihosting dengan penyedia layanan domain lain, konfigurasikan sesuai dengan daftar periksa.

## Petunjuk
1. Login ke [konsol SES](https://console.cloud.tencent.com/ses/domain), klik **Configuration** (Konfigurasi) > **Sender Domain** (Domain Pengirim) untuk membuka halaman **Sender Domain** (Domain Pengirim), dan klik **Create** (Buat).
![](https://main.qcloudimg.com/raw/7e4ba21b39ef0d2eb1de2e7ad8d8147a.png)

| Bidang | Deskripsi |
|---------|---------|
| Domain Pengirim | Domain pengirim yang dikonfigurasi |
| Status |<li>**Verifikasi tertunda**: domain harus lulus verifikasi sebelum dapat digunakan untuk mengirim email. </li><br><li>**Terverifikasi**: domain telah diverifikasi dan dapat digunakan untuk mengirim email.</li> |
| Operasi | Jika statusnya **Pending verification** (Verifikasi tertunda), Anda dapat mengeklik **Verify** (Verifikasi) untuk memverifikasi domain atau klik **Delete** (Hapus) untuk menghapusnya. |

2. Di kotak dialog **Create Sender Domain** (Buat Domain Pengirim), masukkan domain dan klik **Submit** (Kirim) untuk menyelesaikan konfigurasi.
![](https://main.qcloudimg.com/raw/c2c75b71aaaf762f545ad530c6554aeb.png)
>? Untuk menghindari konflik antara data SPF dan MX, jangan gunakan domain email perusahaan.
