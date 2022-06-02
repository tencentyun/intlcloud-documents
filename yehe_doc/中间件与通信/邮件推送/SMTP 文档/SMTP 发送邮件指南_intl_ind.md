## Mengaktifkan Fitur Pengiriman SMTP
## Petunjuk
### Langkah 1. Buka halaman alamat pengirim
Login ke [konsol SES](https://console.cloud.tencent.com/ses) dan klik **Configuration** (Konfigurasi) > **Sender Address** (Alamat Pengirim) di bilah sisi kiri untuk masuk ke halaman alamat pengirim.
![](https://qcloudimg.tencent-cloud.cn/raw/fa124df0a9c52d8712e203e25866a389.png)

### Langkah 2. Konfigurasikan kata sandi SMTP
1. Dalam daftar alamat pengirim, temukan alamat yang ingin Anda aktifkan pengiriman SMTP-nya, dan klik **Set SMTP Password** (Atur Kata Sandi SMTP) di bidang **Operation** (Operasi).
2. Masukkan kata sandi SMTP di jendela pop-up dan klik **OK**.



## Mengirim Email melalui SMTP API
Untuk kode sampel SMTP dan parameter permintaan khusus, parameter respons, dan kode kesalahan, lihat [Panggilan Sampel SMTP](https://intl.cloud.tencent.com/document/product/1084/44456).
>?Email dengan lampiran dapat dikirim seperti yang diinstruksikan di [Mengirim Email dengan Lampiran melalui SMTP](https://intl.cloud.tencent.com/document/product/1084/44454).

## Frekuensi Pengiriman SMTP
Rasio panggilan SMTP API saat ini dibatasi hingga 20 kali per detik di bawah akun `appId` Tencent Cloud yang sama. Selain itu, pengirim yang sama dapat mengirim hingga 10 email per jam ke penerima yang sama.

Kami akan mengirimkan email secepatnya setelah menerimanya. Namun, karena kebijakan pembatasan lalu lintas dan perlindungan reputasi yang berbeda dari sistem email yang berbeda, untuk meningkatkan tingkat keberhasilan pengiriman email Anda, sebaiknya kirim email pada frekuensi yang lebih rendah.


