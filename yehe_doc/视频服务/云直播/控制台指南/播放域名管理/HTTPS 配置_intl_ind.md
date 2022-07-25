## Ikhtisar
Protokol HTTPS adalah protokol jaringan yang dibangun berdasarkan protokol SSL dan HTTP untuk transfer dan autentikasi terenkripsi, yang lebih aman daripada protokol HTTP. Jika ingin mengaktifkan akselerasi HTTPS, Anda dapat melakukannya dengan mengaktifkan fitur HTTPS untuk nama domain pemutaran ulang dan mengonfigurasikan sertifikat yang benar dan valid. Anda dapat membeli sertifikat dari Tencent Cloud [SSL Certificate Service (Layanan Sertifikat SSL)](https://intl.cloud.tencent.com/product/ssl). Jika sudah memiliki sertifikat, Anda dapat mengunggahnya ke konsol CSS untuk konfigurasi. Saat ini, CSS hanya mendukung format PEM. Jika sertifikat Anda menggunakan format lain, Anda harus mengonversinya ke format PEM terlebih dahulu. Berikut adalah persyaratan format dan metode konfigurasi untuk sertifikat:

## Prasyarat
Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live).
- Anda telah [menambahkan nama domain pemutaran ulang](https://intl.cloud.tencent.com/document/product/267/35970).

## Petunjuk 
### Langkah 1. Edit konfigurasi HTTPS
1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik **playback domain name** (nama domain pemutaran ulang) yang akan dikonfigurasi atau **Manage** (Kelola) di sebelah kanan untuk masuk halaman detail nama domain.
2. Pilih **Advanced Configuration** (Konfigurasi Lanjutan) dan temukan bagian **HTTPS Configuration** (Konfigurasi HTTPS).
3. Klik **Edit** dan klik ![](https://main.qcloudimg.com/raw/897761946b06e8f904bfa6301d282817.png) untuk mengaktifkan layanan HTTPS.
4. Pilih sumber sertifikat yang akan dikonfigurasi, masukkan informasi yang relevan, lalu klik **Save** (Simpan).
<table>
<tr><th>Sumber Sertifikat</th><th>Item Konfigurasi yang Diperlukan</th></tr>
<tr>
<td>Sertifikat milik sendiri</td>
<td><ul style="margin:0">
<li>Certificate Name (Nama Sertifikat): masukkan nama kustom yang digunakan untuk mengidentifikasi sertifikat.</li>
<li>Certificate Content (Konten Sertifikat): masukkan konten file <code>.crt</code> untuk Nginx. Informasi lebih lanjut dapat dilihat di <a href="#content">Certificate content (Konten sertifikat)</a>.</li>
<li>Private Key Content (Konten Kunci Privat): masukkan konten file <code>.key</code> untuk Nginx. Informasi selengkapnya dapat dilihat di <a href="#private_key">Kunci sertifikat</a>.</li><ul></td>
</tr><tr>
<td>Sertifikat yang di-hosting oleh Tencent Cloud</td>
<td>Certificate List (Daftar Sertifikat): pilih sertifikat yang diunggah di <a href="https://console.cloud.tencent.com/ssl">SSL Certificate Service</a>.</td>
</tr></table>
<img src="https://main.qcloudimg.com/raw/b42458905e48db6b45def7a1d8ecc349.png"></img>

#### Deskripsi sertifikat
Sertifikat yang diberikan oleh [CA](https://intl.cloud.tencent.com/document/product/1007/30192#354) mencakup file Apache, IIS, Nginx, dan Tomcat. **Layanan enkripsi CSS menggunakan Nginx. Jadi, Anda harus memilih konten file Nginx untuk konfigurasi.** 
Buka **konsol SSL Certificate Service** > **[Certificate Management](https://console.cloud.tencent.com/ssl)** (Manajemen Sertifikat), pilih sertifikat target, klik **Download** (Unduh) di kolom "Operation" (Operasi), lalu dekompresi paket yang diunduh untuk mendapatkan file-file berikut:
  ![](https://main.qcloudimg.com/raw/f67e31bfa2c233cf8dc0c4a1e58cb6fc.png)
- <b id="content">Certificate content (Konten sertifikat)</b>: masukkan seluruh konten antara `-----BEGIN CERTIFICATE-----` dan `-----END CERTIFICATE-----` dalam file `.crt` untuk Nginx.
**Contoh konten:**
![](https://main.qcloudimg.com/raw/e6c61fda3637a2f11e56cec30f0f7bd3.png)
>?Jika sertifikat Anda diterbitkan oleh CA perantara dan berisi beberapa sertifikat, konten sertifikat harus disambung sebagai berikut:
> -----BEGIN CERTIFICATE-----
> -----END CERTIFICATE-----
> -----BEGIN CERTIFICATE-----
> -----END CERTIFICATE-----
- <b id="private_key">Certificate private key (Kunci privat sertifikat)</b>: masukkan seluruh konten antara ` -----BEGIN RSA PRIVATE KEY----- ` dan `-----END RSA PRIVATE KEY----- ` dalam file `.key` untuk Nginx.
**Contoh konten:**
![](https://main.qcloudimg.com/raw/1ca20b0021b49ccb407df43675be37ba.png)

### Langkah 2. Verifikasi konfigurasi
Konfigurasi HTTPS akan diterapkan dalam waktu sekitar 2 jam. Silakan kunjungi nama domain sekitar 2 jam setelah sertifikat dikirim. Jika HTTPS ditampilkan di bilah alamat browser, konfigurasi berhasil.
![](https://main.qcloudimg.com/raw/b1f54ec35855e5d2adbaeae96a04ef13.png)

### Langkah 3. Modifikasi konfigurasi
Fitur HTTPS dapat diaktifkan dan dinonaktifkan. Setelah fitur dinonaktifkan, CSS tidak akan lagi menyediakan layanan HTTPS untuk nama domain terkait. Sertifikat yang telah kedaluwarsa harus diganti dengan sertifikat baru yang valid.

