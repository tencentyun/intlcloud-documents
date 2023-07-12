## Ikhtisar
Saat disk cloud tidak lagi digunakan dan **data penting telah dicadangkan**, Anda dapat melepas sumber daya virtual dengan menghentikan disk cloud.Anda tidak akan ditagih untuk pembayaran layanan disk cloud setelah penghentian.**Ketika disk cloud dihentikan, semua data di disk cloud akan dihapus dan tidak dapat dipulihkan.Harap diperhatikan bahwa disk cloud yang telah dihentikan tidak dapat dipulihkan.**
Siklus hidup disk cloud non-elastis sama dengan CVM.Hanya dapat dihentikan ketika instance CVM dihentikan.Untuk informasi selengkapnya, lihat [Menghentikan Instance](https://intl.cloud.tencent.com/document/product/213/4930).
Siklus hidup disk cloud elastis tidak bergantung pada CVM.Oleh karena itu, disk ini dapat dihentikan secara terpisah.Dokumen ini menjelaskan cara menghentikan disk cloud elastis.
Disk cloud elastis dapat dihentikan dengan metode berikut:
- Penghentian manual
- Penghentian manual didukung untuk disk cloud yang dibayar sesuai pemakaian, dan segera berlaku.
- Penghentian otomatis
- Disk cloud yang dibayar sesuai pemakaian akan dihentikan secara otomatis jika saldo Anda menjadi negatif selama lebih dari 24 jam.Anda dapat terus menggunakannya jika Anda [mengisi ulang](https://intl.cloud.tencent.com/document/product/362/36874) akun Anda dalam waktu yang ditentukan.


## Penghapusan Data
Data yang dihapus selama penghentian disk cloud tidak dapat diakses oleh siapa pun, sementara data yang dihapus dari disk cloud CBS akan terhapus sepenuhnya.Mekanisme berikut memastikan bahwa semua data dihapus.
* Menghapus ruang logis dari disk cloud akan dicatat sebagai metadata.Ruang disk fisik akan dihapus, yang secara paksa menghapus semua data secara permanen.Semua pembacaan ke ruang logis mengembalikan `0`.
* Metadata akan segera dimusnahkan ketika disk cloud dilepas untuk memastikan bahwa data tidak dapat diakses lagi.Ruang penyimpanan fisik disk cloud akan diambil alih dan dihapus sebelum ditetapkan kembali.

## Prasyarat
- Disk cloud dalam status **To be attached** (Akan dilampirkan).Untuk disk cloud yang sedang digunakan, [lepaskan](https://intl.cloud.tencent.com/document/product/362/32400) terlebih dahulu.
- **Semua data penting sudah dicadangkan**.


## Menghentikan Disk Cloud Yang Dibayar Sesuai Pemakaian Secara Manual
1.Masuk ke [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
2.Hentikan disk cloud seperti yang diinstruksikan di bawah ini:
a.Hentikan satu disk cloud: cari disk cloud target yang berada dalam status **To be attached** (Akan dilampirkan), dan klik **More** > **Terminate/Return** (Selengkapnya > Hentikan/Kembalikan).
b.Hentikan disk cloud dalam batch: pilih beberapa disk cloud target yang berada dalam status **To be attached** (Akan dilampirkan) dan klik **Terminate/Return** (Hentikan/Kembalikan) di bagian atas daftar.
>!Ketika disk cloud dihentikan, semua data di disk cloud juga akan dihapus, dan tidak dapat dipulihkan.Harap diperhatikan bahwa disk cloud yang telah dihentikan tidak dapat dipulihkan.
>
3.Di kotak pop-up **Terminate Cloud Disk** (Hentikan Disk Cloud), klik **Submit** (Kirim) untuk menyelesaikan penghentian.
Disk cloud target tidak akan ditagih lagi.Ini **dihentikan secara permanen dan tidak dapat dipulihkan**.

 

