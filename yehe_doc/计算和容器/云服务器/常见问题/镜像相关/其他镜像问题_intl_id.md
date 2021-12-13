### Apa yang dimaksud dengan citra?
Citra adalah templat untuk konfigurasi perangkat lunak CVM (sistem operasi, program yang sudah diinstal sebelumnya, dll.). Tencent Cloud mengharuskan pengguna menggunakan citra untuk meluncurkan instans. Citra dapat meluncurkan beberapa instans, dan pengguna dapat menggunakannya berulang kali. Untuk informasi selengkapnya tentang citra, lihat [Ikhtisar](https://intl.cloud.tencent.com/document/product/213/4940).

### Apa yang harus saya lakukan sebelum mengimpor citra?
Sebelum mengimpor citra, Anda harus menyelesaikan dua langkah utama: mengajukan izin dan menyiapkan file citra. Untuk informasi selengkapnya, lihat [Ikhtisar](https://intl.cloud.tencent.com/document/product/213/4945).

### Bagaimana cara mengekspor citra untuk pengujian lokal?
Migrasi Layanan Tencent Cloud mendukung citra dalam format qcow2, vhd, raw, dan vmdk.
Anda dapat menggunakan alat ekspor citra dari platform virtualisasi seperti VMWare vCenter Convert atau Citrix XenConvert. Untuk informasi selengkapnya, lihat setiap dokumentasi alat ekspor platform. Anda juga dapat mengekspor citra [menggunakan Disk2vhd (Windows)](https://intl.cloud.tencent.com/document/product/213/17815) atau [dengan menjalankan perintah (Linux)](https://intl.cloud.tencent.com/document/product/213/17814).

### Dapatkah saya menghapus citra kustom yang telah digunakan untuk membuat instans CVM?
Ya. Setelah citra kustom dihapus, citra tersebut tidak dapat lagi digunakan untuk meluncurkan instans CVM baru. Tindakan ini tidak akan memengaruhi instans yang telah diluncurkan. Jika Anda ingin menghapus semua instans yang diluncurkan dari citra ini, lihat [Mengklaim Kembali Instans](https://intl.cloud.tencent.com/document/product/213/4931) atau [Menghentikan Instans](https://intl.cloud.tencent.com/document/product/213/4930).

### Dapatkah saya menghapus citra kustom yang telah dibagikan dengan akun lain?
Tidak. Anda tidak dapat menghapus citra kustom yang telah dibagikan dengan akun lain. Untuk menghapusnya, Anda harus membatalkan berbagi citra terlebih dahulu. Untuk informasi selengkapnya, lihat [Membatalkan Berbagi Citra](https://intl.cloud.tencent.com/document/product/213/7148).


