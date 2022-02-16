## Skenario Operasi 
Dokumen ini menjelaskan cara menghapus tabel di Konsol TcaplusDB.
>Jika Anda menghapus tabel sepenuhnya, semua datanya akan dihapus sepenuhnya dan tidak dapat dipulihkan; dengan demikian, harap lakukan dengan hati-hati.
>
Tabel dalam status "RUNNING" (BERJALAN) dapat dihapus. Setelah dihapus, tabel akan dipindahkan ke keranjang sampah (recycle bin), tetapi datanya masih ada.

## Prasyarat
Anda telah membuat tabel. Untuk informasi selengkapnya, silakan lihat [Membuat Tabel](https://intl.cloud.tencent.com/document/product/1016/32715).

## Petunjuk
1. Masuk ke halaman [Daftar Tabel](https://console.cloud.tencent.com/tcaplusdb/table) dan pilih tabel target. Pilih **More** (Lainnya) > **Delete** (Hapus) di kolom "Operation" (Operasi) atau pilih beberapa tabel dan klik **Batch Delete** (Hapus Massal) di bagian atas.
![](https://main.qcloudimg.com/raw/4698c628245093b1597caa2166f68cae.png)
2. Pada kotak dialog "Delete" (Hapus) yang muncul, klik **Confirm** (Konfirmasi), dan tabel akan dipindahkan ke keranjang sampah (recycle bin).
3. Pilih **Recycle Bin** (Keranjang Sampah) di bilah sisi kiri. Di recycle bin, Anda dapat **delete** (menghapus) tabel sepenuhnya dari sistem Anda atau **restore** (memulihkannya) ke status "RUNNING" (BERJALAN).
![](https://main.qcloudimg.com/raw/f752d04243ff5bdf7aff655d493781fa.png)

   
