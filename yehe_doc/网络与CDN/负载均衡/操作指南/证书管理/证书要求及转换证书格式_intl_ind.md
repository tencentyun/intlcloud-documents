Dokumen ini berisi persyaratan terkait sertifikat SSL dan menjelaskan tentang cara mengonversi format sertifikat.

## Proses Permohonan Sertifikat
1.Gunakan OpenSSL untuk membuat file kunci private secara lokal, misalnya: `privateKey.pem`.Harap rahasiakan kunci ini.
```
openssl genrsa -out privateKey.pem 2048
```
2.Gunakan OpenSSL untuk membuat file permintaan sertifikat, misalnya: `server.csr`.File ini dapat digunakan untuk permohonan sertifikat.
```
openssl req -new -key privateKey.pem -out server.csr
```
3.Simpan isi file permintaan sertifikat, lalu kunjungi situs CA untuk memohon sertifikat.

## Persyaratan Format Sertifikat
- Sertifikat yang perlu diminta harus menggunakan format PEM di Linux.CLB tidak mendukung sertifikat dalam format lain.Untuk informasi selengkapnya, lihat [Mengonversi Sertifikat ke format PEM](#PEM).
- Jika sertifikat Anda dikeluarkan oleh CA root, sertifikat akan bersifat unik, dan situs web yang dikonfigurasi akan dianggap tepercaya oleh peramban dan perangkat lain yang mengakses tanpa memerlukan sertifikat tambahan.
- Jika sertifikat Anda dikeluarkan oleh CA perantara, file sertifikat Anda akan terdiri dari beberapa sertifikat.Dalam kasus ini, Anda harus mengombinasikan secara manual sertifikat server dan sertifikat perantara untuk diunggah.
- Jika sertifikat Anda memiliki rantai sertifikat, silakan konversi sertifikat ke format PEM dan gabungkan dengan konten sertifikat untuk diunggah.
- Aturan urutannya sebagai berikut: terapkan sertifikat server sebelum sertifikat perantara tanpa baris kosong di antaranya.
>?Anda dapat memeriksa aturan yang berlaku atau instruksi yang disediakan oleh CA ketika mengeluarkan sertifikat.

**Format sertifikat dan format rantai sertifikat**
Berikut adalah contoh format sertifikat dan rantai sertifikat.Pastikan format sudah benar sebelum diunggah:
1.Sertifikat dikeluarkan oleh CA root:Format PEM di Linux, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/cdea186a04d6f84e08fb38b19540189c.jpg)
Aturan sertifikat antara lain:
- Sertifikat Anda harus diawali dengan "——-BEGIN CERTIFICATE——-" dan diakhiri dengan "——-END CERTIFICATE——-", yang harus diunggah bersama-sama.
- Setiap baris harus berisi 64 karakter, sedangkan baris terakhir boleh berisi kurang dari 64 karakter.
2.Rantai sertifikat dari CA perantara:
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-

Aturan rantai sertifikat:
- Tidak boleh ada baris kosong antar sertifikat.
- Semua sertifikat harus memenuhi persyaratan yang disebutkan di atas.

## Persyaratan Format Kunci Privat RSA
Berikut contohnya:
![](https://main.qcloudimg.com/raw/bb9f866becc38dd28b8e62c53c1e551a.jpg)
Kunci privat RSA dapat mencakup semua kunci privat (RSA dan DSA), kunci publik (RSA dan DSA), serta sertifikat (X.509).Kunci ini menyimpan data dalam format DER dalam kode Base64 dan dibungkus oleh header ASCII sehingga sesuai untuk ditransmisikan dalam mode teks antar sistem.

Aturan kunci privat RSA:
- Sertifikat Anda harus diawali dengan "——-BEGIN RSA PRIVATE KEY——-" dan diakhiri dengan "——-END RSA PRIVATE KEY——-", yang harus diunggah bersama-sama.
- Setiap baris harus berisi 64 karakter, sedangkan baris terakhir boleh berisi kurang dari 64 karakter.

Jika kunci privat Anda tidak diawali dengan "——-BEGIN PRIVATE KEY——-" dan diakhiri dengan "——-END PRIVATE KEY——-", Anda dapat mengonversinya dengan cara berikut:
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```
Setelah itu, Anda dapat mengunggah konten `new_server_key.pem` bersama sertifikat.

## [](id:PEM)Mengonversi Sertifikat ke Format PEM
Saat ini, CLB hanya mendukung sertifikat dalam format PEM.Sertifikat dalam format lain perlu dikonversi ke format PEM terlebih dahulu sebelum diunggah ke CLB.Kami menyarankan Anda menggunakan OpenSSL.Berikut adalah cara mengonversi beberapa format umum ke PEM.
<dx-tabs>
::: DER\sto\sPEM\s
Format DER umumnya digunakan pada platform Java.
Konversi sertifikat:
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
Konversi kunci privat:
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```
:::
::: P7B\sto\sPEM\s
Format P7B umumnya digunakan pada Windows Server dan Tomcat.
Konversi sertifikat:
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
Anda harus menyimpan konten antara "——-BEGIN CERTIFICATE——-" dan "——-END CERTIFICATE——-" dalam `outcertificat.cer` untuk diunggah sebagai sertifikat.
Konversi kunci privat: kunci privat umumnya dapat diekspor ke server IIS.
:::
::: PFX\sto\sPEM\s
Format PFX umumnya digunakan pada Windows Server.
Konversi sertifikat:
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
Konversi kunci privat:
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```	
:::
::: CER/CRT\sto\sPEM\s
Anda dapat mengonversi sertifikat dalam format CER/CRT ke PEM dengan langsung memodifikasi nama ekstensi file.Misalnya, Anda dapat langsung mengganti nama file sertifikat `servertest.crt` sebagai `servertest.pem`.
:::
</dx-tabs>








