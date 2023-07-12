Anda bisa membuat disk cloud dan memasangnya ke instance CVM Anda yang tersedia.Disk cloud dapat digunakan sebagai disk data instance CVM setelah prosedur inisialisasi sederhana.Untuk melakukan ini, ikuti langkah-langkah berikut:
- [Langkah 1.Membuat Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31647)
- [Langkah 2.Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/39991)
- [Langkah 3.Menginisialisasi Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31645)
- [Langkah 4.Memperluas Disk Cloud (opsional)](https://intl.cloud.tencent.com/document/product/362/31646)

## Ikhtisar
Dokumen ini berisi panduan tentang cara membuat `cbs-test` disk cloud di Zona 2 Beijing di konsol.

## Catatan
- Pastikan Anda memiliki instance CVM yang tersedia di zona ketersediaan (yaitu Zona 2 Beijing dalam contoh ini) tempat disk cloud akan dibuat.
- Untuk informasi selengkapnya tentang cara membeli dan memulai instance CVM, silakan lihat [Mengustomisasi Konfigurasi CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517) dan [Mengustomisasi Konfigurasi CVM Windows](https://intl.cloud.tencent.com/document/product/213/10516).

## Petunjuk
>?Dalam contoh ini, disk cloud premium elastis dibeli melalui konsol.Untuk informasi selengkapnya tentang pembuatan disk cloud, silakan lihat [Membuat Disk Cloud](https://intl.cloud.tencent.com/document/product/362/5744).

1.Masuk ke konsol CVM dan klik [**Cloud Block Storage** (Penyimpanan Blok Cloud)](https://console.cloud.tencent.com/cvm/cbs) di bilah sisi kiri.
2.Pilih **Beijing** di bagian atas halaman daftar Cloud Block Storage, kemudian klik **Create** (Buat).
3.Konfigurasikan parameter berikut di jendela pop-up:
- **Availability Zone** (Zona Ketersediaan): pilih **Beijing Zone 2** (Zona 2 Beijing).
- **Cloud Disk Type** (Jenis Disk Cloud): pilih **Premium Cloud Storage** (Penyimpanan Cloud Premium).
- **Capacity** (Kapasitas): pilih 20 GB.
- **Disk Name** (Nama Disk): masukkan `cbs-test`.

4.Klik **OK**.
5.Setelah mengonfirmasi konfigurasi, klik **OK** dan selesaikan pembayaran.
Kembali ke halaman daftar Cloud Block Storage.Anda kini dapat melihat `cbs-test` disk cloud elastis yang telah dibeli, yang berstatus **To be attached** (Akan dipasang).


## Operasi Berikutnya
Setelah disk cloud dibuat, Anda perlu terlebih dahulu memasangnya ke CVM di zona ketersediaan yang sama dengan sebuah disk data.Untuk informasi selengkapnya tentang operasi ini, lihat [Langkah 2.Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/39991).
