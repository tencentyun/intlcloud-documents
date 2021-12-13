Konfigurasi kustom menyediakan lebih banyak platform citra dan konfigurasi lanjutan untuk penyimpanan, bandwidth, dan grup keamanan. Anda dapat memilih mode konfigurasi sesuai kebutuhan. Dokumen ini menggunakan konfigurasi kustom sebagai contoh.

## Pendaftaran dan Verifikasi

Sebelum menggunakan CVM, Anda perlu melakukan operasi berikut:
1. Daftar akun Tencent Cloud dan selesaikan proses verifikasi identitas. Verifikasi identitas adalah wajib jika Anda ingin membeli instans CVM di daratan Tiongkok.
Pengguna baru perlu [mendaftar](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F) untuk mendapatkan akun di situs web Tencent Cloud. Untuk informasi selengkapnya, lihat [Mendaftar Akun Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985).
2. Kunjungi halaman [Pengantar CVM Tencent](https://intl.cloud.tencent.com/product/cvm), dan klik **Get Started** (Memulai).

<span id="SelectType"></span>
## Memilih Model Perangkat

1. Konfigurasi informasi berikut seperti yang diminta oleh halaman:
![Pilih wilayah dan model](https://main.qcloudimg.com/raw/40c2812ff1294f901238cc3e39ba25f9.png)
<table>
<tr><th style="width: 20%">Kategori</th><th style="width: 12%">Wajib/Opsional</th><th>Deskripsi Konfigurasi</th></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/213/2180">Mode Penagihan</a></td><td>Wajib</td><td><ul><li><b>Bayar sesuai pemakaian</b>: mode penagihan elastis untuk CVM.</li></ul></td></tr>
<tr><td>Wilayah</td><td>Wajib</td><td>Sebaiknya pilih wilayah yang paling dekat dengan pelanggan Anda untuk mengurangi latensi akses dan meningkatkan kecepatan akses.</td></tr>
<tr><td>Zona Ketersediaan</td><td>Wajib</td><td>Pilih zona ketersediaan sesuai kebutuhan.</br>Jika Anda ingin membeli beberapa CVM, sebaiknya pilih zona ketersediaan yang berbeda untuk menerapkan pemulihan bencana.</td></tr>
<tr><td>Jaringan</td><td>Wajib</td><td>Ruang jaringan yang terisolasi secara logis yang dibangun di Tencent Cloud. Virtual private cloud (VPC) mencakup setidaknya satu subnet. Sistem ini menyediakan VPC dan subnet default untuk setiap wilayah.</br>
Jika VPC atau subnet yang ada tidak memenuhi persyaratan Anda, Anda dapat membuat VPC atau subnet di konsol VPC.</br><b>Catatan</b>:<ul><li>Sumber daya di VPC yang sama dapat dibagikan dalam jaringan pribadi.</li><li>Saat membeli CVM, pastikan CVM dan subnet tempat CVM dibuat memiliki zona ketersediaan yang sama.</li></ul></td></tr>
<tr><td>Instans</td><td>Wajib</td><td>Tencent Cloud menyediakan berbagai jenis instans berdasarkan perangkat keras yang mendasarinya. Untuk mendapatkan performa yang optimal, sebaiknya gunakan jenis instans generasi terbaru.</br>Untuk informasi selengkapnya tentang instans, lihat <a href="https://intl.cloud.tencent.com/document/product/213/11518">Jenis Instans</a>.</td></tr>
<tr><td>Citra</td><td>Wajib</td><td>Tencent Cloud menyediakan citra publik, citra kustom, dan citra bersama. Untuk informasi selengkapnya tentang citra, lihat<a href="https://intl.cloud.tencent.com/document/product/213/4941">Ikhtisar Jenis Citra</a>.</br>Jika Anda baru saja mulai menggunakan Tencent Cloud, sebaiknya pilih citra publik, yang berisi sistem operasi Windows resmi yang telah diaktivasi dan tidak memerlukan pembayaran tambahan (kecuali untuk wilayah Amerika Utara).</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">Disk Sistem</a></td><td>Wajib</td><td>Digunakan untuk menginstal sistem operasi. Kapasitas defaultnya adalah 50 GB.</br>Jenis Cloud Block Storage (CBS) yang tersedia berbeda-beda, bergantung pada wilayahnya. Harap pilih nilai seperti yang diinstruksikan oleh halaman.</br>Untuk informasi selengkapnya tentang CBS, lihat <a href="https://intl.cloud.tencent.com/document/product/362/31636">Jenis CBS</a>.</td></tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/362/31636">Disk Data</a></td><td>Opsional</td><td>Digunakan untuk meningkatkan kapasitas penyimpanan CVM guna memastikan efisiensi dan keandalan yang tinggi. Disk data CBS tidak ditambahkan secara default.</br>Untuk informasi selengkapnya tentang CBS, lihat <a href="https://intl.cloud.tencent.com/document/product/362/31636">Jenis CBS</a>.</td></tr>
<tr><td>Bandwidth Jaringan Publik</td><td>Wajib</td><td>Tencent Cloud menyediakan dua mode penagihan jaringan. Atur nilai sesuai kebutuhan.<ul><li><b>Tagihan per bandwidth</b>: pilih bandwidth tetap. Kehilangan paket akan terjadi ketika bandwidth melebihi nilai ini. Ini berlaku untuk skenario ketika koneksi jaringan sedikit berfluktuasi.</li><li><b>Tagihan per lalu lintas</b>: penagihan didasarkan pada lalu lintas yang benar-benar digunakan. Anda dapat menentukan bandwidth puncak untuk mencegah biaya yang ditimbulkan oleh lalu lintas yang tidak terduga. Kehilangan paket akan terjadi ketika bandwidth instan melebihi nilai ini. Ini berlaku untuk skenario ketika koneksi jaringannya berfluktuasi secara signifikan.</li></ul></td></tr>
<tr><td>Kuantitas</td><td>Wajib</td><td>Jumlah CVM yang akan dibeli.</td></tr>
</table>
2. Klik **Next (Selanjutnya): Complete Configuration** (Selesaikan Konfigurasi) untuk mengakses halaman konfigurasi CVM.

## Mengonfigurasi CVM
1. Konfigurasi informasi berikut seperti yang diminta oleh halaman:
![Grup keamanan dan CVM](https://main.qcloudimg.com/raw/be9b22616da76afd527f855368707899.png)
<table>
<tr><th style="width: 20%">Kategori</th><th style="width: 12%">Wajib/Opsional</th><th>Deskripsi Konfigurasi</th></tr>
<tr><td>Grup Keamanan</td><td>Wajib</td><td>Digunakan untuk mengonfigurasi kebijakan akses jaringan untuk satu atau beberapa CVM.</br><b>Pastikan port login 3389 terbuka.</b>Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/12452">Grup Keamanan</a>.</td></tr>
<tr><td>Proyek</td><td>Wajib</td><td>Proyek default dipilih. Anda dapat memilih proyek yang ada sesuai kebutuhan untuk mengelola CVM yang berbeda.</td></tr>
<tr><td>Tag</td><td>Opsional</td><td>Digunakan untuk mengategorikan dan mengelola instans CVM. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/19548">Mengelola Instans melalui Tag</a>.</td></tr>
<tr><td>Nama Instans</td><td>Opsional</td><td>Nama CVM yang akan dibuat.</br>Ini ditentukan oleh pengguna. Sebaiknya gunakan <b>CVM-01</b>.</td></tr>
<tr><td>Metode Login</td><td>Wajib</td><td>Konfigurasikan metode untuk masuk ke CVM sesuai kebutuhan.<ul><li><b>Kata Sandi Kustom</b>: sesuaikan kata sandi untuk masuk ke instans.</li><li><b>Pasangan Kunci SSH</b>: pilih pasangan kunci sebagai kredensial login instans (hanya tersedia untuk sistem operasi Linux)</li><li><b>Kata Sandi Acak</b>: kata sandi yang dibuat secara otomatis akan dikirim melalui <a href="https://console.cloud.tencent.com/message">Pusat Pesan</a>.</li></ul></td></tr>
<tr><td>Layanan Keamanan</td><td>Opsional</td><td>Secara default, layanan keamanan diaktifkan secara gratis untuk membantu Anda membangun sistem keamanan CVM guna mencegah kebocoran data.</td></tr>
<tr><td>Pemantauan Cloud</td><td>Opsional</td><td>Secara default, pemantauan cloud diaktifkan secara gratis. Pemantauan ini menyediakan pemantauan data CVM yang komprehensif, analisis data cerdas, alarm kesalahan waktu nyata, dan laporan data kustom untuk secara tepat memantau layanan Tencent Cloud dan kondisi kesehatan CVM.</td></tr>
<tr><td>Pengaturan Lanjutan</td><td>Opsional</td><td>Konfigurasikan pengaturan tambahan untuk instans sesuai kebutuhan.<ul><li><b>Nama host</b>: Anda dapat menyesuaikan nama komputer dalam sistem operasi CVM. Setelah CVM dibuat, Anda dapat login ke dalamnya untuk melihat nama host.</li><li><b>Peran CAM</b>: Anda dapat menetapkan peran dan menggunakannya untuk memberikan izin kepada entitas peran untuk mengakses CVM layanan dan sumber daya dan melakukan operasi di Tencent Cloud. Untuk informasi selengkapnya tentang pengaturan, lihat<a href="https://intl.cloud.tencent.com/document/product/213/38290">Mengelola Peran</a>.</li><li><b>Grup Penempatan</b>: Anda dapat menambahkan instans ke grup penempatan jika diperlukan untuk meningkatkan ketersediaan layanan. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/15486">Grup Penempatan</a>.</li><li><b>Data Kustom</b>: Anda dapat mengonfigurasi instans dengan menetapkan data kustom, dan skrip yang dikonfigurasi akan berjalan saat instans diluncurkan. Jika beberapa CVM dibeli bersamaan, data kustom akan berjalan di semua CVM. Sistem operasi Windows mendukung format PowerShell dan maksimum 16 KB data mentah. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/17526">Mengonfigurasi Data Kustom (Windows CVM)</a>.</br><b>Catatan</b>: konfigurasi data kustom hanya mendukung citra publik di Windows. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/19670">Cloud-Init & Cloudbase-Init</a>.</li></ul></td></tr>
</table>
2. Klik **Next (Selanjutnya): Confirm Configuration** (Konfirmasi Konfigurasi) untuk mengakses halaman konfirmasi informasi konfigurasi.

## Mengonfirmasi Informasi Konfigurasi

1. Periksa informasi CVM yang akan dibeli dan detail biaya setiap item konfigurasi.
2. Klik **Purchase** (Beli) dan selesaikan pembayaran. Kemudian, Anda dapat masuk ke [konsol CVM](https://console.cloud.tencent.com/cvm) untuk melihat CVM Anda.
Informasi seperti nama instans, alamat IP publik, alamat IP pribadi, nama pengguna login, dan kata sandi login awal CVM akan dikirimkan ke akun Anda melalui [Pusat Pesan](https://console.cloud.tencent.com/message). Anda dapat menggunakan informasi ini untuk login dan mengelola instans Anda. Untuk memastikan keamanan, ubah kata sandi login CVM Anda sesegera mungkin.

## Login ke dan Menghubungkan Instans

Setelah menyelesaikan operasi CVM, Anda dapat login ke CVM Anda di konsol Tencent Cloud dan melakukan operasi seperti membangun situs sesuai kebutuhan.
Pilih metode untuk login ke CVM di konsol Tencent Cloud sesuai kebutuhan:
- [Login ke Instans CVM Windows Menggunakan File RDP (Direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5435)
- [Login ke Instans CVM Windows Menggunakan Desktop Jarak Jauh](https://intl.cloud.tencent.com/document/product/213/32498)

## Memformat dan Mempartisi Disk Data

Jika Anda menambahkan disk data saat [memilih jenis instans](#SelectType), Anda perlu memformat dan mempartisi disk data setelah login ke instans CVM. **If you have not added any data disks, skip this step.** (Jika Anda belum menambahkan disk data apa pun, lewati langkah ini)
Pilih panduan operasi yang sesuai kapasitas disk dan sistem operasi CVM.
- Untuk disk kurang dari 2 TB:
[Menginisialisasi Disk Cloud (Windows)](https://intl.cloud.tencent.com/document/product/362/31597)
- Untuk disk yang sama dengan atau lebih besar dari 2 TB:
[Menginisialisasi Disk Cloud (Windows)](https://intl.cloud.tencent.com/document/product/362/31598)

Untuk operasi lainnya, lihat [Skenario Inisialisasi](https://intl.cloud.tencent.com/document/product/362/31596).
