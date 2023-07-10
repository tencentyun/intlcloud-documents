## Skenario Pengoperasian
Ketika tidak perlu menggunakan snapshot lagi, Anda dapat menghapus snapshot untuk melepaskan sumber daya virtual.


## Deskripsi
- Saat Anda menghapus snapshot, hanya data eksklusif untuk snapshot yang akan dihapus, dan disk cloud tempat snapshot dibuat tidak akan terpengaruh.
- Anda dapat menggunakan snapshot untuk memulihkan disk cloud ke status data saat snapshot dibuat.Menghapus snapshot yang dibuat sebelumnya untuk disk cloud tidak akan memengaruhi penggunaan snapshot yang dibuat nanti secara berkelanjutan.
- **Ketika snapshot dihapus, semua data dalam snapshot akan dihapus secara bersamaan, dan data tidak dapat diambil.Snapshot yang dihapus tidak dapat dipulihkan, jadi harap gunakan dengan hati-hati.**



## Petunjuk
### Menghapus Snapshot di Konsol
1.Masuk ke halaman [Daftar Snapshot](https://console.cloud.tencent.com/cvm/snapshot).
2.Anda dapat menghapus snapshot menggunakan metode berikut:
a.Penghapusan tunggal: klik **Delete** (Hapus) di baris snapshot yang akan dihapus.
b.Penghapusan dalam batch: pilih semua snapshot yang ingin Anda hapus (pastikan snapshot tidak terlibat dalam tugas apa pun) dan klik **Delete** (Hapus) di bagian atas daftar.
3.Klik **OK**.

### Menghapus Snapshot dengan API
Anda dapat menggunakan API DeleteSnapshots untuk menghapus snapshot.Untuk petunjuk mendetail, lihat [Menghapus Snapshot](https://intl.cloud.tencent.com/document/product/362/15645).
