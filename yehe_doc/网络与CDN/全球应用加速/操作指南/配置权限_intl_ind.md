Akun root atau akun lain dengan izin AdministratorAccess dapat menetapkan akun kolaborator dengan izin akses baca-tulis atau baca-saja dari GAAP dengan mengonfigurasi izin pengelolaan akses.

Pengguna memiliki dua cara agar dapat mengotorisasi akun kolaborator: dengan menghubungkan kebijakan dengan pengguna, atau dengan menghubungkan pengguna dengan kebijakan. Untuk informasi selengkapnya, lihat [Manajemen Akses Cloud (CAM)](https://intl.cloud.tencent.com/document/product/598/10583).

## Persiapan
1. Login ke akun root atau akun lain dengan izin AdministratorAccess di [Konsol Tencent Cloud](https://console.cloud.tencent.com/).
2. Pada navigasi atas, pilih **Cloud Products** (Produk Cloud) > **Manage and Audit** (Kelola dan Audit) > **[Cloud Access Management](https://console.cloud.tencent.com/cam/policy)** (Manajemen Akses Cloud) untuk masuk ke konsol CAM.
>Anda juga dapat masuk ke konsol pengelolaan akses dengan memilih **Your Account Name** (Nama Akun Anda) > **Access Management** (Pengelolaan Akses) di sudut kanan atas konsol.

## Petunjuk
### Menghubungkan Pengguna dengan Kebijakan
1. Klik **Reserved Instance** (Instans Cadangan) di bilah sisi kiri untuk masuk ke halaman manajemen.
2. Di bilah pencarian, masukkan **GAAP**. 2 hasil ditemukan. Pilih Izin Kebijakan, dan klik **Associate user/group** (Hubungkan pengguna/grup).
![1](https://main.qcloudimg.com/raw/06fc88f33dbc935ca2b65948fb3343e3.png)
3. Pilih pengguna yang akan diotorisasi, dan klik **OK** (Oke). Pengguna diotorisasi.
![](https://main.qcloudimg.com/raw/61df6a1fd920c302c0f2b2f68c79f4a2.png)

### Menghubungkan Kebijakan dengan Pengguna
1. Di bilah sisi kiri, klik **User** (Pengguna) > **User List** (Daftar Pengguna) untuk masuk ke halaman manajemen.
2. Temukan baris dalam daftar yang berisi pengguna yang akan diotorisasi. Di kolom operasi, klik **Authorize** (Otorisasi).
![](https://main.qcloudimg.com/raw/740bfd484b9df92eb13bb9517c6238e1.png)
3. Telusuri **GAAP** di daftar hubungan. Pilih kebijakan yang akan diotorisasi dan klik **OK** (Oke). Pengguna diotorisasi.
![](https://main.qcloudimg.com/raw/7a602d2eefa9ed3ba69ca72df39616a7.png)

### Memeriksa dan Menghapus Izin
Pengguna yang diotorisasi dapat memeriksa dan menghapus izin dengan mengeklik nama pengguna di [Daftar Pengguna](https://console.cloud.tencent.com/cam).
![](https://main.qcloudimg.com/raw/da41405cfc21806881e2c86d9bc2823e.png)
