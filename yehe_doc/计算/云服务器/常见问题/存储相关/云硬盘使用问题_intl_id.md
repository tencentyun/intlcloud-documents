### Bagaimana cara melihat disk data?
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm).
2. Klik **Cloud Block Storage** di bilah sisi kiri untuk mengakses halaman pengelolaan **Cloud Block Storage**.
3. Klik ikon filter di samping judul kolom **Attribute** (Atribut), pilih **Data disk** (Disk data) dan klik **OK** (OKE) untuk melihat semua disk data di wilayah tersebut.

### Bagaimana cara membaca dan menulis disk data NTFS asli setelah sistem operasi Windows diinstal ulang ke Linux?
Windows menggunakan dua sistem file utama, NTFS atau FAT32, sedangkan EXT adalah sistem file untuk Linux. Ketika sistem operasi diubah dari Windows ke Linux setelah penginstalan ulang, disk data tetap dalam format aslinya. Oleh karena itu, sistem mungkin tidak dapat mengakses sistem file disk data. Dalam kasus ini, Anda perlu menggunakan konverter format untuk membaca disk data. Untuk mengetahui detailnya, lihat [Membaca/Menulis Disk Data NTFS setelah Menginstal Ulang CVM Windows ke CVM Linux](https://intl.cloud.tencent.com/document/product/213/3857).

### Bagaimana cara membaca disk data dalam format EXT setelah sistem operasi Linux diinstal ulang ke Windows?
Windows menggunakan dua sistem file utama, NTFS atau FAT32, sedangkan EXT adalah sistem file untuk Linux. Ketika sistem operasi diubah dari Linux ke Windows setelah penginstalan ulang, disk data tetap dalam format aslinya. Oleh karena itu, sistem mungkin tidak dapat mengakses sistem file disk data. Dalam kasus ini, Anda perlu menggunakan konverter format untuk membaca disk data. Untuk mengetahui detailnya, lihat [Membaca/Menulis Disk Data EXT setelah Menginstal Ulang CVM Linux ke CVM Windows](https://intl.cloud.tencent.com/document/product/213/3856).

### Apa perbedaan antara HDD cloud disk, Penyimpanan Cloud Premium, SDD, Enhanced SSD, dan Tremendous SSD?

- **HDD cloud disk** (Disk cloud HDD): Disk cloud Tencent Cloud HDD adalah disk cloud generasi sebelumnya. Disk ini sangat cocok untuk kasus penggunaan dengan beban I/O rendah dan akses yang jarang.
- **Premium Cloud Storage** (Penyimpanan Cloud Premium): Penyimpanan Cloud Premium Tencent Cloud adalah jenis penyimpanan hibrida. Penyimpanan ini mengadopsi mekanisme Cache untuk menyediakan penyimpanan seperti SSD berperforma tinggi, dan menggunakan mekanisme terdistribusi tiga salinan untuk memastikan keandalan data. Penyimpanan Cloud Premium cocok untuk aplikasi kecil dan menengah dengan persyaratan tinggi untuk keandalan data serta persyaratan standar untuk performa.
- **SSD**: SSD menggunakan NVMe SSD sebagai media penyimpanan, dan menggunakan mekanisme terdistribusi tiga salinan. SSD menyediakan penyimpanan berperforma tinggi dengan latensi rendah, IOPS acak tinggi, I/O throughput tinggi, dan keamanan data hingga 99,9999999%, sehingga cocok untuk aplikasi dengan persyaratan tinggi untuk performa I/O.
- **Enhanced SSD**: Enhanced SSD didasarkan pada mesin penyimpanan terbaru Tencent Cloud dan media penyimpanan NVMe SSD. SSD ini menggunakan mekanisme terdistribusi tiga salinan untuk menyediakan penyimpanan berperforma tinggi dengan latensi rendah, IOPS acak tinggi, I/O throughput tinggi, dan keamanan data hingga 99,9999999%, sehingga cocok untuk aplikasi intensif I/O dengan persyaratan tinggi untuk latensi, seperti database medium dan NoSQL.
- **Tremendous SSD**: Tremendous SSD didasarkan pada mesin penyimpanan terbaru Tencent Cloud, perangkat keras penyimpanan Intel terbaru, dan infrastruktur jaringan terbaru. SSD ini menggunakan mekanisme terdistribusi tiga salinan untuk menyediakan penyimpanan berperforma tinggi dengan latensi sangat rendah, IOPS acak tinggi, I/O throughput tinggi, dan keamanan data hingga 99,9999999%. Tremendous SSD cocok untuk aplikasi intensif I/O dengan persyaratan latensi tinggi, seperti database besar, rekomendasi NoSQL, KV, ES, dan AI.

>?
>- Harga jenis disk cloud ini berbeda-beda tergantung pada wilayahnya. Anda dapat memilih disk cloud yang paling sesuai dengan kebutuhan dan anggaran aplikasi Anda. Untuk mengetahui detail harga, lihat [Ikhtisar Harga](https://intl.cloud.tencent.com/document/product/362/2413).
>- Untuk informasi selengkapnya mengenai jenis dan performa disk, lihat [Jenis Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31636).
>

### Bagaimana cara menguji performa disk?
Sebaiknya gunakan FIO untuk melakukan uji tekanan dan verifikasi pada disk cloud. Untuk petunjuknya, lihat [Mengukur Performa Disk Cloud](https://intl.cloud.tencent.com/document/product/362/6741).

### Apa operasi disk cloud yang paling umum?
Untuk operasi umum disk cloud, lihat [Ikhtisar Operasi](https://intl.cloud.tencent.com/document/product/362/33140).

### Bagaimana cara memeriksa ruang yang tersedia dan yang telah digunakan pada disk cloud?
Anda dapat login ke instans CVM untuk memeriksa ruang yang tersedia dan yang telah digunakan pada disk cloud. Informasi ini juga dapat dilihat pada konsol CVM sebagai berikut.
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/instance/index) dan akses halaman **Instances** (Instans).
2. Pilih ID/Nama instans target untuk mengakses halaman detail.
3. Klik tab **Monitoring** (Pemantauan) untuk melihat penggunaan disk instans:
![](https://main.qcloudimg.com/raw/25270ae80b513d497527a0e9f2af1bac.png)

### Mengapa disk cloud yang saya buat secara terpisah dirilis bersama dengan instans saya?
Saat memasang disk cloud, Anda dapat memutuskan apakah disk cloud harus dirilis dengan instans secara otomatis. Hal ini dapat dikonfigurasi melalui [konsol CBS](https://console.cloud.tencent.com/cvm/cbs/index) atau [`ModifyDiskAttributes`](https://intl.cloud.tencent.com/document/product/362/15659) API.

### Bagaimana cara mempartisi dan memformat disk cloud yang terpasang?
Untuk informasi selengkapnya, lihat [Menginisialisasi Disk Cloud (<2 TB)](https://intl.cloud.tencent.com/document/product/362/31597) atau [Menginisialisasi Disk Cloud (≥2 TB)](https://intl.cloud.tencent.com/document/product/362/31598).



