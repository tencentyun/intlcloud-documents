## Wilayah
Wilayah adalah area geografis tempat pusat data fisik berada. Di Short Message Service (SMS) Tencent Cloud, wilayah sepenuhnya terisolasi satu sama lain, yang berarti data tidak dapat disimpan di seluruh wilayah kecuali di wilayah lokal. Kami menyarankan Anda memilih wilayah sesuai dengan persyaratan penyimpanan data di wilayah yang berbeda.
Fitur dan harga layanan SMS di setiap wilayah sama, tetapi datanya tidak saling terhubung. Hanya tanda tangan dan templat yang disetujui yang dapat disalin di seluruh wilayah.
Klik [di sini](https://intl.cloud.tencent.com/document/api/382/40466?lang=en#region-list) untuk melihat daftar wilayah lengkap.

## Format Pesan SMS
Pesan SMS terdiri atas tanda tangan dan isi. Sebelum mengirim pesan SMS, Anda harus mengajukan tanda tangan SMS dan templat isi SMS.
Misalnya, jika tanda tangan SMS adalah `Tencent Technology` dan isi SMS adalah `Kode verifikasi login untuk akun QQ Anda adalah 1234 dan valid selama 5 menit.`, isi pesan SMS lengkapnya adalah sebagai berikut:
```
[Tencent Technology] Kode verifikasi login untuk akun QQ Anda adalah 1234 dan valid selama 5 menit.
```
Sebelum mengirim sampel pesan SMS di atas, Anda perlu melakukan langkah-langkah berikut:
1. Ajukan tanda tangan SMS dengan `Tencent Technology` sebagai **Konten Tanda Tangan**.
2. Ajukan templat isi SMS dengan `Kode verifikasi login untuk akun QQ Anda adalah {1} dan valid selama {2} menit.` sebagai **Konten SMS**. Variabel {1} dan {2} adalah parameter yang dapat disesuaikan saat Pesan SMS dikirim.

## Tanda Tangan SMS
Tanda tangan SMS adalah tanda tangan yang tercantum di [] sebelum isi SMS, yang digunakan untuk mengidentifikasi perusahaan atau bisnis. Untuk mengajukan tanda tangan SMS, pengguna perusahaan perlu mengunggah sertifikat kualifikasi, sementara pengguna individu perlu mengunggah sertifikat identitas. Hanya tanda tangan SMS yang disetujui yang dapat digunakan.
**Sampel tanda tangan SMS:**
Shenzhen Tencent Computer Systems Company Limited dapat mengajukan tanda tangan yang terkait dengan nama perusahaannya, seperti: `[Tencent Technology]`, atau yang terkait dengan nama produk apa pun yang disediakan olehnya, seperti `[WeChat]` atau `[Tencent Cloud]`.

>!Anda tidak perlu memasukkan "[]" saat mengajukan tanda tangan SMS di konsol. Misalnya, jika ingin menggunakan `[Tencent Technology]` sebagai tanda tangan, Anda cukup memasukkan `Tencent Technology` sebagai **Signature Content** (Konten Tanda Tangan).

## Templat SMS
Templat SMS adalah konten isi SMS. Templat SMS terbagi menjadi templat kode verifikasi, templat pemberitahuan, dan templat SMS pemasaran. Konten SMS dapat disesuaikan melalui parameter templat.
>!Anda tidak dapat mengajukan templat SMS pemasaran atau mengirim pesan SMS pemasaran jika Anda adalah pengguna individu.

Sebelum mengajukan templat SMS, Anda harus mengajukan tanda tangan SMS terlebih dahulu. Hanya templat SMS yang disetujui yang dapat digunakan.
**Sampel templat SMS:**
Jika Tencent Technology ingin mengirim kode verifikasi SMS: `[Tencent Technology] Kode verifikasi login untuk akun QQ Anda adalah 1234 dan valid selama 2 menit.`. Kode verifikasi (1234 dalam sampel) dan periode validitas (2 menit dalam sampel) dapat diubah dalam keadaan tertentu, kemudian:
Anda dapat mengajukan tanda tangan dan templat seperti di bawah ini:
- Tanda tangan SMS: `Tencent Technology`
- Templat SMS: `Kode verifikasi login untuk akun QQ Anda adalah {1} dan valid selama {2} menit.`
 {1} dan {2} adalah variabel yang disusun secara berurutan, dan nilainya dapat disesuaikan dengan mengatur nilai parameter templat saat Anda mengirim pesan SMS.

## SMS Biasa
Pesan SMS biasa terbagi menjadi SMS kode verifikasi dan SMS pemberitahuan.
- **SMS kode verifikasi**: pesan kode verifikasi untuk pendaftaran atau verifikasi login, konfirmasi pembayaran, verifikasi identitas, dll.
 Sampel:
 ```
Kode verifikasi login Anda adalah 1234. Masukkan kode verifikasi dalam 2 menit. Abaikan pesan ini jika bukan Anda yang melakukan login.
```
- **SMS Pemberitahuan**: pesan pemberitahuan sistem, seperti pemberitahuan pengiriman, penerimaan pembayaran, dan pemberitahuan status.
 Sampel:
 ```
Dokumen pendukung yang diajukan untuk permintaan aplikasi izin ICP 201700001234 telah disetujui. Silakan kirim dokumen pendukung tambahan sesegera mungkin. Jika Anda sudah mengirimkannya, Tencent Cloud akan meninjaunya sesegera mungkin.
```

## SMS Pemasaran
SMS Pemasaran biasanya mengacu pada pesan SMS yang dikirim kepada anggota terdaftar dari situs web atau perusahaan untuk tujuan pemasaran selama kampanye promosi atau acara anggota. Konten pesan SMS pemasaran biasanya tentang layanan pelanggan atau pemberitahuan peluncuran produk baru atau acara.

Sampel 1:
```
Kabar gembira! Anda sekarang dapat mengajukan permohonan untuk meningkatkan peringkat toko di situs web resmi. Dengan sejumlah besar sumber daya yang tersedia secara gratis, langkah ini membantu meningkatkan pengenalan merek Anda. Cobalah sekarang juga! Berhenti berlangganan dengan membalas T.
```
Sampel 2:
```
Akan ada promosi tahun baru yang segera hadir! Ada diskon hingga 30% untuk berbagai item penataan rambut. Flash sale akan dimulai tanggal 17 Februari pukul 09.00. Ketuk xxx untuk informasi selengkapnya. Berhenti berlangganan dengan membalas T.
```
