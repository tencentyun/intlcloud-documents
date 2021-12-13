## Ikhtisar
Dokumen ini menjelaskan cara login ke instans Linux dari perangkat seluler yang berbeda. Alat berikut digunakan sebagai contoh.
 - Perangkat iOS: Klien Termius-SSH
 - Perangkat Android: JuiceSSH

## Perangkat Seluler yang Berlaku
Perangkat iOS dan Android

## Prasyarat
- Instans CVM dalam status **Running** (Berjalan).
- Anda sudah memiliki akun admin dan kata sandi (atau kunci) untuk digunakan login ke instans.
 - Jika Anda menggunakan kata sandi default sistem untuk login ke instans, buka [Pusat Pesan](https://console.cloud.tencent.com/message) untuk mendapatkan kata sandi terlebih dahulu.
 - Jika lupa kata sandi, Anda dapat [atur ulang sandi instans](https://intl.cloud.tencent.com/document/product/213/16566).
- IP publik telah dibeli untuk instans CVM Anda, dan port 22 terbuka. Port ini terbuka secara default untuk instans CVM yang dibeli dengan konfigurasi cepat.

## Petunjuk
Login ke instans dari perangkat seluler yang Anda gunakan:

<dx-tabs>
::: iOS\sdevice
1. Unduh klien Termius-SSH dari App Store, dan daftar seperti yang diinstruksikan.
2. Ketuk **New Host** (Host Baru) di layar beranda.
3. Akses halaman **New Host** (Host Baru) dan konfigurasikan informasi login sebagai berikut:
![](https://main.qcloudimg.com/raw/b0a672d2fae5ed3cb8e08be6492987cd.jpg)
 - **Hostname** (Nama host): alamat IP publik instans CVM Anda. Untuk informasi selengkapnya, lihat [Mendapatkan Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/17940).
 - **Use SSH** (Gunakan SSH): diaktifkan secara default.
 - **Username** (Nama Pengguna): masukkan akun admin `root`, atau `ubuntu` jika instans Anda menggunakan sistem operasi Ubuntu.
 - **Password** (Kata Sandi): masukkan kata sandi login instans.
4. Ketuk **Save** (Simpan) di sudut kanan atas untuk menyimpan konfigurasi login.
5. Pilih informasi login di halaman **Hosts** (Host), lalu ketuk **Continue** (Lanjutkan) di kotak prompt di bagian bawah halaman.
![](https://main.qcloudimg.com/raw/2c1e0518f8bf4377c36ce92d0d484b57.jpg)
6. Login berhasil jika Anda melihat hal berikut.
![](https://main.qcloudimg.com/raw/54a7fde256f500b32a2b0753c0966b2d.jpg)
:::
::: Android\sdevice
#### Membuat identitas[](id:newAuthentication)
1. Unduh dan instal JuiceSSH.
2. Dari layar beranda, ketuk **Connections** (Koneksi) untuk membuka tab **Identity** (Identitas).
3. Ketuk **+** (+) di sudut kanan bawah.
4. Konfigurasikan nama akun dan kata sandi di halaman **Identity** (Identitas).
 - **Nickname** (Nama panggilan): masukkan nama kustom untuk identitas, hal ini bersifat opsional.
 - **Username** (Nama Pengguna): masukkan akun admin `root`, atau `ubuntu` jika instans Anda menggunakan sistem operasi Ubuntu.
 - **Password** (Kata Sandi): ketuk **Set (optional)** (Atur (opsional)), lalu masukkan kata sandi login instans di jendela pop-up.
5. Ketuk **✔** (✔) di sudut kanan atas halaman.

#### Membuat koneksi
1. Dari layar beranda, ketuk **Connection** (Koneksi), lalu ketuk **+** (+) di sudut kanan bawah halaman **Connections** (Koneksi).
2. Konfigurasikan informasi login untuk koneksi baru.
 - **Nickname** (Nama Panggilan): masukkan nama koneksi khusus, hal ini bersifat opsional.
 - **Type** (Jenis): pilih **SSH** (SSH).
 - **Address** (Alamat): alamat IP publik instans CVM Anda. Untuk informasi selengkapnya, lihat [Mendapatkan Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/17940).
 - **Identity** (Identitas): pilih identitas yang dibuat di [Membuat identitas](#newAuthentication).
 - **Port** (Port): masukkan port 22.
 Pertahankan pengaturan default untuk parameter lainnya.
3. Ketuk **Add to team** (Tambahkan ke tim) di bagian bawah halaman untuk menyimpan konfigurasi login.

#### Login ke instans
1. Pada halaman **Connections** (Koneksi), pilih instans untuk login dan ketuk **Accept** (Terima).
2. Login berhasil jika Anda melihat hal berikut.
  ![](https://main.qcloudimg.com/raw/a07b70fa518c0d474073515147487264.jpg)

:::
</dx-tabs>

