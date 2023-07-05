## Skenario
Dokumen ini menjelaskan cara mengelola grup penempatan sebaran. Untuk informasi selengkapnya tentang grup penempatan, lihat [Grup Penempatan](https://intl.cloud.tencent.com/document/product/213/15486).

## Petunjuk
### Membuat grup penempatan

1. Login ke [konsol grup penempatan CVM](https://console.cloud.tencent.com/cvm/ps).
2. Klik **Create** (Buat).
3. Di jendela yang muncul, masukkan nama untuk grup penempatan, dan pilih lapisan grup penempatan.
4. Klik **OK** (OKE) untuk menyelesaikan pembuatan.

### Memulai instans di grup penempatan
1. Buka [halaman pembelian CVM](https://buy.cloud.tencent.com/?tab=custom&step=1&devPayMode=hourly&regionId=33&instanceType=SA2.SMALL1&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR).
2. Selesaikan pembelian seperti yang diminta di halaman.
Selama proses pembelian, pastikan untuk melakukan operasi berikut:
 - Saat mengatur CVM, klik **Advanced Configuration** (Konfigurasi Lanjutan), pilih **Add Instance to Placement Group** (Tambahkan Instans ke Grup Penempatan), dan pilih grup penempatan yang sudah ada.
 Jika tidak ada grup penempatan yang memenuhi persyaratan Anda, [buat satu](https://console.cloud.tencent.com/cvm/ps?regionId=1) di konsol.
 - Saat mengonfirmasi informasi konfigurasi, masukkan jumlah total instans yang akan ditambahkan ke grup penempatan, yang harus kurang dari batas kuantitas yang ditetapkan untuk grup penempatan.


### Memodifikasi grup penempatan instans
> Saat ini, Anda hanya dapat mengubah nama grup penempatan. Untuk melakukannya, selesaikan langkah-langkah berikut.
>
1. Login ke [konsol grup penempatan CVM](https://console.cloud.tencent.com/cvm/ps).
2. Arahkan kursor ke ID atau nama grup penempatan target, lalu klik <img src="https://main.qcloudimg.com/raw/beb5eae230dc169f7274bda7a19a5aa6.png" style="margin: 0;"></img>.
3. Di jendela yang muncul, masukkan nama baru.
4. Klik **OK** (OKE) untuk menyelesaikan modifikasi.

### Menghapus grup penempatan
> Anda dapat menghapus grup penempatan yang perlu diganti atau tidak lagi diperlukan. Anda harus menghentikan semua instans yang berjalan di grup penempatan sebelum dapat menghapusnya. Untuk melakukannya, selesaikan langkah-langkah berikut.
>
1. Login ke [konsol grup penempatan CVM](https://console.cloud.tencent.com/cvm/ps).
2. Klik **Number of Instances** (Jumlah Instans) untuk grup penempatan yang akan dihapus untuk membuka halaman pengelolaan instans, dan menghentikan semua instans dalam grup penempatan.
3. Kembali ke konsol grup penempatan, pilih grup penempatan yang akan dihapus, lalu klik **Delete** (Hapus).
6. Di jendela yang muncul, klik **OK** (OKE) untuk menyelesaikan penghapusan.
Anda dapat menghapus satu grup penempatan atau beberapa grup penempatan secara massal.
