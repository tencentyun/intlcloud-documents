Anda dapat membuat koneksi ke CDN untuk mengirimkan konten di server asal Anda ke simpul layanan terdekat dengan pengguna akhir, yang dapat menanggapi langsung permintaan pengguna sehingga secara efektif mengurangi latensi akses pengguna dan meningkatkan ketersediaan. 
Untuk mengonfigurasi CDN, Anda harus mendaftar akun Tencent Cloud, mengaktifkan CDN, menambahkan nama domain, dan mengonfigurasi CNAME. Langkah-langkah di atas dijabarkan dalam dokumen ini.

## Langkah 1. Daftar akun Tencent Cloud
Jika akun Tencent Cloud sudah ada, Anda dapat mengabaikan langkah ini.
<div style="background-color:#00A4FF; width: 270px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn1">Daftar akun Tencent Cloud</a></div>

## Langkah 2. Aktifkan layanan CDN
#### 1. Selesaikan verifikasi identitas
Pengguna terdaftar harus terlebih dahulu menyelesaikan verifikasi identitas agar dapat mengaktifkan CDN. Anda dapat memverifikasi identitas di konsol CDN atau Pusat Akun. Untuk informasi selengkapnya tentang proses verifikasi, silakan baca [Panduan Verifikasi Identitas](https://intl.cloud.tencent.com/document/product/378/3629).
<div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;;"><a href="https://console.cloud.tencent.com/cdn" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3149.btn2">Go to CDN console</a></div><br>

![](https://main.qcloudimg.com/raw/e593cf6199d64fbcc5c6f50089778cf9.png)
#### 2. Aktifkan layanan CDN
Setelah menyelesaikan verifikasi identitas, Anda dapat mengaktifkan layanan CDN.
(1) Pilih cara penagihan
Tencent Cloud CDN memiliki dua wilayah penagihan, yaitu **Chinese mainland** (Tiongkok daratan) dan **outside the Chinese mainland** (di luar Tiongkok daratan). Untuk pengguna yang mengaktifkan CDN setelah 7 Desember 2020 21.30, **bill-by-hourly-traffic** (tagihan-berdasarkan-lalu–lintas-per-jam) adalah satu-satunya opsi penagihan. Untuk informasi selengkapnya, silakan baca [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/228/2949).
![](https://main.qcloudimg.com/raw/5f75a3047566df1413233c2c0ac2736f.png)
(2) Aktifkan CDN
Nyatakan persetujuan Anda dengan Ketentuan Layanan, klik **Activate CDN** (Aktifkan CDN), dan mulai gunakan layanan akselerasi.
![](https://main.qcloudimg.com/raw/4b1997247ae88641d1c2af0289b7ad2a.png)

## Langkah 3. Buat koneksi nama domain
Anda harus menghubungkan nama domain bisnis untuk layanan akselerasi. CDN meng-cache sumber daya dari server asal bisnis Anda ke simpul cache CDN melalui nama domain akselerasi untuk merealisasi akselerasi akses sumber daya sehingga pengguna akhir dapat meminta sumber daya dari simpul terdekat. Untuk informasi selengkapnya, silakan baca <a href="https://intl.cloud.tencent.com/document/product/228/5734" hotrep="document.guide.3149.linkdomain">Menambahkan Nama Domain</a>.

## Langkah 4. Mengonfigurasi CNAME
Setelah nama domain Anda terhubung ke CDN, Anda harus menyelesaikan konfigurasi CNAME di penyedia layanan nama domain Anda. Setelah konfigurasi aktif, CDN dapat digunakan sebagaimana mestinya. Untuk informasi selengkapnya, silakan lihat <a href="https://intl.cloud.tencent.com/document/product/228/3121" hotrep="document.guide.3149.linkcname">Konfigurasi CNAME</a>.
