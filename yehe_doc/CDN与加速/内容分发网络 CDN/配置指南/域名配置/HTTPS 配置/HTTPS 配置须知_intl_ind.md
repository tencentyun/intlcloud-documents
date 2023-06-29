Jika Anda perlu mengonfigurasi sertifikat yang ada untuk nama domain Anda, silakan lihat di bawah ini. Jika sertifikat yang Anda konfigurasikan berasal dari Layanan Sertifikat SSL Tencent Cloud, Anda dapat melewati langkah ini.
## Mengunggah Sertifikat
Umumnya, CA menyediakan jenis sertifikat berikut, dan **Nginx** digunakan oleh CDN.
Masuk ke folder Nginx, gunakan editor teks untuk membuka file ".crt" (sertifikat) dan ".key" (kunci privat), dan lihat konten sertifikat dan kunci privat tersebut dalam format PEM.

### Sertifikat
Ekstensi sertifikat umum termasuk ".pem", ".crt", dan ".cer". Buka file sertifikat dalam editor teks dan Anda dapat melihat konten yang mirip dengan yang ditunjukkan di bawah ini.
Sertifikat ".pem" dimulai dengan "-----BEGIN CERTIFICATE-----" dan diakhiri dengan "-----END CERTIFICATE-----". Setiap baris di antaranya berisi 64 karakter, sedangkan baris terakhir mungkin memiliki kurang dari 64 karakter:
![img](https://main.qcloudimg.com/raw/60ea02d1a2c9623526d7fa79403e658a.jpg)
Jika sertifikat Anda dikeluarkan oleh CA perantara, file sertifikat Anda akan terdiri dari beberapa sertifikat. Dalam hal ini, Anda perlu menyambungkan sertifikat server dan sertifikat perantara secara manual untuk diunggah dengan meletakkan konten sertifikat server sebelum konten sertifikat perantara tanpa ada baris kosong di antaranya. Silakan merujuk ke aturan atau instruksi yang disertakan dengan sertifikat.

>
> + Tidak boleh ada baris kosong di antara sertifikat
> + Semua sertifikat dalam format PEM

Rantai sertifikat dari CA perantara tersedia dalam format ini:
```
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
```

### Kunci privat
Ekstensi kunci privat yang umum termasuk ".pem" dan ".key". Buka file kunci privat di editor teks dan Anda akan melihat konten yang mirip dengan yang ditunjukkan di bawah ini.
Kunci privat ".pem" dimulai dengan "-----BEGIN RSA PRIVATE KEY-----" dan diakhiri dengan "-----END RSA PRIVATE KEY-----". Setiap baris di antaranya berisi 64 karakter, sedangkan baris terakhir mungkin memiliki kurang dari 64 karakter.
![img](https://main.qcloudimg.com/raw/e10009916aeb00d5158a3703115d0354.jpg)
Jika kunci privat Anda dimulai dengan "-----BEGIN PRIVATE KEY-----" dan diakhiri dengan "-----END PRIVATE KEY-----", kami sarankan Anda mengonversi formatnya menggunakan OpenSSL dengan perintah berikut:
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```

### Mengonversi format lain ke PEM
Saat ini, CDN hanya mendukung sertifikat dalam format PEM. Sertifikat dalam format lain perlu dikonversi ke format PEM. Kami menyarankan Anda menggunakan OpenSSL. Di bawah ini menunjukkan cara mengonversi beberapa format umum ke PEM.
#### DER ke PEM
Format DER umumnya digunakan pada platform Java.
Konversi sertifikat:
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
Konversi kunci privat:
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```
#### P7B ke PEM
Format P7B umumnya digunakan pada Windows Server dan Tomcat.
Konversi sertifikat:
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
Buka outcertificat.cer dengan editor teks untuk melihat konten sertifikat PEM.
Konversi kunci privat: kunci privat umumnya dapat diekspor ke server IIS.
#### PFX ke PEM
Format PFX umumnya digunakan pada Windows Server.
Konversi sertifikat:
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
Konversi kunci privat:
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```
### Menyelesaikan rantai sertifikat
Saat mengonfigurasi sertifikat privat, Anda mungkin mengalami masalah bahwa **rantai sertifikat tidak dapat diselesaikan**, seperti yang ditunjukkan di bawah ini.

Dalam hal ini, Anda dapat menempelkan konten sertifikat (dalam format PEM) yang dikeluarkan oleh CA setelah sertifikat nama domain (dalam format PEM) untuk menyelesaikan rantai sertifikat. Anda juga dapat mengirimkan tiket untuk bantuan.

## Sertifikat yang Di-hosting

Tencent Cloud menyediakan layanan hosting sertifikat: [Layanan Sertifikat SSL](http://console.cloud.tencent.com/ssl). Anda dapat mengunggah sertifikat yang ada ke Konsol Layanan Sertifikat SSL untuk hosting terpadu dan deployment pada produk Tencent Cloud lainnya. Ini juga memungkinkan Anda untuk membeli dan membuat pengajuan permintaan sertifikat.

Layanan Sertifikat SSL memberi Anda 20 sertifikat SSL DV yang dikeluarkan oleh TrustAsia secara gratis.
