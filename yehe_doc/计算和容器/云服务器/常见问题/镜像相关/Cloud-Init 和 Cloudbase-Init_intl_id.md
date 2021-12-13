## Cloud-init

### Apa yang dimaksud dengan cloud-init?
Cloud-init adalah alat open source atau dikenal dengan sumber terbuka yang berjalan di dalam instans CVM sebagai layanan non-residen. Alat ini dijalankan saat startup dan keluar segera setelah dijalankan. Alat ini juga tidak memproses port apa pun.
Semua citra publik Linux dari Tencent Cloud sudah diinstal sebelumnya dengan layanan cloud-init. Anda perlu menjalankan layanan sebagai pengguna root karena layanan ini terutama digunakan untuk inisialisasi instans CVM seperti mengonfigurasi DNS, nama host, dan IP, dan eksekusi beberapa skrip kustom yang ditentukan pengguna untuk dijalankan selama boot pertama saat membuat instans CVM.

### Bagaimana cara memeriksa apakah layanan cloud-init di dalam instans Linux berfungsi dengan baik?

<span id="checkcloud-init"></span>
#### Memeriksa operasi cloud-init
Pertama, login ke instans dan jalankan perintah berikut untuk melihat apakah ada kesalahan yang ditampikan. Jika hasil eksekusi ditampilkan, artinya layanan berjalan normal. Jika tidak, kesalahan akan ditampilkan. Anda dapat memecahkan masalah sesuai dengan pesan kesalahan.
1. Hapus direktori cache cloud-init.
```
rm -rf /var/lib/cloud
```
2. Lakukan inisialisasi cloud-init lengkap.
```
cloud-init init --local
```
3. Ambil data dari sumber data yang dikonfigurasi.
```
cloud-init init
```
4. Inisialisasi cloud-init berlangsung dalam beberapa tahap. Untuk memastikan kecukupan dependensi antara tahap, tahap konfigurasi ditentukan untuk modul cloud-init.
```
modul cloud-init --mode=config
```
5. Tentukan tahap akhir untuk modul cloud-init.
```
modul cloud-init --mode=final
```

### Operasi inisialisasi apa yang dilakukan cloud-init pada instans?

Tencent Cloud mengimplementasikan semua operasi inisialisasi instans melalui cloud-init, sehingga memastikan transparansi operasi di dalam instans. Berikut ringkasan yang mencakup beberapa operasi inisialisasi. Untuk detail selengkapnya, lihat [dokumentasi cloud-init](http://cloudinit.readthedocs.io/en/latest/).

<table>
<tr><th style="width: 25%;">Operasi inisialisasi</th><th style="width: 25%;">Perilaku default</th><th style="width: 25%;">Penyesuaian</th><th style="width: 25%;">Catatan</th></tr>
<tr>
<td>inisialisasi nama host</td>
<td>Selama <b>peluncuran pertama</b> instans, cloud-init akan mengatur nama host instans sesuai dengan informasi nama host di <code>vendor_data.json</code>.</td>
<td>Jika membuat atau menginstal ulang instans dengan citra kustom dan Anda ingin mempertahankan nama host kustom dari citra, Anda dapat menghapus konfigurasi, <code>- scripts-user</code>, dari <code>/etc/cloud/cloud.cfg</code> sebelum membuat citra kustom.</td>
<td>Setelah Anda menonaktifkan <code>- scripts-user</code>, skrip inisialisasi, <code>/var/lib/cloud/instance/scripts/runcmd</code>, di dalam instans tidak akan dijalankan. Menonaktifkan konfigurasi juga akan memengaruhi inisialisasi sub-item lain seperti peginstalan cloud monitor dan keamanan cloud serta pengaturan sumber perangkat lunak. Selain itu, skrip kustom tidak akan dijalankan saat Anda membuat CVM.</td>
</tr>

<tr>
<td>inisialisasi /etc/hosts</td>
<td>Selama <b>peluncuran pertama</b> instans, cloud-init akan menginisialisasi <code>/etc/hosts</code> ke <code>127.0.0.1 $hostname</code> secara default.</td>
<td>Jika Anda membuat atau menginstal ulang instans dengan citra kustom dan ingin mempertahankan pengaturan /etc/hosts kustom pada citra, Anda dapat menghapus konfigurasi <code>- scripts-user</code> dan <code>- ['update_etc_hosts', 'once-per-instans']</code> dari <code>/etc/cloud/cloud.cfg</code> sebelum membuat citra kustom.</td>
<td>
<ul style="margin: 0px;">
<li>Setelah Anda menonaktifkan <code>- scripts-user</code>, skrip inisialisasi, <code>/var/lib/cloud/instance/scripts/runcmd</code>, di dalam instans tidak akan dijalankan. Menonaktifkan konfigurasi juga akan memengaruhi inisialisasi sub-item lain seperti peginstalan cloud monitor dan keamanan cloud serta pengaturan sumber perangkat lunak. Selain itu, skrip kustom tidak akan dijalankan saat Anda membuat CVM.</li>
<li>Setiap kali CVM dimulai ulang, pengaturan <code>/etc/hosts</code> dari beberapa CVM yang sudah ada akan ditimpa. Untuk mengatasi masalah ini, lihat <a href="https://intl.cloud.tencent.com/document/product/213/32504">Memodifikasi Pengaturan etc/hosts dari Instans Linux</a>.</li>
</ul>
</td>
</tr>

<tr>
<td>Inisialisasi DNS (skenario non-DHCP)</td>
<td>Selama <b>peluncuran pertama</b> instans, cloud-init akan mengatur DNS instans sesuai dengan informasi server nama di <code>vendor_data.json</code>.</td>
<td>Jika Anda membuat atau menginstal ulang instans dengan citra kustom dan ingin mempertahankan pengaturan DNS kustom dari citra, Anda dapat menghapus konfigurasi, <code>- resolv_conf</code> dan <code>unverified_modules: ['resolv_conf']</code>, dari <code>/etc/cloud/cloud.cfg</code> sebelum membuat citra kustom.</td>
<td>Tidak ada.</td>
</tr>

<tr>
<td>Inisialisasi sumber perangkat lunak</td>
<td>Selama <b>peluncuran pertama</b> instans, cloud-init akan mengatur sumber perangkat lunak instans sesuai dengan informasi write_files di <code>vendor_data.json</code>.</td><td>Jika Anda membuat atau menginstal ulang instans dengan citra kustom dan Anda ingin mempertahankan pengaturan sumber perangkat lunak kustom dari citra tersebut, Anda dapat menghapus konfigurasi, <code>- write-files</code>, dari <code>/etc/cloud /cloud.cfg</code> sebelum membuat citra kustom.</td>
<td>Tidak ada.</td>
</tr>

<tr>
<td>Inisialisasi NTP</td>
<td>Selama <b>peluncuran pertama</b> instans, cloud-init akan mengatur konfigurasi server NTP instans sesuai dengan informasi server NTP di <code>vendor_data.json</code> dan memulai layanan NTP.</td>
<td>Jika Anda membuat atau menginstal ulang instans dengan citra kustom dan Anda ingin mempertahankan konfigurasi NTP kustom dari citra, Anda dapat menghapus konfigurasi, <code>- ntp<code/>, dari <code>/etc/cloud/cloud.cfg</code> sebelum membuat citra kustom.</td>
<td>Tidak ada.</td>
</tr>

<tr>
<td>Inisialisasi kata sandi</td>
<td>Selama <b>peluncuran pertama</b> instans, cloud-init akan mengatur kata sandi akun default instans sesuai dengan informasi chpasswd di <code>vendor_data.json</code>.</td>
<td>Jika membuat atau menginstal ulang instans dengan citra kustom dan Anda ingin menyimpan kata sandi default kustom dari citra, Anda dapat menghapus konfigurasi, <code>- set-passwords</code>, dari <code>/etc/cloud/cloud.cfg</code> sebelum membuat citra kustom.</td>
<td>Tidak ada.</td>
</tr>

<tr>
<td>Pengikatan kunci</td>
<td>Selama <b>peluncuran pertama</b> instans, cloud-init akan mengatur kunci akun default dari instans berdasarkan informasi ssh_authorized_keys di <code>vendor_data.json</code>.</td>
<td>Jika Anda membuat atau menginstal ulang instans dengan citra kustom dan ingin menyimpan kunci default kustom dari citra, Anda dapat menghapus konfigurasi, <code>- users-groups</code>, dari <code>/etc/cloud/cloud.cfg</code> sebelum membuat citra kustom.</td>
<td>Jika Anda mengikat instans secara manual ke kunci di dalam instans, kunci sebelumnya akan ditimpa saat operasi pengikatan kunci dilakukan melalui konsol. </td>
</tr>

<tr>
<td>Inisialisasi jaringan (skenario non-DHCP)</td>
<td>Selama <b>peluncuran awal</b> instans, cloud-init akan mengatur IP, Gateway, dan Mask sesuai dengan informasi di <code>network_data.json</code>.</td>
<td>Jika Anda membuat atau menginstal ulang instans dengan citra kustom dan ingin menyimpan informasi jaringan kustom dari citra, Anda dapat menambahkan <code>jaringan: {config: disabled}</code> ke <code>/etc/cloud/cloud.cfg</code> sebelum membuat citra kustom.</td>
<td>Tidak ada.</td>
</tr>
</table>

### Bagaimana cara memperbaiki masalah yang terkait dengan cloud-init?

#### 1. Kesalahan karena pelepasan dependensi cloud-init
- Deskripsi masalah:
Saat perintah digunakan untuk memeriksa apakah layanan cloud-init berfungsi dengan benar, kesalahan berikut akan ditampilkan:
```
Traceback (panggilan terakhir yang dilakukan):
  File "/usr/bin/cloud-init", baris 5, di
    ********
    meningkatkan DistributionNotFound(req)
pkg_resources.DistributionNotFound: pyyaml
```
- Analisis masalah:
“pkg_resources.DistributionNotFound: xxxxx” menunjukkan bahwa dependensi cloud-init telah dilepas instalannya.
- Solusi:
 1. Instal ulang dependensi.
 2. Lihat [Memeriksa operasi cloud-init](#checkcloud-init) untuk melihat apakah kesalahan ditampilkan lagi.

#### 2. Kesalahan karena modifikasi penerjemah Python default
- Deskripsi masalah:
Kesalahan ditampilkan saat cloud-init dijalankan selama peluncuran.
- Analisis masalah:
Saat cloud-init diinstal, Python 2 digunakan sebagai penerjemah Python default, yang berarti bahwa tautan simbolik, `/usr/bin/python` dan `/bin/python`, ditautkan ke Python 2. Pengguna dapat mengubah penerjemah Python default ke Python 3 di dalam instans dengan mengalihkan tautan simbolik, `/usr/bin/python` dan `/bin/python`, ke Python 3. Karena masalah kompatibilitas, kesalahan akan ditampilkan saat cloud-init dijalankan selama startup.
- Solusi:
 1. Ubah penerjemah Python yang ditentukan dalam file `/usr/bin/cloud-init` dengan mengubah `#/usr/bin/python` atau `#/bin/python` menjadi `#! user/bin/python`.
> Jangan gunakan tautan simbolik. Arahkan langsung ke penerjemah tertentu.
>
 2. Lihat [Memeriksa operasi cloud-init](#checkcloud-init) untuk melihat apakah kesalahan ditampilkan lagi.

## Cloudbase-Init

### Apa yang dimaksud dengan Cloudbase-Init?
Seperti cloud-init, Cloudbase-Init adalah jembatan yang digunakan untuk berkomunikasi dengan instans CVM Windows. Layanan Cloudbase-Init dijalankan saat pertama kali peluncuran instans. Layanan akan membaca informasi konfigurasi inisialisasi instans dan menginisialisasinya. Operasi selanjutnya seperti mengatur ulang kata sandi dan mengubah alamat IP juga dilakukan melalui Cloudbase-Init.

### Bagaimana cara memeriksa apakah layanan Cloudbase-Init di dalam instans Windows berfungsi dengan benar?

<span id="checkcloudbase-init"></span>
#### Memeriksa operasi layanan Cloudbase-Init
1. Login ke instans.
> Jika Anda lupa kata sandi atau gagal mengatur ulang kata sandi karena pengecualian layanan Cloudbase-Init, Anda dapat mengatur ulang kata sandi dengan mengikuti [langkah 2](#step02).
>
2. <span id="step02">Buka **Control Panel** (Panel Kontrol) > **Administrative Tools** (Alat Administratif) > **Services** (Layanan).
3. Temukan layanan Cloudbase-Init, klik kanan, lalu buka **Properties** (Properti). </span>
 - Periksa apakah "Startup type" (Jenis startup) sudah diatur ke "Automatic" (Otomatis), seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/310a278dd2eaf2124d0d52055e0b5b6f.png)
 - Lihat "Logon identity" (Identitas login) dan pastikan "Local System account" (Akun Sistem Lokal) dipilih, seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/5a3f623aaf44d55cfe2eaa6aeadb4c12.png)
 - Luncurkan layanan Cloudbase-Init secara manual dan lihat apakah ada kesalahan yang ditampilkan.
Jika ada kesalahan yang muncul, Anda harus memperbaiki masalah terlebih dahulu dan memeriksa apakah Anda telah menginstal perangkat lunak keamanan apa pun yang dapat menghentikan Cloudbase-Init saat melakukan operasi terkait.
![](https://main.qcloudimg.com/raw/dbbe8f9fc05b07d8011705d9d217b76c.png)
 - Buka registri, temukan semua kunci "LocalScriptsPlugin", dan pastikan nilainya adalah 2, seperti yang ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/16106e540d8cf4ef39e5dccb44251350.png)
 - Periksa apakah pemuatan CD-ROM dinonaktifkan. Jika terdapat optical disc drive seperti yang ditampilkan pada gambar di bawah, berarti pemuatan belum dinonaktifkan; jika tidak, artinya telah dinonaktifkan dan perlu diaktifkan.
![](https://main.qcloudimg.com/raw/7707e694b475ba4d70b4d1d52a6c98bb.png)

### Bagaimana cara memperbaiki masalah umum terkait Cloudbase-Init?
#### Gagal mengatur ulang kata sandi selama inisialisasi
- Kemungkinan alasan:
 - Kata sandi akun Cloudbase-Init diubah secara manual, yang mengakibatkan kegagalan untuk meluncurkan layanan Cloudbase-Init, yang selanjutnya menyebabkan kegagalan operasi seperti mengatur ulang kata sandi selama inisialisasi.
 - Layanan Cloudbase-Init dinonaktifkan, yang menyebabkan kegagalan operasi seperti mengatur ulang kata sandi selama inisialisasi.
 - Perangkat lunak keamanan yang diinstal memblokir layanan Cloudbase-Init untuk mengatur ulang kata sandi, sehingga operasi menampilkan hasil yang berhasil tetapi sebenarnya gagal.
- Solusi:
Ikuti solusi yang sesuai untuk setiap kemungkinan alasan guna memperbaiki masalah.
 1. Ubah layanan Cloudbase-Init ke layanan LocalSystem. Untuk detailnya, lihat [langkah 2](#step02) di [Memeriksa operasi layanan Cloudbase-Init](#checkcloudbase-init).
 2. Ubah jenis peluncuran layanan Cloudbase-Init menjadi otomatis. Untuk detailnya, lihat [langkah 2](#step02) di [Memeriksa operasi layanan Cloudbase-Init](#checkcloudbase-init).
 3. Lepas perangkat lunak keamanan yang melekat atau tambahkan operasi yang relevan dari layanan Cloudbase-Init ke daftar perangkat lunak keamanan yang diizinkan.
