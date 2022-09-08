## Saluran pembelian disk cloud

Tencent Cloud menyediakan dua cara bagi Anda untuk membeli disk cloud, baik melalui konsol atau melalui API.


### Membeli langsung melalui konsol[](id:CreateDisk)
1.Masuk ke [Konsol CBS](https://console.cloud.tencent.com/cvm/cbs), pilih wilayah dan klik **Create** (Buat).
2.Konfigurasikan jenis dan kapasitas disk cloud.
3.Pilih metode penagihan.
4.Konfirmasi pesanan lalu bayar.
5.Disk cloud dibuat segera setelah pembayaran pesanan.Disk cloud dapat digunakan setelah dipasang dan diinisialisasi.

### Menggunakan snapshot untuk membeli melalui konsol
Jika Anda ingin menyimpan data snapshot dari disk data ke disk baru secara default, Anda dapat menggunakan snapshot untuk membuat disk cloud di [Daftar Snapshot](https://console.cloud.tencent.com/cvm/snapshot ).Anda juga dapat mengonfigurasi parameter **Snapshot** untuk menentukan snapshot target untuk membuat disk saat Anda [membelinya secara terpisah melalui konsol](#CreateDisk).
1.Buka [Daftar Snapshot](https://console.cloud.tencent.com/cvm/snapshot) di konsol.
2.Di baris snapshot target, pilih **More**>**Create new disk** (Selengkapnya > Buat disk baru).
<dx-alert infotype="explain" title="">
3.Konfigurasikan jenis dan kapasitas disk cloud.
Saat Anda menggunakan snapshot untuk membuat disk cloud, ukuran kapasitas tidak boleh lebih kecil dari ukuran snapshot.Jika Anda tidak menentukan kapasitas disk cloud, kapasitasnya akan sama dengan kapasitas snapshot secara default.
</dx-alert>
4.Pilih metode penagihan.
5.Konfirmasi pesanan lalu bayar.
6.Disk cloud dibuat segera setelah pembayaran pesanan.Disk cloud dapat digunakan setelah dipasang dan diinisialisasi.

### Membeli bersama dengan CVM
- Saat Anda membeli CVM Tencent Cloud, Anda juga dapat membeli disk cloud non-elastis dengan mengatur **System Disk** (Disk Sistem) ke disk cloud.Untuk informasi selengkapnya, lihat [Membuat Instance](https://intl.cloud.tencent.com/document/product/213/4855).
- Anda dapat membeli disk cloud elastis dengan mengatur parameter **Data Disk** (Disk Data) saat membeli CVM.Untuk informasi selengkapnya, lihat [Membuat Instance](https://intl.cloud.tencent.com/document/product/213/4855).

### Membeli melalui API
Anda dapat menggunakan API `CreateDisks` untuk membuat disk cloud.Untuk informasi selengkapnya, lihat [Membuat disk cloud](https://intl.cloud.tencent.com/document/product/362/16312).

## Membeli saluran untuk disk lokal
Saat ini, disk lokal hanya dapat dibeli saat Anda membeli instance CVM IO Tinggi atau Data Besar, dan tidak dapat dibeli secara terpisah.Untuk informasi selengkapnya, lihat [Membuat Instance](https://intl.cloud.tencent.com/document/product/213/4855).

