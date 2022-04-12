Dokumen ini akan menjelaskan cara memigrasikan layanan CLB jaringan publik Anda dengan lancar dari jaringan klasik ke VPC.
>? Contoh ini hanya untuk referensi. Dalam migrasi aktual, harap berhati-hati menilai dampaknya dan mengembangkan rencana migrasi terlebih dahulu.

### Skenario
Konfigurasi sumber daya bisnis berbasis jaringan klasik: 
+ Nama domain DNS diselesaikan ke VIP CLB jaringan publik di jaringan klasik.
+ CLB jaringan publik terikat dengan dua CVM (CVM 1 dan CVM 2) sebagai server backend.
+ Aplikasi yang di-deploy di CVM 1 dan CVM 2 dapat mengakses layanan TencentDB for Redis dan TencentDB for MySQL backend.


### Proses migrasi
<dx-steps>
- Buat VPC
- Migrasikan layanan TencentDB
- Buat instans CVM dan deploy aplikasi
- Buat CLB jaringan publik dan hubungkan dengan CVM
- Ubah alamat IP nama domain DNS
- Rilis sumber daya jaringan klasik
</dx-steps>

### Petunjuk migrasi
1.  Buat VPC seperti yang diinstruksikan di [Membuat VPC](https://intl.cloud.tencent.com/document/product/215/31805).
![]()
2.  Migrasikan instans [TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236/31915) dan [TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/31944) ke VPC.
>? Selama migrasi, instans TencentDB tetap terhubung. Baik IP jaringan klasik asli maupun alamat IP VPC tetap valid selama jangka waktu tertentu setelah migrasi, sehingga menjaga ketersediaan layanan Anda. Selesaikan migrasi sumber daya lain dalam periode tersebut.
>
![]()
3.  Buat gambar untuk CVM 1 dan CVM 2 berbasis jaringan klasik seperti yang diinstruksikan di [Membuat Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4942) dan [gunakan gambar](https://intl.cloud.tencent.com/document/product/213/36304) untuk membuat dua instans CVM di VPC. Kemudian uji apakah CVM dapat mengakses instans TencentDB.
 >? Jika memulai ulang instans CVM selama migrasi dapat diterima oleh bisnis Anda, Anda dapat langsung beralih ke VPC selama jam tidak sibuk. Untuk petunjuk mendetail, lihat [Beralih ke VPC](https://intl.cloud.tencent.com/document/product/213/20278).
 >
![]()
4.  Buat CLB jaringan publik di VPC dan hubungkan dengan dua CVM yang dibuat pada langkah sebelumnya. Untuk informasi selengkapnya, lihat [Mulai Menggunakan CLB](https://intl.cloud.tencent.com/document/product/214/8975). Lakukan pemeriksaan kesehatan untuk menghindari gangguan layanan karena pengecualian.
![]()
5.  Selesaikan nama domain DNS ke VIP CLB jaringan publik di VPC.
![]()
6.  Periksa apakah VPC berfungsi dengan baik. Jika ya, lepaskan sumber daya CLB dan CVM jaringan publik asli di jaringan klasik untuk menyelesaikan migrasi.
 >? IP jaringan klasik asli dari instans TencentDB akan dilepaskan secara otomatis setelah habis masa berlakunya.
 >
![]()
