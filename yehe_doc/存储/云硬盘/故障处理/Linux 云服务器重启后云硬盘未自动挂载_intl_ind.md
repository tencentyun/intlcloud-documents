## Deskripsi Kesalahan
Sistem file dibuat dan dikonfigurasikan untuk dipasang secara otomatis ke disk cloud di CVM Linux, tetapi pemasangan otomatis gagal saat memulai ulang CVM.

## Kemungkinan Penyebab
- **Reason 1** (Sebab 1): pemasangan otomatis disk cloud tidak dikonfigurasi di file konfigurasi `fstab` CVM.
- **Reason 2** (Sebab 2): kesalahan konfigurasi pada file konfigurasi `fstab`.
Misalnya, apabila nama perangkat digunakan untuk pemasangan otomatis dan nama tersebut berubah pada saat CVM dimulai ulang, startup akan gagal.

## Solusi
- **Solution to reason 1** (Solusi untuk sebab 1):
Gunakan cara berikut untuk mengonfigurasi ulang file `/etc/fstab` untuk memasang disk cloud secara otomatis setelah memulai ulang CVM:
- Menggunakan tautan lunak disk (direkomendasikan)
- Menggunakan Pengidentifikasi Unik Universal (Universally Unique Identifier/UUID) sistem file
- Menggunakan nama perangkat (tidak direkomendasikan)
Untuk petunjuk lengkapnya, baca [Mengonfigurasi file `/etc/fstab`](#ConfigurationFile).
- **Solution to reason 2** (Solusi untuk sebab 2):
Masuk ke CVM Linux menggunakan VNC dan pilih mode pengguna tunggal.Dalam mode ini, perbaiki dan konfigurasi ulang file konfigurasi `/etc/fstab`.Untuk petunjuk lengkapnya, baca [Memperbaiki file `/etc/fstab`] (#RepairConfiguration).


## Prosedur Penanggulangan Masalah


### Mengonfigurasi file `/etc/fstab` [](id:ConfigurationFile)
1.[Masuk Ke Instance Linux Menggunakan Metode Masuk Standar](https://intl.cloud.tencent.com/document/product/213/5436).
2.Pilih metode konfigurasi untuk mendapatkan informasi.[](id:Step2)

<dx-tabs>
::: Menggunakan\stautan\slunak\sdisk\scloud\selastis\s(direkomendasikan)
#### Menganalisis metode konfigurasi
- **Pros** (Kelebihan): tautan lunak disk cloud elastis bersifat tetap dan unik.Tautan ini tidak berubah dengan operasi seperti pemasangan, pelepasan, dan pemformatan partisi.
- **Cons** (Kekurangan): hanya disk cloud elastis yang bisa menggunakan tautan lunak, yang hampir tidak tampak ketika beroperasi untuk pemformatan partisi.

#### Mendapatkan informasi
Jalankan perintah berikut untuk melihat tautan lunak disk cloud elastis.
```
plaintext
ls -l /dev/disk/by-id
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/99c7d8362b4313a0366adace46563bb7.png)
:::
::: Menggunakan\sUUID\ssistem\sfile

#### Menganalisis metode konfigurasi
Konfigurasi pemasangan otomatis mungkin gagal karena perubahan UUID sistem file.
Misalnya, memformat ulang sistem file akan mengubah UUID-nya.

#### Mendapatkan informasi
Jalankan perintah berikut untuk melihat UUID dari sistem file.
```
blkid /dev/vdb1
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/a1f6204b8f95f71609571612ff45aa42.png)
:::
::: Menggunakan\snama\sperangkat\s(tidak\sdirekomendasikan)

#### Menganalisis metode konfigurasi
Konfigurasi pemasangan otomatis mungkin gagal karena perubahan nama perangkat.
Misalnya, jika disk cloud elastis di CVM dilepas dan dipasang kembali, nama perangkat dapat berubah saat sistem operasi mengenali sistem file lagi.

#### Mendapatkan informasi
Jalankan perintah berikut untuk melihat nama perangkat.
```
fdisk -l
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/1d09eba0c658fed0e9f5303e273b5539.png)
:::
</dx-tabs>
3.Jalankan perintah berikut untuk mencadangkan file `/etc/fstab` ke direktori `/home`, misalnya:
```
cp /etc/fstab /home
```
4.Jalankan perintah berikut untuk menggunakan editor VI untuk membuka file `/etc/fstab`.
```
vi /etc/fstab
```
5.Tekan **i** untuk masuk ke mode edit, dan tambahkan konten berikut ke baris berikutnya dari baris terakhir file.
```
<Device information> <Mount point> <File system format> <File system installation option> <File system dump frequency> <Urutan pemeriksaan sistem file saat peluncuran>
```
Lihat contoh berikut sesuai dengan metode konfigurasi yang dipilih di [langkah 2](#Step2).
- (Direkomendasikan) Gunakan tautan lunak disk cloud elastis sebagai contoh.Tambahkan konten berikut:
```
/dev/disk/by-id/virtio-disk-drkhklpe-part1 /data/newpart   ext4 defaults     0   2
```
Gunakan UUID sistem file sebagai contoh.Tambahkan konten berikut:
```
UUID=d489ca1c-5057-4536-81cb-ceb2847f9954 /data/newpart   ext4 defaults     0   2
```
- (Tidak direkomendasikan) Gunakan nama perangkat sebagai contoh.Tambahkan konten berikut:
```
/dev/vdb1 /data/newpart   ext4 defaults     0   2
```
6.Tekan **ESC**, masukkan **:wq**, dan tekan **Enter** untuk menyimpan konfigurasi dan keluar dari editor.
7.Jalankan perintah berikut untuk memeriksa apakah file `/etc/fstab` telah berhasil ditulis.
```
mount -a
```
Jika muncul informasi seperti yang ditampilkan di bawah ini, file telah berhasil ditulis.Sistem file akan terpasang secara otomatis saat sistem operasi dijalankan.Anda dapat memulai ulang CVM untuk memverifikasi hasilnya.
![](https://main.qcloudimg.com/raw/4289f335d3373074d7fc799863fba498.png)

[](id:RepairConfiguration)
### Memperbaiki file `/etc/fstab`
1.[Masuk Ke Instance Linux Menggunakan VNC](https://intl.cloud.tencent.com/document/product/213/32494).
2.Pilih mode pengguna tunggal.Untuk petunjuk lengkapnya, lihat [Mengonfigurasi CVM Linux untuk Boot ke Mode Pengguna Tunggal](https://intl.cloud.tencent.com/document/product/213/34819).
3.Jalankan perintah berikut untuk mencadangkan file `/etc/fstab` ke direktori `/home`, misalnya:
```
cp /etc/fstab /home
```
4.Jalankan perintah berikut untuk menggunakan editor VI untuk membuka file `/etc/fstab`.
```
vi /etc/fstab
```
5.Tekan **i** untuk masuk ke mode edit.Pindahkan kursor ke awal baris eror dan masukkan `#` mengomentari konfigurasi ini, seperti yang ditunjukkan di bawah ini.
>?Baris ini mengonfigurasi pemasangan otomatis disk data.Namun, akibat kesalahan konfigurasi, disk cloud tidak dapat dipasang ketika CVM dimulai ulang.
>
![](https://main.qcloudimg.com/raw/2e6106588877801aa38fbe4af3dc52a6.png)
6.Tekan **ESC**, masukkan **:wq**, dan tekan **Enter** untuk menyimpan konfigurasi dan keluar dari editor.
7.Masukkan `exit` untuk keluar dari mode pengguna tunggal.
8.Tunggu hingga selesai dimulai ulang.Masuk ke CVM.
9.Konfigurasi ulang file seperti yang dijelaskan di [Mengonfigurasi file `/etc/fstab`](#ConfigurationFile).
